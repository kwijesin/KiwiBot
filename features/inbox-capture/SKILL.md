---
name: inbox-capture
description: >-
  Captures one of the user's rough ideas into KiwiBot's inbox, word for word:
  writes a new file in inbox/, then commits and pushes only that file. Use when
  the user says "capture: …", "inbox: …", "add to the inbox" or similar, from
  any chat-style interface.
metadata:
  type: prompt
  status: active
  approval_tier: "0"
  model_class: any
  model_needs: file_write,shell
  decisions: "0034,0035"
  depends_on: ""
---

# Inbox capture

## Purpose
Get the user's idea into the inbox in their own words, with as little friction as possible (0034, 0035). The inbox holds only human-written text, so this feature is a careful copy, not a writer.

## Inputs
- The user's message.
- [inbox/README.md](../../inbox/README.md): the captured item format.

## Steps
1. **Find the idea.** It's the text after the trigger (e.g. after "capture:"), or the text the user points to. If it's unclear where the idea starts or ends, ask. Don't guess.
2. **Copy it exactly.** Keep spelling, punctuation, capitals, line breaks and typos. Don't fix, summarize, reword or add anything to the body.
3. **Name the file** `inbox/YYYY-MM-DD-HHMM-<slug>.md`, in local time. `<slug>` is 2–5 `kebab-case` words taken from the idea. If the name exists, add `-2`.
4. **Write the file:**

   ```markdown
   ---
   captured: YYYY-MM-DDTHH:MM
   source: <the interface, e.g. chat (Claude Code)>
   ---

   <the idea, exactly as given>
   ```
5. **Commit only that file**, so anything else staged stays out: `git add -- <file>`, then `git commit -m "inbox: <slug>" -- <file>`.
6. **Push:** `git push`. If it fails, say so and leave the commit in place.
7. **Reply** in one or two lines: the file path, and that it's committed and pushed.

## Output
- One new file in `inbox/`, and one commit, `inbox: <slug>`, containing only that file.
- A short confirmation in the chat.

## Rules
- **Never change the body** (0034). Front matter is the only thing you add.
- Never capture your own ideas or suggestions, only the user's words (0034). If the user asks you to "capture that" about something you wrote, say the inbox is for their words and offer to draft a Proposed decision or task instead.
- One idea per call, one file per idea. If the user gives several clearly separate ideas, ask whether to capture them as one item or several.
- Don't triage, act on or comment on the idea. That's [inbox-triage](../inbox-triage/SKILL.md).
- **Tier 0:** no approval or notice. The user asked for it, the content is their own, and the result is shown in the chat.
