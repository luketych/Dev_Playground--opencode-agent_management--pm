---
id: M2
title: "Agent Discovery Logic"
phase: 1
duration: "1 Hour"
status: "Complete"
priority: "High"
branch: "feature/agent-discovery"
tags: [logic, fs, nodejs]
dependencies: [M1]
---
# Milestone 2: Agent Discovery Logic

**Phase**: 1 - Foundation  
**Duration**: 1 Hour  
**Status**: Complete  
**Priority**: High

## Deliverable
Robust logic for scanning and validating potential agent directories.

## Objectives
- Implement `process.cwd()` detection for project root.
- Develop scanner for `opencode-agents/` filtering for `.opencode/` subdirectories.
- Handle "no agents found" and "missing directory" error states with specific exit codes.

## Proposed Tasks
- [1-2-1] Implement CWD Detection and Root Validation
- [1-2-2] Develop Agent Scanner Function
- [1-2-3] Implement Error Handling for Discovery Failures

## Success Criteria
- [x] Correctly identifies eligible agents in a test directory (e.g., `viscera/opencode-agents`).
- [x] Correctly ignores directories missing the `.opencode/` marker.
- [x] Prints PRD-compliant error message when `opencode-agents/` is missing.
- [x] Prints "No eligible agents found" when directory is empty or all agents are invalid.

## Dependencies
- Milestone 1 (Project Scaffolding) completed.
- POSIX file system access.

## Risks
- Symlink loops or unexpected directory depths (mitigated by direct-child rule).
- Edge cases in `fs` operations (e.g., restricted permissions).

## Notes
- Ensures the tool is strictly local to the project root.
- Establishes the internal data structure for "selectable" agents.

## Review Notes
- M2 tasks (1-2-1 through 1-2-3) are archived with proofs in `actionable.🟢/tasks/archive/`.
- Success criteria validated via task-level verification commands.
