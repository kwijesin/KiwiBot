# Decision loop: quick-capture inbox

- **Started:** 2026-11-03 · **Status:** Closed
- **Source:** chat, task T13 (first end-to-end run of the loop; the user chose the inbox as the item)

## Input
> The inbox is going to be a landing place for rough and ready ideas to be dropped in from a variety of sources. I think a key differentiator for this inbox should probably be that the ideas inside are human-written, as a theoretical inbox coming from other agents will naturally be more "polished" if they arose from an agentic process. for the first iteration of the inbox I imagine that it will exist first as a simple folder, in which either I drop in a text file containing the rough idea, or I trigger a skill in any related chat-style interface for Kiwibot

## Candidates
| # | Candidate | Kind | From the input | Draft |
|---|---|---|---|---|
| C1 | KiwiBot has an inbox: a landing place for rough ideas from any source, and everything in it is human-written | New; partly resolves D03 | "a landing place for rough and ready ideas to be dropped in from a variety of sources", "the ideas inside are human-written" | 0034 |
| C2 | Inbox v0 is a folder of plain text files, filled by dropping in a file or by a capture skill | New | "it will exist first as a simple folder, in which either I drop in a text file containing the rough idea, or I trigger a skill in any related chat-style interface" | 0035 |
| C3 | How items leave the inbox: triage routes each one into the loop | New (knock-on of C1: an inbox needs a way out) | none; raised by the consequence check | 0036 |
| C4 | An inbox for agent-originated ideas | Defer | "a theoretical inbox coming from other agents will naturally be more 'polished'" | D39 |
| C5 | Ideas arriving by voice, phone or other apps | Already covered by 0026 (any input method), with 0018 (voice) and 0008 (apps) | "from a variety of sources" | none |

## Consequences
**C1 (0034):**
- **Dependencies:** 0026 (intake from any input) and 0019 (the pipeline). The inbox sits in front of step 1, as a buffer. Direct intake in the chat, as in this loop, still works.
- **Knock-on decisions:** the inbox needs a form (C2) and a way out (C3). "Human-written" needs a working definition: the user's words, verbatim. Do agent-added metadata or voice transcripts count? (question 3)
- **Deferred items:** partly resolves D03 (decision intake details). D03's trigger ("once the self-improvement loop is finished") is effectively firing in T13.
- **Approval:** agents already raise their own ideas through tier 1 routes (Proposed decisions, `☐ Todo` tasks, deferred rows; 0028 rule 4). Keeping them out of the inbox loses nothing.
- **Security:** rough ideas may hold private details. The repo is private (0006), but triage sends items to a cloud model (D34). Note only; the user writes the items knowing that.
- **Models, resources, external dependencies:** nothing.

**C2 (0035):**
- **Style and conventions:** a folder of user files is **markdown data** (0030). It needs a README (0032). Drop-in files can't be held to a naming or front matter rule, because the user writes them freely. The capture skill can follow one.
- **Tasks:** the inbox folder and README, and a capture prompt feature. T11 creates the tasks.
- **Git:** if items are committed, the user can also drop a file in from the GitHub mobile app or web, which is a second source for free. Captures happen outside tasks, so a capture commit is an exception to the two-commits-per-task rule (D07 interim). That's an input to D07 (question 2).
- **Approval:** the capture skill writes only the user's own words, at the user's request. A low tier fits; the tier is set when the feature is accepted (0033).
- **Testing:** a prompt test case in a worktree: the case gives a capture request and checks the file is verbatim and correctly placed.
- **Models:** any model can capture (`model_class: any`).
- **Docs:** `AGENTS.md` map, `README.md` layout, `docs/README.md`, `architecture.md` (intake).

**C3 (0036):**
- **Dependencies:** routes go to existing features: `decision-loop`, `task-planner`. Items that are the user's own to-dos have nowhere to go until the task system has a "my tasks" list (0016, D13, T14).
- **Approval:** each route starts a feature with its own approval gates, but the routing choice itself should be seen by the user before anything runs.
- **Testing:** a prompt case with fixture inbox items of each kind, checking the proposed routes and that nothing runs before confirmation.
- **Tasks:** a triage prompt feature, and a hook so a session start mentions waiting items (likely a small change to `review-queue` or `task-runner` step 1).
- **Docs:** `docs/history/README.md`, if processed items are archived there.

**C4 (D39):** revisit when agents generate ideas outside a chat with the user, e.g. scheduled runs (D04) or the task system (T14).

## Rounds
### Round 1
**Questions asked:**
1. Where does the inbox live? *Recommended:* `inbox/` at the repo root, so it's the most visible place to drop a file.
2. Are inbox items committed to git? *Recommended:* yes. The repo is private (0006), the history is kept, and the user can drop a file in from the GitHub app. The capture skill commits and pushes only its new file, as `inbox: <slug>`. That's an exception to two commits per task, recorded as a D07 input.
3. What counts as "human-written"? *Recommended:* the body is the user's own words, verbatim. Typing, a file the user wrote, or a voice transcript all count. Agents may add front matter (date, source), but never edit, summarize or tidy the body.
4. What format do dropped-in files need? *Recommended:* none. Any plain text file (`.txt` or `.md`), any name. The capture skill names its files `YYYY-MM-DD-HHMM-<slug>.md`.
5. When is the inbox triaged? *Recommended:* when the user asks ("triage the inbox"). Also, a session start reports a one-line count of waiting items, right after the review queue.
6. What routes does triage use? *Recommended:* `decision-loop`, `task-planner`, "add to an existing task", "park" (the user's own to-dos until there's a "my tasks" list, D13) and "drop". The agent proposes one route per item, and the user confirms them all in one reply before anything runs.
7. What happens to an item after triage? *Recommended:* it moves to `docs/history/inbox/`, with front matter recording the date and where it went. Parked items stay in `inbox/`.

**Answers:**
1–7. "all as reccomended."

**Changes made:** none needed. All seven answers match the drafts.

## Outcome
Closed 2026-11-03. The user: "accept all those three and the deferral".
- **Accepted:** 0034 (inbox for human-written ideas), 0035 (inbox v0: a folder of text files), 0036 (inbox triage).
- **Deferred:** D39 added (agent inbox).
- **Partly resolved:** D03 → 0034–0036.
- **Rejected:** none.
- **Inputs for D07:** capture commits (`inbox: <slug>`) are a commit kind outside tasks (0035). The user, in the T13 plan: "The one commit per task rule may require some leeway as I'm sure we'll make other tasks that require it - tasks that examine other tasks, tasks that get started and then find that it depends on a different task finishing first, etc."
- **Suggested next step:** plan → task (T11) for 0034–0036. Synthesis comes later in T13 (round 4, with D07).
