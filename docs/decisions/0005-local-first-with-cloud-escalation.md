# 0005. Local-first, with frontier models for important tasks

- **Status:** Accepted
- **Date:** 2026-11-02
- **Tags:** architecture
- **Revised:** 2026-11-02 (round 1 cascade)

## Decision
KiwiBot uses **local agents first** for day-to-day operation.

It uses **frontier cloud models for important tasks**, such as self-improvement. This needs a system for escalating certain features or tasks to stronger models.

**For now, frontier models are used for all core programming.** What triggers escalation is deferred to a future decision.

This replaces the earlier "local-first with optional cloud models" decision, where cloud use was opt-in by policy with a hard `local_only` switch.

## Related decisions
- Depends on: 0004 (self-improvement is the main escalation case)
- Affects: 0007

---

## Optional sections

### Context *(optional)*
KiwiBot will hear conversations and control devices. Privacy, reliability during internet outages and running cost all favour local processing, but local models are weaker than frontier models for complex reasoning, long tasks and changing KiwiBot's own code.

### Consequences *(optional)*
- An escalation system (model router) is needed. What triggers escalation is still open.
- Some data may need filtering before it reaches a cloud model. Carried over from the earlier decision, and still to be re-checked.
- Self-improvement depends on internet access, but day-to-day use shouldn't.
