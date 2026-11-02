# 0029. Bootstrap workflow: tasks and reviews

- **Status:** Proposed
- **Date:** 2026-11-02
- **Tags:** process

## Decision
These rules cover how work flows until KiwiBot's own task system (0016, T15) and review system (0021) exist.

### Tasks
1. **[docs/tasks/task-list.md](../tasks/task-list.md) is the task list** until the custom task system replaces it (T15).
2. **Adding tasks.** Anyone can add a task. When an agent adds one:
   - it goes in as `☐ Todo` (tier 1 under 0028);
   - it has the same fields as the other tasks: status, size, dependencies, decisions, goal and done-when;
   - it gets the next free ID and goes in the right milestone;
   - it carries a note saying where it came from, e.g. "Added during T07".
3. **Updating tasks.**
   - Tick done-when boxes as each item is met.
   - Never renumber task IDs.
   - Never delete a task. A task that's no longer needed is marked `✕ Dropped` with a one-line reason.
   - Only the user's approval moves a task to `☑ Done` (0028).

### Reviews
4. **Each review note is a file**, `docs/reviews/Txx-short-name.md`. It's committed in the same commit as the task's work, and the same text is given in the chat. The format comes from T06; until then, use the headings in `AGENTS.md`. Feedback and approval are given in the chat (0028), and the outcome is recorded in the note's file when the task is closed.
5. **The review cycle** (0022):
   1. The agent stops at a clean point, with the task at `⏸ Awaiting review` and its review note written.
   2. The **review queue** is every `⏸` task in the task list.
   3. In a review session (morning, and again later in the day), the user goes through the queue and replies with approval or feedback.
   4. The agent then:
      - marks approved tasks `☑ Done` and records the approval in the review note;
      - turns feedback into fixes, or into new tasks;
      - plans the next task.
6. **A session that starts fresh checks the review queue first.** It only picks a new task when the queue is empty, or when the user says to.

## Related decisions
- Depends on: 0016, 0021, 0022, 0028
- Affects: 0006 (review history is kept in git), 0019
- Resolves: D06 (D07, git conventions, is deferred to the end of M1)

---

## Optional sections

### Options considered *(optional)*
1. **Review notes in the chat only.** This is simpler, but the review history is lost when a session ends, and the user can't read reviews from another device.
2. **Review notes as files in `docs/reviews/`, plus the chat.** Reviews are kept in git (0006) and can be read on GitHub. Chosen.
3. **GitHub pull requests.** Not usable while work is committed straight to `main` (D07 interim).

### Consequences *(optional)*
- T06 puts its review template in `docs/reviews/`.
- `AGENTS.md` needs a review-queue step at the start of each session.
- These rules are replaced when T15 (task system) and the review system are built.
