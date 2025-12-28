# AGENTS.md

## Scope
This file defines everything needed to complete **Task 1-1-1: Initialize NPM Package and ESM Configuration**. It is intentionally limited to that task only and should not include work from later tasks or milestones.

## Task Reference
- Task file: `actionable.🟢/tasks/1-1-1_npm_init.md`
- Milestone file: `actionable.🟢/milestones/m1_scaffolding.md`
- PRD: `descriptions/_0/prd.md`

## Goal
Create or update the root `package.json` so this repo is a valid **Node.js ESM** project for the `opencode-agent-link` CLI.

## Requirements (Source of Truth)
From Task 1-1-1 and PRD:
- Project must be **ESM** (set `"type": "module"`).
- Package name: `opencode-agent-link`.
- Version: `1.0.0` (initial).
- Add a concise description based on the PRD:
  - Suggested: `"Small CLI with TUI to link a project into OpenCode agent repos"`.
- Keep dependencies minimal (none required for this task).
- Do **not** add `bin` mappings yet (handled in Task 1-1-4).
- Do **not** add external dependencies yet (handled later).

## Files to Create/Modify
- `package.json` (repo root)

## Out of Scope (Do NOT Do)
- Do not create `bin/` or `src/` directories (Task 1-1-2).
- Do not implement CLI flag logic (Task 1-1-3).
- Do not add `bin` field or run `npm link` (Task 1-1-4).
- Do not add dependencies.
- Do not modify any files outside `package.json`.

## Implementation Notes
- If `package.json` does not exist, initialize a basic one (e.g., `npm init -y`) and then edit fields.
- If it exists, update only the required fields.
- Keep ASCII-only content.

## Verification (Good Enough)
- `package.json` exists at repo root.
- Contains: `"name": "opencode-agent-link"`.
- Contains: `"version": "1.0.0"`.
- Contains: `"type": "module"`.
- Contains a short PRD-based description.

## Completion Criteria
Task 1-1-1 is complete when `package.json` meets the above requirements and no other files are changed.
