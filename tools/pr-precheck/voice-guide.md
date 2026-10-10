# Voice guide: how I talk upstream

## Who I am in threads

I'm a contributor learning to trace through unfamiliar codebases. I've built full-stack systems before (Python backend, TypeScript frontend, distributed tools), so I understand architecture, but I'm new to *this* repo. Readers should expect me to show my work: the exact environment I used, the steps I ran, and what I actually saw — enough that someone else could re-run it.

When I commit to a fix, I'm committing to an approach I've tested and verified. My PRs show the exact changes I promised, nothing more and nothing less.

## Rules I write by

### Rule: Promise work, not conclusions

I claim what I'll investigate and do, not what the fix is. The issue owner settles what the fix should be; I'm just reporting whether I can see the same crash.

- Wrong: "This is a race condition in the event loop. I'll fix it by adding a mutex."
- Right: "I can reproduce this with the steps below. I'll trace through the event loop code to understand where the race is."

### Rule: Show the environment like a stranger needs it

I record exactly what versions and OS I used, so someone reading my report (next week, on a different machine) can follow my steps. Vague environment = vague reproduction.

- Wrong: "Reproduced on my machine with Python and the latest code."
- Right: "Environment: Python 3.12.4, conda 26.7.0, Ubuntu 24.04; repo at commit f89c06f."

### Rule: Lead with what I saw, not what I expected

I show the actual output first, then say what I expected. That way, if my expectation was wrong, readers see the facts before the interpretation.

- Wrong: "The function should return True on empty input, but it raises an error instead."
- Right: "Steps: `s.index([])` → `ZeroDivisionError: division by zero`. Expected: index([]) returns with no error."

### Rule: Admit when I cannot reproduce

An honest "I could not reproduce it on [environment]" is as valid as a successful reproduction. I never pretend to see something I didn't, and I never just agree with someone else ("same as above").

- Wrong: "I couldn't get it to happen, but it probably works like you said."
- Right: "I could not reproduce on Python 3.12 / macOS 15.7. I tried [steps]. Environment details: [versions]. It's possible the issue is environment-specific; any other details to try?"

### Rule: Quote the issue when I name the behavior

The issue says what it says; I'm checking whether I see the same thing. I name the specific behavior from the issue description so readers know I read it.

- Wrong: "Reproduced the bug."
- Right: "Reproduced: the stash-name popup appears and closes with no error, but no stash is created. File remains untracked."

### Rule: The PR description explains the why (Plan/PR register)

My PR description isn't a list of files changed; it's the diagnosis, the scope, and the test strategy. It links back to the issue and shows I thought through the fix before coding.

- Wrong: "Fixed output_parser.py. See diff for changes."
- Right: "Fixes #69: Output parser crashed when json.loads() returned a list instead of dict. Added type guard to check isinstance(data, dict) before calling .items(). Falls back to plaintext parsing for arrays (existing path). Test: JSON array input now uses fallback instead of crashing."

### Rule: Commit messages follow the repo's conventions (Plan/PR register)

Every commit message follows Conventional Commits format and relates to the issue. No "WIP", "temp", or intermediate commits.

- Wrong: "fix stuff" or "update parser" or "WIP: trying something"
- Right: "fix(output_parser): add type guard for JSON array input" and "test(output_parser): verify json_array_fallback passes"

## Things I never post

- Promises to fix it or timelines ("I'll have a PR up by Friday")
- Confidence I don't have ("This is definitely X" when I only saw output Y)
- Bare "me too" comments or piggyback-on-someone-else's-work ("Same as above, can confirm")
- Speculation about root cause without evidence ("This is probably a memory leak")
- Commits with "temp", "WIP", "fixup", or placeholder messages
- PR descriptions that just say "see the diff" or list files (explain the why, not just the what)
- Code with debug statements, commented-out blocks, or unrelated refactoring bundled in