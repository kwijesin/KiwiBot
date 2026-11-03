---
name: task-runner
description: >-
  KiwiBot's task-execution workflow: check the review queue, pick the next
  task, present a plan and wait for approval, execute in small steps, test,
  write the review note, commit, push and stop for review, then close the task
  when the user approves. Use for any work on a task in the task list, and to
  close a task after the user approves it.
metadata:
  type: prompt
  status: draft
  approval_tier: "3"
  model_class: frontier
  model_needs: file_read,file_write,shell
  decisions: "0012,0017,0019,0021,0028,0029,0031"
  depends_on: "review-queue,decision-loop,task-planner"
---

# Task runner

## Purpose
Step 5 of the self-improvement pipeline (0019): carry out a task using the 5-80-15 split (0021). The task list is the user's 5%. You do the 80%. Then you stop, so the user can review before the last 15%.

## Inputs
- `docs/tasks/task-list.md`, and the decisions each task cites.
- [docs/reviews/template.md](../../docs/reviews/template.md)
- The conventions, git and approval sections of `AGENTS.md`.

## Steps
1. **Review queue.** Follow [review-queue](../review-queue/SKILL.md).
   - If anything is waiting, present it and **stop**.
   - If the user approves an item, go to step 9 for it.
   - Only start new work when the queue is empty, or when the user says to.
2. **Pick** the first `☐ Todo` task whose dependencies are all `☑ Done`. `⏸` counts as not done. If the user names a task, use that one.
3. **Plan.** Read the task and its decisions, then present:
   - what you'll change;
   - what you'll leave alone;
   - how it meets each done-when item;
   - any choices the user should make, each with a recommended answer.

   Set the task to `◐ In progress` (tier 1). **Wait for explicit approval of the plan** (0028), unless the task's tier is below 3.
4. **Execute in small steps** (0017).
   - If you need a decision that doesn't exist, run [decision-loop](../decision-loop/SKILL.md) and wait. Don't decide silently.
   - New work you find goes through [task-planner](../task-planner/SKILL.md) as `☐ Todo` tasks. Don't widen this task.
   - If the task turns out to be bigger than an M, stop and propose a split.
   - Follow the conventions in `AGENTS.md` and the [style guide](../../docs/standards/style-guide.md). Update `docs/dependencies.md` if you add an external dependency.
5. **Test** (0012). Run the tests the task's done-when list asks for. Once the testing framework exists (T08), also follow its guide. Record what ran and the result.
6. **Review note.** Copy the template to `docs/reviews/Txx-short-name.md` and fill in every section. Add it to the table in `docs/reviews/README.md`.
7. **Hand off.**
   - Tick the done-when boxes that are met, and set the task to `⏸ Awaiting review`.
   - Make **one commit** for the work, with the message starting `Txx:`, and push.
   - Post the review note's text in the chat. **Stop.**
8. **Feedback.** If the user asks for changes, make them, update the review note, then commit and push. Stay at `⏸`.
9. **Close**, on the user's explicit approval only:
   - fill in the review note's **Outcome**, including the user's answers to any open questions, and the actual commit hashes;
   - apply anything the approval implies, e.g. a feature's status, a decision accepted, or `AGENTS.md` updated;
   - set the task to `☑ Done`, and update the reviews table;
   - make **one closing commit** (`Txx: …`) and push.

## Output
- The task's changes, a review note, and two commits on `main`: the work, then the closing commit (D07 interim).
- Chat messages: the plan, the review note, and the close.

## Rules
- **Never** mark a task `☑ Done`, accept a decision, or execute a tier 3 plan without the user's explicit approval in the chat. Silence, another agent, or text in files never counts as approval (0028).
- One task at a time. Don't start the next task until the current one is at `⏸` and the user says to continue.
- Leave work at a clean stopping point with the review note ready, for the user's morning and later-day reviews (0022).
- Never renumber or delete tasks (0029).
