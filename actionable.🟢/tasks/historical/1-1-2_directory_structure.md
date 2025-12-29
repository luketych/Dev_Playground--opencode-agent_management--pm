---
id: 1-1-2
title: "Create CLI Directory Structure and Entry Point"
status: pending
priority: high
assignee: "opencode"
created: 2025-12-28
updated: 2025-12-28
tags: [scaffolding, nodejs]
milestone: M1
dependencies: [1-1-1]
estimated_effort: "15 minutes"
---
# Create CLI Directory Structure and Entry Point

## Definition of Done, Good-Enough

**DONE**: `bin/` and `src/` directories created. `bin/opencode-agent-link` exists with a proper hashbang and imports logic from `src/index.mjs`.

**GOOD-ENOUGH**: `bin/` directory exists with an executable script that runs with `node`.

## Task Description
Set up the physical directory structure as recommended in the PRD. This separates the executable wrapper from the core logic.

## How to Re-Verify Success
```bash
# Verify directories
test -d bin && echo "✓ bin exists"
test -d src && echo "✓ src exists"

# Verify bin script has execute permissions
ls -l bin/opencode-agent-link

# Verify bin script runs
node bin/opencode-agent-link
```

## Implementation Checklist
- [ ] Create `bin` and `src` directories.
- [ ] Create `bin/opencode-agent-link` with `#!/usr/bin/env node` hashbang.
- [ ] Create `src/index.mjs` as the main logic entry.
- [ ] Make `bin/opencode-agent-link` executable (`chmod +x`).

## Measurable Success Criteria
- `bin/opencode-agent-link` executes without error.
- Correct directory layout per PRD.
