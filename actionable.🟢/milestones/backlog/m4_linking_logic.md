---
id: M4
title: "Symlink Creation & Idempotency"
duration: "1 Hour"
status: "In Progress"
priority: "High"
branch: "feature/linking-logic"
tags: [core, fs, symlink]
dependencies: [M3]
---
# Milestone 4: Symlink Creation & Idempotency

**Phase**: 3 - Core Logic  
**Duration**: 1 Hour  
**Status**: In Progress  
**Priority**: High

## Deliverable
Core linking functionality with idempotency and safety checks.

## Objectives
- Implement symlink creation from agent's `.opencode/cwd` to project root.
- Implement idempotency checks to prevent redundant operations.
- Ensure PRD-compliant success and "already exists" output messages.

## Proposed Tasks
- [1-4-1] Implement Symlink Creation Logic
- [1-4-2] Add Idempotency and Safety Checks
- [1-4-3] Finalize Output Formatting for Linking Operations
- [1-4-4] Extend Scripted E2E Harness for Linking

## Success Criteria
- [ ] Symlink `cwd` is created in the correct location pointing back to project root.
- [ ] Symlink target is an absolute path.
- [ ] Second run on the same agent prints "Already exists" and does not error.
- [ ] Conflicting existing path emits a clear error and non-zero exit.
- [ ] Output exactly matches the PRD examples.

## Dependencies
- Milestone 3 (TUI Interaction) completed.
- Write permissions for the target agent directory.

## Risks
- Absolute vs Relative path confusion for symlink targets.
- Race conditions if multiple instances run (minimal risk).

## Notes
- This is the primary functional achievement of the tool.
- Verifies path resolution logic.
