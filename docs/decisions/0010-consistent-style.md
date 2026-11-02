# 0010. Consistent style within and across feature systems

- **Status:** Accepted
- **Date:** 2026-11-02
- **Tags:** philosophy, standards

## Decision
KiwiBot's systems and features can range from **full compiled apps** to **prompt files stored in plain folders**.

They should keep:
- **a consistent style between features that use the same system**: folders with folders, apps with apps, and so on;
- **some consistency between features that use different systems**, such as choosing camelCase or snake_case across the different programming levels.

## Related decisions
- Depends on: 0004
- Affects: 0011
