# 0090. Keep a changelog

- **Status:** Accepted
- **Date:** 2026-01-01
- **Tags:** process

## Decision
KiwiBot keeps a changelog at `docs/changelog.md`.

- One entry per closed task: the date, task ID, one line on what changed, and a link to its review note.
- Entries are grouped under milestone headings (M0, M1, …).
- The task-runner feature writes the entry when it closes a task.
- Existing closed tasks (T01–T12) are backfilled once.

## Related decisions
- Depends on: 0029, 0031
