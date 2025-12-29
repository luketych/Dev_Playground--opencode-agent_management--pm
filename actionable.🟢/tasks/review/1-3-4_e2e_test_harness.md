---
id: 1-3-4
title: "Add Scripted E2E Harness for opencode-agent-link"
status: complete
priority: medium
assignee: "opencode"
created: 2025-12-28
updated: 2025-12-28
completed: 2025-12-28
tags: [test, e2e, tui]
milestone: M3
dependencies: [1-3-3]
estimated_effort: "45 minutes"
actual_effort: "45 minutes"
---
# Add Scripted E2E Harness for opencode-agent-link

## Definition of Done, Good-Enough

**DONE**: A `scripts/e2e_agent_link/` subdir exists under `perimembrane/membrane/viscera/` with:
- `setup.mjs` that creates a local test workspace populated with example `opencode-agents/`.
- `teardown.mjs` that removes the workspace.
- `help.mjs` that explains usage and expectations.

**GOOD-ENOUGH**: Setup script creates a usable workspace and prints how to run the CLI.

## Task Description
Create a script-driven E2E harness that sets up a local test project so a human can run the CLI and verify behavior. Cleanup must be separate.

## Context (What’s needed)
- Code location: `perimembrane/membrane/viscera/scripts/e2e_agent_link/`.
- CLI entry: `bin/opencode-agent-link`.
- Node.js 18+.

## How to Re-Verify Success
```bash
node perimembrane/membrane/viscera/scripts/e2e_agent_link/help.mjs
node perimembrane/membrane/viscera/scripts/e2e_agent_link/setup.mjs
# cd <workspace> (printed by setup)
# node <repo>/bin/opencode-agent-link
node perimembrane/membrane/viscera/scripts/e2e_agent_link/teardown.mjs
```

## Implementation Checklist
- [x] Create `perimembrane/membrane/viscera/scripts/e2e_agent_link/`.
- [x] Add `setup.mjs` to create workspace and seed agents.
- [x] Add `teardown.mjs` to remove workspace.
- [x] Add `help.mjs` to explain usage.

## Measurable Success Criteria
- Workspace contains an `opencode-agents/` directory with valid `.opencode` markers.
- CLI runs successfully from the workspace.
- Teardown removes the workspace.

## Tests
- Run `node perimembrane/membrane/viscera/scripts/e2e_agent_link/help.mjs`.
- Run `node perimembrane/membrane/viscera/scripts/e2e_agent_link/setup.mjs`.
- Run the CLI from the printed workspace path.
- Run `node perimembrane/membrane/viscera/scripts/e2e_agent_link/teardown.mjs`.

## Proof of Completion
Verification run (2025-12-28):
```
WORKSPACE: /Users/luketych/_/Dev/Dev_Playground/opencode-agent_management/code/perimembrane/membrane/viscera/scripts/e2e_agent_link/workspace
RUN: cd "/Users/luketych/_/Dev/Dev_Playground/opencode-agent_management/code/perimembrane/membrane/viscera/scripts/e2e_agent_link/workspace" && node "/Users/luketych/_/Dev/Dev_Playground/opencode-agent_management/code/bin/opencode-agent-link"
TEARDOWN: node "/Users/luketych/_/Dev/Dev_Playground/opencode-agent_management/code/perimembrane/membrane/viscera/scripts/e2e_agent_link/teardown.mjs"
? Select agent to link current project into:
❯ gemini
  gpt
✔ Select agent to link current project into: gemini
REMOVED: /Users/luketych/_/Dev/Dev_Playground/opencode-agent_management/code/perimembrane/membrane/viscera/scripts/e2e_agent_link/workspace
```
