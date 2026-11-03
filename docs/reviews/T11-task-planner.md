# Review: T11, plan → task feature

- **Task:** T11 · **Status:** ☑ Done · **Date:** 2026-11-03
- **Commits:** `12aa4b3`, plus the closing commit
- **Tier:** 3 (plan + result)

## What changed
- [features/task-planner/SKILL.md](../../features/task-planner/SKILL.md): a prompt feature. Status `draft`, **declared tier 1** (it only adds `☐ Todo` tasks, which are on the 0028 tier 1 list), frontier model, depends on `decision-loop`. Its steps:
  1. read the source;
  2. check it's settled, and stop with a `decision-loop` suggestion if not;
  3. write a short plan;
  4. split the work into S or M tasks from the template;
  5. add them as `☐ Todo` with the next free IDs;
  6. present them for approval and stop;
  7. apply the answer (rejected tasks become `✕ Dropped`).
- [docs/tasks/template.md](../tasks/template.md): a new optional **Approval** line. It defaults to tier 3, and existing tasks count as tier 3.
- [docs/tasks/README.md](../tasks/README.md): points to the feature.
- T11 set to `⏸`.

## Why
0019 steps 3–4: decisions become a plan, then tasks. With `decision-loop` and `synthesis`, three of the four loop features now exist. T12 (the task-execution workflow) is the last.

## Consequences
- The round 3 items 4.8 (T08 replay input) and 4.9 (doc sync), and the two pending decision loops, are left for the first end-to-end runs (T13), as the user asked.
- The task template change is a markdown data format change, so it's listed under approval below.

## Test results
None. No demo, at the user's request: the first end-to-end runs of the loop (T13) will exercise it.

## Approval needed
- Tier 3: accept the `task-planner` feature, **declared tier 1** (0033).
- Tier 3: accept the optional **Approval** line in the task template.

## Done without approval (tier 1)
- Task status change (T11 → `⏸`).

## Open questions
1. Should it be `active` on acceptance, like the others?

## Outcome
Approved by the user in the chat on 2026-11-03 ("task planner can go active, continue"). `task-planner` set to `active` (tier 1). The task template's Approval line was accepted with it.
