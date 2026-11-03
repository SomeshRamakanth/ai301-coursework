# Contribution: Filter Users to RSE Team Only (proCAT)

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in the repository is not read. **Keep every section header below under its exact name** — the format criteria grade exactly that. Your course repo link is the whole submission: no tool files and no evidence uploads are part of Assignment 5.

**Contribution Number:** 1
**Student:** Somesh Ramakanth
**GitHub Username:** SomeshRamakanth
**Issue:** https://github.com/ImperialCollegeLondon/proCAT/issues/862
**Pull Request:** https://github.com/ImperialCollegeLondon/proCAT/pull/865

One repository, built across units 5 to 8, telling the whole story of your real contribution. Fill it as you work, not at the end — the sections below ask for evidence that is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull Request, ends with a Toolkit block: which tool did that phase's work and how you used it, what it produced, what difficulties or shortcomings it presented, and what you changed or would change because of them. Together the blocks are the thread the rubric's Toolkit points read, and they are the raw material for your unit-9 portfolio, so keep them current as you work rather than reconstructing them later.

A Toolkit block looks like this (copy it into each story section and fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work, starting below: what you built or changed that week, what broke, and what you changed because of it. The blocks tell the story where it happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each one in the week it belongs to.

**Unit 5: Issue selection and strategy for Django form filtering**

Explored open-source contributions beyond pure UI fixes, seeking more substantial backend work. Selected proCAT issue #862 (filter users in forms to show only RSE Team members) from a curated list of candidates. The issue required understanding Django form customization, group-based filtering, and professional coding standards. Selected this contribution because it involved more complex logic than simple CSS fixes: Django ORM filtering, test writing (4 comprehensive tests), type safety handling, and code review iteration.

**Unit 6: Django form implementation and test suite development**

Implemented user filtering in ProjectForm and AllocationInlineForm by overriding __init__ to filter querysets. Added 4 comprehensive tests covering filtering behavior and alphabetical sorting. All tests passed locally (12/12 in test_forms.py). Configured fork setup with proper dependency management (uv, pre-commit hooks). Learned: Django form field customization via queryset filtering; pytest patterns for testing form behavior; best practices for managing form field type safety.

**Unit 7: Code review iteration and type safety refinement**

First code review from Diego Alonso Álvarez focused on type safety: initial approach used redundant `cast()` with `# type: ignore`, combining two approaches unnecessarily. Refined to use only `# type: ignore[attr-defined]` per professional Python standards. Plan-check validation confirmed measurable test criteria (filtering logic, sorting order). Created detailed test evidence showing pass/fail criteria. Learned: understanding when to use type casting vs type ignoring; professional code review teaches standards, not just bug fixes; iterating on feedback improves code quality.

**Unit 8: Code approval and PR merge completion**

Final code review approved by Diego with comment "Brilliant! All good!" PR #865 merged into ImperialCollegeLondon:main on Nov 3, 2026. Codecov confirmed 100% coverage on modified lines (89.92% project coverage). 4 checks passed. Code successfully integrated into production codebase. Learned: responding to code review feedback professionally; understanding type safety best practices; recognizing when intermediate feedback leads to better solutions.

---

## Why I Chose This Issue

After exploring the issue-scout skill with Python/TypeScript candidates, I identified that a second contribution focusing on backend logic rather than UI fixes would demonstrate more comprehensive engineering capability. I selected proCAT issue #862 (filter users to show only RSE Team members in forms) because:

1. **Complexity**: Requires Django form customization, ORM filtering, and understanding group-based permissions — more substantial than CSS changes.
2. **Test coverage**: Demands writing 4 comprehensive tests covering filtering and sorting behavior, not just visual verification.
3. **Type safety**: Involves understanding Python's typing system and proper use of mypy with Django forms.
4. **Code review**: Provides opportunity to learn professional standards through real feedback iteration.

The issue had clear scope (filter two form fields), active maintainers (Diego Alonso Álvarez actively reviewed), and was well-documented. This contribution better demonstrates full-stack engineering: implementation, testing, type safety, and professional code review iteration.

**Toolkit**

- Tool: GitHub issue-scout and proCAT issue selection from curated list
- What it produced: Clear, scoped contribution with learning opportunity in backend logic and professional coding standards
- Difficulties: none met
- What changed: Selected backend/testing focus over UI-only work to demonstrate broader engineering capability

---

## Understanding the Issue

**Problem Description**

When selecting a project lead or assigning allocations in proCAT, the form dropdown shows all users. However, the application should restrict this to only members of the RSE Team group, maintaining team boundaries in the interface.

**Expected Behavior**

Form fields (project lead, allocation user) should display only RSE Team members, sorted alphabetically by first and last name.

**Affected Components**

- `ProjectForm.lead` field (project detail view)
- `AllocationInlineForm.user` field (allocations view)

**Root Cause**

Forms were using default querysets without filtering. proCAT uses Django Groups for team management; the RSETeam group existed in migrations but wasn't referenced in form field querysets.

**Toolkit**

- Tool: Code inspection, Django documentation, pytest
- What it produced: Understanding of Django form queryset filtering and group-based permissions
- Difficulties: Understanding how Django form fields relate to model queryset filtering
- What changed: Identified need to override form __init__ to customize field querysets

---

## Solution Approach

**Analysis**

Django ModelForm fields pull their queryset from the related model by default. To filter users by group membership, override the `__init__` method to set a custom queryset after calling super().__init__().

**Proposed Solution**

Add custom `__init__` methods to:
1. `ProjectForm` - filter `lead` field to RSETeam users
2. `AllocationInlineForm` - filter `user` field to RSETeam users

Query: `User.objects.filter(groups__name="RSETeam").order_by("first_name", "last_name")`

**Implementation Plan**

1. Override `__init__` in ProjectForm
2. Override `__init__` in AllocationInlineForm
3. Write 4 tests covering filtering and sorting
4. Verify mypy type safety
5. Submit PR for code review

**Deviation Note**

Initial implementation used `cast()` to handle type safety. Code review feedback identified this was redundant with `# type: ignore` comments. Final solution uses only `# type: ignore[attr-defined]` per professional Python standards.

**Toolkit**

- Tool: Edit (modify forms.py), pytest (write tests), mypy (type checking)
- What it produced: Form implementations with custom queryset filtering and 4 comprehensive tests
- Difficulties: Type safety with Django form fields; mypy initially required both cast() and type: ignore
- What changed: Refined type handling to use only type: ignore comments, removing redundant casting

---

## Testing Strategy

**Test Coverage**

Added 4 tests in `tests/main/test_forms.py`:
1. ProjectForm lead field filters to RSETeam users only
2. ProjectForm lead field sorts users alphabetically
3. AllocationInlineForm user field filters to RSETeam users only
4. AllocationInlineForm user field sorts users alphabetically

**Test Results**

- All 12 form tests pass (8 existing + 4 new)
- 100% coverage on modified lines
- 89.92% project coverage
- No regressions

**Toolkit**

- Tool: pytest, test fixtures, assertions
- What it produced: 4 comprehensive tests covering filtering and sorting logic
- Difficulties: Understanding how to properly test Django form field querysets
- What changed: Tests verify both filtering (RSETeam only) and sorting (alphabetical) behavior

---

## Implementation Notes

**Nov 2, 2026**

Submitted initial PR #865 with form filtering implementation and 4 tests. All tests passed locally. Pre-commit.ci reported passing checks.

**Nov 3, 2026 - Code Review Iteration**

Diego Alonso Álvarez reviewed code and identified type safety issue: initial implementation used both `cast(forms.Field, ...)` and `# type: ignore[attr-defined]` together, which is redundant.

**Nov 3, 2026 - Type Safety Refinement**

Refined type handling to use only `# type: ignore[attr-defined]` per professional Python standards. mypy: no issues found. PR approved and merged.

**Key Learnings**

- Django form customization: override `__init__` to set custom querysets
- Type safety: choose between casting OR type-ignoring, not both
- Code review: feedback often teaches professional standards, not just bug fixes
- Testing: comprehensive tests improve confidence in form behavior

**Toolkit**

- Tool: mypy (type checking), code review feedback, git (commits and push)
- What it produced: Final implementation passing mypy, 4 comprehensive tests, merged PR
- Difficulties: Understanding proper type safety approach in Django forms
- What changed: Simplified from redundant cast() + type: ignore to just type: ignore comments

---

## Pull Request

**Status:** ✅ Merged into ImperialCollegeLondon:main (Nov 3, 2026)

**Link:** https://github.com/ImperialCollegeLondon/proCAT/pull/865

**Claim Comment:** https://github.com/ImperialCollegeLondon/proCAT/issues/862#issuecomment-6593068136

**Summary**

Filters project lead and allocation user dropdowns to display only RSE Team members, sorted alphabetically. Added 4 comprehensive tests with 100% coverage. Includes code review iteration on type safety.

**Changes**

- `main/forms.py`: Added `__init__` methods to ProjectForm and AllocationInlineForm
- `tests/main/test_forms.py`: Added 4 tests covering filtering and sorting

**Verification**

- ✅ All tests pass (12/12)
- ✅ mypy: no issues
- ✅ Codecov: 100% coverage on modified lines (89.92% project)
- ✅ Code review: approved by Diego Alonso Álvarez
- ✅ Status: merged

**Maintainer Feedback**

- Nov 3: Diego identified type safety redundancy
- Nov 3: Refined per professional standards
- Nov 3: "Brilliant! All good!" - approved and merged

**Toolkit**

- Tool: GitHub PR creation, code review process, gh CLI
- What it produced: Merged PR with code owner approval, 4 tests, 100% coverage
- Difficulties: Type safety iteration required understanding professional Python standards
- What changed: Refined type handling based on code review feedback

---

## Learnings and Reflections

**Technical Skills Gained**

- Django form customization: overriding `__init__` to customize field querysets
- Django ORM filtering: using `filter(groups__name="RSETeam")` for group-based filtering
- Type safety in Python: understanding when to use `cast()` vs `# type: ignore`
- Professional code review: feedback teaches standards, not just fixes bugs
- Test writing: comprehensive tests for form behavior and edge cases

**Challenges Overcome**

The main challenge was type safety. Initial approach used both `cast()` and `# type: ignore`, which code review identified as redundant. Learning to choose the proper approach — using only `# type: ignore[attr-defined]` — taught me professional Python standards and the value of code review feedback.

**What I'd Do Differently Next Time**

- Research Django form best practices before implementation (would have avoided type safety issues)
- Recognize that code review feedback often teaches professional standards, not just fixing bugs
- Be more thoughtful about type safety from the start: use one approach (casting OR ignoring), not both
- Understand that merged, complete PRs demonstrate more capability than pending ones

---

## Resources Used

- [proCAT CONTRIBUTING.md](https://github.com/ImperialCollegeLondon/proCAT/blob/main/CONTRIBUTING.md) — Project contribution guidelines and code of conduct
- [Django Form Documentation](https://docs.djangoproject.com/en/6.1/topics/forms/) — Model form field customization and queryset filtering
- [proCAT GitHub Issues](https://github.com/ImperialCollegeLondon/proCAT/issues) — Issue tracking and feature requests
- [Code Review Feedback](https://github.com/ImperialCollegeLondon/proCAT/pull/865) — Type safety discussions and professional standards
