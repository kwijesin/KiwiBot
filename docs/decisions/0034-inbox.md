# 0034. An inbox for human-written rough ideas

- **Status:** Accepted
- **Date:** 2026-11-03
- **Tags:** features, process

## Decision
KiwiBot has an **inbox**: a landing place for rough, unfinished ideas, dropped in from any source (0026).

- **Everything in the inbox is human-written.** An item's body is the user's own words, verbatim: typed, written in a file, or transcribed from speech. Agents may add metadata (e.g. date, source), but never edit, summarize or tidy the body.
- **Agents don't add ideas to the inbox.** An idea that comes out of an agentic process is already more polished, and it has its own routes: Proposed decisions, `☐ Todo` tasks and deferred rows (0028 rule 4).
- The inbox is a **buffer in front of the pipeline** (0019). Items wait there until they're triaged into it (0036). Direct intake, e.g. the user talking to an agent at the root, still works as before.

## Related decisions
- Depends on: 0019, 0026, 0028
- Affects: 0016 (some items will be the user's own to-dos), 0018 (voice is a future source)
- Partly resolves: D03 (decision intake details)

---

## Optional sections

### Context *(optional)*
Chosen by the user as the item for T13, the first end-to-end run of the loop. Raw input: [loop-2026-11-03-inbox](../history/decision-loops/loop-2026-11-03-inbox.md).

### Consequences *(optional)*
- An inbox for agent-originated ideas is deferred (D39).
- Triage sends items to a cloud model, so the user writes them knowing that (D34).
