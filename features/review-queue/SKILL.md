---
name: review-queue
description: >-
  Lists KiwiBot's review queue: every task awaiting the user's review, with a
  link to its review note, what needs approval and any open questions, then a
  one-line count of items waiting in the inbox. Use at the start of a session,
  or when the user asks what's waiting for review.
metadata:
  type: prompt
  status: active
  approval_tier: "1"
  model_class: any
  model_needs: file_read
  decisions: "0028,0029,0031,0036"
  depends_on: ""
---

# Review queue

## Purpose
Show the user everything waiting for their review, so they can approve or give feedback in one pass (0029).

## Inputs
- `docs/tasks/task-list.md`
- `docs/reviews/` (one review note per task or milestone)
- `inbox/` (0036)

## Steps
1. Read `docs/tasks/task-list.md`. Find every task whose status is `⏸ Awaiting review`.
2. For each one, find its review note in `docs/reviews/`: `Txx-*.md` for a task, `Mx-*.md` for a milestone.
3. Also include any milestone review in `docs/reviews/` with status `⏸ Awaiting review`.
4. From each review note, take:
   - the **Approval needed** items, with their tiers;
   - the **Open questions**, keeping their numbers.
5. If a `⏸` task has no review note, say so. That breaks the rule in 0029.
6. **Inbox count.** Count the files in `inbox/` other than `README.md`. Of those, count the parked ones: `status: parked` in their front matter (0036).

## Output
If the queue is empty, start with one line: "The review queue is empty."

Otherwise, give one block per item, oldest task ID first:

```
### T07: Style framework v0
Review: docs/reviews/T07-style-framework.md
Approval needed:
- Tier 3: accept 0032 …
Open questions:
1. …
```

In both cases, end with one line for the inbox:
- No items at all: `The inbox is empty.`
- Otherwise: `Inbox: N items waiting (M parked).` N doesn't include parked items. Leave out `(M parked)` when M is 0, and write "1 item" for one.

## Rules
- **Read only.** Don't change any file, and don't approve, close or start anything.
- Quote the review notes rather than rewording them.
