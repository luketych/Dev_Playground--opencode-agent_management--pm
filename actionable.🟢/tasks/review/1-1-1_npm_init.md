---
id: 1-1-1
title: "Initialize NPM Package and ESM Configuration"
status: complete
priority: high
assignee: "opencode"
created: 2025-12-28
updated: 2025-12-28
completed: 2025-12-28
tags: [npm, nodejs, setup]
milestone: M1
dependencies: []
estimated_effort: "15 minutes"
actual_effort: "10 minutes"
---
# Initialize NPM Package and ESM Configuration

## Definition of Done, Good-Enough

**DONE**: `package.json` exists at repo root, parses as JSON, and contains:
- `name`: `opencode-agent-link`
- `version`: `1.0.0`
- `description`: non-empty string matching the PRD intent
- `type`: `module`

**GOOD-ENOUGH**: `package.json` exists with `name` and `type` set correctly.

## Task Description
Initialize the Node.js project. Since we are building a modern CLI, we must use ESM (EcmaScript Modules) to ensure compatibility with modern libraries and provide a better development experience.

## How to Re-Verify Success
```bash
node -e "const fs=require('fs'); const pkg=JSON.parse(fs.readFileSync('package.json','utf8')); const checks=[['name', pkg.name==='opencode-agent-link'], ['version', pkg.version==='1.0.0'], ['type', pkg.type==='module'], ['description', typeof pkg.description==='string' && pkg.description.length>0]]; for (const [label, ok] of checks) console.log((ok ? 'OK' : 'FAIL') + ' ' + label); const all=checks.every(([,ok])=>ok); process.exit(all?0:1);"
```

## Implementation Checklist
- [x] Create `package.json` (manual or `npm init -y`).
- [x] Set `name` to `opencode-agent-link`.
- [x] Add `"type": "module"` to `package.json`.
- [x] Set `version` to `1.0.0`.
- [x] Add PRD-aligned project description.

## Measurable Success Criteria
- `package.json` parses successfully with `JSON.parse`.
- `name`, `version`, and `type` values match the expected literals.
- `description` is present and non-empty.

## Tests
- Not applicable (metadata-only). Use the verification command above.

## Proof of Completion
Verification run (2025-12-28):
```
OK name
OK version
OK type
OK description
```
