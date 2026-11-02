# 0021. Human in the loop: review and approval

- **Status:** Accepted
- **Date:** 2026-11-02
- **Tags:** philosophy, features

## Decision
A human (me) stays **in the loop most of the time**, especially at the start.

A **review and approval system** will be built. It **explains changes and their consequences** and **lets me give feedback**.

A design process worth adopting is the **5-80-15 split**:
- **5%:** the human gives the first instruction.
- **80%:** the AI gets most of the way to a finished feature.
- **15%:** the AI comes back to the human for review before finishing the rest.

## Related decisions
- Depends on: 0002, 0019
- Affects: 0014 (review is an early safeguard), 0015 (costs attention), 0022
