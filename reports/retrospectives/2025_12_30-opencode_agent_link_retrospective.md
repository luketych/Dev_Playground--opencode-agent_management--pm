# Project Retrospective — opencode-agent-link (2025-12-30)

## Summary
This project started as a tool to manage large sets of OpenCode agents by selectively linking agent markdown files into a project's `.opencode/agents` directory. The implementation evolved into a different tool: a CLI that links the current project root into an agent repository via `.opencode/cwd`. That works for a different workflow, but it does not solve the original problem of `/agents` list clutter. This document records the original intent, the evolution, the challenges, and what we would do differently if we restarted the effort.

## Original Purpose (Vision)
- Problem: `/agents` in OpenCode looks only at `.opencode/agents/*.md`, which gets cluttered when many agents exist.
- Desired flow:
  - Maintain a master repository of agent definitions at `~/_/Dev_Classic/classic/dotfiles/opencode/...`.
  - Organize agents into bundle folders (for example, `review/`, `build/`, `research/`).
  - Run a script from a project with a `.opencode` folder.
  - Pick a bundle folder (single-select).
  - The script replaces the project's `.opencode/agents` contents with symlinks to the selected bundle (plus defaults: `plan` and `build`).
  - `/agents` now shows only the selected bundle, not the full master list.
- Conflict policy: hard fail if two agents share the same filename.
- Storage: folder-based bundles (no manifest file required).
- Linking method: symlinks are acceptable and preferred over snapshots to avoid multiple sources of truth.

## What Was Implemented
- A CLI called `opencode-agent-link` that:
  - Scans `opencode-agents/*/.opencode` under the current working directory.
  - Shows a TUI selection of eligible agent directories.
  - Creates a symlink at `opencode-agents/<agent>/.opencode/cwd` pointing to the current project root.
  - Handles idempotency and conflicts.
- This aligns with the PRD in `pm/descriptions/_0/prd.md`, but diverges from the original goal (managing `.opencode/agents` for `/agents`).

## Evolution and Decision Points
- We followed the PRD, which framed the tool as a linker from project root into an agent repo (`.opencode/cwd`).
- The tool became effective for linking a project to an agent repository but did not address `/agents` clutter.
- Later, we realized the original vision should have been a bundle selector that links agent files into `.opencode/agents`.
- A branch taxonomy correction happened after PRs were merged; a `feature_set/m4-linking` branch was created to align naming without rewriting history.

## Challenges and Friction
- **Direction mismatch**: The implemented symlink points from agent repo to project root, while the original need was to link agent definitions into the project.
- **Clutter vs. discoverability**: `/agents` only reads `.opencode/agents`. Linking `cwd` does not impact `/agents` at all.
- **Renames during experimentation**: Agents are renamed frequently while evolving. Symlinks are fine, but renames will break them if they point directly to source files.
- **Symlink loops**: If `opencode-agents/` lives inside the project root, symlinks can create a directory graph cycle (not a symlink to itself, but confusing to navigate).
- **Testing harness complexity**: We needed a scripted workspace and an `expect`-based test to automate TUI selection.

## What We Would Do Differently
If restarting with the original goal in mind:
1. Start with the `/agents` contract (OpenCode reads `.opencode/agents/*.md`).
2. Build a bundle selector for agent files, not a project-to-agent linker.
3. Define defaults (`plan`, `build`) that always remain in `.opencode/agents`.
4. On bundle selection:
   - Clear non-default agents.
   - Symlink all `.md` files from the selected bundle folder into `.opencode/agents`.
5. Hard fail on filename conflicts (consistent with OpenCode expectations).
6. Optional: maintain a single lightweight marker file for the current bundle (for example, `.opencode/agents/.bundle`), not a full manifest.
7. Keep the implementation minimal and aligned with the actual UX pain: clutter in `/agents`.

## Is This Still Useful?
- The current tool is useful if you want to link a project root into an agent repository using `.opencode/cwd`.
- It does not solve `/agents` clutter. For that, a bundle-based linker (project-side) is still needed.
- Given the mismatch, archiving this project is reasonable unless the `cwd` linking workflow becomes a priority in your OpenCode usage.

## Alternatives and Future Paths
- Build a new, smaller tool focused solely on bundle selection and `.opencode/agents` linking.
- Keep a large master repo and create thin wrapper files in each project that reference stable agent IDs.
- Introduce stable IDs in agent frontmatter to decouple filenames from agent identity.
- Wait for OpenCode to support agent collections or external include paths.

## Breadcrumbs (for Future Recall)
- PRD: `pm/descriptions/_0/prd.md`
- Code repo: `Dev_Playground--opencode-agent_management--code`
- PRs:
  - #11: scripted E2E harness
  - #12: prompt cancellation cleanup
  - #13: linking logic (`.opencode/cwd`)
- Merge commit: `ffdd0a3b121f6b9aebab04f3f5ba0754853cabc7`
- Feature commit: `81c28cb` — "feat: link project root in selected agent"
- Test harness update commit: `4522054` — "test: add test-mode workspace for e2e scripts"
- Branches:
  - `feature/linking-logic-1-4`
  - `feature_set/m4-linking`
- Key files:
  - `perimembrane/membrane/viscera/src/index.mjs`
  - `perimembrane/membrane/viscera/scripts/e2e_agent_link/setup.mjs`
  - `perimembrane/membrane/viscera/scripts/e2e_agent_link/help.mjs`

## Decision
Archive this project as-is and treat it as a documented experiment. If the original goal remains important, build a new tool that directly manages `.opencode/agents` with bundle selection.
