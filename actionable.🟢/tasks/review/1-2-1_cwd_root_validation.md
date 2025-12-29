---
id: 1-2-1
title: "Implement CWD Detection and Root Validation"
status: pending
priority: high
assignee: "opencode"
created: 2025-12-28
updated: 2025-12-28
tags: [nodejs, fs, discovery]
milestone: M2
dependencies: [M1]
estimated_effort: "20 minutes"
---
# Implement CWD Detection and Root Validation

## Definition of Done, Good-Enough

**DONE**: The CLI resolves `process.cwd()` as the project root, verifies `opencode-agents/` exists as a direct child, and exits non-zero with a clear error when missing.

**GOOD-ENOUGH**: `process.cwd()` is used and `opencode-agents/` presence is validated before any scanning.

## Task Description
Establish the root context and fail fast when the expected `opencode-agents/` directory is missing. This is the foundation for all discovery logic.

## How to Re-Verify Success
```bash
# From a directory missing opencode-agents/
node bin/opencode-agent-link
# Expect: non-zero exit + clear error about missing opencode-agents/

# From a directory containing opencode-agents/
node bin/opencode-agent-link
# Expect: no missing-directory error
```

## Implementation Checklist
- [ ] Read `process.cwd()` as the project root.
- [ ] Resolve `opencode-agents/` as a direct child path.
- [ ] If missing, print a clear error and exit non-zero.

## Measurable Success Criteria
- Missing `opencode-agents/` produces a clear error and non-zero exit.
- Presence of `opencode-agents/` allows discovery to proceed.
