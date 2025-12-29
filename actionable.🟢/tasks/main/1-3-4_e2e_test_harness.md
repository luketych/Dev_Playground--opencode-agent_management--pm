---
id: 1-3-4
title: "Add E2E Test Harness for opencode-agent-link"
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
# Add E2E Test Harness for opencode-agent-link

## Definition of Done, Good-Enough

**DONE**: A test folder exists under `perimembrane/membrane/viscera/` with a `resources/` subfolder and an E2E test that creates example `opencode-agents` and runs the CLI to validate expected behavior.

**GOOD-ENOUGH**: A scriptable test exists that exercises the CLI with a temporary `opencode-agents/` layout.

## Task Description
Create a minimal E2E test harness that can simulate agent directories and run the CLI to validate behavior end-to-end.

## Context (What’s needed)
- Code location: `perimembrane/membrane/viscera/` in the code repo.
- The CLI entry: `bin/opencode-agent-link`.
- Node.js 18+.
- This should be a test-only addition (no production logic changes).

## How to Re-Verify Success
```bash
# Example (paths may change based on test harness)
node perimembrane/membrane/viscera/test/e2e_agent_link.test.mjs
```

## Implementation Checklist
- [ ] Create `perimembrane/membrane/viscera/test/`.
- [ ] Create `perimembrane/membrane/viscera/test/resources/`.
- [ ] Add an E2E test that:
  - Creates a temp directory with `opencode-agents/<agent>/.opencode`.
  - Runs `opencode-agent-link` from that temp dir.
  - Verifies prompt, selection, and error paths.
- [ ] Document how to run the test.

## Measurable Success Criteria
- Test executes without external dependencies.
- Test validates at least one happy path and one error path.
