# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Environment is recorded | The repro report's environment section (or intro paragraph), naming specific versions of the relevant tools/languages/OS and the repo commit/branch | Names at least three of: language/tool version (Python 3.x, ripgrep 15.2.0, etc.), package manager or install method if relevant (conda, cargo install, npm, etc.), OS and architecture or version (Ubuntu 24.04, Arch Linux x86_64, etc.), git commit hash or branch with date. Vague versions like "latest" or "current" fail. | required |
| Steps are complete and followable | The "Steps and observed" section of the repro report, read against the issue's original steps | A stranger with the same environment could run the steps in order and observe the same behavior. No unexplained jumps ("then run the thing"), no assumed knowledge of the repo's setup. If the report references setup docs, it names them; if setup is needed, setup is in the steps. | required |
| Observed output matches the issue | The "Actual:" or final output of the repro report, read against the issue's description of the unwanted behavior | The behavior shown in the report is the specific behavior the issue describes (same error type, same silent failure, same wrong output), not an adjacent or unrelated problem. A "could not reproduce" verdict is a pass if honestly stated; a confident wrong-target is a fail. | required |
| Outcome stated honestly | The full repro report's tone and claims | The report shows what was observed without overconfidence or speculation. Honest "I could not reproduce" or "I see the crash but not the root cause" passes. Confident conclusions beyond what the evidence shows (e.g. "this is definitely a memory leak" without a trace) fail. | required |
| Claim comment respects voice | The candidate claim comment, read against the repo's conventions and `voice-guide.md` | The claim names the issue or its behavior, promises investigation/reproduction (not a fix), and respects the student's own voice-guide rules (no timelines, no bare "me too", no unfounded confidence). | required |
| Claim follows repo's AI policy | The repo-facts block's "contribution policy" line, read against the claim comment | If the repo's policy requires AI disclosure (states "must disclose" or "AI usage must be disclosed"), the claim comment discloses the use. If the policy forbids AI-generated content outright, the claim is rejected (the student should not contribute this way). If the policy is silent or permits with conditions, it passes. | required |

## Verdict rule

Accept if every required check passes. A single required `fail` or `unclear` rejects the package — unclear means the evidence needed is genuinely absent or the package cannot be verified, and a reproduction that cannot be verified is not ready to post. `preferred` checks never affect the verdict; they rank accepted packages only.
