# 0031. Review format

- **Status:** Proposed
- **Date:** 2026-11-03
- **Tags:** process

## Decision
Every review note uses [docs/reviews/template.md](../reviews/template.md).

- **Header:** task, status, date, commits (hashes) and approval tier.
- **Sections, in order:**
  - What changed
  - Why
  - Consequences
  - Test results
  - Approval needed
  - Done without approval (tier 1)
  - Open questions (numbered)
  - Outcome (filled in at close)
- Every section is kept; an empty one says "None".
- Milestone reviews use the same template and are named `Mx-short-name.md`.

The template is changed by editing it, which is tier 3 under 0028, like the working rules.

## Related decisions
- Depends on: 0021, 0028, 0029
- Affects: 0019 (step 5 ends in a review)
- Resolves: D14
