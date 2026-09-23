# Scope: where to look, and who is looking

<!--
This file is the skill's field of view. The rubric (rubric.md) decides
whether an issue is GOOD; the scope decides which issues are candidates
at all, and whose hands the issue would land in. It applies in live mode
only: in eval mode the bundle is the whole world and this file is
ignored.

Two parts. Staff wrote the first; you write the second.
-->

## Where candidates come from

Only issues in the course's Path Review repository are candidates:

- Repo: `codepath/pathreview-ai301-fa26-s1`

Do not search, fetch, or grade issues from any other repository, however
promising. The wider GitHub comes later in the course; for now the field
is Path Review.

**Path Review house rule.** Path Review is a classroom, and your
classmates are not strangers. Ignore the usual claim signals here: other
students' claim comments (and there may be several on one issue) do not
block an issue, and finding some on the issue you want is normal. Claim
anyway: course credit attaches to the pull request you open, not to
whether it merges, so a shared issue costs nobody anything. Everything
else in the rubric applies as written.

## Your fit profile

<!-- YOU write this part: a few sentences about you. What languages and
tools you have actually used, what you want to get better at, anything
you want to avoid. The skill uses this only to RANK the issues your
rubric accepts, never to change a verdict: fit cannot rescue an issue
your rubric rejects, and cannot sink one it accepts. -->

I've built a full-stack Python + TypeScript project before (FastAPI
backend with SQLAlchemy/Alembic migrations, a React + Vite frontend,
Docker Compose for local services, pytest for tests, pre-commit hooks),
including an LLM/RAG agent system with retrieval, tool orchestration, and
a safety/guardrails layer. I'm comfortable in Python and TypeScript/React,
and with Docker-based dev setups. I'd like to get better at reading
someone else's large, unfamiliar codebase well enough to land a
correctly-scoped change on the first try, rather than only working in
code I designed myself. I'd rather avoid front-end-only CSS/pixel-pushing
issues with no logic to them, and issues in languages I have never
touched (e.g. Rust, Go, C++) for this first contribution — I'd rather
save picking those up for a later, less time-pressured unit.
