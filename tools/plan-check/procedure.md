# Procedure: how this skill grades a plan package

<!--
THIS IS THE PART YOU WRITE, and it is a new kind of part. Weeks 1 and
2, SKILL.md carried a numbered workflow and you only wrote judgment
files. This week the workflow is gone from the frame: SKILL.md says
"execute procedure.md", and these are the operating steps you author.
The machinery is in your hands now.

Your operator swap is the design brief. When your executor stalled
because your rubric said WHAT to decide but not HOW to find the
evidence, that was a procedure gap. This file is where those gaps get
closed: a complete procedure lets someone who has never seen a plan
package before (a groupmate, or the skill itself) grade one exactly the
way you would.

Under each stage heading below, write the concrete steps for that
stage. The one-line note under each heading says what a complete
procedure must decide there. Write steps, not intentions: "read the
repro evidence before the plan, and note what behavior it pins down"
is a step; "understand the context" is a wish.
-->

## Read order

1. **Read the Issue section first** — This establishes what the bug is, what the expected behavior is, and what the actual behavior is. Note down: the title/nature of the bug, the observed failure mode, and any explicit environmental constraints (e.g., "Python 3.11/3.12 only").

2. **Read all of Repro evidence next** — This shows the steps that trigger the bug and the control runs that isolate the root cause. Note down: all the commands run, the actual output/error shown, the control runs and their outcomes, and any debug output or logs. This is the ground truth against which the plan's diagnosis will be checked.

3. **Read Thread highlights** — This shows what the maintainer or other contributors have said about the issue. Note down: any explicit direction on what needs fixing (e.g., "the bug is in component X"), any attempted solutions and why they failed, and any constraints on the fix (e.g., "this must not break existing behavior").

4. **Read Repo facts** — This provides context about the repository's policies. Note down: the contribution policy (especially AI disclosure requirements) and any other stated conventions.

5. **Read the entire Candidate plan** — This is what will be graded. Read the Diagnosis, Scope, Files, Approach, and Test plan sections in order. Note the stated root cause, the scope boundaries, the files named, the steps outlined, and the test strategy.

6. **Read the Candidate plan comment** — This is what would be posted to GitHub. Note its tone and whether it references the issue, the repro, the maintainer's direction, and any AI usage disclosure.

---

## Evidence gathering

For each check, gather evidence as follows:

### Check 1: Diagnosis grounded in repro
- **Where to pull from:** The plan's "Diagnosis" section and the "Repro evidence" block
- **What to record:** (a) The plan's stated root cause; (b) all repro steps and their outcomes (including control runs); (c) whether the diagnosis explains all observed behaviors, including why controls succeed or fail
- **Example:** If repro shows "command fails with `-v` but succeeds without `-v`, and `--debug` shows argparse consuming positionals before the item parser runs", the diagnosis must explain why the `-v` flag causes argparse to behave differently AND why controls without `-v` work

### Check 2: Scope is bounded
- **Where to pull from:** The plan's "Scope" section and any "In scope" / "Not in scope" statements
- **What to record:** (a) The statement of what will be changed; (b) the explicit "not in scope" statement (if absent, note that); (c) whether the change is one focused fix or a broader redesign
- **Example:** "In scope: clamp the subtraction with saturating_sub at two sites. Not in scope: redesigning wide-char wrapping" is bounded. "In scope: fix the empty-tar save, upgrade containerd, add a cross-runtime abstraction, modernize the CI matrix" is scope creep.

### Check 3: Stranger can execute it
- **Where to pull from:** The plan's "Files", "Approach", and any explicit steps/changes sections
- **What to record:** (a) The files named (must include test files if tests are planned); (b) the approach described (specific changes, line numbers/function names if helpful, not vague investigations); (c) whether a reader could start implementing without asking for clarification
- **Example:** "Replace line 934's `cursor_max - cursor` with `cursor_max.saturating_sub(cursor)`" is executable. "Investigate the input stack" is not.

### Check 4: Test plan is decisive
- **Where to pull from:** The plan's "Test plan" section
- **What to record:** (a) What will be tested; (b) what observable outcome(s) prove the fix works (must be measurable: exit code, error message presence/absence, timing, output content); (c) whether the test directly targets the issue or only proves the full suite still passes
- **Example:** "Re-run the failing command, expect exit 0; add a regression test for this case" is decisive. "Run the full test suite" is not (proves nothing about this specific fix).

### Check 5: Comment respects thread and conventions
- **Where to pull from:** The "Candidate plan comment", the "Thread highlights", and the "Repo facts" policy section
- **What to record:** (a) Any explicit direction in the thread; (b) whether the comment engages that direction; (c) the repo's AI disclosure policy (from repo-facts); (d) whether the comment discloses AI usage if required
- **Example:** If thread shows "we tried approach X and it didn't work", a good comment engages that ("I verified your finding and am trying approach Y"). If repo policy says "must disclose AI usage", a good comment says "I used Claude to help trace the code".

---

## Check execution

Execute checks in this order (1 → 5):

1. **For each check:** Read the gathered evidence against the pass condition in the rubric
2. **Grade:** Mark as `pass`, `fail`, or `unclear`
3. **Evidence for output:** Note the one-line fact that decided the grade (a quote from the plan, a detail from the repro, a statement of what's missing)
4. **When evidence is absent:** If a check requires evidence that is genuinely not in the package (e.g., no test plan section at all), mark as `unclear` and note that evidence is absent
5. **No re-reading needed:** Once you've gathered evidence, each check can be graded from that gathered evidence without re-reading the package

---

## Verdict assembly

After all 5 checks are graded:

1. **Apply the verdict rule:** "Accept if all 5 required checks pass. A single required check that fails or is unclear rejects the package."
2. **If all 5 are pass:** Verdict is `accept`
3. **If any check is fail or unclear:** Verdict is `reject`
4. **Quote the deciding check:** In the output summary, quote the one-line evidence from the first check that was fail or unclear (this is what held the package)

Examples:
- All 5 pass → `accept`
- Check 1 (diagnosis) is fail → `reject`; quote: "Plan blames the tokenizer; control run (same items, no flag) rules that out."
- Check 2 (scope) is unclear (no "not in scope" statement) → `reject`; quote: "Scope not explicitly bounded; unclear whether work beyond the issue is included."
