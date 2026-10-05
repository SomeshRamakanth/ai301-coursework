# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/69

**Verdict output**

```
I'll load the issue-select skill.

● Skill(issue-select)
Successfully loaded skill

I'll read the skill's scope, rubric, and evidence guide first.

  Read 3 files, ran 1 shell command

Scope confirmed: all three are in codepath/pathreview-ai301-fa26-s1. Gathering evidence.

  Ran 4 shell commands

No gh available — using the public GitHub API via curl.

  Ran 11 shell commands

All three are in codepath/pathreview-ai301-fa26-s1, so all are in scope. Graded independently against rubric.md; the Path Review house rule applies (classmates' claim comments don't block).

Shared repo-level evidence (same repo for all three): last push 2026-09-16 (7 days ago), last 5 default-branch commits all authored by Aburke225 / Andrew Burke, a human Collaborator; archived: false; 2 stars, no releases; no Owner/Member/Collaborator reply in any of 5 sampled issues (#72, #63, #62, #70, #68); no CONTRIBUTING.md at root — docs/CONTRIBUTING.md and the PR template say nothing about AI, and there's no AI_POLICY.md/AGENTS.md, so the policy is silent.

All three: accept — every required check passes. All three also fail both preferred checks (no sampled maintainer reply; 2 stars and no releases), so preferred checks can't separate them and ranking falls to the fit profile.

One thing worth naming on the claim check: #69 and #72 carry cross-references from open/closed PRs, but both are classmates' coursework write-up PRs in their own repos (e.g. charancherry0/ai301-coursework#1 changes only tools/issue-select/* and beat-1-sandbox/* — no PathReview code). They aren't formally linked in the Development box, aren't mentioned in the thread, and aren't fix attempts. The only PR in PathReview itself is #74, against issue #60. So nothing is actually being worked in-repo on any of the three.

Ranked (fit order):

1. #69 — output parser crashes on a top-level JSON array. Pure Python in rag/generator/, and parsing/normalizing structured LLM output is the closest match to the RAG + tool-orchestration system you've built. It's also the most logic-bearing of the three: you have to decide how an array maps into the parser's normalized shape, not just add a guard — which is exactly the "read unfamiliar code well enough to scope the change right" practice you asked for. Two named files, an xfail test (H-02) to flip, 2–4h.
2. #68 — ZeroDivisionError on empty BM25 index. Same repo area (rag/retriever/), squarely in your retrieval experience, but the fix is an early-return guard mirroring the one search() already has — less to reason about than #69.
3. #72 — verify_password doesn't fail closed. Still Python and still fail-closed security thinking, but it sits in core/security.py (auth), furthest from your RAG/agent work, and at 1–2h with a try/except around one passlib call it gives the least practice at scoping in unfamiliar code.

[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/69",
    "checks": [
      {"name": "Repo actively pushed", "grade": "pass", "evidence": "pushed_at 2026-09-16 (7 days before today); last 5 default-branch commits all authored by human Collaborator Aburke225 (Andrew Burke)"},
      {"name": "Repo not archived", "grade": "pass", "evidence": "repo API reports archived: False, disabled: False"},
      {"name": "Issue is one bounded piece of work", "grade": "pass", "evidence": "Single bug with two named files (rag/generator/output_parser.py, tests/unit/test_output_parser.py) and one xfail marker (H-02) to remove; no sub-issue list, no closed/unmerged fix PRs, not a feature request or support question"},
      {"name": "Nobody is already on it", "grade": "pass", "evidence": "assignees: []; no PR in this repo references it (only open PR #74 -> issue #60); the open cross-referenced PR charancherry0/ai301-coursework#1 changes only tools/issue-select/* and beat-1-sandbox/* in a classmate's own repo, and jacho15's claim comment is a classmate's (house rule)"},
      {"name": "AI-contribution policy allows this workflow", "grade": "pass", "evidence": "docs/CONTRIBUTING.md contains no AI/generated/assistant mention, no AI_POLICY.md or AGENTS.md exists, and .github/PULL_REQUEST_TEMPLATE.md has no AI disclosure — silence"},
      {"name": "Maintainer responds quickly", "grade": "fail", "evidence": "0 of 5 sampled recently-updated issues (#72, #63, #62, #70, #68) have any OWNER/MEMBER/COLLABORATOR comment; all comments are author_association NONE"},
      {"name": "Repo has real users", "grade": "fail", "evidence": "stargazers_count: 2 and the releases endpoint returns none"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/68",
    "checks": [
      {"name": "Repo actively pushed", "grade": "pass", "evidence": "pushed_at 2026-09-16 (7 days before today); last 5 default-branch commits all authored by human Collaborator Aburke225 (Andrew Burke)"},
      {"name": "Repo not archived", "grade": "pass", "evidence": "repo API reports archived: False, disabled: False"},
      {"name": "Issue is one bounded piece of work", "grade": "pass", "evidence": "Single bug with two named files (rag/retriever/keyword_search.py, tests/unit/test_keyword_search.py) and one xfail marker (H-01) to remove; no closed/unmerged fix PRs, not a feature request or support question"},
      {"name": "Nobody is already on it", "grade": "pass", "evidence": "assignees: []; timeline has no linked PR, only two commit references from yulijasso/ai301-coursework; yulijasso's claim comment is a classmate's (house rule) and no maintainer confirmed anyone"},
      {"name": "AI-contribution policy allows this workflow", "grade": "pass", "evidence": "docs/CONTRIBUTING.md contains no AI/generated/assistant mention, no AI_POLICY.md or AGENTS.md exists, and .github/PULL_REQUEST_TEMPLATE.md has no AI disclosure — silence"},
      {"name": "Maintainer responds quickly", "grade": "fail", "evidence": "0 of 5 sampled recently-updated issues (#72, #63, #62, #70, #68) have any OWNER/MEMBER/COLLABORATOR comment; all comments are author_association NONE"},
      {"name": "Repo has real users", "grade": "fail", "evidence": "stargazers_count: 2 and the releases endpoint returns none"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72",
    "checks": [
      {"name": "Repo actively pushed", "grade": "pass", "evidence": "pushed_at 2026-09-16 (7 days before today); last 5 default-branch commits all authored by human Collaborator Aburke225 (Andrew Burke)"},
      {"name": "Repo not archived", "grade": "pass", "evidence": "repo disabled: False"},
      {"name": "Issue is one bounded piece of work", "grade": "pass", "evidence": "Single bug with two named files (core/security.py, tests/unit/test_security.py) and one xfail marker (H-05) to remove; the single closed cross-referenced PR (foojanbabaeeian/ai301-coursework-Fozhan#1) is a classmate's write-up, not a fix attempt, so the 2+ abandoned-PR pattern does not apply"},
      {"name": "Nobody is already on it", "grade": "pass", "evidence": "assignees: []; no open PR linked to it in this repo and the cross-referenced PR is closed and in a classmate's own repo; claim comments from mikeng07 and DilanCaro are classmates' (house rule) and no maintainer responded confirming either"},
      {"name": "AI-contribution policy allows this workflow", "grade": "pass", "evidence": "docs/CONTRIBUTING.md contains no AI/generated/assistant mention, no AI_POLICY.md or AGENTS.md exists, and .github/PULL_REQUEST_TEMPLATE.md has no AI disclosure — silence"},
      {"name": "Maintainer responds quickly", "grade": "fail", "evidence": "0 of 5 sampled recently-updated issues (#72, #63, #62, #70, #68) have any OWNER/MEMBER/COLLABORATOR comment; all four comments on #72 are author_association NONE"},
      {"name": "Repo has real users", "grade": "fail", "evidence": "stargazers_count: 2 and the releases endpoint returns none"}
    ],
    "verdict": "accept"
  }
]
```

---

## Eval iterations

**Run history**

1. `--limit 3` smoke run (before fixing two Windows-only bugs in `run_eval.py`: a `claude.cmd` PATH-resolution issue, and a `cp1252` stdin-encoding crash on non-ASCII characters in the bundle text) — 2 of 3 items (`issue-02`, `issue-03`) errored on the encoding bug before grading even happened; the one that completed, `issue-01`, disagreed (rubric: reject, gold: accept). Agreement: 0/1 scored items (partial, and not a real read on the rubric — two of the three never got graded at all).
2. `--only issue-01`, after tightening the "Issue is one bounded piece of work" check's umbrella clause (below). Agreement: 1/1 scored items.
3. `--only issue-02,issue-03,issue-05,issue-08,issue-09,issue-12,issue-14,issue-15,issue-20` (one issue from each of the five categories, plus the two I judged riskiest by hand before running anything). Agreement: 9/9 scored items.
4. Full run, `--save-run eval-run.txt`. Agreement: 20/20 scored items (bar: 18/20: PASS). This is the run committed as `eval-run.txt`.

**Issue analysis**

`issue-01` (conda/conda#16475, category `clear-accept`). My rubric's verdict: accept. Gold label: accept. Both agree, but this is the issue that actually broke my rubric on the very first real run (see Run history #1): my "Issue is one bounded piece of work" check originally rejected it, reading its multi-step docs plan (a new task page, plus edits to three existing pages, plus an optional troubleshooting entry) as an "umbrella issue with sub-items to split up" — the same shape my check is supposed to catch in `issue-05` and `issue-10`. The actual difference is that `issue-01` names a handful of specific files for one contributor to edit in one PR, while a real umbrella (like `issue-05`'s "PRs welcome, big and small... anywhere in the codebase") either lists separate GitHub issue/PR numbers as sub-items or explicitly invites many different people to split the work. I rewrote the check's first sub-condition to say this directly, re-ran just `issue-01`, and it flipped to accept — matching gold.

**Check rationale**

From `rubric.md`, the "Issue is one bounded piece of work" row, condition (a) as currently written: *"the issue's own text either lists multiple separate GitHub issue/PR numbers as sub-items meant to be split across separate contributions, or explicitly invites many different contributors to open independent PRs across open-ended, unrelated parts of the codebase (e.g. 'PRs welcome, big and small, anywhere in the codebase') — a single checklist of edits across a handful of named files, meant to land as one PR from one contributor, is NOT this; it is just a multi-step task."*

It's worded this way because "the issue lists several things to do" is not, by itself, evidence of an unbounded scope — plenty of legitimate first issues (docs cleanups especially) name several files or steps but are still one person's one PR. What actually marks an umbrella is who the work is meant to be split across: a tracking issue names separate sub-issues/PRs for separate contributors, or a maintainer explicitly invites indefinitely many independent submissions. Before I added the carve-out, my check conflated "has multiple steps" with "is unbounded," which is exactly what made it misread `issue-01`.

**Trade-offs**

A different clause on the same check — (b), "2 or more PRs formally linked to this issue (or mentioned in its thread) are closed/unmerged with no PR currently open" — sets its threshold at 2, not 1, and `issue-09` (conda/conda#7617, gold: accept) is the canary that shows why: it has exactly one closed linked PR (conda/conda#11627), and the issue itself is fine. If I'd written the condition as "1 or more closed PR fails," `issue-09` would have been wrongly rejected. Two or more closed attempts at the same fix is a real pattern (people keep trying and stalling); one closed PR is unremarkable — someone could have gone inactive for any reason unrelated to the issue's difficulty.

What this costs: my check can't tell "one abandoned PR that reveals real hidden difficulty" apart from "one abandoned PR that means nothing," because it only counts closed PRs, and never reads why the closed one stalled. A first issue where one serious, well-informed contributor already tried and gave up for a real technical reason will still read as `accept` under my rubric, identically to one nobody has ever attempted — a newcomer could walk into more difficulty than the verdict suggests. I accept that miss rather than lower the threshold to 1, because `issue-09` shows the false-reject cost of doing that is worse and more common in the eval set than this specific false-negative.

---

## Selection rationale

**Selection rationale**

1. **Fit and time.** `#69` is Python, in `rag/generator/`, in the same architecture (FastAPI + RAG + agent orchestration) I built for the previous course's PathReview project, so I'm not starting cold on the domain. Its stated estimate (2–4h) is realistic for a first issue alongside everything else due this unit.
2. **What the verdict caught vs. what I weighed myself.** The rubric correctly cleared liveness, scope, claim status, and AI policy on all three candidates — and correctly flagged that neither preferred check (maintainer response speed, star count/releases) could separate them, since this is a small class repo with no outside users and a maintainer who doesn't reply on a sample of issues. What the rubric can't measure is how much actual unfamiliar-code reasoning each fix demands: `#68`'s fix is a guard clause that mirrors code `search()` already has; `#69` requires deciding how a JSON array should map into the parser's existing normalized output shape, which is a real (if small) design decision. That gap — between "passes every check" and "is the one that will actually teach me to read someone else's code" — is exactly what the fit profile exists to catch, and it's on me, not the rubric, to have weighed it.
3. **Anticipated difficulty in claiming it.** A classmate (`jacho15`) already has a claim comment and a full reproduction on `#69`. Under the Path Review house rule this doesn't block me, and course credit attaches to my own PR regardless of whether either of ours merges — but it does mean my Unit 2 claim comment should acknowledge the existing thread rather than read like the first comment on it, and there's a real chance they open a PR first.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
