---
id: 1-1-4
title: "Global CLI Link Configuration"
status: complete
priority: medium
assignee: "opencode"
created: 2025-12-28
updated: 2025-12-28
completed: 2025-12-28
tags: [npm, config]
milestone: M1
dependencies: [1-1-3]
estimated_effort: "15 minutes"
actual_effort: "15 minutes"
---
# Global CLI Link Configuration

## Definition of Done, Good-Enough

**DONE**: `package.json` has a `bin` field mapping `opencode-agent-link` to `bin/opencode-agent-link`, and the command runs via the global PATH after `npm link`.

**GOOD-ENOUGH**: `bin` field is present and maps to `bin/opencode-agent-link`.

## Task Description
Ensure the tool can be installed and used as a global command, fulfilling the distribution requirement of the PRD.

## How to Re-Verify Success
```bash
node -e "const fs=require('fs'); const {spawnSync}=require('child_process'); const pkg=JSON.parse(fs.readFileSync('package.json','utf8')); const binOk=pkg.bin && pkg.bin['opencode-agent-link']==='bin/opencode-agent-link'; console.log((binOk ? 'OK' : 'FAIL') + ' bin mapping'); const cmd=spawnSync('opencode-agent-link',['--help'],{encoding:'utf8'}); const helpOk=cmd.stdout.includes('Usage: opencode-agent-link'); console.log((helpOk ? 'OK' : 'FAIL') + ' global help'); process.exit(binOk && helpOk ? 0 : 1);"
```

## Implementation Checklist
- [x] Add `bin` section to `package.json`.
- [x] Verify path in `bin` section is correct.
- [x] Test local `npm link`.

## Measurable Success Criteria
- `package.json` exposes `opencode-agent-link` in the `bin` field.
- `opencode-agent-link --help` runs from PATH.

## Tests
- Not applicable (metadata/installation). Use the verification command above.

## Proof of Completion
Verification run (2025-12-28):
```
OK bin mapping
OK global help
```
