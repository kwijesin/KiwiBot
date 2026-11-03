# Test: <feature-name> / <case-name>

<!-- Copy to features/<feature-name>/tests/<case-name>.md. See the testing guide. -->

- **Feature:** [<feature-name>](../SKILL.md) · **Kind:** prompt
- **What it checks:** one sentence.

## Fixture
The prompt given to the fresh agent, word for word:

> You are an agent at the root of the repository <worktree>. Follow features/<feature-name>/SKILL.md …

Fixture files (if any): `fixtures/<case-name>/…`

## Setup
1. Steps to prepare the worktree, e.g. replace or remove files, or copy `fixtures/<case-name>/` over the worktree root.
2. Commit the setup in the worktree.

## Checklist
1. Observable pass/fail item.
2. **No unexpected file changes:** `git status` in the worktree shows only …

## Last run
*(Not run yet.)*

<!-- When run:
- **Date:** YYYY-MM-DD · **Agent under test:** e.g. Claude subagent · **Judge:** user / agent
- **Result:** PASS / FAIL (n/m items)

| # | Result | Notes |
|---|---|---|
| 1 | PASS | |

**Feedback** (one entry per failed item): Expected / Observed / Evidence / Likely cause. -->
