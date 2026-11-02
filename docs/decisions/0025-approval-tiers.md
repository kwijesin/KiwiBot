# 0025. Approval tiers

- **Status:** Accepted
- **Date:** 2026-11-02
- **Tags:** philosophy, features

## Decision
How much approval a change needs **varies**, and it will change over time.

- **Early on, more approval is needed.** Some features that would make less review safe (such as KiwiBot sandboxing itself) don't exist yet.
- As KiwiBot's scope and capability grow, **automated approval can be relaxed**. An **early decision** sets the initial approval rules, and **later decisions relax the automated approval tiers**.
- **Approval tiers are a design consideration for every new feature.** Some features won't need approval at all, and some may be prioritized for review.

## Related decisions
- Depends on: 0004, 0021
- Affects: 0012, 0019, 0027
