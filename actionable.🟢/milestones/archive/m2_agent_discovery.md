---
id: M2
title: "Agent Discovery Logic"
phase: 1
duration: "1 Hour"
status: "Not Started"
priority: "High"
branch: "feature/agent-discovery"
tags: [logic, fs, nodejs]
dependencies: [M1]
---
# Milestone 2: Agent Discovery Logic

**Phase**: 1 - Foundation  
**Duration**: 1 Hour  
**Status**: Not Started  
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
- [ ] Correctly identifies eligible agents in a test directory (e.g., `viscera/opencode-agents`).
- [ ] Correctly ignores directories missing the `.opencode/` marker.
- [ ] Prints PRD-compliant error message when `opencode-agents/` is missing.
- [ ] Prints "No eligible agents found" when directory is empty or all agents are invalid.

## Dependencies
- Milestone 1 (Project Scaffolding) completed.
- POSIX file system access.

## Risks
- Symlink loops or unexpected directory depths (mitigated by direct-child rule).
- Edge cases in `fs` operations (e.g., restricted permissions).

## Notes
- Ensures the tool is strictly local to the project root.
- Establishes the internal data structure for "selectable" agents.
