# AI 301 Unit 3: Plan-Check Skill - Summary

## Status: ✅ COMPLETE

**Eval Results:** 19/20 agreement (PASS - goal was 18/20)
**All 5 category floors met**

---

## What Was Built

A grading skill (`plan-check`) that evaluates implementation plans for open-source issues.

### Skill Components

1. **rubric.md** — 5 required checks:
   - Diagnosis grounded in repro evidence
   - Scope is bounded
   - Stranger can execute it
   - Test plan is decisive
   - Comment respects thread and conventions

2. **evidence-guide.md** — Detailed guidance on where to find evidence for each check

3. **procedure.md** — Step-by-step workflow for executing the rubric consistently

4. **voice-guide.md** — Carries forward from Unit 2 (personal communication rules)

### Installation
- Copied to `~/.claude/skills/plan-check/`
- Ready for live grading of real issues

---

## Eval Results Breakdown

### Overall Performance
- **Scored items:** 20 packages
- **Agreement:** 19/20 (95%)
- **Pass bar:** 18/20
- **Status:** ✅ PASS

### Category Floors (All Met)
| Category | Result | Performance |
|----------|--------|-------------|
| clear-accept | 6/7 | 86% |
| scope-creep | 4/4 | 100% |
| thread-convention | 2/2 | 100% |
| unbuildable | 3/3 | 100% |
| wrong-cause | 4/4 | 100% |

### Single Disagreement
**pkg-14** (zellij-org/zellij#5174)
- Gold verdict: ACCEPT
- Your verdict: REJECT
- Failed check: "Stranger can execute it"
- Analysis: Gold label itself notes "arguable on deferral"; plan was scoped-down with acknowledged limitations. Check was slightly strict on this edge case.

---

## Key Design Decisions

### Check Philosophy
All 5 checks are **required** because they represent distinct failure modes:
1. **Diagnosis** — Prevents wrong root cause identification
2. **Scope** — Prevents scope creep and feature bloat
3. **Executability** — Prevents vague/incomplete plans
4. **Test plan** — Prevents untestable fixes
5. **Thread/conventions** — Respects community norms and policies

### Evidence Grounding
Every check is evidence-based:
- Diagnosis grounded in repro evidence (including control runs)
- Scope verified against explicit scope statements
- Executability checked against named files and approaches
- Test plan must name observable outcomes
- Communication checked against thread history and repo policy

### Failure Categories Caught
The skill successfully catches all 5 gold-label failure modes:
- ✓ Wrong cause (diagnoses contradicting evidence)
- ✓ Scope creep (designs over fixes)
- ✓ Unbuildable plans (vague or unexecutable)
- ✓ Weak test plans (unobservable or absent)
- ✓ Thread/convention violations (ignored maintainer direction, missing AI disclosure)

---

## Lessons Learned

1. **Grounding matters** — Plans must be traced back to specific evidence, not rely on diagnosis confidence
2. **Scope statements are critical** — Explicit "not in scope" statements help distinguish bounded fixes from scope creep
3. **Observable outcomes** — Test plans must name concrete, measurable results (exit code changes, output differences, timing improvements)
4. **Thread awareness** — Maintainers often provide hints about the real culprit; good plans engage those hints
5. **Borderline cases exist** — pkg-14 shows that "ready to post" can be subjective; the rubric caught a real issue even though gold says it's acceptable

---

## Files & Locations

| File | Location | Purpose |
|------|----------|---------|
| rubric.md | ~/.claude/skills/plan-check/ | 5 required checks |
| evidence-guide.md | ~/.claude/skills/plan-check/references/ | Evidence mapping |
| procedure.md | ~/.claude/skills/plan-check/ | Grading workflow |
| run_eval.py | ai301-unit3-starter/eval/ | Fixed for Windows PATH |

---

## Next Steps

### Ready for Live Mode
The skill is ready to grade real plans from GitHub issues:
- Apply to issue #69 (PathReview output parser JSON array fix)
- Create a plan, post to GitHub, grade with skill
- Refine if needed based on feedback

### Optional Refinement
- Test calibration packages (4 class activity packages)
- Loosen "executability" check slightly if targeting 20/20 (pkg-14 edge case)
- But: 19/20 is solid; moving forward is also valid choice

---

## Comparison: Unit 2 vs Unit 3

| Aspect | Unit 2 (repro-check) | Unit 3 (plan-check) |
|--------|-----|-----|
| What it grades | Bug reproductions | Fix plans |
| Gold packages | 20 | 20 |
| First eval | 20/20 ✓ | 19/20 ✓ |
| Checks | 6 checks | 5 checks |
| Failure modes | Vague reproduction | Wrong/vague fixes |
| Key evidence | Repro steps + control runs | Diagnosis + scope + approach |

Both skills are calibrated and ready for live use.

---

**Unit 3 Complete** ✅

Ready to apply the skill to real issues and open pull requests!
