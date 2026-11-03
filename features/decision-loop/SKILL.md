---
name: decision-loop
description: >-
  Turns raw input from the user (a paragraph, chat message, transcript or a
  task like "make decisions about X") into Proposed KiwiBot decisions. It checks
  them against existing decisions and the deferred register, lists their
  consequences, asks numbered questions, and repeats until the user is
  satisfied. Use whenever new intent, direction or a decision comes in, or when
  work needs a decision that doesn't exist yet.
metadata:
  type: prompt
  status: draft
  approval_tier: "1"
  model_class: frontier
  model_needs: file_read,file_write
  decisions: "0001,0019,0026,0028"
  depends_on: ""
---

# Decision loop

## Purpose
Steps 1–2 of the self-improvement pipeline (0019): a decision comes in, it's checked for consequences, questions are asked, and this repeats until there's a satisfactory set of decisions. This is the same process as the planning rounds in `docs/history/planning/`, turned into a repeatable feature.

## Inputs
- **The raw input**, word for word. Don't summarize it yet.
- `docs/decisions/README.md` (index), the decisions related to the input, and `docs/decisions/deferred.md`.
- [references/consequence-checklist.md](references/consequence-checklist.md)
- [references/loop-record-template.md](references/loop-record-template.md)

## Steps
1. **Intake.**
   - Copy the loop record template to `docs/decisions/planning/loop-YYYY-MM-DD-<slug>.md`.
   - Paste the raw input into it word for word.
   - If the input came from a task, note the task ID.
2. **Gather context.**
   - Read the decisions index.
   - Read every decision whose title, tags or topic touch the input, and the decisions they depend on.
   - Read `deferred.md`.
3. **Break the input into candidates.** Each distinct statement or intent in the input becomes **exactly one** of:
   - **New:** nothing covers it yet.
   - **Supersede NNNN:** it changes an accepted decision. Accepted decisions aren't edited; a new decision supersedes them (`docs/decisions/README.md`).
   - **Resolves Dxx:** it answers a deferred item.
   - **Defer:** it's real but can wait. Give a revisit trigger.
   - **Already covered by NNNN:** give the pointer and draft nothing.

   Record every candidate in the loop record, with the words from the input it came from.
4. **Check consequences.** Run each candidate through the [consequence checklist](references/consequence-checklist.md). A consequence that needs its own decision becomes a new candidate; go back to step 3 for it. Record the consequences in the loop record.
5. **Draft.** This is all tier 1 under 0028:
   - **New, Supersede, Resolves:** write a decision file from `docs/decisions/0000-template.md`. Use the next free number, status **Proposed**, and fill in the related decisions. Add a Proposed row to the index.
   - **Defer:** add a row to `deferred.md` with the next free D-number, its source and a revisit trigger.
   - Keep each decision to one choice. Split rather than bundle.
6. **Ask.** Reply to the user with:
   - a short summary of what was drafted, as a list of decision numbers with one line each, plus any deferrals and "already covered" items;
   - the main knock-on effects;
   - **numbered questions**, each with a recommended answer the user can accept by number. Only ask what the user needs to decide. Don't ask about what the decisions already settle.

   Then **stop and wait**.
7. **Loop.**
   - Apply the user's answers to the drafts and the loop record.
   - Re-check consequences for what changed, not for everything.
   - If anything new comes up, go to step 6 again.
   - Repeat until the user says the set is satisfactory, or no open questions remain and the user confirms.
8. **Close.** Only on the user's **explicit acceptance** (0028):
   - set the accepted decisions to **Accepted**, in each file and in the index;
   - mark each resolved deferred item **Decided → NNNN**;
   - write the outcome in the loop record;
   - mark any rejected drafts `Rejected` in their file and the index, rather than deleting them;
   - suggest the next step: a synthesis summary (T10) if several decisions changed, or plan → task (T11) to turn them into work.

## Output
- Proposed (later Accepted) decision files and index rows.
- `deferred.md` rows.
- A loop record in `docs/decisions/planning/` with the input, candidates, consequences, questions, answers and outcome.
- A chat message per round with the summary, knock-on effects and numbered questions.

## Rules
- **Never set a decision to Accepted without the user's explicit acceptance** (0028). Silence, or approval from another agent, doesn't count.
- Don't edit accepted decisions; supersede them. The exception is typos and broken links (tier 1).
- Don't execute anything the decisions imply, such as code, tasks or doc rewrites. That's for plan → task (T11) and task execution.
- Quote the user's words when recording where a candidate came from. Don't put words in the user's mouth.
- If the input is ambiguous, ask rather than guess. A question with a recommended answer is cheap for the user (0015).
