---
id: 1-3-2
title: "Implement Agent Selection Prompt"
status: complete
priority: high
assignee: "opencode"
created: 2025-12-28
updated: 2025-12-28
completed: 2025-12-28
tags: [tui, prompt]
milestone: M3
dependencies: [1-3-1]
estimated_effort: "40 minutes"
actual_effort: "40 minutes"
---
# Implement Agent Selection Prompt

## Definition of Done, Good-Enough

**DONE**: CLI displays a single-select prompt of eligible agents and returns the chosen agent name.

**GOOD-ENOUGH**: Prompt renders with a static list and returns a selection.

## Task Description
Wire the discovery list into an interactive TUI prompt using `@inquirer/prompts`.

## Context (What’s needed)
- Code location: `perimembrane/membrane/viscera/src/index.mjs`.
- Existing functions: `scanEligibleAgents`, root validation from M2.
- Library: `@inquirer/prompts` `select` API.
- PRD prompt text: "Select agent to link current project into:".

## How to Re-Verify Success
```bash
node --input-type=module -e "import fs from 'node:fs'; import os from 'node:os'; import path from 'node:path'; const repo='/Users/luketych/_/Dev/Dev_Playground/opencode-agent_management/code'; const cli=path.join(repo,'bin','opencode-agent-link'); const root=fs.mkdtempSync(path.join(os.tmpdir(),'opencode-tui-')); const agents=path.join(root,'opencode-agents'); fs.mkdirSync(agents); fs.mkdirSync(path.join(agents,'gemini')); fs.mkdirSync(path.join(agents,'gemini','.opencode')); const res=await import('node:child_process').then(({spawnSync})=>spawnSync('node',[cli],{cwd:root,encoding:'utf8',input:'\n'})); console.log(res.stdout.includes('Select agent to link current project into:') ? 'OK prompt' : 'FAIL prompt');"
```

## Implementation Checklist
- [x] Import `select` from `@inquirer/prompts`.
- [x] Build choices from eligible agent list.
- [x] Display prompt with PRD message.
- [x] Return/handle selected agent name.

## Measurable Success Criteria
- Prompt displays only eligible agents.
- Selected agent name is captured for downstream use.

## Tests
- Not applicable (manual prompt). Use the verification command above.

## Proof of Completion
Verification run (2025-12-28):
```
OK prompt
```
