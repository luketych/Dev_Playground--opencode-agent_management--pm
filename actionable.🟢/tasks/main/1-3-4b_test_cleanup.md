---
id: 1-3-4b
title: "Add Explicit E2E Workspace Cleanup"
status: in_progress
priority: low
assignee: "opencode"
created: 2025-12-28
updated: 2025-12-28
tags: [test, e2e, cleanup]
milestone: M3
dependencies: [1-3-4]
estimated_effort: "15 minutes"
actual_effort: "15 minutes"
---
# Add Explicit E2E Workspace Cleanup

## Definition of Done, Good-Enough

**DONE**: `teardown.mjs` removes the workspace created by `setup.mjs` even if the workspace already exists or is partially created.

**GOOD-ENOUGH**: Running teardown removes the workspace directory without errors.

## Task Description
Ensure cleanup is its own script and reliably removes the scripted E2E workspace.

## Context (What’s needed)
- Code location: `perimembrane/membrane/viscera/scripts/e2e_agent_link/teardown.mjs`.
- Workspace path defined by `setup.mjs`.
- Node.js filesystem APIs for cleanup (`fs.rmSync`).

## How to Re-Verify Success
```bash
node perimembrane/membrane/viscera/scripts/e2e_agent_link/setup.mjs
node perimembrane/membrane/viscera/scripts/e2e_agent_link/teardown.mjs
# Verify the workspace path printed by setup no longer exists
```

## Implementation Checklist
- [x] Use a deterministic workspace path.
- [x] Remove workspace with `fs.rmSync(..., { recursive: true, force: true })`.
- [x] No errors when workspace is missing.

## Measurable Success Criteria
- Teardown removes the workspace path every time.
- No leftovers remain after teardown.

## Tests
- Run `node perimembrane/membrane/viscera/scripts/e2e_agent_link/setup.mjs`.
- Run `node perimembrane/membrane/viscera/scripts/e2e_agent_link/teardown.mjs`.

## Proof of Completion
Verification run (2025-12-28):
```
REMOVED: /Users/luketych/_/Dev/Dev_Playground/opencode-agent_management/code/perimembrane/membrane/viscera/scripts/e2e_agent_link/workspace
```
