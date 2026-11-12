# Filtering Django Form Dropdowns to Enforce Team Boundaries in Production Code

## Overview

I contributed to ImperialCollegeLondon/proCAT, a Django web application for research project management. The issue was that form dropdowns for selecting a project lead or allocation user showed all 50+ users in the system, allowing anyone to assign work outside the RSE Team group. I fixed this by overriding Django form `__init__` methods to filter querysets to show only RSE Team members, sorted alphabetically. The fix included 4 comprehensive tests with 100% coverage. The PR merged on November 3, 2026, with code owner approval from Diego Alonso Álvarez. **PR:** https://github.com/ImperialCollegeLondon/proCAT/pull/865

## What happened

**The Problem Emerged in Code Review**

I started by cloning the proCAT repository and reproducing the issue locally. Running the Django shell, I confirmed the bug:

```python
from main.forms import ProjectForm
form = ProjectForm()
print(f"Lead field options: {form.fields['lead'].queryset.count()} users")
# Output: 50+ users, including all non-RSE team members
```

This exact unfiltered behavior matched the issue description. The form was using Django's default queryset without filtering, which meant non-RSE team members were selectable in critical fields.

**Initial Implementation**

I overrode the `__init__` method in both `ProjectForm` and `AllocationInlineForm` to customize the querysets:

```python
def __init__(self, *args, **kwargs):
    super().__init__(*args, **kwargs)
    self.fields['lead'].queryset = User.objects.filter(
        groups__name="RSETeam"
    ).order_by("first_name", "last_name")
```

I wrote 4 tests covering filtering and sorting behavior. All 12 form tests passed (8 existing + 4 new), and coverage hit 100% on modified lines.

**The Type Safety Problem**

I opened PR #865 on November 2. Diego Alonso Álvarez reviewed the code and identified a type safety issue: my initial approach used both `cast(forms.Field, ...)` AND `# type: ignore[attr-defined]` together—combining two approaches unnecessarily.

```python
# What I had (redundant):
cast(forms.Field, self.fields['lead']).queryset = ...  # type: ignore[attr-defined]

# What Diego suggested (professional Python):
self.fields['lead'].queryset = ...  # type: ignore[attr-defined]
```

Diego's comment: "I think the cast might be redundant here since we're already using the type ignore comment."

**Learning from Feedback**

This feedback taught me the difference between casting and type-ignoring—you choose one approach, not both. I refined the code to use only `# type: ignore[attr-defined]` per professional Python standards. Mypy confirmed no issues.

Diego approved the refined version on November 3 with comment: **"Brilliant! All good!"**

**The Result**

The PR merged into ImperialCollegeLondon:main the same day. Codecov confirmed 100% coverage on modified lines (89.92% project coverage). The fix is now in production code.

Before:
```
ProjectForm.lead: 50+ users (including non-RSE team members)
AllocationInlineForm.user: 50+ users (including non-RSE team members)
Order: Random
```

After:
```
ProjectForm.lead: 8 RSE Team members
AllocationInlineForm.user: 8 RSE Team members
Order: Alphabetical by first_name, then last_name
```

## Limitations and what's next

**What This Doesn't Do**

The fix assumes users are added to the RSETeam group by administrators—there's no self-service group management. If a new team member isn't added to the group, they won't appear in dropdowns even if authorized. The solution also doesn't prevent direct database queries from bypassing the form layer, though that's an application-level concern, not a form-level one.

**What I'd Do Differently**

I'd research Django form best practices earlier instead of learning through code review feedback. Understanding when to use `cast()` vs `# type: ignore` from the start would have avoided the refinement round. I'd also check the maintainers' existing codebase for type-safety patterns before implementing.

**What's Next**

The next step would be to add role-based access control (RBAC) to allow different permission levels within RSE Team. A future enhancement could let project leads delegate allocation assignments to other team members, requiring a more granular permission model than just group membership.
