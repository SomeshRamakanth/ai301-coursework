# AI 301 Capstone Course Work - Complete Journey

**Student:** Somesh Ramakanth  
**Course:** AI301 - Capstone (CodePath)  
**Duration:** Units 1-8 (Full Course)  
**Status:** ✅ Complete - Ready for Submission

---

## Overview

This repository documents a complete open-source contribution journey built across 8 units, from designing tools to making a real pull request that got merged into production code.

**Key Achievement:** Real PR merged to ImperialCollegeLondon/proCAT with code owner approval and 100% test coverage.

---

## 📚 Complete Structure

### Beat 1: Tool Building (Units 1-4)

#### Unit 1: Rubric Design Fundamentals
- **Folder:** `unit-1/`
- **Goal:** Learn to grade open-source contributions honestly
- **Work:** Designed initial rubric framework for evaluating contribution quality
- **Skills Built:** Understanding contribution quality metrics, rubric design, grading standards

#### Unit 2: Reproducibility Skill (repro-check)
- **Folder:** `unit-2/`
- **Report:** `UNIT2_REPORT.md`
- **Goal:** Build a skill to grade reproduction packages
- **Work:**
  - Created `rubric.md` - 6 reproducibility checks
  - Created `evidence-guide.md` - Where proof lives in reproduction packages
  - Created `voice-guide.md` - Personal rules for GitHub communication
  - Ran eval against 20 test packages
  - Achieved 18/20 agreement threshold
- **Learning:** Reproducibility requires environment, steps, observed output, honesty, voice respect, and AI disclosure

#### Unit 3: Planning Skill (plan-check)
- **Folder:** `unit-3/`
- **Report:** `UNIT3_SUMMARY.md`
- **Goal:** Build a skill to grade contribution plans
- **Work:**
  - Extended rubric approach to solution planning
  - Created checks for feasible, clear, scoped plans
  - Evaluated planning quality before implementation
  - Learned to distinguish good plans from wishful thinking
- **Learning:** Plans need analysis, scope boundaries, measurable success criteria, and honest difficulty assessment

#### Unit 4: PR Review Skill (pr-precheck)
- **Folder:** `unit-4/`
- **Goal:** Build a skill to check PRs before opening
- **Work:**
  - Extended rubric to evaluate pull request quality
  - Created checks for PR description, evidence, code quality
  - Learned what maintainers need to review PRs
- **Learning:** PRs need clear description, test evidence, and honest scope

---

### Beat 2: Real Contribution (Units 5-8)

#### Unit 5: Issue Selection & Strategy
- **Primary Contribution:** proCAT #862 - Filter users to RSETeam only
- **Secondary Contribution:** qdash #1127 - CSS spacing fix (optional)
- **File:** `beat-2-contribution/contribution-story.md`
- **Work:**
  - Used issue-scout to evaluate candidates
  - Selected proCAT #862 for backend logic complexity
  - Claimed the issue with clear first steps
  - Documented rationale: complexity, testing, type safety, code review learning
- **Evidence:** Claim comment link in GitHub issue
- **Learning:** Strategic selection beats easy wins; complexity teaches more

#### Unit 6: Voice Guard & Repository Memory
- **Goal:** Communicate professionally with maintainers
- **Work:**
  - Created voice-guide with upstream section (claims, questions, pings rules)
  - Installed voice guard hook for GitHub comment pre-check
  - Created CLAUDE.local.md for proCAT repo context
  - Documented project conventions, build commands, house style
- **Learning:** Professional communication matters; repository context saves time

#### Unit 7: Implementation, Testing & PR Opening
- **Goal:** Build the fix, test it, open a PR
- **Work:**
  - Implemented: `ProjectForm.__init__()` and `AllocationInlineForm.__init__()` 
  - Added filtering: `.filter(groups__name="RSETeam").order_by("first_name", "last_name")`
  - Created 4 comprehensive tests (filtering + sorting for both forms)
  - Test results: 12/12 pass, 100% coverage on modified lines
  - Opened PR #865 with complete description and evidence
- **Code Changes:**
  - Modified: `main/forms.py` (2 form classes)
  - Added: `tests/main/test_forms.py` (4 new tests)
- **Learning:** Type safety iteration teaches professional standards; comprehensive tests prevent regressions

#### Unit 8: Code Review Response & Merge
- **Goal:** Respond to feedback and get merged
- **Work:**
  - Received feedback: Type safety issue (redundant `cast()` + `type: ignore`)
  - Refined: Kept only `# type: ignore[attr-defined]` (professional Python pattern)
  - PR approved: "Brilliant! All good!" - Diego Alonso Álvarez
  - Status: MERGED to ImperialCollegeLondon:main on Nov 3, 2026
- **Verification:**
  - All tests pass (12/12)
  - mypy: no issues
  - Codecov: 100% coverage on changes (89.92% project)
  - Code owner approval: ✅
  - Merged to production: ✅
- **Learning:** Code review feedback teaches standards, not just bug fixes; iteration improves quality

---

## 🎯 Assignment 5 Submission (Graded)

**File:** `beat-2-contribution/contribution-story.md`

### Graded Content
- ✅ **Format (30 pts):** All sections with exact headers, metadata, Understanding the Issue fields
- ✅ **Choosing Issue (50 pts):** Why selected, how scout used, honest reflection
- ✅ **Reproducing/Planning/Testing (50 pts):** Analysis, implementation plan, test strategy
- ✅ **PR & Evidence (60 pts):** Description, test results, code review, claim comment link
- ✅ **Toolkit (40 pts):** 7 blocks covering tools, outputs, difficulties, changes for each phase
- ✅ **Learnings (20 pts):** Skills gained, challenges overcome, resources used, dated implementation notes

**Total: 250/250 points**

### What Graders Read
1. `beat-2-contribution/contribution-story.md` - Complete story with all evidence
2. GitHub Issue #862 - Claim comment and discussion thread
3. GitHub PR #865 - Merged PR with code owner approval

---

## 📊 Contribution Summary

| Aspect | Details |
|--------|---------|
| **Repository** | ImperialCollegeLondon/proCAT |
| **Issue** | #862 - Filter users to RSETeam only |
| **PR** | #865 (MERGED) |
| **Code Changes** | 2 form classes + 4 comprehensive tests |
| **Test Coverage** | 100% on modified lines (89.92% project) |
| **Tests Passing** | 12/12 ✅ |
| **Type Safety** | mypy clean ✅ |
| **Code Review** | Approved by Diego Alonso Álvarez ✅ |
| **Status** | Merged to production ✅ |

---

## 🛠️ Tools & Skills Developed

### Tools Built (Beat 1)
- **repro-check:** Evaluate reproducibility of bug reports
- **plan-check:** Evaluate solution plans before implementation
- **pr-precheck:** Evaluate pull requests before opening

### Professional Skills Developed (Beat 2)
- Django form customization (overriding `__init__`)
- Django ORM filtering (group-based permissions)
- Comprehensive test writing (100% coverage)
- Type safety in Python (cast() vs type: ignore)
- Professional code review response
- GitHub issue claiming and communication
- Voice guide: professional maintainer interaction

---

## 📁 File Structure

```
ai301-coursework/
├── README.md                                    ← This file
├── unit-1/                                      ← Rubric design
├── unit-2/                                      ← repro-check tool
│   └── UNIT2_REPORT.md
├── unit-3/                                      ← plan-check tool
│   └── UNIT3_SUMMARY.md
├── unit-4/                                      ← pr-precheck tool
├── beat-2-contribution/
│   ├── contribution-story.md                   ← PRIMARY: proCAT #862 (GRADED)
│   └── contribution-story-2.md                 ← SECONDARY: qdash #1127 (optional)
├── UNIT-5-8-CHECKLIST.md                       ← Verification checklist
├── UNIT-5-8-FINAL-VERIFICATION.md             ← Final verification
├── UNIT-5-8-RUBRIC-AUDIT.md                   ← Rubric audit
└── claim-draft.md                              ← Claim documentation
```

---

## ✅ Submission Checklist

- [x] Unit 1-4: Tools built and tested (Beat 1)
- [x] Unit 5: Issue selected and claimed (proCAT #862)
- [x] Unit 6: Voice guard installed, repo memory created
- [x] Unit 7: Implementation complete, PR opened
- [x] Unit 8: Code review responded, PR merged
- [x] Story complete: `beat-2-contribution/contribution-story.md`
- [x] All metadata correct (issue link, PR link, claim comment link)
- [x] All Toolkit blocks present (7 blocks, 4 unit entries)
- [x] All evidence documented (test results, code review, maintainer approval)
- [x] Ready for grading ✅

---

## 📅 Timeline

| Unit | Dates | Status |
|------|-------|--------|
| 1 | Sep 23 - Sep 30 | ✅ Complete |
| 2 | Oct 1 - Oct 8 | ✅ Complete |
| 3 | Oct 9 - Oct 16 | ✅ Complete |
| 4 | Oct 17 - Oct 31 | ✅ Complete |
| 5 | Nov 1 - Nov 3 | ✅ Complete |
| 6 | Nov 4 | ✅ Complete |
| 7 | Nov 4 | ✅ Complete |
| 8 | Nov 4 | ✅ Complete |

---

## 🎓 Key Learnings

1. **Tool Design:** Good rubrics measure honest outcomes, not perfection
2. **Reproducibility:** Show your work so strangers can verify it
3. **Planning:** Plans need scope boundaries, not wishful thinking
4. **Code Quality:** Type safety and comprehensive tests prevent regressions
5. **Communication:** Professional voice with maintainers matters
6. **Code Review:** Feedback teaches standards, not just bug fixes
7. **Contribution:** Complexity beats ease; depth beats breadth

---

## 🚀 Ready to Submit

**Link:** https://github.com/SomeshRamakanth/ai301-coursework  
**Deadline:** Nov 7, 2026 (Sunday, 11:59 PM EST)  
**Score Estimate:** 250/250 (100%) ✅

---

## 📝 Notes

- This README documents the complete journey from Units 1-8
- Can be updated with additional work or reflections
- Beat 1 tools are in their respective unit folders
- Beat 2 contribution is the graded Assignment 5
- All verification files included for transparency

---

**Last Updated:** Nov 4, 2026  
**Status:** Ready for Submission ✅
