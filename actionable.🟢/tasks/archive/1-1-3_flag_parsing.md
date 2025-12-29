---
id: 1-1-3
title: "Implement Argument Parsing for Help and Version"
status: pending
priority: high
assignee: "opencode"
created: 2025-12-28
updated: 2025-12-28
tags: [cli, logic]
milestone: M1
dependencies: [1-1-2]
estimated_effort: "30 minutes"
---
# Implement Argument Parsing for Help and Version

## Definition of Done, Good-Enough

**DONE**: CLI handles `--help` and `--version` flags. `--help` prints usage instructions and exits 0. `--version` prints the version from `package.json` and exits 0.

**GOOD-ENOUGH**: Flags are detected via `process.argv` and print something relevant.

## Task Description
Implement the first layer of CLI interaction. The tool must respond correctly to standard help and version requests before any core logic is executed.

## How to Re-Verify Success
```bash
# Test help flag
node bin/opencode-agent-link --help | grep "Usage"

# Test version flag
node bin/opencode-agent-link --version | grep "1.0.0"
```

## Implementation Checklist
- [ ] Import `package.json` (using `fs` or `import` with attributes) to get version.
- [ ] Check `process.argv` for `--help`, `-h`, `--version`, `-v`.
- [ ] Implement `printHelp()` function.
- [ ] Implement `printVersion()` function.

## Measurable Success Criteria
- Exits with code 0 on help/version.
- Correct version displayed.
- Clear usage instructions displayed.
