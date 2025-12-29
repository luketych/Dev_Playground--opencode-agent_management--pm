---
id: 1-3-4b
title: "Add Explicit E2E Test Cleanup"
status: in_progress
priority: low
assignee: "opencode"
created: 2025-12-28
updated: 2025-12-28
tags: [test, e2e, cleanup]
milestone: M3
dependencies: [1-3-4]
estimated_effort: "15 minutes"
---
# Add Explicit E2E Test Cleanup

## Definition of Done, Good-Enough

**DONE**: E2E test explicitly cleans up any created directories or files (including temporary resources) before exit.

**GOOD-ENOUGH**: Test cleanup runs on success and failure to avoid leaving artifacts.

## Task Description
Add explicit cleanup logic to the E2E test so it removes any created resources and leaves no residue after execution.

## Context (What’s needed)
- Code location: `perimembrane/membrane/viscera/test/e2e_agent_link.test.mjs`.
- Node.js filesystem APIs for cleanup (`fs.rmSync`, `fs.rmdirSync`).
- Keep test-only changes; no production code impact.

## How to Re-Verify Success
```bash
node perimembrane/membrane/viscera/test/e2e_agent_link.test.mjs
# After run, verify temp dirs are removed
```

## Implementation Checklist
- [ ] Track created temp directories.
- [ ] Ensure cleanup runs on success and failure.
- [ ] Confirm no leftover test artifacts.

## Measurable Success Criteria
- No temp directories remain after test completes.
- Cleanup runs even on error conditions.
