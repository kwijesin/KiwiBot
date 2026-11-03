# Test: review-queue / mixed-queue

- **Feature:** [review-queue](../SKILL.md) · **Kind:** prompt
- **What it checks:** with two waiting tasks (one of them missing its review note), a pending task and a done task, the queue shows exactly the waiting ones, quotes the note, flags the missing note, ends with the inbox count, and changes nothing.

## Fixture
The prompt given to the fresh agent, word for word:

> You are an agent at the root of the repository <worktree>. Follow the instructions in features/review-queue/SKILL.md exactly, and reply with only the output it specifies. Do not modify any files.

Fixture files: `fixtures/mixed-queue/docs/tasks/task-list.md`, `fixtures/mixed-queue/docs/reviews/T90-widget-docs.md`, `fixtures/mixed-queue/docs/reviews/T93-fix-doohickey.md`, and three inbox items in `fixtures/mixed-queue/inbox/` (two waiting, one parked; added in T22).

## Setup
1. In the worktree, delete every `docs/reviews/T*.md` and `docs/reviews/M*.md`.
2. Copy `features/review-queue/tests/fixtures/mixed-queue/` over the worktree root. This replaces `docs/tasks/task-list.md`, and adds the two fixture reviews and three inbox items next to `inbox/README.md`.
3. Commit the setup in the worktree.

## Checklist
1. The output has an entry for **T90** that links or names `docs/reviews/T90-widget-docs.md`.
2. The T90 entry lists **both** approval items with their tiers: "Tier 3: accept the widget docs." and "Tier 2: accept the new glossary entry."
3. The T90 entry lists **both** open questions, numbered 1 and 2, worded as in the note.
4. The output has an entry for **T91** that says its review note is **missing**.
5. **T92** (☐ Todo) and **T93** (☑ Done) don't appear, and nor does T93's question.
6. Entries are in task-ID order (T90 before T91).
7. **No file changes:** `git status --short` in the worktree is empty after the run.
8. The output ends with the line `Inbox: 2 items waiting (1 parked).` (added in T22).

## Last run
- **Date:** 2026-11-03 (T22) · **Agent under test:** fresh Claude subagent (general-purpose) · **Judge:** Claude (the T13 session)
- **Result:** PASS (8/8). The earlier 7/7 run (T08) is in git history.

| # | Result | Notes |
|---|---|---|
| 1 | PASS | `Review: docs/reviews/T90-widget-docs.md` |
| 2 | PASS | Both items, with tiers, quoted exactly. |
| 3 | PASS | Both questions, numbered 1 and 2, quoted exactly. |
| 4 | PASS | "Review: none. T91 is at `⏸ Awaiting review` but there is no review note…" |
| 5 | PASS | T92 and T93 don't appear. |
| 6 | PASS | T90 comes before T91. |
| 7 | PASS | `git status --short` was empty. |
| 8 | PASS | Last line: `Inbox: 2 items waiting (1 parked).` |
