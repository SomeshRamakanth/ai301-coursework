# Rubric: is this plan ready to post and build from?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here (via your procedure.md). It ships empty on
purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the plan's scope statement, the test plan read against
     the repro evidence's steps, the plan comment read against the
     thread highlights, the repo-facts block) or a location from your
     references/evidence-guide.md. "The plan" is not a source; "the
     plan's stated cause read against what the repro evidence shows"
     is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (is
     this one bounded change? could a stranger start executing it?),
     never the write-up's shape (how many sections it has, how long it
     is, whether it uses headings). Structure-shaped checks are what
     make graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad plans posted. The lecture named the
failure families: the diagnosis ignores or contradicts the reproduced
evidence, the change is unbounded (scope creep), the plan targets the
symptom while the evidence points at the cause, a stranger could not
start executing it, the test plan proves nothing observable, the
unknowns are dressed up as certainty, and the comment ignores what the
thread or the repo's stated conventions ask. A rubric that ignores a
family will fail eval packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Diagnosis grounded in repro | Plan's stated cause, read against all repro steps (including control runs) and thread evidence | Plan's diagnosis is consistent with what the repro evidence shows. Diagnosis must explain the observed behavior AND why control runs differ (e.g., why removing a flag fixes it). Contradicting or ignoring evidence (like blaming a tokenizer when control run proves the tokenizer works) is a fail. | required |
| Scope is bounded | Plan's stated scope section and "in scope" / "not in scope" statements | Change is one focused fix to address the issue's root cause, not a broader redesign. Must have explicit "not in scope" statement. Scope creep includes: drive-by refactors, migrations, or bundling the fix inside a redesign (rebuilding subsystems, modularizing, framework upgrades). | required |
| Stranger can execute it | Plan's files section, approach section, and explicit steps or changes | A reader with access to the repo could start executing the steps without guessing. Files are named (including test files). Approach describes the specific changes, not just "investigate" or "fix". Code locations are identified if needed (line numbers, function names, or clear context). | required |
| Test plan is decisive | Plan's test plan section, read against the repro evidence | Test plan names one or more observable outcomes that prove the fix works (e.g., "re-run repro, expect exit 0", "timing drops from 26s to 1s", "error message changes"). Vague tests fail (e.g., "run full test suite", "should feel fast", "nothing else should break"). Test must be runnable on the target environment and must demonstrate the fix. | required |
| Comment respects thread and conventions | Plan comment read against thread highlights and repo-facts policy section | If thread contains explicit maintainer direction (e.g., "fix in component X", "we tried Y"), comment engages that direction (accepts it, declines with reasons, or proposes alternative). If repo policy requires AI disclosure, comment discloses AI use. Does not ignore maintainer guidance or stated repo conventions. | required |

## Verdict rule

Accept if all 5 required checks pass. A single required check that fails or is unclear (evidence genuinely absent) rejects the package. Unclear counts as fail.
