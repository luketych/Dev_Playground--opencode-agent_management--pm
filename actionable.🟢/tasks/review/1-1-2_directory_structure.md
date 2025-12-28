---
id: 1-1-2
title: "Create CLI Directory Structure and Entry Point"
status: complete
priority: high
assignee: "opencode"
created: 2025-12-28
updated: 2025-12-28
completed: 2025-12-28
tags: [scaffolding, nodejs]
milestone: M1
dependencies: [1-1-1]
estimated_effort: "15 minutes"
actual_effort: "15 minutes"
---
# Create CLI Directory Structure and Entry Point

## Definition of Done, Good-Enough

**DONE**: `bin/` and `src/` directories exist, `bin/opencode-agent-link` is executable, starts with `#!/usr/bin/env node`, and imports `src/index.mjs`. `src/index.mjs` exists as the entry module.

**GOOD-ENOUGH**: `bin/` and `src/` directories exist and `node bin/opencode-agent-link` exits 0.

## Task Description
Set up the physical directory structure as recommended in the PRD. This separates the executable wrapper from the core logic.

## How to Re-Verify Success
```bash
node -e "const fs=require('fs'); const {spawnSync}=require('child_process'); const checks=[['bin dir', fs.existsSync('bin') && fs.statSync('bin').isDirectory()], ['src dir', fs.existsSync('src') && fs.statSync('src').isDirectory()], ['bin entry', fs.existsSync('bin/opencode-agent-link')], ['bin executable', (fs.statSync('bin/opencode-agent-link').mode & 0o111) !== 0], ['hashbang', fs.readFileSync('bin/opencode-agent-link','utf8').startsWith('#!/usr/bin/env node')], ['src entry', fs.existsSync('src/index.mjs')]]; let ok=true; for (const [label, pass] of checks) { console.log((pass ? 'OK' : 'FAIL') + ' ' + label); if (!pass) ok=false; } const run=spawnSync('node',['bin/opencode-agent-link'],{stdio:'ignore'}); const runOk=run.status===0; console.log((runOk ? 'OK' : 'FAIL') + ' run'); if (!runOk) ok=false; process.exit(ok?0:1);"
```

## Implementation Checklist
- [x] Create `bin` and `src` directories.
- [x] Create `bin/opencode-agent-link` with `#!/usr/bin/env node` hashbang.
- [x] Create `src/index.mjs` as the main logic entry.
- [x] Make `bin/opencode-agent-link` executable (`chmod +x`).

## Measurable Success Criteria
- `bin/` and `src/` directories exist.
- `bin/opencode-agent-link` is executable and has the correct hashbang.
- `src/index.mjs` exists.
- `node bin/opencode-agent-link` exits 0.

## Tests
- Not applicable (structure-only). Use the verification command above.

## Proof of Completion
Verification run (2025-12-28):
```
OK bin dir
OK src dir
OK bin entry
OK bin executable
OK hashbang
OK src entry
OK run
```
