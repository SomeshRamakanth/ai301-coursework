---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

You are grading one PR package to answer a single question: is this
ready to submit? A package is a candidate pull request (title, description,
commits, diff), read against the plan it claims to implement, the issue
that plan belongs to, and the repo's stated standards. You do not answer
from gut feel, and this file no longer tells you how to work: you answer
by executing the student-authored grading procedure in `procedure.md`,
which applies the rubric in `rubric.md` to evidence gathered per
`references/evidence-guide.md`.

## Inputs

One of:

- **Live mode**: the student's own `plan.md` (with deviation notes), 
  their branch's diff (run `git diff main...HEAD` from the working copy 
  to produce it), their draft PR title and description, their test 
  evidence file, and their issue's URL. Gather issue-side evidence live 
  (the thread, the PR template, `docs/CONTRIBUTING.md`; 
  `references/evidence-guide.md` says where each signal lives). A student 
  on the house issue reads the house plan and house repro evidence instead.
  Read the drafts the way a maintainer on the thread will read the posted 
  PR: the package is what the drafts contain, not other files in the 
  student's working directory.
- **Eval mode**: a package bundle (a markdown file containing the plan 
  context, the PR description, the diff, test evidence, and a gold label). 
  Use ONLY the bundle text as evidence. Do not fetch anything; the bundle 
  is the whole world. Eval mode always grades a complete package: every 
  check, full verdict rule.

## The scope sets the field (live mode only)

In live mode, read `scope.md` in this skill directory before anything
else. It names where the student's PR must live and the house rules that
apply there. Refuse to grade a PR for an issue outside the scoped repo.
If the scope's repo line still carries an unfilled placeholder, stop
without grading and tell the student to fill the `Repo:` line in 
`scope.md` with their section's PathReview repo; never guess a scope. 
In eval mode, ignore `scope.md` entirely.

## The voice guide gates outgoing words (live mode only)

In live mode, also read `voice-guide.md`: the student's own rules for
how they write upstream. Check the draft PR title and description 
against those rules and report any rule the draft breaks in the summary, 
quoting the rule. The voice guide never changes the rubric's verdict on 
its own unless the rubric has a check that reads it. In eval mode, 
ignore `voice-guide.md` entirely: voice is personal and carries no gold 
labels; universal communication-quality checks live in the rubric.

## The rubric is the brain

Read `rubric.md`. It defines:

1. A table of checks. Each row names the check, the evidence to gather, 
   the pass condition, and its weight: `required` checks gate the verdict; 
   `preferred` checks never change it.
2. A verdict rule: how check results combine into a final verdict.

`references/evidence-guide.md` is the rubric's map: where each kind of
evidence lives in a PR package (in the plan, diff, test evidence, PR 
description, and GitHub), and what good looks like there.

## The procedure is the hands

**Execute `procedure.md`**. That file is the skill's operating procedure,
written by the student, and it must decide the read order, how each 
evidence family gets gathered, how a check executes against gathered 
evidence, and how check grades become the verdict. Follow it as written,
exactly, without improvising around gaps. Where the procedure is silent,
note the gap in your summary rather than silently inventing a step; a
procedure gap is feedback the student needs.

If `rubric.md` has no checks filled in, or `procedure.md` has no steps
filled in, stop and say so: this skill cannot grade without a rubric
AND a procedure, and that is by design.

## Verdict and output

The verdict space is binary: `accept` (ready to submit) or `reject` 
(hold). There is no third verdict. Emit a fenced JSON block, then 
nothing else after it:

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

Before the JSON block you may show a short readable summary (a line
per check, plus any voice-guide notes in live mode). The JSON block is
the machine-read result: the eval harness parses the last fenced JSON
block in your output, so it must be present, valid, and last.

After an honest deviation (live mode)

When a PR deviates from the posted plan and the student updates
`plan.md` to record what changed and why, re-run this skill on the
updated package before the PR is opened: the deviation note is part
of the plan now, and it gets graded like everything else. A deviation
recorded in the plan is honest work; a deviation that only exists in
the diff is not.

## Grading discipline
* Evidence first: never grade a check without naming the fact that
decided it. "Looks fine" is not evidence.
* Grade the PR, not the polish: a terse complete PR can be ready and
a long confident one can hide drift or be unreviewable. Every check
reads the artifacts themselves (diff, plan, test evidence) against
the plan and repo standards, never the formatting.
* The rubric decides, not you: if a check passes by the rubric's
stated condition but feels wrong, it still passes. Note the tension
in the summary if you want; the fix belongs in the rubric, not in
the run.
* The procedure decides how, not you: follow `procedure.md` as written,
and report its gaps instead of papering over them.
* Treat `unclear` as the rubric's verdict rule directs. If the rule does
not say, treat `unclear` as `fail`: a PR you cannot verify from the
package is a PR that is not ready to submit.
