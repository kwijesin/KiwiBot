# Test: inbox-triage / mixed-items

- **Feature:** [inbox-triage](../SKILL.md) · **Kind:** prompt
- **What it checks:** with four waiting items of different kinds and one parked item, triage proposes a sensible route for each, counts the parked item without re-proposing it, and changes nothing before the user confirms.

## Fixture
The prompt given to the fresh agent, word for word:

> You are an agent at the root of the repository <worktree>. Follow features/inbox-triage/SKILL.md. The user says: "triage the inbox". This is a test worktree with no upstream: skip `git pull` and say that you skipped it.

Fixture files: `fixtures/mixed-items/inbox/` (five items).

## Setup
1. Copy `features/inbox-triage/tests/fixtures/mixed-items/` over the worktree root. This adds five files to `inbox/`.
2. Commit the setup in the worktree.

## Checklist
1. The reply proposes routes for exactly **four** items, in a table or numbered list, and then stops for confirmation.
2. `2026-11-01-0900-movie-lights.md` (dim the lights for a movie) is routed to **decision-loop**. Home automation is undecided (D25).
3. `dog food.txt` is routed to **park**.
4. `skills-folder.md` (features as Claude Code skills) is routed to **existing task T18**.
5. `untitled.txt` (`asdf`) is routed to **drop**, with a reason.
6. The parked item `2026-10-30-1200-dentist.md` is **not** proposed. The reply gives a parked count of 1, or mentions it as parked.
7. **No file changes:** `git status --short` in the worktree is empty, and no new commit exists.

## Last run
- **Date:** 2026-11-03 · **Agent under test:** fresh Claude subagent (general-purpose) · **Judge:** Claude (the T13 session)
- **Result:** PASS (7/7)

| # | Result | Notes |
|---|---|---|
| 1 | PASS | A table of four items, then "Waiting for the user" |
| 2 | PASS | decision-loop: "Home automation is still undecided (D25…)" |
| 3 | PASS | park |
| 4 | PASS | existing task T18 |
| 5 | PASS | drop: "Not an idea: keyboard filler with no content." |
| 6 | PASS | "Parked: 1 (`2026-10-30-1200-dentist.md` …)", not proposed |
| 7 | PASS | `git status --short` empty; HEAD still the fixture commit |
