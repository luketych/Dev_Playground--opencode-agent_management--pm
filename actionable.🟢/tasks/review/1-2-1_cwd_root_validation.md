---
id: 1-2-1
title: "Implement CWD Detection and Root Validation"
status: complete
priority: high
assignee: "opencode"
created: 2025-12-28
updated: 2025-12-28
completed: 2025-12-28
tags: [nodejs, fs, discovery]
milestone: M2
dependencies: [M1]
estimated_effort: "20 minutes"
actual_effort: "20 minutes"
---
# Implement CWD Detection and Root Validation

## Definition of Done, Good-Enough

**DONE**: The CLI resolves `process.cwd()` as the project root, verifies `opencode-agents/` exists as a direct child, and exits non-zero with a clear error when missing.

**GOOD-ENOUGH**: `process.cwd()` is used and `opencode-agents/` presence is validated before any scanning.

## Task Description
Establish the root context and fail fast when the expected `opencode-agents/` directory is missing. This is the foundation for all discovery logic.

## How to Re-Verify Success
```bash
node -e "const {spawnSync}=require('child_process'); const fs=require('fs'); const os=require('os'); const path=require('path'); const repo='/Users/luketych/_/Dev/Dev_Playground/opencode-agent_management/code'; const cli=path.join(repo,'bin','opencode-agent-link'); const empty=fs.mkdtempSync(path.join(os.tmpdir(),'opencode-empty-')); const missing=spawnSync('node',[cli],{cwd:empty,encoding:'utf8'}); console.log((missing.status!==0 && missing.stderr.includes('Missing opencode-agents/')) ? 'OK missing' : 'FAIL missing'); const root=fs.mkdtempSync(path.join(os.tmpdir(),'opencode-root-')); fs.mkdirSync(path.join(root,'opencode-agents')); const present=spawnSync('node',[cli],{cwd:root,encoding:'utf8'}); console.log((present.status===0 && !present.stderr.includes('Missing opencode-agents/')) ? 'OK present' : 'FAIL present');"
```

## Implementation Checklist
- [x] Read `process.cwd()` as the project root.
- [x] Resolve `opencode-agents/` as a direct child path.
- [x] If missing, print a clear error and exit non-zero.

## Measurable Success Criteria
- Missing `opencode-agents/` produces a clear error and non-zero exit.
- Presence of `opencode-agents/` allows discovery to proceed.

## Tests
- Not applicable (filesystem check only). Use the verification command above.

## Proof of Completion
Verification run (2025-12-28):
```
OK missing
OK present
```
