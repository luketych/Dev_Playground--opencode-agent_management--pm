---
id: 1-1-4
title: "Global CLI Link Configuration"
status: pending
priority: medium
assignee: "opencode"
created: 2025-12-28
updated: 2025-12-28
tags: [npm, config]
milestone: M1
dependencies: [1-1-3]
estimated_effort: "15 minutes"
---
# Global CLI Link Configuration

## Definition of Done, Good-Enough

**DONE**: `package.json` has `bin` field mapping `opencode-agent-link` to `bin/opencode-agent-link`. `npm link` works and allows running the command from any directory.

**GOOD-ENOUGH**: `bin` field is added to `package.json`.

## Task Description
Ensure the tool can be installed and used as a global command, fulfilling the distribution requirement of the PRD.

## How to Re-Verify Success
```bash
# Run npm link
npm link

# Test command globally
opencode-agent-link --help
```

## Implementation Checklist
- [ ] Add `bin` section to `package.json`.
- [ ] Verify path in `bin` section is correct.
- [ ] Test local `npm link`.

## Measurable Success Criteria
- `opencode-agent-link` command is available in the shell's PATH after linking.
