# 0023. Open source vs custom

- **Status:** Accepted
- **Date:** 2026-11-02
- **Tags:** philosophy, architecture

## Decision
Systems may use custom or open-source solutions.

- **Readily available and easy to integrate** (e.g. a TTS engine): use the open-source option.
- **A toss-up** (e.g. Obsidian as the default markdown viewer vs building our own): decide case by case, with its own decision.
- **Otherwise:** most everything else is **custom**.

## Related decisions
- Depends on: 0004, 0007
- Affects: 0009 (MagicMirror is open source), 0010, 0011
