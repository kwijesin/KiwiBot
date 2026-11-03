# Review: T06, review format

- **Task:** T06 · **Status:** ⏸ Awaiting review · **Date:** 2026-11-03
- **Commits:** see the T06 commit on `main`
- **Tier:** 3 (plan + result)

## What changed
- [template.md](template.md): the review template, with a header (task, status, date, commits, tier) and eight sections. The last section is Outcome, which is filled in at close.
- [README.md](README.md) for `docs/reviews/`: how files are named (`Txx-…`, `Mx-…`) and a table of reviews.
- Decision [0031](../decisions/0031-review-format.md), "Review format", **Proposed**, added to the decisions index.
- [M0-bootstrap.md](M0-bootstrap.md): the first review written with the template.
- T06 set to `⏸`, with both done-when boxes ticked.

## Why
T06 resolves D14 (what a review contains). It gives every later task, and the T12 task-execution workflow, one fixed format. The commits and tier header fields make reviews faster: you can open the diff and see at a glance what kind of approval is needed.

## Consequences
- On acceptance:
  - D14 is marked **Decided → 0031**;
  - rule 8 in `AGENTS.md` points to the template instead of listing headings;
  - `docs/README.md` and `README.md` mention the template.
- T12 builds on this template.

## Test results
None (interim rule: no tests before T08).

## Approval needed
- Tier 3: accept 0031 and the template.
- Tier 2: accept the M0 review ([M0-bootstrap.md](M0-bootstrap.md)), which has two open questions of its own.

## Done without approval (tier 1)
- Task status change (T06 → `⏸`).

## Open questions
None beyond those in the M0 review.

## Outcome
*(Filled in when the task is closed.)*
