# 0004. An orchestration that improves itself

- **Status:** Accepted
- **Date:** 2026-11-02
- **Tags:** architecture, philosophy, features

## Decision
KiwiBot is an orchestration of **agents, scripts, services, hardware and UI apps**, not a single program.

It should be able to **improve itself while it runs**. That may need specific software features that let it view, restart and modify its own services, apps and so on.

## Related decisions
- Depends on: 0002
- Affects: 0005, 0006, 0007
