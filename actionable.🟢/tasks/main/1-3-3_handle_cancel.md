---
id: 1-3-3
title: "Handle User Cancellation (Ctrl+C)"
status: in_progress
priority: medium
assignee: "opencode"
created: 2025-12-28
updated: 2025-12-28
tags: [tui, ux]
milestone: M3
dependencies: [1-3-2]
estimated_effort: "20 minutes"
---
# Handle User Cancellation (Ctrl+C)

## Definition of Done, Good-Enough

**DONE**: User cancellation exits cleanly with code 0 and no stack trace.

**GOOD-ENOUGH**: Ctrl+C stops the program without an unhandled error.

## Task Description
Ensure the prompt handles user cancellation in a clean, predictable way.

## Context (What’s needed)
- `@inquirer/prompts` cancellation behavior.
- Node process exit handling.
- PRD requirement: cancel exits cleanly with code 0.

## How to Re-Verify Success
```bash
# Start prompt and press Ctrl+C
node bin/opencode-agent-link
# Expect: clean exit (code 0), no stack trace
```

## Implementation Checklist
- [ ] Detect prompt cancellation.
- [ ] Exit 0 without logging an error or stack trace.

## Measurable Success Criteria
- Ctrl+C results in exit code 0.
- No error output on cancel.
