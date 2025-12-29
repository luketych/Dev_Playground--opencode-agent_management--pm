---
id: 1-2-3
title: "Implement Error Handling for Discovery Failures"
status: complete
priority: high
assignee: "opencode"
created: 2025-12-28
updated: 2025-12-28
completed: 2025-12-28
tags: [nodejs, fs, errors]
milestone: M2
dependencies: [1-2-2]
estimated_effort: "20 minutes"
actual_effort: "20 minutes"
---
# Implement Error Handling for Discovery Failures

## Definition of Done, Good-Enough

**DONE**: If no eligible agents exist, the CLI prints the PRD message `No eligible agents found (need opencode-agents/*/.opencode/)` and exits non-zero. Permission errors are surfaced directly.

**GOOD-ENOUGH**: No eligible agents triggers a non-zero exit with a clear error.

## Task Description
Ensure the CLI fails clearly when discovery yields zero eligible agents and surfaces filesystem errors without hiding them.

## How to Re-Verify Success
```bash
node --input-type=module -e "import fs from 'node:fs'; import os from 'node:os'; import path from 'node:path'; const repo='/Users/luketych/_/Dev/Dev_Playground/opencode-agent_management/code'; const cli=path.join(repo,'bin','opencode-agent-link'); const root=fs.mkdtempSync(path.join(os.tmpdir(),'opencode-none-')); const agents=path.join(root,'opencode-agents'); fs.mkdirSync(agents); const res=await import('node:child_process').then(({spawnSync})=>spawnSync('node',[cli],{cwd:root,encoding:'utf8'})); console.log((res.status!==0 && res.stderr.includes('No eligible agents found (need opencode-agents/*/.opencode/)')) ? 'OK empty' : 'FAIL empty');"
```

## Implementation Checklist
- [x] Detect empty eligible list.
- [x] Print the PRD-specified message and exit non-zero.
- [x] Surface permission errors from fs operations.

## Measurable Success Criteria
- Exact PRD error message on zero eligible agents.
- Non-zero exit on discovery failures.

## Tests
- Not applicable (filesystem check only). Use the verification command above.

## Proof of Completion
Verification run (2025-12-28):
```
OK empty
```
