# AGENTS.md

## Purpose
Project management source of truth for opencode-agent-link. This repo governs planning, verification, and documentation of work across the codebase.

## Artifact Map
- PRD: `descriptions/_0/prd.md`
- Milestones: `actionable.🟢/milestones/`
- Tasks (active): `actionable.🟢/tasks/main/`
- Tasks (reviewed): `actionable.🟢/tasks/review/`
- Tasks (final): `actionable.🟢/tasks/archive/`
- Tasks (snapshots): `actionable.🟢/tasks/historical/`

## Workflow (Lifecycle)
- New work starts in `tasks/main` (pending).
- Completed work moves to `tasks/review` with proofs, checks, and status update.
- After acceptance, move to `tasks/archive` (final record).
- `tasks/historical` is read-only snapshots (do not edit).

## Breadcrumb Commit Style
Commit messages must capture intent, outcome, proof, and side effects.
Recommended format (multi-line):
- Intent
- Accomplished
- Proof (commands + outputs)
- Hoped / Lacking
- Complexity / Side effects
- Fit / Context
- Worked-by

## Verification Discipline
- Every completed task must include a re-verification command.
- Proof output must be recorded in the task file AND in the commit message.
- Avoid ambiguous checks; prefer deterministic scripts.

## PR / Branching Rules
- Use `gh` for PRs and repo operations.
- One task or cohesive change per branch.
- Merge only after verification artifacts are recorded.

## Scope Boundaries
- PM repo contains planning artifacts only.
- Implementation lives in the code repo: https://github.com/luketych/Dev_Playground--opencode-agent_management--code
