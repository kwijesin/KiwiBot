# Test: synthesis / round-2-replay

- **Feature:** [synthesis](../SKILL.md) · **Kind:** prompt
- **What it checks:** run over decisions 0025–0027 without the round 2 summary available, it finds round 2's main knock-on effects.

## Fixture
The prompt given to the fresh agent, word for word:

> You are an agent at the root of the repository <worktree>. Follow features/synthesis/SKILL.md with the explicit scope "decisions 0025–0027", treating round 1 as the previous round. Write the summary file, then reply with your step 4 message. Do not run git.

## Setup
1. Delete `docs/history/planning/round-02-summary.md` and `docs/decisions/planning/round-03-summary.md` from the worktree, so the expected answer can't be copied.
2. Commit the setup in the worktree.

## Checklist
1. A summary file `docs/decisions/planning/round-02-summary.md` exists, built from the template, with a Covers line naming 0025–0027.
2. **What changed** has a row for each of 0025, 0026 and 0027.
3. A knock-on effect says the **initial approval rules (the "early decision" of 0025) are needed now**, on the critical path before the loop can run.
4. A knock-on effect raises **bootstrapping**: where tasks, reviews or decisions live before KiwiBot's own systems exist.
5. A knock-on effect says the **repo root must be agent-readable** (an entry point for an agent at the root, from 0026).
6. Every knock-on effect ends with a **suggested action** of one of the four kinds.
7. **No other changes:** `git status --short` in the worktree shows only the new summary file.

## Last run
*(Not run yet. Runs in T13.)*
