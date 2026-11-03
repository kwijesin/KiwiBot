# Decision loop: a feature's tier is set when it's accepted

- **Started:** 2026-11-03 · **Status:** Closed
- **Source:** chat, during T10

## Input
> use option a. demo the feature

Context: this answers the T10 plan's question. Under 0028, everything starts at tier 3 apart from the tier 1 list, and only a new decision lowers a tier. `review-queue` (read-only) was accepted at tier 1, and synthesis would only write a working summary. Option (a) was: "Treat your acceptance of a feature, including its declared tier, as the decision that sets its tier. I'd make that explicit with a short decision that supersedes 0028 rule 5."

## Candidates
| # | Candidate | Kind | From the input | Draft |
|---|---|---|---|---|
| C1 | A feature's declared approval tier is set by the user's acceptance of the feature | Supersede 0028 (rule 5, in part) | "use option a" | 0033 |

## Consequences
**C1:**
- **Dependencies:** 0021 and 0025 still hold. A human still sets every tier, through an explicit acceptance (0028 rule 3).
- **Conflicts:** 0028 rule 5 ("a tier is lowered only by a new decision"). 0033 supersedes it for features only. Kinds of change that aren't features, like the rule 1 and rule 4 lists, still need a decision.
- **Approval:** the review that asks to accept a feature must state its declared tier, so acceptance is informed. Otherwise a tier could be lowered without being noticed.
- **Existing features:** this confirms `review-queue` (tier 1) and `decision-loop` (tier 1) retroactively. Both were accepted with their tiers shown.
- **Style and conventions:** the style guide's `approval_tier` field should point to 0033.
- **Docs:** the Approval section of `AGENTS.md` and the style guide. List only; update them on acceptance.
- **Testing, models, resources, security, external dependencies, tasks:** nothing.

## Rounds
### Round 1
**Questions asked:**
1. Later lowering an accepted feature's tier: is that a change to the feature (approved as usual, at tier 3), rather than a new decision? *Recommended:* yes.
2. Must a review that asks to accept a feature state its declared tier under "Approval needed"? *Recommended:* yes.

**Answers:**
1. "that can be just a feature edit rather than a decision, yes"
2. "yes as well to a review stating tier"

**Changes made:** none needed. Both answers match the draft.

## Outcome
Closed 2026-11-03. **0033 accepted.** 0028 now has a "Partly superseded by 0033" line. `AGENTS.md`, the style guide and the review template now point to 0033. Suggested next step: none. The round 3 summary already covers 0033.
