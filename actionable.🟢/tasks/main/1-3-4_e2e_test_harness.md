---
id: 1-3-4
title: "Add Scripted E2E Harness for opencode-agent-link"
status: in_progress
priority: medium
assignee: "opencode"
created: 2025-12-28
updated: 2025-12-28
tags: [test, e2e, tui]
milestone: M3
dependencies: [1-3-3]
estimated_effort: "45 minutes"
---
# Add Scripted E2E Harness for opencode-agent-link

## Definition of Done, Good-Enough

**DONE**: A `scripts/e2e_agent_link/` subdir exists under `perimembrane/membrane/viscera/` with:
- `setup.mjs` that creates a local test workspace populated with example `opencode-agents/` from `resources/`.
- `teardown.mjs` that removes the workspace.
- `resources/opencode-agents/<agent>/.opencode` example tree.

**GOOD-ENOUGH**: Setup script creates a usable workspace and prints how to run the CLI.

## Task Description
Create a script-driven E2E harness that sets up a local test project using example agent files, so a human can run the CLI and verify behavior. Cleanup must be separate.

## Context (What’s needed)
- Code location: `perimembrane/membrane/viscera/scripts/e2e_agent_link/`.
- CLI entry: `bin/opencode-agent-link`.
- Example agents stored under `resources/`.
- Node.js 18+.

## How to Re-Verify Success
```bash
# Setup test workspace (prints instructions + workspace path)
node perimembrane/membrane/viscera/scripts/e2e_agent_link/setup.mjs

# Run the CLI from the workspace path (printed by setup)
# Example:
# cd <workspace>
# node <repo>/bin/opencode-agent-link

# Cleanup
node perimembrane/membrane/viscera/scripts/e2e_agent_link/teardown.mjs
```

## Implementation Checklist
- [ ] Create `perimembrane/membrane/viscera/scripts/e2e_agent_link/`.
- [ ] Create `resources/opencode-agents/<agent>/.opencode` example tree.
- [ ] Add `setup.mjs` to create workspace and copy resources.
- [ ] Add `teardown.mjs` to remove workspace.
- [ ] Print workspace path and CLI command from `setup.mjs`.

## Measurable Success Criteria
- Workspace contains an `opencode-agents/` directory with a valid `.opencode` marker.
- CLI runs successfully from the workspace.
- Teardown removes the workspace.
