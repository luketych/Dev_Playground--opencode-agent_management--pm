---
stickers:
  - 🧠
topics:
  - git
  - pull_requests
  - branching
  - workflow
  - traceability
tags:
  - lessons learned
  - engineering workflow
  - git practices
  - pull requests
  - branching strategy
  - post merge
  - history immutability
date: 2025-12-29
---

# Lesson Learned — PRs, Branch Naming, and Post-Merge Traceability (2025-12-29)

## Context
While implementing Milestone 4 (linking logic), we built the feature on a branch named `feature/linking-logic-1-4` in the code repo and merged it to `main` via PR #13. After the merge, we realized that we wanted all task-related commits to live under a `feature_set/*` branch for easier grouping and review. Because the PR was already merged, renaming or rewriting history would have required heavier steps (revert + re-PR). Instead, we created a new branch that points at the already-merged `main` to preserve the desired branch naming without rewriting history.

## What Actually Happened (Short Timeline)
- Work was done on `feature/linking-logic-1-4`.
- PR #13 was created and merged into `main`.
- After merge, we wanted the work represented on a `feature_set/*` branch.
- We created `feature_set/m4-linking` from `main` to establish the desired branch taxonomy without rewriting history.

## Why This Matters
PRs are durable records. Once a PR is merged, the change is part of the canonical history. Undoing or renaming that history is possible but usually heavier and riskier (revert commits, re-PR, or force-push). In other words, PRs are not "too heavy" for normal work, but they _do_ carry weight: they make changes official. This is great for accountability and review, but it means branch naming and grouping decisions should be made early if we care about clean lineage.

## Lesson
Decide branch taxonomy before opening/merging a PR. If we want all work grouped under `feature_set/*`, then start there. After merge, the cheapest fix is to create a new branch pointer (like `feature_set/m4-linking`) that references `main`. That preserves the naming convention, but it does not retroactively change the origin of the work.

## Alternatives We Considered
1. **Create a new branch pointer from `main` (what we did):**
   - Pros: No history rewrite, minimal risk, immediate traceability.
   - Cons: The original working branch name still exists in history and PR metadata.
2. **Revert main and re-PR from a `feature_set/*` branch:**
   - Pros: The PR and branch lineage would exactly match the desired taxonomy.
   - Cons: More work, more risk, more noise in history.

## Recommended Workflow Going Forward
- Create the feature branch with the final taxonomy up front, e.g. `feature_set/m4-linking`.
- Open a draft PR early if needed, but do not merge until naming/structure is settled.
- If a branch naming change is necessary, do it before the PR is merged.

## Breadcrumbs (for Future Recall)
- Code repo: `Dev_Playground--opencode-agent_management--code`
- PR: https://github.com/luketych/Dev_Playground--opencode-agent_management--code/pull/13
- Merge commit (PR #13): `ffdd0a3b121f6b9aebab04f3f5ba0754853cabc7`
- Feature commit: `81c28cb` — "feat: link project root in selected agent"
- Branches involved:
  - Original: `feature/linking-logic-1-4`
  - Desired taxonomy: `feature_set/m4-linking`
- Files changed:
  - `perimembrane/membrane/viscera/src/index.mjs`
  - `perimembrane/membrane/viscera/scripts/e2e_agent_link/help.mjs`
- PM tasks tied to this work:
  - `actionable.🟢/tasks/review/1-4-1_symlink_creation.md`
  - `actionable.🟢/tasks/review/1-4-2_idempotency_and_safety.md`
  - `actionable.🟢/tasks/review/1-4-3_output_formatting.md`
  - `actionable.🟢/tasks/review/1-4-4_e2e_harness_linking.md`

## Summary
PRs are the right tool, but they freeze the story. If branch naming or grouping matters for long-term traceability, make that decision _before_ the PR is merged. When a mismatch happens, creating a new branch pointer from `main` is the least risky corrective step, even if it does not rewrite history.
