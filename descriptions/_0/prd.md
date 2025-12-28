# PRD.md — `opencode-agent-link`

## Overview

**`opencode-agent-link`** is a small, installable CLI tool that provides a **simple interactive TUI** for linking the current working directory (CWD) into OpenCode agent repositories.

The tool scans for agent repositories under a standard directory layout and allows the user to **select an eligible agent**. Upon selection, it creates a **symbolic link** inside the agent’s `.opencode/` directory pointing back to the original project root.

The tool is designed to be:
- deterministic
- inspectable
- safe (idempotent, non-destructive)
- installable as a **global bash command**

---

## Goals

### Primary Goals
1. Provide a **fast, interactive CLI** for linking a project root into OpenCode agent repos.
2. Ensure **only valid agent directories** are selectable.
3. Create symlinks in a predictable, idempotent way.
4. Be installable globally and runnable from **any directory**.

### Non-Goals
- No OpenCode internals manipulation
- No agent execution or orchestration
- No config file mutation beyond symlink creation
- No GUI or web UI

---

## Target Users

- Developers using **OpenCode**
- Users running **multiple role-based agents** (research, git, synthesis, etc.)
- Users who want **explicit, file-based wiring** between projects and agents

---

## Installation Requirements

### Distribution
- Packaged as an **npm library**
- Installed globally via:
  ```bash
  npm install -g opencode-agent-link
  ```

### Runtime Requirements
- Node.js ≥ 18
- POSIX-compatible OS (macOS, Linux)
- Symlink support (Windows explicitly out of scope for v1)

---

## Invocation

Once installed:

```bash
opencode-agent-link
```

- Must be runnable from **any directory**
- Uses the current working directory (`process.cwd()`) as the project root
- `opencode-agents/` must be a direct child of `process.cwd()` (future: location may be configurable)

### Flags
- `--help` prints usage and exits 0
- `--version` prints version and exits 0

---

## Expected Directory Layout

From the current working directory:

```text
.
└── opencode-agents/
    ├── gemini/
    │   └── .opencode/
    ├── gpt/
    │   └── .opencode/
    └── other/
        └── (ignored if .opencode is missing)
```

### Eligibility Rules
A directory is considered **selectable** if and only if:
- It is a direct child of `opencode-agents/`
- It contains a `.opencode/` subdirectory

---

## User Experience (TUI)

### Library
- Use **`@inquirer/prompts`**
- Single-select list (radio / arrow-key navigation)

### Behavior
- Display **only eligible agent directories**
- Show agent names relative to `opencode-agents/`
- Prompt message example:
  ```
  Select agent to link current project into:
  ```

### Exit Conditions
- If user cancels → exit cleanly with code 0
- If no eligible agents exist → print error and exit non-zero

---

## Core Behavior

### Symlink Creation
Upon agent selection:
- Create a symlink named:
  ```
  cwd
  ```
- Location:
  ```
  opencode-agents/<agent>/.opencode/cwd
  ```
- Symlink target:
  ```
  <original working directory>
  ```

### Idempotency Rules
- If the symlink already exists:
  - Do **not** overwrite
  - Print:
    - existing symlink path
    - symlink target
  - Exit successfully

### Error Handling
- Missing `opencode-agents/` → clear error, non-zero exit
- Missing `.opencode/` → agent excluded from UI
- Permission errors → surfaced directly

---

## Output Examples

### Success
```text
Created: opencode-agents/gemini/.opencode/cwd -> /Users/me/projects/foo
```

### Already Exists
```text
Already exists: opencode-agents/gemini/.opencode/cwd -> /Users/me/projects/foo
```

### No Agents Found
```text
No eligible agents found (need opencode-agents/*/.opencode/)
```

---

## Technical Implementation Notes

### Language & Structure
- Node.js (ESM)
- Minimal dependencies
- No frameworks beyond `@inquirer/prompts`

### Suggested File Layout
```text
opencode-agent-link/
├── bin/
│   └── opencode-agent-link
├── src/
│   └── index.mjs
├── package.json
└── README.md
```

### `package.json` Requirements
- Define `bin` entry so the command is globally available
- Example:
  ```json
  {
    "bin": {
      "opencode-agent-link": "bin/opencode-agent-link"
    }
  }
  ```

---

## Security & Safety Considerations

- Tool must **never delete files**
- Tool must **never modify files other than creating a symlink**
- Tool must not traverse outside `opencode-agents/`
- No network access
- No shell execution

---

## Future Enhancements (Out of Scope for v1)

- Multi-select (“link all”)
- Unlink mode
- Dry-run mode
- Windows support
- Configurable link name
- Detection of mismatched symlink targets
- Integration with OpenCode task metadata

---

## Definition of Done

The feature is complete when:
- The tool installs globally via npm
- Running `opencode-agent-link` from any directory:
  - finds eligible agents
  - shows a TUI picker
  - creates the correct symlink
- The tool is idempotent and safe
- No agent without `.opencode/` is selectable
- Behavior matches this PRD exactly
