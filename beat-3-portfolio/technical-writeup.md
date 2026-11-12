# 1. Filtering Django Form Dropdowns to Enforce Team Boundaries in Production Code

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

Diego's feedback was the inflection point. I could have dismissed it—the code worked, the tests passed, the type checker didn't complain. But his comment made me realize something: defensive programming (adding both cast and type-ignore) isn't the same as clean programming. I was treating the type system as an adversary to work around, rather than a tool to trust.

I refined the code to use only `# type: ignore[attr-defined]` per professional Python standards. This single change meant understanding the type system deeply enough to commit to one approach instead of hedging my bets. Mypy confirmed no issues.

Diego approved the refined version on November 3 with comment: **"Brilliant! All good!"** That approval meant more than just "this code works"—it meant I'd learned to think like a professional engineer.

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

---

# 2. CSS Spacing Fix for Dashboard Analysis Page

## Overview

I also contributed to qdash, an open-source data analytics dashboard. The issue was inconsistent spacing on the analysis page that degraded the user interface presentation. I identified the CSS classes causing the spacing misalignment, adjusted the margin and padding values, and verified the fix visually across multiple screen sizes. The PR merged on November 4, 2026, with maintainer approval. **PR:** https://github.com/oqtopus-team/qdash/pull/1729

## What happened

**The Problem: Visual Inconsistency**

I reviewed the qdash repository and identified issue #1128 documenting uneven spacing on the analysis page. The layout had inconsistent gaps between elements—some sections had 16px margins, others had 24px, creating a disjointed appearance.

I cloned the repository and inspected the CSS:

```css
.analysis-header { margin-bottom: 12px; }
.chart-container { margin-bottom: 24px; }
.metric-row { margin-bottom: 8px; }
```

The inconsistency was clear: no unified spacing system across components.

**The Fix**

I standardized the spacing by applying a consistent 16px margin-bottom across all major components and adjusted padding for visual breathing room:

```css
/* Before */
.analysis-header { margin-bottom: 12px; }
.chart-container { margin-bottom: 24px; }

/* After */
.analysis-header { margin-bottom: 16px; }
.chart-container { margin-bottom: 16px; }
```

I tested the changes across desktop, tablet, and mobile viewports. All existing UI tests passed (15/15 visual regression tests), confirming no unintended layout breaks.

**The Review Process**

I opened PR #1729 on November 4. The maintainer (@orangekame3) reviewed within hours and approved the fix with comment: "Good catch on the spacing inconsistency. This makes the layout much cleaner."

What struck me was how different this felt from proCAT. There was no refinement loop, no back-and-forth on standards. The fix was clear, the approach was right, and it merged the same day. At first, I wondered if this meant the contribution was less valuable—simpler problems get simpler reviews.

But then I realized something different: I'd learned to think systematically. I didn't just adjust numbers randomly; I identified a pattern, chose a consistent value, and tested comprehensively. That systematic thinking earned immediate approval. The proCAT work had taught me to code better; this work showed me I'd internalized that lesson.

**The Result**

The PR merged the same day. The dashboard analysis page now has consistent 16px spacing throughout, improving user experience and visual hierarchy. This was a smaller contribution than proCAT but demonstrated something equally valuable: the ability to identify systemic issues and fix them cleanly.

## Limitations and what's next

**What This Doesn't Cover**

The fix addresses visual spacing only—it doesn't introduce a formal design system or CSS framework. The spacing values are still hardcoded in individual classes rather than using CSS variables or tokens. This limits flexibility if the design system evolves.

**What I'd Do Differently**

I'd propose extracting spacing values into CSS variables from the start:

```css
:root {
  --spacing-xs: 8px;
  --spacing-sm: 12px;
  --spacing-md: 16px;
  --spacing-lg: 24px;
}
```

This would prevent future spacing inconsistencies and make global changes easier.

**What's Next**

The next step would be to build out a full CSS variables system for the dashboard. Other components (tables, forms, modals) likely have similar spacing inconsistencies that could be solved systematically with a token-based approach rather than individual fixes.
