# Evidence guide: where evidence lives in a plan package

<!--
THIS IS THE PART YOU WRITE (second week running: the judgment files
stay in your hands). The skill uses this guide as its map: for every
kind of evidence a rubric check names, this file says WHERE to find it
in a plan package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repro-evidence block,
  the candidate plan's scope statement or test plan, the plan comment,
  the repo-facts block). In live mode (where on GitHub or in the
  draft: the issue thread, the student's posted repro comment, the
  repo's docs, the draft plan and comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the stated cause cites behavior the
  repro evidence actually shows") over adjectives ("diagnosis is
  solid").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute, and this week that cuts twice: your
procedure.md tells the skill WHEN to gather each family, and this
guide tells it WHERE. Write the map you wish your executor had.
-->

## Diagnosis and grounding

**In eval bundles:** the plan's "Diagnosis" section, read against all the repro evidence (Issue description, "Repro evidence" block, all steps, control runs, `--debug` output or test cases showing the actual vs. expected behavior).

**In live mode:** the plan's stated diagnosis, read against the student's posted repro comment on the issue thread.

**What good looks like:** The diagnosis explains all observed behaviors, including why control runs succeed or fail. If the repro shows a control run (e.g., "without the flag, it works"), the diagnosis must explain why the flag causes the problem. If `--debug` or logs show something different than the surface error, diagnosis targets what the logs show, not the surface symptom. Diagnosis contradicts evidence when it blames component A (when A works in the control) or ignores what the evidence pins down (e.g., repro shows "error at line 934" but diagnosis doesn't mention that line). Example bad diagnosis: blaming a tokenizer when the control run (same items, no flag) parses fine.

---

## Scope

**In eval bundles:** the plan's "Scope" section or any "In scope" / "Not in scope" statements.

**In live mode:** the draft plan's scope statement.

**What good looks like:** Plan states what it will change and what it will not. Bounded change targets the root cause pinpointed by the repro: one component, one subsystem, one localized fix. Examples of bounded scope: "saturating_sub at two sites in printer.rs", "rewrite the tokenizer's separator matching", "add retry logic to the cache handler". Scope creep bundling: the fix is part of a redesign (refactoring the entire printer, rewriting the parser, migrating a framework). A good "not in scope" statement names something related but intentionally deferred: "Not in scope: redesigning wide-char wrapping at tiny widths" (the fix removes the abort, visual result still imperfect, redesign deferred).

---

## Executability

**In eval bundles:** the plan's "Files", "Approach", or explicit steps/changes section.

**In live mode:** the draft plan's approach and file list.

**What good looks like:** A reader with repo access could start executing without asking for clarification. Files are named (e.g., `src/printer.rs`, `tests/test_cli.py`, not "the printer module"). Approach names the specific changes (e.g., "replace line 934's `cursor_max - cursor` with `cursor_max.saturating_sub(cursor)`", not "fix the underflow"). If changes span multiple files, the order or dependency is clear. Vague executability fails: "investigate the input stack" (no chosen layer), "fix the cache freshness check" (no file named), "profile and optimize" (no approach or chosen optimization).

---

## Test plan

**In eval bundles:** the plan's "Test plan" section, correlated against the repro evidence's steps and observable artifacts.

**In live mode:** the draft plan's test plan section.

**What good looks like:** Test plan names one or more observable outcomes that prove the fix works. Observable outcome: something you can run and see (exit code changes, output appears, error message changes, timing improves measurably). Test plan should re-run the original failing case and show it now succeeds (or succeeds in the specific way the fix enables). Example good test plan: "Re-run issue's test case 1 on Python 3.11: after tokenizer fix, request prints with `header1: xyz`, exit 0. Run tokenizer unit tests on 3.11, 3.12, and 3.13." Example bad test plan: "Run the full test suite" (no specific observable outcome for this fix), "should feel fast" (not measurable), "nothing else should break" (proves nothing about the fix itself).

---

## Honesty

**In eval bundles:** the plan's "Approach", "Scope", and "Test plan" sections, looking for acknowledged risks, unknowns, or deferred work.

**In live mode:** the draft plan, especially any caveats or limitations stated.

**What good looks like:** Unknowns are named and owned ("this fix assumes X; if X turns out wrong, the approach needs adjustment"). Deferred work is stated with reasons ("Not in scope: full redesign of wide-char handling; this fix removes the abort and makes room for a later redesign"). Honest risk: "I will grep printer.rs for bare `-` on cursor variables and note anything suspicious in the PR rather than fixing beyond this issue." False confidence: stating something as certain when the evidence shows it's an unknown, or claiming a broader fix than the evidence supports (e.g., "this fixes all underflow issues" when you've only addressed two sites).

---

## Comms

**In eval bundles:** the plan comment (the "Candidate plan comment" section), read against the "Thread highlights" section and the "Repo facts" section (especially the contribution policy and AI-use disclosure requirements).

**In live mode:** the draft plan comment, read against the live issue thread and the repo's CONTRIBUTING.md, AI_POLICY.md, or stated policies.

**What good looks like:** If the thread contains explicit direction from the maintainer (e.g., "the bug is in component X", "we tried approach Y and it didn't work"), the comment either engages that direction ("I've adopted your diagnosis and I'm proceeding with approach X") or explains why it's being set aside ("I initially thought X was the cause, but the control run in step 2 rules that out"). If the repo's stated policy requires disclosing AI usage, the comment includes that disclosure (e.g., "I used Claude to help outline the fix"). The comment names the issue or its specific behavior, showing the author read it, and promises investigation or reproduction ("I plan to trace the code") rather than prescribing the exact fix. Example good comms: "I traced the issue to component X, which the thread identified as the culprit. Plan to add the check at [location]; see test plan below." Example bad comms: ignores maintainer's stated preferred approach, omits required AI disclosure, or makes confident fix promises beyond what the evidence supports.
