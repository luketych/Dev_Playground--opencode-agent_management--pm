---
id: 1-1-3
title: "Implement Argument Parsing for Help and Version"
status: complete
priority: high
assignee: "opencode"
created: 2025-12-28
updated: 2025-12-28
completed: 2025-12-28
tags: [cli, logic]
milestone: M1
dependencies: [1-1-2]
estimated_effort: "30 minutes"
actual_effort: "25 minutes"
---
# Implement Argument Parsing for Help and Version

## Definition of Done, Good-Enough

**DONE**: CLI handles `--help` and `--version` flags. `--help` prints usage instructions and exits 0. `--version` prints the version from `package.json` and exits 0.

**GOOD-ENOUGH**: Flags are detected via `process.argv` and print a non-empty response.

## Task Description
Implement the first layer of CLI interaction. The tool must respond correctly to standard help and version requests before any core logic is executed.

## How to Re-Verify Success
```bash
node -e "const {spawnSync}=require('child_process'); const help=spawnSync('node',['bin/opencode-agent-link','--help'],{encoding:'utf8'}); const version=spawnSync('node',['bin/opencode-agent-link','--version'],{encoding:'utf8'}); const okHelp=help.stdout.includes('Usage: opencode-agent-link'); const okVersion=version.stdout.trim()==='1.0.0'; console.log((okHelp ? 'OK' : 'FAIL') + ' help'); console.log((okVersion ? 'OK' : 'FAIL') + ' version'); process.exit(okHelp && okVersion ? 0 : 1);"
```

## Implementation Checklist
- [x] Import `package.json` to read the version.
- [x] Check `process.argv` for `--help`, `-h`, `--version`, `-v`.
- [x] Implement `printHelp()` function.
- [x] Implement `printVersion()` function.

## Measurable Success Criteria
- `--help` outputs a usage line containing `Usage: opencode-agent-link`.
- `--version` outputs `1.0.0` exactly.
- Both commands exit with code 0.

## Tests
- Not applicable (CLI behavior verified via command above).

## Proof of Completion
Verification run (2025-12-28):
```
OK help
OK version
```
