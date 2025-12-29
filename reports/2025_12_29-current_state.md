# Current State Report — 2025-12-29

## Summary
The project is split into two active repos (PM + Code). Milestones 1 and 2 are complete and archived. Milestone 3 is in progress with TUI functionality implemented and merged, while the E2E harness is being reworked from an in-repo test to a script-driven workspace. The script-based harness lives on an open PR.

## Repo Split
- PM repo: https://github.com/luketych/Dev_Playground--opencode-agent_management--pm
- Code repo: https://github.com/luketych/Dev_Playground--opencode-agent_management--code
- Original monorepo is archived.

## PM Repo State (Planning)
**Head commit:** `6746d1c` — marks 1-3-4 and 1-3-4b complete with scripted proof.

### Milestones
- **archive/**: M1 (Scaffolding), M2 (Agent Discovery)
- **main/**: M3 (TUI Interaction)
- **backlog/**: M4 (Linking Logic), M5 (Verification/Distribution)
- **review/**: empty

### Tasks
- **archive/**: M1 tasks (1-1-1..1-1-4, 1-1-1b) and M2 tasks (1-2-1..1-2-3)
- **review/**: M3 tasks complete with proofs: 1-3-1, 1-3-2, 1-3-3
- **main/**: 1-3-4 and 1-3-4b (scripted E2E harness + cleanup)
  - Status fields set to complete with scripted proof, but still in main pending merge of PR #11 in code repo.

## Code Repo State (Implementation)
**Current local branch head:** `d87960a` on `feature/tui-1-3-4-scripts`

### Implemented & Merged
- M2 discovery logic (root validation, scanner, empty-list error handling)
- M3 TUI selection and cancel handling (prompt + Ctrl+C exit)

### E2E Harness State
- **main currently contains** the older `viscera/test` harness from PR #9 (merged).
- **Open PR #11** replaces the test harness with `viscera/scripts/e2e_agent_link`:
  - `setup.mjs` creates a workspace with `opencode-agents/gemini/.opencode` and `opencode-agents/gpt/.opencode`.
  - `help.mjs` explains usage.
  - `teardown.mjs` removes the workspace.
  - Workspace path is ignored in `.gitignore`.

**Open PR:** https://github.com/luketych/Dev_Playground--opencode-agent_management--code/pull/11
- Head branch: `feature/tui-1-3-4-scripts`
- Base: `main`

## How to Use the Scripted Harness (PR #11)
```bash
node perimembrane/membrane/viscera/scripts/e2e_agent_link/help.mjs
node perimembrane/membrane/viscera/scripts/e2e_agent_link/setup.mjs
# cd <workspace> (printed by setup)
# node <repo>/bin/opencode-agent-link
node perimembrane/membrane/viscera/scripts/e2e_agent_link/teardown.mjs
```

## Local Workspace State
- Root folder contains only: `code/`, `pm/`, `.opencode/`.
- PM repo clean and up to date with origin.
- Code repo on `feature/tui-1-3-4-scripts` with PR #11 open.

## Next Steps
1. Merge PR #11 to replace the old test harness with scripts.
2. Move tasks 1-3-4 and 1-3-4b from `tasks/main` to `tasks/review` after merge, then to `tasks/archive` once accepted.
3. Begin Milestone 4 (symlink creation).
