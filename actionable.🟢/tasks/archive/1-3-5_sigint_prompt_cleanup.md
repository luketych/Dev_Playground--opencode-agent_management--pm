---
id: 1-3-5
title: "Preserve Prompt Cleanup on Ctrl+C"
status: complete
priority: low
assignee: "opencode"
created: 2025-12-29
updated: 2025-12-29
completed: 2025-12-29
tags: [tui, ux, cleanup]
milestone: M3
dependencies: [1-3-3]
estimated_effort: "15 minutes"
actual_effort: "10 minutes"
---
# Preserve Prompt Cleanup on Ctrl+C

## Definition of Done, Good-Enough

**DONE**: No custom SIGINT handler preempts @inquirer/prompts cleanup; Ctrl+C during the prompt exits cleanly.

**GOOD-ENOUGH**: Ctrl+C in the selection prompt returns to the shell without terminal corruption.

## Task Description
Remove the manual SIGINT exit handler so prompt cancellation can unwind and restore terminal state.

## Context (What's needed)
- Code location: `perimembrane/membrane/viscera/src/index.mjs`.
- `@inquirer/prompts` throws `ExitPromptError`/`CancelPromptError` on cancellation.

## How to Re-Verify Success
```bash
# From a workspace with opencode-agents/*/.opencode
node /Users/luketych/_/Dev/Dev_Playground/opencode-agent_management/code/bin/opencode-agent-link
# Press Ctrl+C at the prompt, expect clean exit and normal terminal behavior.
```

## Implementation Checklist
- [x] Remove manual `process.once("SIGINT", ...)` handler.
- [x] Keep prompt cancellation handling in the select() try/catch.

## Measurable Success Criteria
- Ctrl+C during the prompt exits without leaving the terminal in raw mode.
- Exit code is 0 on prompt cancellation.

## Tests
- Manual: run CLI, cancel at prompt.

## Proof of Completion
- Removed manual SIGINT handler in `perimembrane/membrane/viscera/src/index.mjs` so prompt cancellation handles cleanup.
- Verification run (2025-12-29):
```
node perimembrane/membrane/viscera/scripts/e2e_agent_link/setup.mjs
# Ctrl+C sent at the prompt (pseudo-tty); expect clean exit
EXIT_CODE: 0
node perimembrane/membrane/viscera/scripts/e2e_agent_link/teardown.mjs
```
