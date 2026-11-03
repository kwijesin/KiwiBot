# Review: T05, initial feature types and conventions

- **Task:** T05 · **Status:** ☑ Done · **Date:** 2026-11-03

## What changed
- New decision [0030](../decisions/0030-initial-feature-types-and-conventions.md), status **Proposed**, added to the decisions index. It sets out:
  - **Feature types:** prompt feature, markdown data and script. Service, app, hardware integration and MagicMirror module are named as later types.
  - **Scripting language:** Python 3.11+ for M1, standard library first.
  - **Casing:** `kebab-case` for folders, files and feature names; `snake_case` for data keys; `UPPER_SNAKE_CASE` for environment variables; each language's own style inside code.
  - **External dependencies:** every external resource is recorded in a register.
- New [docs/dependencies.md](../dependencies.md), the external dependencies register, which you asked for. It lists Python 3.11+, Git, GitHub (the private repo) and the frontier build agent, with MagicMirror² as planned. It's linked from `README.md` and `docs/README.md`.
- T05 set to `⏸`. Two of its three done-when boxes are ticked.

## Why
T05 asks for just enough feature types and conventions for M1. Python fits the likely early runtime work, such as speech-to-text (D21), text-to-speech (D23) and local models, and it's already installed. You asked for the dependencies register so that everything KiwiBot relies on is visible in one place.

## Consequences
- T07 (style framework) builds on these three feature types and casing rules.
- T08 (testing framework) uses Python for script tests. Picking the test runner (e.g. `pytest` or the standard library's `unittest`) is part of T08 and goes in `dependencies.md` if it's external.
- D15 and D16 stay partly open: languages for services and apps, and the later feature types.
- On acceptance:
  - D15 and D16 are marked "partly decided → 0030";
  - `AGENTS.md` gets a short conventions section and links to `dependencies.md`.

## Test results
None (interim rule: no tests before T08).

## Approval needed
Tier 3 (0028): accepting 0030.

## Done without approval (tier 1)
- Task status change (T05 → `⏸`).

## Open questions
1. The `python` on your PATH is the one bundled with Espressif's tools (`C:\Espressif\tools\python`, 3.11.15). It works, but installing packages into it could interfere with ESP-IDF. Should KiwiBot scripts use a separate Python, e.g. a project virtual environment or a standard Python install, once the first dependency is needed? This doesn't block 0030.

## Outcome
Approved by the user in the chat on 2026-11-03. 0030 accepted, D15 and D16 marked partly decided, and `AGENTS.md` updated. Open question 1 answered: use a separate Python install with a per-project virtual environment. This was added to 0030 and `dependencies.md`.
