---
id: 1-4-2
title: "Add Idempotency and Safety Checks"
status: not_started
priority: high
assignee: "opencode"
created: 2025-12-29
updated: 2025-12-29
completed: null
tags: [core, fs, safety]
milestone: M4
dependencies: [1-4-1]
estimated_effort: "20 minutes"
actual_effort: null
---
# Add Idempotency and Safety Checks

## Definition of Done, Good-Enough

**DONE**: A second run on the same agent prints "Already exists" and exits 0 when the symlink already points to the current project root.

**GOOD-ENOUGH**: Existing correct symlink does not error; conflicting paths raise a clear error.

## Task Description
Detect whether `.opencode/cwd` already exists and either short-circuit with an "Already exists" message or raise a safe error if it conflicts.

## Context (What's needed)
- `fs.lstatSync` / `fs.readlinkSync` or async equivalents.
- Behavior for non-symlink files at the target path.

## How to Re-Verify Success
```bash
# First run (creates link)
node /path/to/bin/opencode-agent-link
# Second run (should be idempotent)
node /path/to/bin/opencode-agent-link
```

## Implementation Checklist
- [ ] If `cwd` exists and is a symlink to project root, print "Already exists" and exit 0.
- [ ] If `cwd` exists but points elsewhere, print a clear error and exit non-zero.
- [ ] If `cwd` exists and is not a symlink, print a clear error and exit non-zero.

## Measurable Success Criteria
- Idempotent behavior on second run.
- Safe error on conflicts.

## Tests
- Manual: run twice and verify outputs.

## How to Prove Completion
1. Start from a clean workspace where `.opencode/cwd` does not exist.
2. Run the CLI once and select the same agent to create the symlink.
3. Run the CLI a second time and select the same agent.
4. Confirm the output includes "Already exists" and the exit code is 0.
5. Confirm the symlink target is unchanged: `readlink opencode-agents/<agent>/.opencode/cwd` still equals the project root.
6. Create a conflict case:
   - Replace the symlink with a regular file (remove the symlink, then `touch opencode-agents/<agent>/.opencode/cwd`), or
   - Replace it with a symlink to a different target (for example, `ln -s /tmp opencode-agents/<agent>/.opencode/cwd`).
7. Run the CLI again and confirm:
   - A clear error is printed to stderr.
   - Exit code is non-zero.
   - The conflicting path is not overwritten.
8. DONE if idempotent runs produce "Already exists" with exit code 0 and conflict cases exit non-zero with a clear error. GOOD-ENOUGH if the idempotent case is correct and conflicts are detected even if the exact error text is still pending.

## Proof of Completion
- TBD
