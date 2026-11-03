---
name: task-planner
description: >-
  Turns accepted KiwiBot decisions, round-summary items marked "plan → task",
  or a direct instruction from the user into a short plan and small,
  well-bounded tasks in the task list. Use after a decision loop closes, after
  a synthesis round, or when the user asks for work to be broken into tasks.
metadata:
  type: prompt
  status: draft
  approval_tier: "1"
  model_class: frontier
  model_needs: file_read,file_write
  decisions: "0016,0017,0019,0028,0029"
  depends_on: "decision-loop"
---

# Task planner

## Purpose
Steps 3–4 of the self-improvement pipeline (0019): turn decisions into a plan, then into tasks someone can pick up. Tasks are kept small enough to review in one sitting (0017).

## Inputs
- **The source**, one of:
  - one or more **accepted** decisions;
  - round summary items marked "plan → task";
  - a direct instruction from the user.
- The decisions the source cites, and the decisions they depend on.
- `docs/tasks/task-list.md`, [docs/tasks/template.md](../../docs/tasks/template.md) and `docs/tasks/README.md`.

## Steps
1. **Read** the source and everything it cites. Read the task list, so you know existing tasks, free IDs and milestones.
2. **Check the source is settled.**
   - If the work needs a decision that doesn't exist, or the source is a Proposed decision, **stop**. Say what's undecided and suggest a `decision-loop` input.
   - If an existing task already covers the work, point to it instead of duplicating it.
3. **Plan.** In 3–6 lines: what work the source implies, which files, features or docs it touches, and in what order.
4. **Split into tasks**, following the template:
   - **Size:** S or M only. Split anything bigger (L) into separate tasks.
   - **One well-bounded change per task**: one review and one pair of commits (0029).
   - **Depends on:** only real dependencies, including on existing tasks.
   - **Done when:** items someone can check, not "works well".
   - **Decisions:** the decisions it serves.
   - **Approval:** the tier, tier 3 by default (0028). Use another tier only where an accepted decision or feature tier allows it.
5. **Add the tasks** to `docs/tasks/task-list.md`:
   - status `☐ Todo` (tier 1);
   - the next free IDs;
   - in the right milestone;
   - a note in each: "Added by task-planner from <source>".
6. **Present** to the user: the plan, then each new task as ID, title, size and dependencies, in one line each. Ask for approval of the set. **Stop.**
7. **Apply the user's answer.**
   - Approved tasks stay as they are.
   - Edits are made as asked.
   - Rejected tasks are marked `✕ Dropped` with the reason. They're never deleted (0029).

## Output
- A plan, given in the chat.
- New `☐ Todo` tasks in the task list.
- A chat message listing the tasks for approval.

## Rules
- **Don't execute any task**, and don't change decisions or `deferred.md`.
- Don't renumber or reorder existing tasks (0029). New tasks may depend on existing ones.
- Never invent requirements. Every task traces back to its source.
- Prefer fewer, clearer tasks. If unsure whether to split, split at the review boundary: could the user approve one part without the other?
