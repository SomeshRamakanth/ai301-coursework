# Rubric: is this a good first issue?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Repo actively pushed | "last push to any branch" date in the repo-facts block (live: the newest commit date on the repo's front page), plus the author list on the "last 5 default-branch commits" (live: the recent commit list) | Last push to any branch is within 90 days of the bundle's capture date (live: within 90 days of today), AND at least one of the last 5 default-branch commits is authored or merged by a non-bot account (a bot-only merge queue with no human author anywhere in the 5 does not count) | required |
| Repo not archived | "archived:" flag on the repo line (live: the "This repository has been archived" banner on the front page) | `archived: no` | required |
| Issue is one bounded piece of work | The issue body, its labels, and the full comment thread | Fails if any of: (a) the issue's own text either lists multiple separate GitHub issue/PR numbers as sub-items meant to be split across separate contributions, or explicitly invites many different contributors to open independent PRs across open-ended, unrelated parts of the codebase (e.g. "PRs welcome, big and small, anywhere in the codebase") — a single checklist of edits across a handful of named files, meant to land as one PR from one contributor, is NOT this; it is just a multi-step task; (b) 2 or more PRs formally linked to *this issue* (or mentioned in its thread) are closed/unmerged with no PR currently open — an abandoned-attempt pattern; (c) the issue is a bare feature/enhancement request (not a bug fix or a docs/content task) and either no maintainer/collaborator (author_association Owner/Member/Collaborator) has commented in the thread at all, or the body itself names a specific design/product decision still unresolved (e.g. "TBD", "should we...", a spec the opener admits is undecided) that no maintainer has settled; (d) the issue is a pure usage/support question ("how do I get this to work?") rather than a change to ship. Passes only if none apply. | required |
| Nobody is already on it | Assignees and linked-PR state in the repo-facts "this issue:" line (live: the Assignees box and the Development box in the sidebar), plus claim comments in the thread (live: read the comments; not every claim gets formally linked) | Fails if any of: (a) an assignee is set; (b) any PR linked to this issue (formally, or just mentioned in the thread) is currently open; (c) a maintainer/collaborator has responded to a claim comment confirming a specific person is already working it (e.g. an assignment-bot invite still in effect). In live mode against Path Review, apply the house rule in `scope.md`: classmates' claim comments never trigger this check, and finding some is expected. | required |
| AI-contribution policy allows this workflow | The "contribution policy" line under Repo facts, quoting `CONTRIBUTING.md` or a dedicated AI-policy file (live: `CONTRIBUTING.md` in the repo root or `.github/`, and anything it links to) | Fails only on an outright ban stated in plain terms ("we do not accept AI-generated code/documentation"). Conditions (disclosure, human review, personal understanding, testing) are terms to follow, not a ban, and pass. Silence (no CONTRIBUTING.md, or one that says nothing about AI) passes. | required |
| Maintainer responds quickly | "maintainer first-response sample" list in the repo-facts block (live: open 5 recently-updated issues from the Issues tab and check how long the first Owner/Member/Collaborator-badged reply took) | At least one sampled issue shows a first owner/member/collaborator reply within 14 days | preferred |
| Repo has real users | Star count and "latest release" in the repo-facts block (live: the star count on the repo page, and the Releases box in the sidebar) | 500+ stars, OR a release cut within the last 12 months of the capture date (live: within the last 12 months of today) | preferred |

## Verdict rule

Accept only if every `required` check passes. A single required `fail` or
`unclear` rejects the issue — `unclear` is treated as `fail` throughout,
since a first issue whose liveness, scope, claim status, or AI policy
cannot actually be verified from the evidence is not one a newcomer
should take on faith. `preferred` checks never affect the verdict; report
their grades, and use them only to rank the issues this rubric accepts,
most preferred-checks-passed first, ties broken by whichever fits the
student's stated profile in `scope.md` better.
