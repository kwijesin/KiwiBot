# 0024. Building is part of using

- **Status:** Accepted
- **Date:** 2026-11-02
- **Tags:** philosophy

## Decision
**Building is a core part of using KiwiBot**, not a separate phase. Instead of switching back and forth between building and using, KiwiBot grows while it's in use. This is why the self-improvement tools come first.

## Related decisions
- Depends on: 0002
- Affects: 0004, 0019, 0022

---

## Optional sections

### Context *(optional)*
The idea started as a personal assistant and digital interface. Thinking about how it would actually be built and used showed a problem with "build it, then use it". Each time I tried to use it for something new, I'd find a missing feature and have to:

1. go back into building mode to add it,
2. take the systems down and restart them,
3. set everything up again,
4. use it for a day, then find the next missing feature,

and repeat. Making building part of using the system removes that cycle.
