---
name: inbox-triage
description: >-
  Triages KiwiBot's inbox: proposes one route per item (decision-loop,
  task-planner, an existing task, park or drop), waits for the user to confirm,
  then routes the items and archives them. Use when the user asks to triage or
  process the inbox, or to go through their captured ideas.
metadata:
  type: prompt
  status: active
  approval_tier: "3"
  model_class: frontier
  model_needs: file_read,file_write,shell
  decisions: "0034,0035,0036"
  depends_on: "decision-loop,task-planner"
---

# Inbox triage

## Purpose
Move the user's rough ideas out of the inbox and into the self-improvement loop (0036), without losing or rewording any of them (0034). Triage only chooses where each item goes. Each route's own feature does the work, with its own approval gates.

## Inputs
- Every file in `inbox/` except `README.md`. Each file is one item.
- [inbox/README.md](../../inbox/README.md) and [docs/history/inbox/README.md](../../docs/history/inbox/README.md): the item and triage formats.
- To choose routes: `docs/decisions/README.md`, `docs/decisions/deferred.md` and `docs/tasks/task-list.md`.

## Steps
1. **Pull** (`git pull`), since items can be added from other devices (0035).
2. **List the items.** Items with `status: parked` in their front matter are only counted, unless the user asks to revisit them.
3. **Propose one route per item:**
   - **decision-loop:** new intent, or something that needs a decision.
   - **task-planner:** work that existing accepted decisions already cover.
   - **existing task Txx:** an existing task already covers it. The item becomes a note on that task.
   - **park:** the user's own to-do, not KiwiBot work, until there's a "my tasks" list (D13).
   - **drop:** empty, a duplicate, or not an idea. Give a one-line reason.

   Present a table: the number, the file, the first line of the item (quoted), the route, and why in a few words. Add the parked count. Then **stop and wait** (0036, 0028 rule 3).
4. **Apply the user's reply.** They may confirm all, or change routes by number. Nothing runs before this reply.
5. **Do the quick routes:**
   - **park:** add `status: parked` and `parked: YYYY-MM-DD` to the item's front matter. The item stays in `inbox/`.
   - **existing task:** add `- **Inbox (YYYY-MM-DD):** "<item text, verbatim>"` under that task's Notes in the task list.
   - **drop:** nothing more.
6. **Archive.** `git mv` every routed or dropped item to `docs/history/inbox/` (same file name), and add the triage front matter: `triaged`, `route`, `route_ref`. For decision-loop items, `route_ref` is the loop record name it will get (`loop-YYYY-MM-DD-<slug>`). For task-planner items, it's `task-planner`, and it's updated to the task IDs once they exist.
7. **Commit and push** only the inbox moves, parks and task notes: `git commit -m "inbox: triage YYYY-MM-DD"`.
8. **Run the remaining routes one at a time.**
   - For **decision-loop**, the item's body is the raw input, word for word, and its source is the archived item's path.
   - For **task-planner**, the item's body is a direct instruction from the user.

   Each feature stops for the user as usual. Say which routed items are still waiting to be run.

## Output
- A proposal table in the chat, and after confirmation:
  - parked items marked in `inbox/`;
  - routed and dropped items in `docs/history/inbox/`;
  - task notes;
  - one `inbox: triage` commit;
  - decision loops or task drafts started.

## Rules
- **Never edit an item's body** (0034). Front matter is the only thing you add or change.
- Never run a route, move a file or commit before the user confirms the routes.
- One route per item. If an item holds several ideas, propose the most fitting route and say so in "why". Don't split it.
- Never delete an item. Dropped items are archived like the rest.
- **Tier 3:** the user's confirmation of the routes is the plan approval. Each route's result is approved through that route's own feature.
