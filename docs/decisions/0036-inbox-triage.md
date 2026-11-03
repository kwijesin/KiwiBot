# 0036. Inbox triage

- **Status:** Accepted
- **Date:** 2026-11-03
- **Tags:** features, process

## Decision
Items leave the inbox (0034) through **triage**, a prompt feature.

1. **When:** when the user asks (e.g. "triage the inbox"). A session start also reports a one-line count of waiting items, right after the review queue (0029).
2. **Routes:** the agent proposes exactly one route per item:
   - **decision-loop:** the item's text becomes its raw input, word for word;
   - **task-planner:** for work that's already decided;
   - **existing task:** add it as a note to a named task;
   - **park:** the user's own to-dos, kept in the inbox until there's a "my tasks" list (0016, D13);
   - **drop:** with a one-line reason.
3. **Confirmation:** the user confirms or changes the routes in one reply. Nothing runs before that (0028 rule 3).
4. **Afterwards:** each routed or dropped item moves to `docs/history/inbox/`, with front matter recording the triage date and where it went. Parked items stay in `inbox/`.

## Related decisions
- Depends on: 0016, 0019, 0028, 0029, 0034, 0035
- Affects: D13 (parked items are the first "my tasks")

---

## Optional sections

### Consequences *(optional)*
- Each route still goes through its own feature's approval gates. Triage only chooses where the item goes.
- The session-start count needs a small change to `review-queue` or `task-runner` step 1.
