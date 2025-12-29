---
id: 1-3-2
title: "Implement Agent Selection Prompt"
status: in_progress
priority: high
assignee: "opencode"
created: 2025-12-28
updated: 2025-12-28
tags: [tui, prompt]
milestone: M3
dependencies: [1-3-1]
estimated_effort: "40 minutes"
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
# In code repo with mock agents
node bin/opencode-agent-link
# Expect: interactive selection list of eligible agents
```

## Implementation Checklist
- [ ] Import `select` from `@inquirer/prompts`.
- [ ] Build choices from eligible agent list.
- [ ] Display prompt with PRD message.
- [ ] Return/handle selected agent name.

## Measurable Success Criteria
- Prompt displays only eligible agents.
- Selected agent name is captured for downstream use.
