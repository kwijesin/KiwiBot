# Review: T04, bootstrap workflow

- **Task:** T04 · **Status:** ⏸ Awaiting review · **Date:** 2026-11-02

## What changed
- New decision [0029](../decisions/0029-bootstrap-workflow.md), "Bootstrap workflow: tasks and reviews", status **Proposed**, added to the decisions index.
- T04 set to `⏸ Awaiting review`. Its first done-when box is ticked.
- This file is the first review note kept in `docs/reviews/`. Earlier tasks (T01–T03) were reviewed in the chat only.

## Why
D06 is resolved: before KiwiBot's own task and review systems exist, the markdown task list and review-note files are the workflow. Git conventions (D07) were deferred to the end of M1 by the user, so they aren't covered here.

## Consequences
- T06 puts its review template in `docs/reviews/`.
- On acceptance, `AGENTS.md` gets:
  - the review-queue step: a session that starts fresh checks the `⏸` tasks first;
  - the task-list rules: no renumbering or deleting, `✕ Dropped` with a reason, and a note saying where a task came from;
  - `docs/reviews/` in the map.

## Test results
None. Under the interim rule in `AGENTS.md`, no tests are needed before T08 unless a task's done-when list asks for one.

## Approval needed
Tier 3 (0028): accepting 0029.

## Done without approval (tier 1)
- Task status change (T04 → `⏸`).

## Open questions
None.

## Outcome
*(Filled in when the task is closed.)*
