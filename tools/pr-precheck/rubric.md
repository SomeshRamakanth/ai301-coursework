# Rubric: is this pull request ready to submit?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Diff bounded by plan | The diff read against the plan's "Approach" and "Files to Change" sections | All changed files are listed in the plan; all changes align with the stated approach; no extra refactoring or unrelated fixes bundled in | required |
| Test evidence proves the fix | The test evidence file read against the plan's "Test Plan" section | Test evidence shows the observable outcome the plan promised; the specific test case from the issue (or repro steps) now passes; all tests still pass | required |
| Commits are clean and related | The commit history in the diff | Every commit has a clear, meaningful message (no "fixup", "temp", "WIP", or placeholder commits); all commits relate directly to the issue and plan (not unrelated cleanup or refactoring); commit messages are readable and explain what changed | required |
| PR description matches diff | The PR description read against the actual diff | The description accurately summarizes what changed; it explains why (links back to the issue and plan diagnosis); it does not overstate or understate the fix | required |
| PR follows template and standards | The PR description read against `docs/CONTRIBUTING.md` and the repo's PR template | All template sections are filled with real content; AI use is disclosed if repo requires it; no placeholder text left; description is readable (not just a dump of issue numbers) | required |
| Deviation noted if exists | The plan's "Deviations" section (if live mode) | If the diff deviates from the posted plan, the plan.md has been updated with a Deviations section explaining what changed and why; if no deviations, the section says "Nothing changed" | preferred |

## Verdict rule

**Accept if:**
- All 5 required checks pass
- The PR is honest about any deviations from the plan

**Reject if:**
- Any required check fails
- The diff contradicts the plan without being disclosed
- Test evidence is missing or does not prove the fix works
- The PR ignores the template or fails to disclose required information

**Unclear treatment:**
- If a check is unclear (evidence is missing or contradicts), treat it as fail. A PR you cannot verify is not ready to submit.