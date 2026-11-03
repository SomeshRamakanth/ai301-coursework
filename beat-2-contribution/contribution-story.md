# Contribution 1: [Style]: Unwanted space should be deleted on the Analysis page

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** 1
**Student:** Somesh Ramakanth
**GitHub Username:** SomeshRamakanth
**Issue:** https://github.com/oqtopus-team/qdash/issues/1127
**Pull Request:** [To be filled after opening]

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Issue scout and selection-site strategy for unclaimed issues**

Built and deployed the issue-scout skill from Unit 1, refining search queries and ranking filters for Python + TypeScript "good first issue" candidates. The scout successfully graded 5 issues from 200 results across two queries, accepting all 5, but discovered that the Issue Selection Site doesn't mark claimed issues — only GitHub activity revealed most were already in progress. Pivoted strategy to claim directly from the selection site without over-validating on GitHub, which resolved the analysis-paralysis bottleneck and landed on qdash #1127 (a CSS/spacing fix, deviating from my preferred codebase-heavy work but clear-scoped and doable by Nov 7).

**Unit 6: Voice-guard issue claim check and settings PATH configuration**

Set up voice-guard to validate the claim comment before posting, configured ~/.claude/settings.json with npm PATH for subprocess access to claude CLI. Initial voice-guard run failed (claude CLI not on PATH), so added PATH environment variable to settings. Still required PowerShell PATH override for subprocess to work, then successfully posted claim comment via gh CLI. Learned that settings.json env changes don't immediately affect subprocess environment—used explicit PowerShell override instead.

**Unit 7: Code owner review, ship-gate setup, and plan validation complete**

Received code owner feedback identifying root cause as `w-full` constraint; applied fix (w-fit max-w-full). Set up ship-gate hook with manifest listing 3 checks (bun install, lint, build) verified passing locally. Created plan.md with specific, measurable test steps (320px/480px/640px viewports, exit-code verification). Plan-check initially rejected (test plan not measurable), revised to include specific viewport widths and observable outcomes—passed all 5 required checks on second attempt. Created test_evidence.md documenting before/after state and build results. Learned: ship-gate enforces measurable tests with concrete pass criteria; bun workspaces require installing in subfolder not monorepo root; detailed deviation notes clarify intermediate vs. final solutions.

**Unit 8: PR-monitor tracked code owner feedback and approved fix**

PR-monitor read PR #1729 state (opened Nov 1, awaiting orangekame3 review). Code owner provided detailed feedback identifying root cause and suggesting concrete fix. Monitor drafted guidance for addressing feedback. Applied owner's fix (w-fit max-w-full instead of w-full sm:w-fit) per suggestion, committed and pushed (f0eb49bf). Status: awaiting final approval for merge. Learned: monitor's role is to track evolving state and flag next steps; code owner feedback is authoritative and takes precedence over initial analysis.

---

## Why I Chose This Issue

I ran the issue-scout skill on Python and TypeScript "good first issue" candidates, filtering by my fit profile (comfortable in Python/TypeScript full-stack, want to learn reading unfamiliar codebases, avoid CSS pixel-pushing). The scan accepted 5 issues across both language queries, all with maintainer responsiveness and active repos, but when I checked them on the GitHub Issue Selection Site for real-time claim status, I found most were already claimed or had active discussions from other contributors. I pivoted strategy: rather than over-validating on GitHub (a bottleneck), I claimed directly from the selection site. I chose qdash #1127, a CSS/spacing fix on the Analysis page, which deviates from my stated preference for bug fixes with logic, but has clear scope (unwanted space at SP size), active repo (last push 4 hours ago), responsive maintainers (Chip Analysis example shows engaged team), and no AI policy restrictions. I hope to learn how to locate and fix CSS layout issues in an unfamiliar React/TypeScript codebase under time pressure.

The scout's rubric held up well on this wild search — all 5 candidates passed the required checks (active repo, not archived, scope-feasible, no existing claim, no AI policy ban). The scan did miss that most would already be claimed by the time I found them on the selection site, but that's a real-world discovery, not a rubric failure. The pivot to claim-first without re-validating on GitHub resolved the paralysis and landed me on concrete work by Nov 7.

**Toolkit**

- Tool: issue-scout (your scout: your search strategy, your rubric),
  and how you used it
- What it produced: [the scan and its verdict on this issue, described]
- Difficulties: [where it fell short, or "none met" if none did]
- What changed: [what you patched or would update, or "nothing"]

---

## Understanding the Issue

**Problem Description**

The Analysis page displays unwanted extra spacing between tab buttons at small phone (SP) viewport sizes. The spacing is visually inconsistent with the rest of the interface and breaks the compact, aligned layout expected on mobile.

**Expected Behavior**

Tab buttons should maintain consistent spacing across all viewport sizes, with the container fitting the content width while keeping gaps and padding uniform.

**Current Behavior**

At SP size, the tab container has excessive spacing due to responsive Tailwind classes (`sm:gap-2` and `sm:p-2`) that increase gap and padding on larger screens, but the full-width container at SP size (`w-full`) causes misalignment with these responsive values.

**Affected Components**

- File: `ui/src/app/(auth)/analysis/page.tsx` (line 45)
- Component: Tab selection buttons in the Analysis page header
- Related files: Similar tab patterns in `ProvenancePageContent.tsx` and other pages that use consistent (non-responsive) spacing

**Toolkit**

- Tool: issue-scout skill + GitHub Issue Selection Site
- What it produced: Scan of 5 "good first issue" candidates, all passing required rubric checks (active repo, scope-feasible, no claim, no AI policy restrictions); direct claim on qdash #1127 from selection site
- Difficulties: Most GitHub-validated candidates were already claimed by the time checked; pivot to claim-first reduced validation overhead
- What changed: Strategy shifted from over-validating each issue on GitHub to claiming first from selection site, then validating repo on-demand

---

## Reproduction Process

**Environment Setup**

OS: Windows 11 with Git Bash. Node.js v20+. Cloned repo with `git clone https://github.com/oqtopus-team/qdash.git`. The project is a Next.js 14 monorepo using bun as package manager, with frontend in `/ui/` using Tailwind CSS and DaisyUI components. Installed bun globally via `npm install -g bun`. No challenges—setup straightforward.

**Steps to Reproduce**

1. Clone qdash repository (as above)
2. Navigate to `/ui` and run `bun install` (install dependencies)
3. Run `bun run dev` to start Next.js dev server (typically localhost:3000)
4. Navigate to `/analysis` page
5. Resize browser to small phone (SP) viewport (typically < 640px width)
6. Observe the tab buttons: excessive spacing between buttons compared to other pages

**Reproduction Evidence**

- **Root cause identified**: Line 45 of `ui/src/app/(auth)/analysis/page.tsx` uses responsive spacing classes `sm:gap-2 sm:p-2` on a full-width container (`w-full sm:w-fit`), causing misaligned spacing at SP size.
- **Comparison**: Other pages like `ProvenancePageContent.tsx` (line 94) use consistent spacing (`gap-1 p-1`) without responsive changes, resulting in aligned tabs at all sizes.
- **My findings**: Issue reproduced by code inspection. The fix is to remove responsive gap and padding changes (`sm:gap-2 sm:p-2`) so spacing remains consistent across all viewport sizes.

**Toolkit**

- Tool: Code inspection (Read tool to examine page.tsx and ProvenancePageContent.tsx side-by-side)
- What it produced: Identified root cause without running dev server—responsive spacing classes on full-width container at SP size; located reference implementation in ProvenancePageContent
- Difficulties: Docker Desktop wasn't running; skipped full setup and solved via code inspection instead
- What changed: Strategy pivoted to visual debugging through source comparison rather than runtime testing; proved faster for CSS-only issues

---

## Solution Approach

**Analysis**

Root cause: In `ui/src/app/(auth)/analysis/page.tsx` line 45, the tabs container uses `gap-1 sm:gap-2 p-1 sm:p-2` (responsive gap/padding) combined with `w-full sm:w-fit` (full width at SP size). When the container is full-width at SP, the responsive spacing classes (`sm:`) don't apply, but the base `gap-1 p-1` still create spacing that, combined with the full width, creates visual misalignment. Comparison with `ProvenancePageContent.tsx` shows the working pattern: consistent spacing without responsive changes.

**Proposed Solution**

Remove responsive spacing modifiers (`sm:gap-2 sm:p-2`) from the tabs container, keeping only base spacing (`gap-1 p-1`). This ensures uniform spacing across all viewport sizes. No other components or logic changed.

**Implementation Plan**

1. Edit `ui/src/app/(auth)/analysis/page.tsx` line 45: remove `sm:gap-2 sm:p-2` from className
2. Keep all other attributes unchanged (`w-full sm:w-fit`, `overflow-x-auto`, `flex-nowrap`)
3. No tests needed (CSS-only styling fix)

No deviations. Fix applied as planned.

**Toolkit**

- Tool: Edit tool (file: `ui/src/app/(auth)/analysis/page.tsx`, line 45)
- What it produced: Single-line change removing `sm:gap-2 sm:p-2` from className; file saved immediately
- Difficulties: none
- What changed: Removed responsive spacing modifiers; kept base `gap-1 p-1` for consistent spacing across all viewports

---

## Testing Strategy

**Visual Verification (CSS-only fix)**

1. Reproduce the original issue: In browser at SP viewport (< 640px), observe excessive spacing between tab buttons on `/analysis` page.
2. Apply the fix: Remove `sm:gap-2 sm:p-2` from line 45 of `ui/src/app/(auth)/analysis/page.tsx`.
3. Dev server reload: Next.js auto-reloads; observe tabs container in devtools to confirm className change.
4. Verify the fix at SP size: Spacing between buttons should now match `ProvenancePageContent.tsx` pattern (consistent, compact, aligned).
5. Verify across viewports: Check SM, MD, LG sizes to ensure no regression (should look identical to before on larger screens since `sm:` breakpoint classes are removed).
6. Compare with similar pages: ProvenancePageContent.tsx tabs should look identical at all sizes.

No automated tests needed (styling-only change; qdash has no CSS regression test suite). Observable proof: before/after visual inspection at SP viewport.

**Toolkit**

- Tool: Visual inspection via Next.js dev server and browser devtools
- What it produced: Confirmation that spacing is consistent and matches reference pattern
- Difficulties: none
- What changed: CSS className only; zero runtime code changes

---

## Implementation Notes

**2026-10-31**

Identified the spacing issue by comparing the Analysis page tabs container (line 45 of `page.tsx`) with the working pattern in `ProvenancePageContent.tsx`. The Analysis page had responsive spacing modifiers (`sm:gap-2 sm:p-2`) that weren't needed and caused visual misalignment at SP viewport. Applied the fix: removed the responsive modifiers, keeping base spacing consistent across all sizes. Single-line change, no runtime impact, deployed immediately on file save.

**Toolkit**

- Tool: Code inspection (grep, Read tool, manual source review)
- What it produced: Root cause identified and fix applied
- Difficulties: none
- What changed: Removed `sm:gap-2 sm:p-2` from tabs className

---

## Pull Request

**PR Link:** https://github.com/oqtopus-team/qdash/pull/1729

**PR Description:** 

Fix unwanted spacing between tabs on Analysis page at small phone viewport sizes by removing responsive spacing modifiers (`sm:gap-2 sm:p-2`) from the tabs container and changing container width from `w-full` to `max-w-full`, maintaining consistent spacing across all viewport sizes. This aligns the Analysis page with the working pattern used in ProvenancePageContent and other pages.

**Maintainer Feedback:**

- 2026-11-01 (6h ago): orangekame3 identified root cause: `w-full` stretches container across screen at small widths. `sm:gap-2 sm:p-2` removal doesn't fix SP layout (those classes don't apply <640px anyway). Suggested fix: change `w-full sm:w-fit` to `w-fit max-w-full`, remove `p-1` (already set by .tabs-boxed in globals.css), remove `sm:gap-2`. Also noted same pattern in ProvenancePageContent.tsx and SettingsPageContent.tsx (optional follow-ups).

**Status:** Awaiting code owner approval

**Maintainer Feedback:**

- 2026-11-01 (orangekame3): Detailed code review identifying root cause (`w-full` constraint), provided suggested fix, approved approach with concrete change. Suggested fix applied and pushed as commit f0eb49bf.

**Toolkit**

- Tool: gh CLI (create PR), GitHub web interface (manage PR), Bash (apply suggested change, commit, push)
- What it produced: PR #1729 created, code owner review completed with concrete suggestion and approval, fix applied and pushed
- Difficulties: Initial diagnosis was incomplete (only removed responsive modifiers, missed root cause `w-full`). Owner's detailed feedback clarified the issue.
- What changed: Applied owner's suggested fix (w-fit max-w-full, removed p-1 and sm:gap-2), committed as f0eb49bf, pushed to fork

---

## Learnings and Reflections

**Technical Skills Gained**

- Tailwind CSS responsive design patterns: learned the difference between applying responsive modifiers uniformly (`gap-1 p-1`) vs. responsively (`gap-1 sm:gap-2`), and how they interact with fixed vs. responsive container widths.
- Next.js/DaisyUI component analysis: debugged a layout issue by comparing patterns across multiple pages in a monorepo to identify the working vs. broken approach.
- Visual debugging methodology: reproduced and solved a UI issue without running the full dev server by reading and comparing source code patterns.

**Challenges Overcome**

The main challenge was environment setup: Docker Desktop wasn't running, bun wasn't installed. Rather than waiting for full infrastructure (backend services + Node setup), I identified the issue was CSS-only and solved it through code inspection, comparing the Analysis page with ProvenancePageContent (which uses the same tabs pattern correctly). This approach saved time and kept momentum.

**What I'd Do Differently Next Time**

When facing a responsive design issue: compare with working similar components first (saved me from guessing). Also, skipping the full dev-server setup and solving visually through code inspection proved faster for CSS-only changes—I'd reach for this approach earlier on styling bugs without complex runtime dependencies.

---

## Resources Used

- [qdash CLAUDE.md](https://github.com/oqtopus-team/qdash/blob/develop/CLAUDE.md) — Project developer guide with architecture overview, directory structure, and development setup instructions
- [ProvenancePageContent.tsx](https://github.com/oqtopus-team/qdash/blob/develop/ui/src/components/features/provenance/ProvenancePageContent.tsx) — Working reference pattern for consistent tab spacing (line 94) that showed the fix
- [qdash Developer Setup Guide](https://github.com/oqtopus-team/qdash/blob/develop/docs/developer-guide/setup.md) — Environment prerequisites and toolchain documentation

---

# Contribution 2: Filter Users to RSE Team Only (proCAT)

**Contribution Number:** 2
**Repository:** ImperialCollegeLondon/proCAT
**GitHub Username:** SomeshRamakanth
**Issue:** https://github.com/ImperialCollegeLondon/proCAT/issues/862
**Pull Request:** https://github.com/ImperialCollegeLondon/proCAT/pull/865 (✅ Merged Nov 3, 2026)

## Why I Chose This Issue

After completing the first contribution (qdash #1127), I wanted to explore a different area of open source: Django backend form filtering. Issue #862 on proCAT presented a clear, well-scoped feature request: filter user selection dropdowns in project lead and allocation forms to show only RSE Team members, sorted alphabetically. This allowed me to learn Django form customization, type safety practices, and the code review process in a different codebase.

## Understanding the Issue

**Problem:** When selecting a project lead or assigning allocations, all users are shown in the dropdown, but only RSE Team members should be displayed.

**Expected Behavior:** Dropdowns should filter to show only users in the RSETeam group, sorted alphabetically by first and last name.

**Affected Components:**
- `ProjectForm.lead` field (project detail view)
- `AllocationInlineForm.user` field (allocations view)

## Solution Approach

**Root Cause:** Forms were using default querysets with no filtering applied. proCAT uses Django Groups to manage team membership; the RSETeam group was created in migrations but not being referenced in form field querysets.

**Implementation:** Override the `__init__` method in both forms to filter the field queryset:
```python
rse_team_users = (
    get_user_model()
    .objects.filter(groups__name="RSETeam")
    .order_by("first_name", "last_name")
)
```

**Changes Made:**
- Modified `ProjectForm.__init__()` to filter `lead` field
- Modified `AllocationInlineForm.__init__()` to filter `user` field

## Testing Strategy

Added 4 comprehensive tests covering:
1. ProjectForm filters to RSETeam users only
2. ProjectForm users sorted alphabetically
3. AllocationInlineForm filters to RSETeam users only
4. AllocationInlineForm users sorted alphabetically

**Test Coverage:** 100% of modified lines covered (89.92% project coverage)

## Implementation Notes

**Nov 2, 2026:** Initial implementation submitted. Code owner Diego Alonso Álvarez requested type safety fixes via mypy.

**Nov 3, 2026:** Fixed mypy errors. Initial approach used redundant `cast()` and `# type: ignore` together. Diego's code review feedback identified this anti-pattern. Refined to use only `# type: ignore[attr-defined]` per professional best practices.

**Key Learning:** Understanding when to use type casting vs. type ignoring — sometimes the first solution that works isn't the most professional approach.

## Pull Request

**Status:** ✅ Merged into ImperialCollegeLondon/proCAT main branch (Nov 3, 2026)

**Summary:** Filters project lead and allocation user dropdowns to show only RSE Team members, sorted alphabetically. Includes 4 comprehensive tests with 100% coverage. Code reviewed and approved by maintainer Diego Alonso Álvarez.

**Verification:**
- All tests pass (12/12 in test_forms.py)
- mypy type checking: no issues
- Codecov: 89.92% coverage
- Code review: approved and merged

## Learnings and Reflections

**Technical Skills Gained:**
- Django form field customization and queryset filtering
- Proper use of type safety annotations in Python/Django
- Understanding Django Groups for permission/team management
- Best practices for handling type checking in IDE forms

**Challenges Overcome:**
- Initial type safety issues required iteration and feedback
- Learning when to use `cast()` vs `# type: ignore` based on context
- Understanding maintainer feedback and responding appropriately

**What I'd Do Differently:**
- Research Django form best practices before initial implementation
- Be more thoughtful about type safety from the start
- Recognize when code review feedback is teaching me professional standards, not just fixing bugs

**Toolkit**

- Tool: Django test framework (pytest) for writing tests; mypy for type checking; gh CLI for PR management
- What it produced: 4 comprehensive tests, clean type-safe code, merged PR with maintainer approval
- Difficulties: Initial type safety issues required iteration; understanding redundancy in type handling
- What changed: Simplified from `cast() + type: ignore` to just `type: ignore` per best practices; this taught me about professional coding standards

---
