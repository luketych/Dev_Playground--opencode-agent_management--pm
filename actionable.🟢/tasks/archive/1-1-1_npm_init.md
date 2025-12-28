---
id: 1-1-1
title: "Initialize NPM Package and ESM Configuration"
status: pending
priority: high
assignee: "opencode"
created: 2025-12-28
updated: 2025-12-28
tags: [npm, nodejs, setup]
milestone: M1
dependencies: []
estimated_effort: "15 minutes"
---
# Initialize NPM Package and ESM Configuration

## Definition of Done, Good-Enough

**DONE**: `package.json` created with correct metadata, `"type": "module"` enabled, and basic project info (name, version, description) set.

**GOOD-ENOUGH**: `package.json` exists and allows `import` statements (ESM).

## Task Description
Initialize the Node.js project. Since we are building a modern CLI, we must use ESM (EcmaScript Modules) to ensure compatibility with modern libraries and provide a better development experience.

## How to Re-Verify Success
```bash
# Check package.json exists
ls package.json

# Verify ESM is enabled
grep '"type": "module"' package.json
```

## Implementation Checklist
- [ ] Run `npm init -y`
- [ ] Update `name` to `opencode-agent-link`
- [ ] Add `"type": "module"` to `package.json`
- [ ] Set `version` to `1.0.0`
- [ ] Add project description from PRD

## Measurable Success Criteria
- `package.json` is valid JSON.
- `node` recognizes the project as an ESM module.
