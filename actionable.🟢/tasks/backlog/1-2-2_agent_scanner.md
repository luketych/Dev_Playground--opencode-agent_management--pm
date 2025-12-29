---
id: 1-2-2
title: "Develop Agent Scanner Function"
status: pending
priority: high
assignee: "opencode"
created: 2025-12-28
updated: 2025-12-28
tags: [nodejs, fs, discovery]
milestone: M2
dependencies: [1-2-1]
estimated_effort: "25 minutes"
---
# Develop Agent Scanner Function

## Definition of Done, Good-Enough

**DONE**: The scanner enumerates only direct children of `opencode-agents/` and returns a list of agent names where `.opencode/` exists.

**GOOD-ENOUGH**: Direct children are filtered based on the existence of `.opencode/`.

## Task Description
Implement a deterministic scan for eligible agent directories under `opencode-agents/` with the PRD's direct-child rule.

## How to Re-Verify Success
```bash
# With opencode-agents/gemini/.opencode and opencode-agents/other (no .opencode)
node bin/opencode-agent-link
# Expect: only gemini appears in the eligible list
```

## Implementation Checklist
- [ ] Read direct children of `opencode-agents/`.
- [ ] Check for `.opencode/` subdirectory in each child.
- [ ] Return eligible agent names relative to `opencode-agents/`.

## Measurable Success Criteria
- Eligible list includes only direct children with `.opencode/`.
- No recursion or traversal beyond direct children.
