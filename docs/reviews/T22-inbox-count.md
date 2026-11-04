# Review: T22, inbox count at session start

- **Task:** T22 · **Status:** ☑ Done · **Date:** 2026-11-03
- **Commits:** `57a8dfd`, plus the T19–T22 closing commit
- **Tier:** 3 (plan + result). Trial: part of the T19–T22 set, reviewed together (T13, retrospective input 3).

## What changed
- [features/review-queue/SKILL.md](../../features/review-queue/SKILL.md): it reads `inbox/`, and a new step 6 counts the items and the parked ones. The output now always ends with `Inbox: N items waiting (M parked).` or `The inbox is empty.` The empty-queue line now *starts* the output instead of being the whole reply. The description and `decisions` (now including 0036) are updated. Its status (`active`) and tier (1) are unchanged.
- [features/review-queue/tests/mixed-queue.md](../../features/review-queue/tests/mixed-queue.md): three inbox fixture items (two waiting, one parked), and checklist item 8 for the count line.

## Why
0036 ("a session start also reports a one-line count of waiting items, right after the review queue"). `task-runner` step 1 and the session-start rule (0029) both run `review-queue`, so no other file needed to change.

## Consequences
- Every session start, and every task-runner step 1, now shows the inbox count.
- Item 8 adds coverage for the new behaviour. Items 1–7 are unchanged.

## Test results
**mixed-queue: PASS (8/8).** A fresh subagent ran it in a throwaway worktree. It quoted T90's approval items and questions exactly, flagged T91's missing note, and ended with `Inbox: 2 items waiting (1 parked).` The worktree was unchanged.

## Approval needed
- Tier 3: accept the change to `review-queue`. Its declared `approval_tier` stays 1 (0033).

## Done without approval (tier 1)
- T22 set to `◐`, then `⏸`.

## Open questions
None.

## Outcome
**Approved** 2026-11-03, as one set with T19–T22 (the feature-level approval trial). The user: "approved for 1-4, lets use it for something". The `review-queue` change accepted; its tier stays 1.
