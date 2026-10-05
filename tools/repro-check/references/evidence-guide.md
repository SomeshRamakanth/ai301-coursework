# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

**In eval bundles:** the "Environment:" line or opening paragraph of the "Candidate repro report" section.

**Live mode:** the repro draft's environment section, or the issue's own reporter's environment in the issue body.

**What good looks like:** At least three specific details from: tool version (Python 3.12.4, ripgrep 15.2.0), install/package method (conda 26.7.0, cargo install, npm 9.6), OS and architecture or version (Ubuntu 24.04, Arch Linux x86_64, macOS 14.7), and git commit or branch. Examples: "Python 3.12.4, conda 26.7.0, Ubuntu 24.04, repo at commit f89c06f" or "ripgrep 15.2.0 (cargo install), Arch Linux (x86_64)". Vague versions like "latest" or "current" are not sufficient.

---

## Steps

**In eval bundles:** the "Steps and observed:" section of the "Candidate repro report", where the actual commands or UI actions are listed.

**Live mode:** the same in the repro draft, or the issue's original "Steps to reproduce" section.

**What good looks like:** Each step is explicit and standalone. A stranger who has set up the repo knows what to do next without guessing:
```
$ git init -q t && cd t && touch new.txt
$ lazygit   # focus new.txt in Files, press 's', name it "test", Enter
$ git stash list
$ git status --short
```
No "then run the thing" or "compile it as usual" — every step is spelled out. If a build or install step is needed, it appears in the steps.

---

## Behavior shown

**In eval bundles:** the "Expected:" and "Actual:" lines of the repro report, and any output excerpts or logs shown. Read them against the issue's description of the bug (in the "Issue" section or thread).

**Live mode:** the same in the repro draft, compared to the issue's original description.

**What good looks like:** The behavior shown matches the specific issue described. If the issue says "the popup closes with no error but no stash is created," the report shows that exact sequence. If the issue says "the function raises AttributeError," the report shows that error. Differences (e.g. the error message is slightly different, or the issue is environment-specific) are called out honestly.

---

## Honesty

**In eval bundles:** the full "Candidate repro report" section, especially the conclusion and tone. Look at whether the report claims only what its evidence shows.

**Live mode:** the repro draft's tone and final statements.

**What good looks like:** The report shows what was observed, without reaching beyond it. "Reproduced: [exact behavior]. Environment: [versions]." Or: "Could not reproduce on [environment]. Tried [steps]. It may be environment-specific — any details to try?" An honest "I could not reproduce it" is a pass if evidenced well.

**What fails:** "This is obviously a memory leak caused by [mechanism without proof]," or "Reproduced, I'll fix it by [solution]" when claiming, not yet fixing. Confident conclusions beyond what the evidence supports.

---

## Comms

**In eval bundles:** the "Candidate claim comment" section, read against the repo's stated contribution and AI policy expectations (in the "Repo facts" section, the "Contribution policy" line).

**Live mode:** the draft claim comment, checked against the student's own `voice-guide.md` rules, and the repo's CONTRIBUTING.md, AI_POLICY.md, or PR/issue templates.

**What good looks like for repo AI policy:** 
- If the repo's policy says "AI use must be disclosed" or similar: the claim comment names the AI tool used and the extent of assistance (e.g., "Reproduced with Claude's help (used Claude Code to set up the environment and run the steps)").
- If the policy forbids AI-generated content outright ("no AI-generated code"), the claim is a reject — the student should not contribute this way.
- If the policy is silent or permits AI with conditions (e.g., "human in the loop" with no explicit disclosure), it passes.

**What good looks like overall:** The claim is specific to the issue (names the issue's behavior, not generic), promises investigation or reproduction (not a fix), respects the student's own voice rules (no unfounded confidence, no timelines, no bare "me too"), and follows the repo's stated conventions (discloses AI use if required, uses templates if provided).

Example from a good claim in a disclosure-required repo: "I'd like to reproduce this stash UX issue. Reproduced on [environment] using Claude to assist with setup (report below). Plan: trace the stash-name prompt logic."

Example from a bad claim: "Same as above, can confirm" (bare piggyback) or "I'll fix this race condition by adding a mutex" (promising a fix, not a repro) or in a disclosure-required repo: a claim that doesn't mention AI use at all.
