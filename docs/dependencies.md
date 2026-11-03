# External Dependencies

Every external resource KiwiBot relies on: runtimes, tools, services and hosted accounts ([0030](decisions/0030-initial-feature-types-and-conventions.md)). Add, change or remove a row in the same commit as the change that causes it.

## In use

| Resource | Version / constraint | What it's used for | Decision | Since |
|---|---|---|---|---|
| Python | 3.11+, standalone install, per-project virtual environment (not a tool-bundled interpreter) | M1 scripts | 0030 | 2026-11-03 |
| Git | any recent | Version control and development history | 0006 | 2026-11-02 |
| GitHub | private repository `kwijesin/KiwiBot` | Remote for development history | 0006 | 2026-11-02 |
| Agent Skills format | [specification](https://agentskills.io/specification) | Format of every feature folder (`SKILL.md`) | 0032 | 2026-11-03 |
| Frontier agent (currently Claude, via Claude Code) | n/a | Builds KiwiBot; all core programming | 0005, 0020, 0022 | 2026-11-02 |

## Planned (decided, not yet in use)

| Resource | What it will be used for | Decision |
|---|---|---|
| MagicMirror² | Mirror display platform | 0009 |
