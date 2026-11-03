# Review: T12, task-execution workflow

- **Task:** T12 · **Status:** ☑ Done · **Date:** 2026-11-03
- **Commits:** `9c95ff4`, plus the closing commit
- **Tier:** 3 (plan + result)

## What changed
- [features/task-runner/SKILL.md](../../features/task-runner/SKILL.md): a prompt feature. Status `draft`, **declared tier 3**, frontier model, needs `file_read`, `file_write` and `shell`. Its steps:
  1. check the review queue;
  2. pick the next task;
  3. plan, set `◐` and wait for approval;
  4. execute in small steps, using `decision-loop` for missing decisions and `task-planner` for new work;
  5. test;
  6. write the review note;
  7. hand off: `⏸`, one commit, push, stop;
  8. handle feedback;
  9. close on approval: Outcome, `☑`, closing commit, push.
- [AGENTS.md](../../AGENTS.md): "How to work" shrinks from nine rules to four. The rules now live in `task-runner`, and the other four features are listed. The map gains a Features row. The stale "format in T06" on the Reviews row is fixed (tier 1).
- T12 set to `⏸`, with the first done-when box ticked.

## Why
0019 step 5 and 0021 (5-80-15). This is the last of the four loop features: intake and decisions (`decision-loop`), synthesis, plan → task (`task-planner`), and execution (`task-runner`).

## Consequences
- The working rules now live in one feature, and `AGENTS.md` keeps only the summary, map, conventions, git and approval sections.
- **Tier 3 is declared** because `task-runner` executes tasks, which are tier 3 by default. Its steps wait for plan approval and result approval.
- **New detail:** step 3 sets the task to `◐ In progress` while the plan waits for approval. That's a tier 1 status change, and it shows in the task list which task is under way.
- The second done-when item ("T08 is carried out using it") is checked during T08.

## Test results
None (T08). The second done-when item checks it during T08.

## Approval needed
- Tier 3: accept the `task-runner` feature, **declared tier 3** (0033).
- Tier 3: accept the `AGENTS.md` rewrite of "How to work" (it changes the working rules).

## Done without approval (tier 1)
- Task status change (T12 → `⏸`).
- Fixed the stale "format in T06" in the `AGENTS.md` map.

## Open questions
1. Should it be `active` on acceptance?
2. T12 can't close fully until T08 is carried out using it. Should I close T12 now with that item noted as "checked in T08", or keep it at `⏸` until T08 is done?

## Outcome
Approved by the user in the chat on 2026-11-03 ("activate feature test and task runner, close t12"). `task-runner` set to `active` (tier 3), and the `AGENTS.md` rewrite accepted. Its last done-when item was met by running T08 with `task-runner`.
