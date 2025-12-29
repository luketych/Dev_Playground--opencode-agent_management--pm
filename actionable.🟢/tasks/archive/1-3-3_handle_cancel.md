---
id: 1-3-3
title: "Handle User Cancellation (Ctrl+C)"
status: complete
priority: medium
assignee: "opencode"
created: 2025-12-28
updated: 2025-12-28
completed: 2025-12-28
tags: [tui, ux]
milestone: M3
dependencies: [1-3-2]
estimated_effort: "20 minutes"
actual_effort: "20 minutes"
---
# Handle User Cancellation (Ctrl+C)

## Definition of Done, Good-Enough

**DONE**: User cancellation exits cleanly with code 0 and no stack trace.

**GOOD-ENOUGH**: Ctrl+C stops the program without an unhandled error.

## Task Description
Ensure the prompt handles user cancellation in a clean, predictable way.

## Context (What’s needed)
- `@inquirer/prompts` cancellation behavior.
- Node process exit handling.
- PRD requirement: cancel exits cleanly with code 0.

## How to Re-Verify Success
```bash
node --input-type=module -e "import fs from 'node:fs'; import os from 'node:os'; import path from 'node:path'; import { spawn } from 'node:child_process'; const repo='/Users/luketych/_/Dev/Dev_Playground/opencode-agent_management/code'; const cli=path.join(repo,'bin','opencode-agent-link'); const root=fs.mkdtempSync(path.join(os.tmpdir(),'opencode-cancel-')); const agents=path.join(root,'opencode-agents'); fs.mkdirSync(agents); fs.mkdirSync(path.join(agents,'gemini')); fs.mkdirSync(path.join(agents,'gemini','.opencode')); const child=spawn('node',[cli],{cwd:root}); let stderr=''; child.stderr.on('data',(chunk)=>{stderr+=chunk.toString();}); const timer=setTimeout(()=>{child.kill('SIGINT');},800); const timeout=setTimeout(()=>{console.log('FAIL cancel'); process.exit(1);},3000); child.on('exit',(code)=>{clearTimeout(timer); clearTimeout(timeout); const ok=code===0 && !stderr.includes('ExitPromptError') && !stderr.includes('CancelPromptError'); console.log(ok ? 'OK cancel' : 'FAIL cancel');});"
```

## Implementation Checklist
- [x] Detect prompt cancellation.
- [x] Exit 0 without logging an error or stack trace.

## Measurable Success Criteria
- Ctrl+C results in exit code 0.
- No error output on cancel.

## Tests
- Not applicable (interactive prompt). Use the verification command above.

## Proof of Completion
Verification run (2025-12-28):
```
OK cancel
```
