---
id: 1-2-3
title: "Implement Error Handling for Discovery Failures"
status: in_progress
priority: high
assignee: "opencode"
created: 2025-12-28
updated: 2025-12-28
tags: [nodejs, fs, errors]
milestone: M2
dependencies: [1-2-2]
estimated_effort: "20 minutes"
---
# Implement Error Handling for Discovery Failures

## Definition of Done, Good-Enough

**DONE**: If no eligible agents exist, the CLI prints the PRD message `No eligible agents found (need opencode-agents/*/.opencode/)` and exits non-zero. Permission errors are surfaced directly.

**GOOD-ENOUGH**: No eligible agents triggers a non-zero exit with a clear error.

## Task Description
Ensure the CLI fails clearly when discovery yields zero eligible agents and surfaces filesystem errors without hiding them.

## How to Re-Verify Success
```bash
# With opencode-agents/ present but no .opencode subdirs
node bin/opencode-agent-link
# Expect: No eligible agents found (need opencode-agents/*/.opencode/)
```

## Implementation Checklist
- [ ] Detect empty eligible list.
- [ ] Print the PRD-specified message and exit non-zero.
- [ ] Surface permission errors from fs operations.

## Measurable Success Criteria
- Exact PRD error message on zero eligible agents.
- Non-zero exit on discovery failures.
