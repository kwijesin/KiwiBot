# 0033. A feature's approval tier is set when it's accepted

- **Status:** Accepted
- **Date:** 2026-11-03
- **Tags:** process, features
- **Supersedes:** 0028 rule 5, for features only

## Decision
A feature's approval tier is the `approval_tier` declared in its `SKILL.md` (0032). It takes effect when the user **accepts the feature** (0028 rule 3). That acceptance is the decision that sets the tier, so no separate decision is needed.

- The review asking for acceptance must state the declared tier under "Approval needed" (0031).
- Changing an accepted feature's tier is a change to that feature, approved like any other feature change (tier 3).
- Kinds of change that aren't features, such as the lists in 0028 rules 1 and 4, are still only relaxed by a new decision (0028 rule 5).

## Related decisions
- Depends on: 0021, 0025, 0028, 0031, 0032
- Affects: 0028 (rule 5 now applies only to kinds of change that aren't features)

---

## Optional sections

### Context *(optional)*
`review-queue` was accepted at tier 1, but read-only features aren't on the 0028 tier 1 list. Synthesis (T10) would be in the same position. Writing a separate decision for every feature's tier would cost more of the user's attention (0015) and add no safety, because the user already sees and accepts the tier with the feature.

### Consequences *(optional)*
- `review-queue` and `decision-loop` (both tier 1) are confirmed retroactively. Both were accepted with their tiers shown.
- The style guide's `approval_tier` field and the Approval section of `AGENTS.md` point here.
