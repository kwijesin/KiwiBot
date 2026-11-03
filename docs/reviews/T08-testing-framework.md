# Review: T08, testing framework v0

- **Task:** T08 · **Status:** ☑ Done · **Date:** 2026-11-03
- **Commits:** `0a3cc2e`, plus the closing commit
- **Tier:** 3 (plan + result)

## What changed
- [docs/standards/testing-guide.md](../standards/testing-guide.md): the testing guide.
  - **Prompt tests** are case files with four sections: Fixture, Setup, Checklist and Last run.
  - Each runs in a **throwaway `git worktree`**, optionally at an older commit, with every `features/*/tests/` folder removed so the agent can't see the checklist.
  - A **fresh agent** runs the fixture prompt. A **judge**, which can be the user or an agent, marks each item.
  - A case passes only if every item passes. Every failure records **Expected / Observed / Evidence / Likely cause** (0012).
  - **Script tests** use the standard library's `unittest`, with no new dependency.
- [docs/standards/test-case-template.md](../standards/test-case-template.md): the template for test cases.
- [features/feature-test/SKILL.md](../../features/feature-test/SKILL.md): a prompt feature that runs a feature's cases and records results. Status `draft`, **declared tier 1** (it only writes results), frontier model, needs `shell`. It never fixes a feature during a run, and never edits a case to make it pass.
- **Test cases:**
  - [review-queue / mixed-queue](../../features/review-queue/tests/mixed-queue.md), with fixtures: **run, PASS 7/7**.
  - [decision-loop / replay-feature-tier](../../features/decision-loop/tests/replay-feature-tier.md): replays the 0033 input at commit `dfed91a`. Written, not run.
  - [synthesis / round-2-replay](../../features/synthesis/tests/round-2-replay.md): runs over 0025–0027 with the round 2 summary removed. Written, not run.
  - [task-planner / changelog-decision](../../features/task-planner/tests/changelog-decision.md): uses a fixture decision, 0090 "keep a changelog". Written, not run.
- T08 set to `⏸` with all its done-when boxes ticked. T12's last done-when box is ticked too, because this task was run with `task-runner`.

## Why
0012 and 0013: a consistent way to test each feature type, with output an agent can act on. It works without the sandbox (D02) by using worktrees.

## Consequences
- **Round 3 item 4.8 is resolved.** The decision-loop replay uses the closed 0033 loop's input instead of planning paragraphs that weren't kept. The task list records the change.
- **Found during the run:** the first worktree setup left the case file, with its checklist, visible to the agent under test. Hiding `tests/` is now a required setup step in the guide and in `feature-test`.
- **T13** is the first task to use testing. It will run the other three cases.
- **Proposed working-rule change** (tier 3, so not applied yet): the guide says that **from T13 on**, a new or changed feature comes with at least one test case. If accepted, the "no tests until T08" line in `AGENTS.md` is replaced with that rule.

## Test results
**review-queue / mixed-queue: PASS (7/7).** A fresh Claude subagent ran it, and this session judged it. It listed T90 with both approval items and both questions quoted exactly, flagged T91's missing review note, left out T92 and T93, kept them in order, and made no file changes (`git status` was empty). The details are in the case's Last run section.

## Approval needed
- Tier 3: accept the testing guide and the test case template.
- Tier 3: accept the `feature-test` feature, **declared tier 1** (0033).
- Tier 3: accept the four test cases. Three of them run in T13.
- Tier 3: the working-rule change above, for `AGENTS.md`.

## Done without approval (tier 1)
- Task status changes: T08 `◐` → `⏸`; T12's done-when box ticked.

## Open questions
1. Should `feature-test` be `active` on acceptance?
2. Should the "from T13 on, every new or changed feature comes with a test case" rule go into `AGENTS.md` now?

## Outcome
Closed on 2026-11-03. The user said "activate feature test … and then lets get an end to end run of the loop going". `feature-test` set to `active` (tier 1), with the guide, template and cases accepted with it. Open question 2 (the "from T13 on" testing rule in `AGENTS.md`) wasn't answered, so `AGENTS.md` is unchanged. T13 tests its own outputs under its done-when list anyway.
