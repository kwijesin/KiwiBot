# 0035. Inbox v0: a folder of text files

- **Status:** Accepted
- **Date:** 2026-11-03
- **Tags:** features, implementation

## Decision
The first version of the inbox (0034) is a **folder of plain text files**, `inbox/` at the repo root. It's markdown data (0030), with a README (0032).

Items get in two ways:
1. **The user drops in a file.** Any plain text file (`.txt` or `.md`) with any name. No format or front matter is required.
2. **The user triggers a capture skill** from any chat-style interface to KiwiBot. The skill writes the user's words, verbatim, to `inbox/YYYY-MM-DD-HHMM-<slug>.md`, with front matter for the date and source.

Inbox items are **committed to git** (0006). The capture skill commits and pushes only its new file, with the message `inbox: <slug>`. This is an exception to the two-commits-per-task rule (D07 interim), because a capture isn't a task.

## Related decisions
- Depends on: 0006, 0030, 0032, 0034
- Affects: D07 (a commit kind outside tasks)

---

## Optional sections

### Options considered *(optional)*
1. **`inbox/` at the root.** The most visible place to drop a file. Chosen.
2. **`docs/inbox/`.** Tidier, but the inbox isn't documentation.
3. **Not committed (git-ignored).** More private, but items would only exist on one machine, with no history.

### Consequences *(optional)*
- Because items are committed, the user can also drop a file in from the GitHub app or website. Triage must `git pull` first.
- Later sources (voice, 0018; the phone and PC apps, 0008) write into the same folder, or replace it when the task system exists (0016).
