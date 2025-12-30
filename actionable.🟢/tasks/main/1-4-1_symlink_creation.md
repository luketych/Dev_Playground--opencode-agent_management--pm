---
id: 1-4-1
title: "Implement Symlink Creation Logic"
status: not_started
priority: high
assignee: "opencode"
created: 2025-12-29
updated: 2025-12-29
completed: null
tags: [core, fs, symlink]
milestone: M4
dependencies: [M3]
estimated_effort: "30 minutes"
actual_effort: null
---
# Implement Symlink Creation Logic

## Definition of Done, Good-Enough

**DONE**: `.opencode/cwd` symlink is created under the selected agent and points to the project root.

**GOOD-ENOUGH**: Running the CLI once creates a valid symlink to the current project root.

## Task Description
Create the `.opencode/cwd` symlink inside the selected agent directory, pointing to the absolute project root path.

## Context (What's needed)
- Selected agent name from the TUI prompt.
- Project root path from `process.cwd()`.
- Target path: `opencode-agents/<agent>/.opencode/cwd`.

## How to Re-Verify Success
```bash
# From a workspace with opencode-agents/<agent>/.opencode
node /path/to/bin/opencode-agent-link
# Then verify the symlink points to the project root
ls -l opencode-agents/<agent>/.opencode/cwd
```

## Implementation Checklist
- [ ] Build absolute path to project root.
- [ ] Resolve selected agent path.
- [ ] Create symlink at `.opencode/cwd`.

## Measurable Success Criteria
- Symlink target resolves to the project root.
- CLI exits 0 on success.

## Tests
- Manual: run CLI, inspect symlink.

## How to Prove Completion
1. Create or use a workspace that contains `opencode-agents/<agent>/.opencode`.
2. `cd` into the workspace (this is the project root) and run the CLI.
3. Select a known agent (for example, `gemini`) at the prompt.
4. Verify the link exists and is a symlink: `ls -l opencode-agents/<agent>/.opencode/cwd` should show `cwd -> /absolute/path`.
5. Verify the target equals the project root: `readlink opencode-agents/<agent>/.opencode/cwd` should match `pwd` and be an absolute path.
6. Check the CLI exit code is 0 (for example, `echo $?`).
7. DONE if the symlink exists, is a symlink, and its target equals the project root. GOOD-ENOUGH if the symlink exists and points to the project root, even if you did not inspect the exit code.

## Proof of Completion
- TBD
