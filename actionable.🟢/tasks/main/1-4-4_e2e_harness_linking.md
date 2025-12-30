---
id: 1-4-4
title: "Extend Scripted E2E Harness for Linking"
status: not_started
priority: low
assignee: "opencode"
created: 2025-12-29
updated: 2025-12-29
completed: null
tags: [test, e2e, docs]
milestone: M4
dependencies: [1-4-1, 1-4-2]
estimated_effort: "15 minutes"
actual_effort: null
---
# Extend Scripted E2E Harness for Linking

## Definition of Done, Good-Enough

**DONE**: Scripted harness usage notes include linking verification steps (first run + idempotent second run).

**GOOD-ENOUGH**: Manual steps are documented in help.mjs or task proof.

## Task Description
Update the scripted E2E harness documentation or flow to include link creation and idempotency verification.

## Context (What's needed)
- `perimembrane/membrane/viscera/scripts/e2e_agent_link/help.mjs`.
- Link behavior and expected output.

## How to Re-Verify Success
```bash
node perimembrane/membrane/viscera/scripts/e2e_agent_link/help.mjs
# Follow the documented steps and verify a symlink is created and idempotent.
```

## Implementation Checklist
- [ ] Add linking verification steps to help output.
- [ ] Include idempotent second-run instruction.

## Measurable Success Criteria
- E2E harness instructions cover linking verification.

## Tests
- Manual: follow updated help instructions.

## How to Prove Completion
1. Update `perimembrane/membrane/viscera/scripts/e2e_agent_link/help.mjs` with explicit steps for:
   - Running the CLI to create the `.opencode/cwd` symlink.
   - Verifying the symlink target (for example, `ls -l` and `readlink`).
   - Running the CLI a second time to confirm the "Already exists" path.
2. Run `node perimembrane/membrane/viscera/scripts/e2e_agent_link/help.mjs` and confirm the new steps are visible in the output.
3. Follow the documented steps in a fresh workspace and confirm:
   - The symlink is created and points to the project root.
   - The second run is idempotent and reports "Already exists".
4. DONE if the help text includes all three verification steps and the documented flow works end-to-end. GOOD-ENOUGH if the help text includes the steps even if you have not re-run the flow yet.

## Proof of Completion
- TBD
