# Review: T10, synthesis/cascade feature

- **Task:** T10 · **Status:** ☑ Done · **Date:** 2026-11-03
- **Commits:** `9179412`, plus the closing commit
- **Tier:** 3 (plan + result)

## What changed
- [features/synthesis/SKILL.md](../../features/synthesis/SKILL.md): a prompt feature. Status `draft`, **declared tier 1**, frontier model, depends on `decision-loop`. It:
  - sets the scope (by default, everything since the last round summary);
  - writes `docs/decisions/planning/round-NN-summary.md`;
  - lists knock-on effects, each with a suggested action (decision-loop / plan → task / defer / none), then stops.

  It never edits decisions, tasks or docs itself.
- [references/round-summary-template.md](../../features/synthesis/references/round-summary-template.md), modelled on the round 2 summary.
- **First real run of `decision-loop`**, on your "option a" answer:
  - [loop record](../history/decision-loops/loop-2026-11-03-feature-tier-on-acceptance.md), still open with 2 questions;
  - draft [0033](../decisions/0033-feature-tier-set-on-acceptance.md): a feature's tier is set when the user accepts the feature (supersedes 0028 rule 5 for features only). **Proposed.**
- **Demo:** a fresh agent following only `SKILL.md` wrote [round-03-summary.md](../decisions/planning/round-03-summary.md), covering 0028–0033.

## Why
0019 and the planning process: synthesis keeps the decision set coherent as decisions arrive one loop at a time. 0033 settles the tier question raised in the T10 plan. `review-queue` and `decision-loop` were accepted at tier 1, and synthesis would be in the same position.

## Consequences
- Decision changes now always go through `decision-loop`, and synthesis only reports. Every change has one owner.
- The demo turned up **9 knock-on effects** (section 4 of the round 3 summary). The most useful:
  - **#8:** T08's replay test assumes your original planning paragraphs are in `docs/history/planning/`, but only the round summaries are there. The test needs a different input.
  - **#3:** six working rules exist only in reviews and `AGENTS.md`, with no decision number.
  - **#2:** there's no way to record a partial supersession, like 0033 superseding part of 0028.
  - **#9:** several docs have fallen behind, e.g. `README.md` still says "building starts with M0" and lists decisions 0001–0027.
- **One overstatement in the demo:** #1 says tier 1 isn't valid for `decision-loop` until 0033 is accepted. In fact, `decision-loop` only does things on the 0028 tier 1 list, so it was already valid. Only `review-queue` and `synthesis` depend on 0033.

## Test results
None (T08). The demo above is a demonstration, not a test. It followed the template, cited decisions throughout, edited no other files, and its findings check out apart from the overstatement noted above.

## Approval needed
- Tier 3: accept the `synthesis` feature, **declared tier 1** (per 0033, once accepted).
- Tier 3: accept 0033. First answer the 0033 loop's questions:
  1. Lowering an accepted feature's tier later counts as a feature change (tier 3), not a new decision. *Recommended:* yes.
  2. A review asking to accept a feature must state its declared tier. *Recommended:* yes.
- The round 3 knock-on effects (1–9 in the summary): what to do with each. Suggested answers:
  - 1–6: `decision-loop` inputs. I'd batch 2, 3, 4 and 6 into one loop, since they're all about how decisions and working rules are recorded, and run 5 on its own.
  - 7: defer.
  - 8 and 9: become tasks once T11 exists.

## Done without approval (tier 1)
- Task status change (T10 → `⏸`).
- Proposed decision 0033 and its open loop record.
- The round 3 summary (a working file in `planning/`).

## Open questions
1. Should synthesis be `active` on acceptance, like the other two?
2. For the round 3 knock-on effects, is the batching suggested above OK? If so, I'd run those loops before T11. Or should T11 come first, so 8 and 9 can become tasks straight away?

## Outcome
Approved by the user in the chat on 2026-11-03.
- `synthesis` accepted and set to `active` (tier 1).
- 0033: both loop questions answered "yes". 0033 accepted and the loop closed. `AGENTS.md`, the style guide and the review template updated.
- Round 3 knock-on effects: go ahead with the suggestions. 7 deferred as D38. The decision loops for 2, 3, 4, 6 and for 5 are pending. 8 and 9 go through T11.
- "go straight to 11": T11 comes before those loops.
