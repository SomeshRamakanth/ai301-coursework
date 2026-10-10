# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

**In eval packages:** 
- The plan-context block's "Approach" and "Files to Change" sections
- The candidate PR's "Description" section
- The unified diff showing what files changed and what lines were modified

**In live mode (your own PR):**
- Your plan.md's "Approach", "Files to Change", and "Deviations" sections (if present)
- Your branch's diff (`git diff main...HEAD`)
- Your draft PR title and description

**What good looks like:**
- Every file changed in the diff is listed in the plan's "Files to Change" section
- Every code change aligns with the plan's "Approach" section
- No extra refactoring or unrelated fixes are bundled into the diff
- If the diff deviates from the plan, the plan.md has a "Deviations" section explaining what changed and why
- The PR description accurately describes what was changed, not more and not less

**What bad looks like:**
- Diff includes files not mentioned in the plan
- Changes go beyond the stated approach (e.g., refactoring an entire module when only one function needed fixing)
- Diff shows the fix but plan says something different (silent drift)
- Deviations from plan exist but are not disclosed in plan.md

## Test evidence (harness category: not-tested)

**In eval packages:**
- The plan-context block's "Test Plan" section
- The candidate PR's "Test Evidence" section (the before/after output)

**In live mode (your own PR):**
- Your plan.md's "Test Plan" section
- Your test_evidence.md file (the actual command output, before and after)

**What good looks like:**
- The test evidence shows the exact observable outcome the plan promised
- The failing case from the issue (or repro steps) is explicitly shown passing after the fix
- Test evidence includes actual output/logs, not just "tests pass"
- All existing tests still pass (no regressions)
- The test plan's promised observable outcome is visible in the evidence (e.g., exit code 0, error message gone, test case passes)

**What bad looks like:**
- Test evidence is missing or incomplete
- Test evidence shows a generic "all tests pass" but doesn't prove the specific fix works
- Plan promises "test case X now passes" but evidence only shows "suite passed"
- No before/after comparison in the evidence

## Diff quality (harness category: unreviewable)

**In eval packages:**
- The candidate PR's unified diff
- The commit list and commit messages

**In live mode (your own PR):**
- Your branch's diff (`git diff main...HEAD`)
- Your commit history (check with `git log main...HEAD --oneline`)

**What good looks like:**
- Every commit message is clear and meaningful (e.g., "console: clear recorded output only after save_* writes succeed" or "fix(output_parser): add type guard for JSON arrays")
- Each commit relates directly to the issue and plan (no cleanup, no refactoring other areas, no "WIP" or "temp" commits)
- The diff is easy to review: the fix is visible, logic is clear
- No debug code, commented-out blocks, or formatting churn
- Commits are atomic (each commit does one logical thing)
- No fixup or intermediate commits like "WIP: trying something"

**What bad looks like:**
- Commit messages are vague ("Update file") or missing
- Multiple unrelated fixes bundled into one PR
- "WIP:", "temp", "fixup", or similar temporary commit messages
- Debug print statements or commented code left in
- Massive formatting changes mixed with the actual fix
- Too many intermediate/fixup commits

## Standards and comms (harness category: standards-wall)

**In eval packages:**
- The repo-facts block's "PR template" sections
- The repo-facts block's "Stated policy" (AI disclosure, contribution guidelines)
- The candidate PR's description (checked against template sections)

**In live mode (your own PR):**
- The repo's PR template (from GitHub when you open the PR draft)
- The repo's docs/CONTRIBUTING.md file
- Your draft PR title and description
- Your branch name (should follow `fix/<issue>-<slug>` convention)

**What good looks like:**
- All PR template sections have real content (no "[describe...]" placeholders)
- AI usage is disclosed if docs/CONTRIBUTING.md requires it (e.g., "I used Claude to help trace the code")
- PR title is clear and follows convention (e.g., "fix(output_parser): handle JSON arrays" not "fixes stuff")
- PR description explains the why (links back to the issue and diagnosis), not just listing what changed
- Branch name follows the format `fix/<issue-number>-<slug>` (e.g., `fix/69-json-array-fix`)
- Description is readable and complete (not a dump of issue numbers)

**What bad looks like:**
- PR template sections left blank or with placeholder text
- AI usage is not disclosed when repo policy requires it
- PR title is vague ("Update", "Changes", "Fixes")
- PR description says "See the diff" instead of explaining the fix
- Branch name doesn't follow convention (e.g., `my-fix` or `work-in-progress`)
- Template sections are filled but with low-effort content