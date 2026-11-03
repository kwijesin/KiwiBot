---
name: synthesis
description: >-
  Writes a KiwiBot round summary: what changed in the decisions since the
  last round, how it fits together, deferred items added or resolved, knock-on
  effects with a suggested next action for each, and docs that no longer
  match. Use after one or more decision loops have closed, or when the user
  asks for a round summary or "what's changed".
metadata:
  type: prompt
  status: active
  approval_tier: "1"
  model_class: frontier
  model_needs: file_read,file_write
  decisions: "0001,0019"
  depends_on: "decision-loop"
---

# Synthesis

## Purpose
Steps 2–3 of the planning process ([docs/decisions/planning/README.md](../../docs/decisions/planning/README.md)): summarize a round of decisions, then follow each change through to its knock-on effects. This keeps the decision set coherent as it grows one loop at a time (0001, 0019).

## Inputs
- **Scope.** By default, everything since the last round summary. You can also be given an explicit range, e.g. "0025–0027".
  - Find the last summary: the highest `round-NN-summary.md` in `docs/history/planning/` or `docs/decisions/planning/`. Its **Covers** line gives the last decision it included.
  - In scope: decisions after that, plus any earlier decision revised, superseded or rejected since; loop records in `docs/history/decision-loops/` closed since; and rows in `docs/decisions/deferred.md` added or resolved since.
- The decisions in scope, and the decisions they depend on or affect.
- `docs/decisions/deferred.md`, the previous round summary, and the docs listed in its "docs that no longer match" section.
- [references/round-summary-template.md](references/round-summary-template.md)

## Steps
1. **Set the scope** as above. List the decisions in scope and their statuses. Proposed decisions are included and labelled as Proposed.
2. **Read** everything in scope, plus the decisions they touch.
3. **Write** `docs/decisions/planning/round-NN-summary.md` from the template, where NN is the next round number:
   - **What changed:** one table row per change, with its decisions.
   - **The picture now:** a short narrative of how the changes fit together and what KiwiBot's working process or architecture now looks like. Only cover what this round changed.
   - **Deferred changes:** items added, resolved or partly resolved.
   - **Knock-on effects and new questions:** numbered. Each one ends with a **suggested next action**, one of:
     - **decision-loop:** give the text to feed in;
     - **plan → task (T11):** say what work it implies;
     - **defer:** give a revisit trigger;
     - **none:** it's already handled; say where.
   - **Docs that no longer match:** a table of each doc and how it conflicts.
   - **Decision map:** only if the structure of the decision tree changed.
4. **Cascade.** Reply to the user with the knock-on effects and their suggested actions, numbered so the user can answer by number. Then **stop**.

## Output
- `docs/decisions/planning/round-NN-summary.md`.
- A chat message listing the knock-on effects and suggested actions.

## Rules
- **Don't edit decisions, tasks, `deferred.md` or other docs.** Changes go through `decision-loop` (decisions, deferrals) or plan → task (work). That way every change has one owner.
- Every statement cites its decision numbers in brackets, e.g. (0028), so it can be traced.
- Report, don't decide. Where something is unclear or conflicting, make it a knock-on question.
- Once the user has worked through the knock-on effects, the summary is moved to `docs/history/planning/` with an **Archived** note at the top, matching rounds 1 and 2.
