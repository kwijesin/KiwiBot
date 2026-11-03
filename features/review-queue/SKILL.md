---
name: review-queue
description: >-
  Lists KiwiBot's review queue: every task awaiting the user's review, with a
  link to its review note, what needs approval and any open questions. Use at
  the start of a session, or when the user asks what's waiting for review.
metadata:
  type: prompt
  status: draft
  approval_tier: "1"
  model_class: any
  model_needs: file_read
  decisions: "0028,0029,0031"
  depends_on: ""
---

# Review queue

## Purpose
Show the user everything waiting for their review, so they can approve or give feedback in one pass (0029).

## Inputs
- `docs/tasks/task-list.md`
- `docs/reviews/` (one review note per task or milestone)

## Steps
1. Read `docs/tasks/task-list.md`. Find every task whose status is `⏸ Awaiting review`.
2. For each one, find its review note in `docs/reviews/`: `Txx-*.md` for a task, `Mx-*.md` for a milestone.
3. Also include any milestone review in `docs/reviews/` with status `⏸ Awaiting review`.
4. From each review note, take:
   - the **Approval needed** items, with their tiers;
   - the **Open questions**, keeping their numbers.
5. If a `⏸` task has no review note, say so. That breaks the rule in 0029.

## Output
If the queue is empty, reply with one line: "The review queue is empty."

Otherwise, give one block per item, oldest task ID first:

```
### T07: Style framework v0
Review: docs/reviews/T07-style-framework.md
Approval needed:
- Tier 3: accept 0032 …
Open questions:
1. …
```

## Rules
- **Read only.** Don't change any file, and don't approve, close or start anything.
- Quote the review notes rather than rewording them.
