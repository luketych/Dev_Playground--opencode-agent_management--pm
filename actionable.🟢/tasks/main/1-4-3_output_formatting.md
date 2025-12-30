---
id: 1-4-3
title: "Finalize Output Formatting for Linking"
status: not_started
priority: medium
assignee: "opencode"
created: 2025-12-29
updated: 2025-12-29
completed: null
tags: [cli, output]
milestone: M4
dependencies: [1-4-1, 1-4-2]
estimated_effort: "15 minutes"
actual_effort: null
---
# Finalize Output Formatting for Linking

## Definition of Done, Good-Enough

**DONE**: Success and idempotency messages match PRD examples exactly.

**GOOD-ENOUGH**: Output is stable and unambiguous for success and already-exists cases.

## Task Description
Implement user-facing messages for success and "already exists" in the linking flow.

## Context (What's needed)
- PRD output examples.
- Existing CLI output conventions for errors.

## How to Re-Verify Success
```bash
node /path/to/bin/opencode-agent-link
# Observe output and compare to PRD examples.
```

## Implementation Checklist
- [ ] Implement success message.
- [ ] Implement "Already exists" message.
- [ ] Keep error output on stderr.

## Measurable Success Criteria
- Output matches PRD examples.

## Tests
- Manual: run CLI with a real agent selection.

## How to Prove Completion
1. Locate the PRD output examples for success and "Already exists".
2. Run the CLI for a fresh agent (success case).
3. Capture stdout and stderr separately (for example, `node ... >out.txt 2>err.txt`).
4. Compare stdout to the PRD success example; stderr should be empty and exit code should be 0.
5. Run the CLI again for the same agent (idempotent case).
6. Capture stdout/stderr again and compare stdout to the PRD "Already exists" example; exit code should be 0.
7. If error messages are defined in the PRD, trigger a conflict case and verify error output goes to stderr with a non-zero exit code.
8. DONE if the success and idempotent outputs match PRD examples exactly. GOOD-ENOUGH if output meaning and exit codes are correct and any minor formatting differences are documented.

## Proof of Completion
- TBD
