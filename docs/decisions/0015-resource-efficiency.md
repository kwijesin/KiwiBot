# 0015. Resource efficiency and trade-offs

- **Status:** Accepted
- **Date:** 2026-11-02
- **Tags:** philosophy, architecture
- **Revised:** 2026-11-02 (round 1 cascade)

## Decision
KiwiBot should be **partially optimized for token efficiency**.

The resources KiwiBot consumes are:
- **tokens**,
- **human attention** (mine),
- **local compute**, and
- eventually **real cash**, as hardware is added.

Some automations may trade attention for tokens, and vice versa.

**For now, KiwiBot runs without token or attention metering.** Letting KiwiBot check its own token use, and metering human attention, are likely ways to improve efficiency later. That's left for a future decision.

## Related decisions
- Depends on: 0005, 0007
- Affects: 0019
