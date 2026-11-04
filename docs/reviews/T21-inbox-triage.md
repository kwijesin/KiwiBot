# Review: T21, inbox-triage feature

- **Task:** T21 · **Status:** ☑ Done · **Date:** 2026-11-03
- **Commits:** `927f5d1`, plus the T19–T22 closing commit
- **Tier:** 3 (plan + result). Trial: part of the T19–T22 set, reviewed together (T13, retrospective input 3).

## What changed
- [features/inbox-triage/SKILL.md](../../features/inbox-triage/SKILL.md): a prompt feature with status `draft`, **declared tier 3**, `model_class: frontier`, needing `file_read`, `file_write` and `shell`, and depending on `decision-loop` and `task-planner`. Its steps:
  1. pull;
  2. list the items (parked items are only counted);
  3. propose one route per item in a table, then **stop**;
  4. apply the user's reply;
  5. do the quick routes: park, a task note, drop;
  6. archive with `git mv` and add the triage front matter;
  7. commit `inbox: triage YYYY-MM-DD` and push;
  8. run the decision-loop and task-planner routes one at a time.
- [features/inbox-triage/tests/mixed-items.md](../../features/inbox-triage/tests/mixed-items.md), with fixtures: four waiting items (a decision, a to-do, one covered by T18, junk) and one parked item.

## Why
0036, with 0034 (bodies never edited) and 0035 (pull first). Built via T13.

## Consequences
- **Item order.** Items are archived and committed **before** their decision-loop or task-planner routes run. Those features stop for the user, so waiting on them would hold the commit open. `route_ref` for a task-planner item is filled in once the task IDs exist.
- `inbox: triage` commits are a second commit kind outside tasks. They're a D07 input (T13 retrospective input 1).
- Decision-loop and task-planner output started by triage isn't in the triage commit. Where it gets committed is round 3's open item 4.4 (tier 1 work outside a task).
- `AGENTS.md` gets inbox-triage in "How to work" when it's accepted.

## Test results
**mixed-items: PASS (7/7).** A fresh subagent ran it in a throwaway worktree. It proposed decision-loop, park, T18 and drop for the four items, and gave a reason for the drop. It counted the parked item without proposing it, and stopped. The worktree was unchanged.

## Approval needed
- Tier 3: accept `inbox-triage` at its **declared `approval_tier` of 3** (0033), and set its status to `active`.

## Done without approval (tier 1)
- T21 set to `◐`, then `⏸`.

## Open questions
None.

## Outcome
**Approved** 2026-11-03, as one set with T19–T22 (the feature-level approval trial). The user: "approved for 1-4, lets use it for something". `inbox-triage` accepted at tier 3, status `active`.
