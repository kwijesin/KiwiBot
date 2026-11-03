# Review: T09, decision-loop feature

- **Task:** T09 · **Status:** ⏸ Awaiting review · **Date:** 2026-11-03
- **Commits:** see the T09 commit on `main`
- **Tier:** 3 (plan + result)

## What changed
- [features/decision-loop/SKILL.md](../../features/decision-loop/SKILL.md): a prompt feature (status `draft`, tier 1, frontier model) with eight steps:
  1. intake into a loop record;
  2. gather context;
  3. break the input into candidates (New / Supersede / Resolves Dxx / Defer / Already covered);
  4. check consequences;
  5. draft Proposed decisions and deferred rows;
  6. ask numbered questions with recommended answers, then stop;
  7. loop on the answers;
  8. close only on the user's explicit acceptance.
- [references/consequence-checklist.md](../../features/decision-loop/references/consequence-checklist.md): 13 checks, covering dependencies, conflicts, knock-on decisions, deferred items, approval, testing, models, resources, style, security, external dependencies, tasks and docs.
- [references/loop-record-template.md](../../features/decision-loop/references/loop-record-template.md): the working file for one run, saved as `docs/decisions/planning/loop-YYYY-MM-DD-<slug>.md`.
- [docs/decisions/planning/README.md](../decisions/planning/README.md): points to the feature and to where loop records live.
- [docs/decisions/README.md](../decisions/README.md): adds a **`Rejected`** status for Proposed decisions the user turns down. They're kept rather than deleted.
- T09 set to `⏸`.

## Why
0019 steps 1–2 and 0022: the first piece of the self-improvement loop. It's the planning process from rounds 1–2 (and how decisions were made in T03–T07), turned into a repeatable feature that any input can enter (0026).

## Consequences
- Loop records keep each raw input word for word, which makes T08's replay test possible: feed in an original planning paragraph and compare the result.
- The feature's tier is **1**, because running it only creates drafts and questions. Accepting a decision is still tier 3, and step 8 enforces that.
- On acceptance, rule 6 in `AGENTS.md` ("don't decide silently") will say to run `decision-loop`.
- The `Rejected` status changes the decisions data format. That's why it's listed under approval below.

## Test results
None. The replay test moved to T08.

## Approval needed
- Tier 3: accept the `decision-loop` feature.
- Tier 3: accept the new `Rejected` decision status.

## Done without approval (tier 1)
- Task status change (T09 → `⏸`).

## Open questions
1. When accepted, should `decision-loop` stay `draft` until T08 tests it, or become `active` now? `review-queue` went active without a test.
2. Should closed loop records stay in `docs/decisions/planning/`, or move to `docs/history/planning/` like the round summaries? I'd move them on close, so `planning/` only holds open loops.

## Outcome
*(Filled in when the task is closed.)*
