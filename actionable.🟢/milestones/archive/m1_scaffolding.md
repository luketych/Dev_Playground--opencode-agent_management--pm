---
id: M1
title: "Project Scaffolding & CLI Skeleton"
phase: 1
duration: "1 Hour"
status: "Not Started"
priority: "High"
branch: "feature/scaffolding"
tags: [setup, nodejs, cli, scaffolding]
dependencies: []
---
# Milestone 1: Project Scaffolding & CLI Skeleton

**Phase**: 1 - Foundation  
**Duration**: 1 Hour  
**Status**: Not Started  
**Priority**: High

## Deliverable
Established project structure and basic CLI entry point.

## Objectives
- Initialize npm project as an ESM module.
- Setup the recommended file layout (`bin/`, `src/`).
- CLI argument parsing for `--help` and `--version` implemented.
- `package.json` configured with the `bin` field for global execution.

## Proposed Tasks
- [1-1-1] Initialize NPM Package and ESM Configuration
- [1-1-2] Create CLI Directory Structure and Entry Point
- [1-1-3] Implement Argument Parsing for Help and Version
- [1-1-4] Global CLI Link Configuration

## Success Criteria
- [ ] `package.json` created with `"type": "module"` and correct metadata.
- [ ] `bin/opencode-agent-link` exists with proper hashbang and execute permissions.
- [ ] `node bin/opencode-agent-link --help` prints usage instructions.
- [ ] `node bin/opencode-agent-link --version` prints current version.
- [ ] `npm link` allows running `opencode-agent-link` from any directory.

## Dependencies
- Node.js 18+ installed.
- Basic understanding of ESM and Node CLI patterns.

## Risks
- Permissions issues during `npm link` on some POSIX systems.
- ESM import syntax differences if not handled correctly.

## Notes
- Foundation for the entire project.
- Establishes the core module system and development workflow.
- Context: `descriptions/_0/prd.md` for CLI requirements.
