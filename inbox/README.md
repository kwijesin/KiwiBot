# Inbox

A landing place for the user's rough ideas ([0034](../docs/decisions/0034-inbox.md), [0035](../docs/decisions/0035-inbox-v0-folder.md)). Drop them in here when there's no time to work them through. They're triaged into the self-improvement loop later ([0036](../docs/decisions/0036-inbox-triage.md)).

## What belongs here
- **Only human-written ideas.** An item's body is the user's own words, verbatim: typed, written in a file, or transcribed from speech.
- Agents **never** add ideas here. Their ideas go in as Proposed decisions, `☐ Todo` tasks or deferred rows (0028 rule 4).
- Agents may add front matter (metadata), but **never** edit, summarize or tidy an item's body.

## Adding an item
Either:
1. **Drop in a file.** Any plain text file (`.txt` or `.md`), with any name. No format or front matter is needed. It can be added from the GitHub app or website too, since the folder is committed.
2. **Ask an agent to capture it**, e.g. "capture: …". The [inbox-capture](../features/inbox-capture/SKILL.md) feature writes the file, commits it and pushes.

### Captured item format
File name `YYYY-MM-DD-HHMM-<slug>.md`, where `<slug>` is a few `kebab-case` words from the idea:

```markdown
---
captured: 2026-11-03T14:05
source: chat (Claude Code)
---

The user's words, exactly as given.
```

## What happens next
[inbox-triage](../features/inbox-triage/SKILL.md) proposes one route per item, and runs nothing until the user confirms (0036):
- **Routed or dropped items** move to [docs/history/inbox/](../docs/history/inbox/).
- **Parked items** (the user's own to-dos, until there's a "my tasks" list, D13) stay here, with this front matter added:

```markdown
---
status: parked
parked: 2026-11-03
---
```

Every file here except this README is an item.
