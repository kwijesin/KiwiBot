# Review: T19, inbox folder v0

- **Task:** T19 · **Status:** ☑ Done · **Date:** 2026-11-03
- **Commits:** `ce5c07f`, plus the T19–T22 closing commit
- **Tier:** 3 (plan + result). Trial: the plan was approved for T19–T22 as one set, and the result is reviewed with them in one combined review (T13, retrospective input 3).

## What changed
- [inbox/README.md](../../inbox/README.md): the inbox. It says what belongs there (human-written only, verbatim), the two ways in (drop a file, or capture), the captured item format, and how triage parks or moves items.
- [docs/history/inbox/README.md](../history/inbox/README.md): where triaged items land, and the front matter triage adds (`triaged`, `route`, `route_ref`).
- [style-guide.md](../standards/style-guide.md): an Inbox row in the markdown data table, noting that it lives at the root (0035).
- `AGENTS.md` (map row), `README.md` (layout), `docs/README.md` and `docs/history/README.md`: list the inbox.

## Why
0034 and 0035, via T13's inbox decision loop. This partly resolves D03.

## Consequences
- The READMEs link to `inbox-capture` and `inbox-triage`, which T20 and T21 create.
- Every file in `inbox/` except `README.md` counts as an item. T21 and T22 rely on that.

## Test results
None. This is markdown data with no behaviour of its own. It's exercised by the T20–T22 test cases.

## Approval needed
- Tier 3: accept the inbox folder and its format (in the combined T19–T22 review).

## Done without approval (tier 1)
- T19 set to `◐`, then `⏸`.

## Open questions
None.

## Outcome
**Approved** 2026-11-03, as one set with T19–T22 (the feature-level approval trial). The user: "approved for 1-4, lets use it for something". The inbox folder and its format accepted.
