---
id: M3
title: "TUI Interaction"
phase: 2
duration: "1 Hour"
status: "Not Started"
priority: "Medium"
branch: "feature/tui-interaction"
tags: [ui, tui, inquirer]
dependencies: [M2]
---
# Milestone 3: TUI Interaction

**Phase**: 2 - User Interface  
**Duration**: 1 Hour  
**Status**: Not Started  
**Priority**: Medium

## Deliverable
Interactive selection prompt for selecting the target agent.

## Objectives
- Integrate `@inquirer/prompts` into the project.
- Implement single-select list populated by discovery logic results.
- Ensure clean exit behavior (Ctrl+C) without stack traces.

## Proposed Tasks
- [1-3-1] Install and Configure @inquirer/prompts
- [1-3-2] Implement Agent Selection Prompt
- [1-3-3] Handle User Cancellation (SIGINT)
- [1-3-4] Add E2E Test Harness for opencode-agent-link

## Success Criteria
- [ ] TUI appears with list of discovered agents when run in a valid directory.
- [ ] Selection can be navigated with arrow keys.
- [ ] Pressing Ctrl+C exits the program cleanly with code 0.
- [ ] Selected agent name is correctly passed to the next stage of logic.

## Dependencies
- Milestone 2 (Discovery Logic) completed.
- `@inquirer/prompts` package.

## Risks
- Asynchronous prompt execution conflicts with CLI exit flow.
- Terminal compatibility issues with complex TUI (minimal risk for single-select).

## Notes
- User flow now matches the PRD vision for interactivity.
- Sets up asynchronous infrastructure for the linking step.
