# Procedure: how this skill grades a PR package

## Read order

1. **Read the Plan first** — This establishes what the student promised to do. Read all sections (Diagnosis, Scope, Approach, Files to Change, Test Plan, Deviations if present). Note down: what files will be changed, what the approach is, what test evidence should exist, and any deviations from the original plan.

2. **Read the PR description** — This is what will be posted to GitHub. Note down: whether it explains the fix, whether it references the issue and plan, whether it discloses AI usage if required, and whether it follows the repo's template structure.

3. **Read the Diff** — This is the actual code change. Note down: what files were changed, which lines were modified, whether there are unrelated changes, and whether the commits are clean.

4. **Read the Test Evidence** — This shows whether the fix actually works. Note down: what test case was run, what the output was (before and after), whether the fix passes, and whether any other tests broke.

5. **Read Repo standards** — This provides the expectations. Note down: the PR template structure, AI disclosure requirements (from `docs/CONTRIBUTING.md`), and branch naming conventions.

---

## Evidence gathering

For each check, gather evidence as follows:

### Check 1: Diff bounded by plan
- **Where to pull from:** The plan's "Approach" and "Files to Change" sections, and the actual diff
- **What to record:** (a) The files named in the plan; (b) the files actually changed in the diff; (c) whether all changes align with the stated approach; (d) whether any extra refactoring or unrelated fixes are bundled in
- **Example:** Plan says "Add type guard at line 36 in output_parser.py and update test at line 137". Diff shows exactly those changes and no others = pass. Diff includes "refactor the entire parser" = fail.

### Check 2: Test evidence proves the fix
- **Where to pull from:** The plan's "Test Plan" section and the test evidence file
- **What to record:** (a) What the plan promised to test; (b) what observable outcomes the plan promised (exit code, error message, specific behavior); (c) whether the test evidence shows those outcomes happening; (d) whether the test case from the issue is explicitly shown passing
- **Example:** Plan says "Re-run the failing case, expect no crash and plaintext fallback". Test evidence shows the case now returns gracefully with fallback output = pass.

### Check 3: Commits are clean and related
- **Where to pull from:** The commit messages and commit count in the diff
- **What to record:** (a) Each commit message and whether it's clear/meaningful; (b) whether all commits relate to the issue/plan or if any are cleanup/fixup/temp; (c) whether there are unnecessary intermediate commits; (d) no "WIP", "temp", "fixup", or placeholder messages
- **Example:** Commits say "console: clear recorded output only after save_* writes succeed" and each relates to the fix = pass. One commit says "WIP: temp fix" or is labeled "fixup" = fail.

### Check 4: PR description matches diff
- **Where to pull from:** The PR description and the actual diff
- **What to record:** (a) What the description claims changed; (b) what the diff actually shows; (c) whether the description explains why (links back to diagnosis and issue); (d) whether the description overstates or understates the fix
- **Example:** Description says "Add type guards to handle JSON arrays" and diff shows exactly that = pass. Description says "Rewrote the entire parser" but diff only adds one type guard = fail.

### Check 5: PR follows template and standards
- **Where to pull from:** The PR description, the repo's PR template, and `docs/CONTRIBUTING.md`
- **What to record:** (a) Whether all template sections have real content (not placeholders); (b) whether AI usage is disclosed if the repo requires it (check `docs/CONTRIBUTING.md`); (c) whether the description is readable and complete; (d) whether the branch name follows `fix/<issue>-<slug>` convention
- **Example:** Template has all sections filled, AI disclosure is present if required, branch name is "fix/69-json-array-fix" = pass. Template has "[describe your fix here]" placeholder left = fail.

---

## Check execution

Execute checks in this order (1 → 5):

1. **For each check:** Read the gathered evidence against the pass condition in the rubric
2. **Grade:** Mark as `pass`, `fail`, or `unclear`
3. **Evidence for output:** Note the one-line fact that decided the grade (a quote from the diff, a detail from test evidence, a missing section)
4. **When evidence is absent:** If a check requires evidence that is genuinely not in the package (e.g., no test evidence file), mark as `unclear` and note that evidence is absent
5. **No re-reading needed:** Once you've gathered evidence, each check can be graded from that gathered evidence without re-reading the package

---

## Verdict assembly

After all 5 checks are graded:

1. **Apply the verdict rule:** "Accept if all 5 required checks pass. If any required check fails or is unclear, reject."
2. **If all 5 are pass:** Verdict is `accept`
3. **If any check is fail or unclear:** Verdict is `reject`
4. **Quote the deciding check:** In the output summary, quote the one-line evidence from the first check that was fail or unclear (this is what held the package)

Examples:
- All 5 pass → `accept`
- Check 1 (diff bounded) fails → `reject`; quote: "Diff includes refactoring of entire parser beyond the plan's scope."
- Check 2 (test evidence) is unclear → `reject`; quote: "Test evidence file is missing; cannot verify the fix works."