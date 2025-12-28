# OpenCode Agent Management Playground 🧪🤖

This repository is a sandbox for exploring how to manage multiple OpenCode agents in a clean, repeatable way. It focuses on **explicit, file-based wiring** between a project and one or more agent workspaces, with an emphasis on clarity, safety, and ease of use.

## Purpose
- Provide a safe place to prototype multi-agent workflows without touching production repos.
- Explore how role-based agents (research, git, synthesis, etc.) can be isolated yet connected to the same project.
- Document patterns and tooling that make agent setup **deterministic and inspectable**.

## What we're building
The primary concept in this playground is **`opencode-agent-link`** — a small, global CLI that links the current project into a selected agent repo by creating a symlink in `.opencode/cwd`. It uses a simple TUI to show **eligible agent directories** (direct children of `opencode-agents/` that contain `.opencode/`) and creates the link **idempotently** (safe to re-run).

## Why it exists
Multi-agent setups are powerful but can drift over time. This repo is about making the relationship between a project and its agents:
- **explicit** (file-based links you can inspect)
- **fast** (one command instead of manual linking)
- **safe** (no destructive changes)

## Repository contents
- `descriptions/prd.md` — detailed product requirements for `opencode-agent-link`
- prototypes and experiments (as they evolve)

## Tags / Keywords / SEO 🔎✨
Tags: #OpenCode #LLM #AI #MultiAgent #AgentManagement #CLI #TUI #NodeJS #Symlink #DevTools #WorkspaceLinking #Automation #DeveloperExperience

Keywords: opencode agent link, agent repository wiring, multi-agent workflow, agent sandbox, role-based agents, symlinked workspace, interactive CLI, inquirer prompts, POSIX tooling, local developer tools, LLM tooling, agent ops

Also known as: OpenCode agent linking, agent workspace connector, agent repo linker, agent management playground
