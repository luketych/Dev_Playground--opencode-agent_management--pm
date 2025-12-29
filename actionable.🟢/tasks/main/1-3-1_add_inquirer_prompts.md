---
id: 1-3-1
title: "Add @inquirer/prompts Dependency"
status: in_progress
priority: high
assignee: "opencode"
created: 2025-12-28
updated: 2025-12-28
tags: [tui, deps, nodejs]
milestone: M3
dependencies: [M2]
estimated_effort: "20 minutes"
---
# Add @inquirer/prompts Dependency

## Definition of Done, Good-Enough

**DONE**: `@inquirer/prompts` is added to `package.json` dependencies and install is verified locally.

**GOOD-ENOUGH**: Dependency entry exists in `package.json`.

## Task Description
Introduce the TUI library required for Milestone 3 using a minimal dependency footprint.

## Context (What’s needed)
- PRD section: User Experience (TUI) requires `@inquirer/prompts`.
- Code repo root: `package.json` in the code repo.
- Node.js 18+ available.

## How to Re-Verify Success
```bash
# In code repo
npm install
node -e "const pkg=require('./package.json'); console.log(pkg.dependencies['@inquirer/prompts'] ? 'OK dep' : 'FAIL dep')"
```

## Implementation Checklist
- [ ] Add `@inquirer/prompts` to dependencies in `package.json`.
- [ ] Run `npm install`.
- [ ] Verify dependency exists in `package.json`.

## Measurable Success Criteria
- Dependency is present in `package.json`.
- `npm install` completes without errors.
