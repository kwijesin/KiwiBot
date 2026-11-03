# Test: task-planner / changelog-decision

- **Feature:** [task-planner](../SKILL.md) · **Kind:** prompt
- **What it checks:** given one accepted decision (a fixture: keep a changelog), it produces a short plan and small, sensible tasks in the right format, and doesn't execute them.

## Fixture
The prompt given to the fresh agent, word for word:

> You are an agent at the root of the repository <worktree>. Follow features/task-planner/SKILL.md. The source is the accepted decision docs/decisions/0090-changelog.md. Run steps 1–6, then stop and reply with your step 6 message. Do not run git.

Fixture files: `fixtures/changelog-decision/docs/decisions/0090-changelog.md`.

## Setup
1. Copy `features/task-planner/tests/fixtures/changelog-decision/` over the worktree root.
2. Commit the setup in the worktree.

## Checklist
1. The reply has a **plan** of 3–6 lines before the task list.
2. **New `☐ Todo` tasks** are added to `docs/tasks/task-list.md`, using IDs after the highest existing one (no reuse) and placed in a milestone.
3. Every new task has **status, size, depends on, decisions (citing 0090), goal and done-when**, and a note "Added by task-planner from …".
4. **Sizes are S or M** only, and the work covers the decision: creating the changelog, changing task-runner's close step, and the backfill. The backfill can be its own task or part of another.
5. Done-when items are **checkable**: no "works well".
6. **Nothing is executed:** no `docs/changelog.md`, `features/task-runner/SKILL.md` unchanged, and no existing task changed or renumbered (`git diff` touches only `docs/tasks/task-list.md`).
7. The reply asks the user to **approve the set**, and stops.
8. **Judged by the user:** the tasks are sensible and small enough that the user would approve them.

## Last run
*(Not run yet. Runs in T13.)*
