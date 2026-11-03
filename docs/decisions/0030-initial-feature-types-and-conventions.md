# 0030. Initial feature types and conventions

- **Status:** Accepted
- **Date:** 2026-11-03
- **Tags:** standards, architecture

## Decision
This decision defines just enough for M1. Early features are mostly prompt-based (0027), with some scripts.

### Feature types
| Type | What it is |
|---|---|
| **Prompt feature** | An agent instruction set: markdown prompt files that an agent follows to do a job, e.g. the decision loop or plan → task. Most of M1 is this type. |
| **Markdown data** | Structured markdown documents that features read and write, e.g. decisions, tasks and reviews. |
| **Script** | A small command-line program, run by an agent or a person, for work that has become repeatable (0007). |

Expected later types are **service**, **app**, **hardware integration** and **MagicMirror module**. Each is defined by a new decision when it's first needed.

### Scripting language
- **Python 3.11+** for M1 scripts.
- Scripts use the standard library unless a dependency is really needed. Dependency management is decided with the first script that needs a dependency.
- Scripts run from a **separate, standalone Python install** in a **per-project virtual environment**, never from interpreters bundled with other tools (e.g. ESP-IDF's).
- Languages and runtimes for services and apps (e.g. JavaScript for the MagicMirror module, 0009) are decided when they're first needed.

### Casing
Names that cross between parts are consistent. Code follows its own language's style.

| What | Convention | Example |
|---|---|---|
| Folders, feature names, markdown and other non-code files | `kebab-case` | `decision-loop/`, `task-list.md` |
| Data keys (YAML, JSON, markdown front matter) | `snake_case` | `approval_tier` |
| Environment variables | `UPPER_SNAKE_CASE` | `KIWIBOT_DATA_DIR` |
| Python | `snake_case` for modules, functions and variables; `PascalCase` for classes | `task_list.py`, `TaskList` |
| JavaScript | `camelCase`; `PascalCase` for classes | `showTimer` |

Python module files are `snake_case` so they can be imported. That's the one exception to `kebab-case` file names.

### External dependencies
Every external resource KiwiBot relies on is recorded in [docs/dependencies.md](../dependencies.md): runtimes, tools, services and hosted accounts. A change that adds, removes or changes one updates that file in the same commit.

## Related decisions
- Depends on: 0007, 0010, 0011, 0013, 0027
- Affects: 0012 (Python tests, T08), 0020, 0023
- Partly resolves: D15 (M1 language, casing), D16 (initial feature types)
