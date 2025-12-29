---
id: 1-2-2
title: "Develop Agent Scanner Function"
status: complete
priority: high
assignee: "opencode"
created: 2025-12-28
updated: 2025-12-28
completed: 2025-12-28
tags: [nodejs, fs, discovery]
milestone: M2
dependencies: [1-2-1]
estimated_effort: "25 minutes"
actual_effort: "25 minutes"
---
# Develop Agent Scanner Function

## Definition of Done, Good-Enough

**DONE**: The scanner enumerates only direct children of `opencode-agents/` and returns a list of agent names where `.opencode/` exists.

**GOOD-ENOUGH**: Direct children are filtered based on the existence of `.opencode/`.

## Task Description
Implement a deterministic scan for eligible agent directories under `opencode-agents/` with the PRD's direct-child rule.

## How to Re-Verify Success
```bash
node --input-type=module -e "import fs from 'node:fs'; import os from 'node:os'; import path from 'node:path'; const repo='/Users/luketych/_/Dev/Dev_Playground/opencode-agent_management/code'; const module=await import('file://' + path.join(repo,'perimembrane/membrane/viscera/src/index.mjs')); const root=fs.mkdtempSync(path.join(os.tmpdir(),'opencode-scan-')); const agents=path.join(root,'opencode-agents'); fs.mkdirSync(agents); fs.mkdirSync(path.join(agents,'gemini')); fs.mkdirSync(path.join(agents,'gemini','.opencode')); fs.mkdirSync(path.join(agents,'other')); fs.writeFileSync(path.join(agents,'file.txt'),'x'); const list=module.scanEligibleAgents(agents); const ok=list.length===1 && list[0]==='gemini'; console.log(ok ? 'OK eligible' : 'FAIL eligible');"
```

## Implementation Checklist
- [x] Read direct children of `opencode-agents/`.
- [x] Check for `.opencode/` subdirectory in each child.
- [x] Return eligible agent names relative to `opencode-agents/`.

## Measurable Success Criteria
- Eligible list includes only direct children with `.opencode/`.
- No recursion or traversal beyond direct children.

## Tests
- Not applicable (filesystem scan only). Use the verification command above.

## Proof of Completion
Verification run (2025-12-28):
```
OK eligible
```
