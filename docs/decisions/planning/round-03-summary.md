# KiwiBot: Round 3 Synthesis

- **Round:** 3
- **Date:** 2026-11-03
- **Builds on:** [Round 2 synthesis](../../history/planning/round-02-summary.md)
- **Covers:** Decisions 0028–0033 (6 new: 5 Accepted, 1 still Proposed; none superseded in full, 0028 rule 5 partly superseded by Proposed 0033; none rejected), and decision loops closed since the last round (none closed; one open: [loop-2026-11-03-feature-tier-on-acceptance](loop-2026-11-03-feature-tier-on-acceptance.md)).

Round 2 ended planning. This round covers what building has decided since: M0's working rules (0028–0030), M1's first standards (0031, 0032), and one Proposed change to how feature tiers are set (0033). Round 2's critical-path questions are now answered: the initial approval rules (0028) and the bootstrap workflow (0029). The decision loop is now a feature and has run once. This is the first round summary written by the synthesis feature (T10), so it's also a demo of it.

---

## 1. What changed

| Change | Decisions |
|---|---|
| **Approval tiers 0–3** (plan + result, result, notify, none). Everything starts at tier 3, except a short tier 1 list (status changes other than ☑, new ☐ tasks, Proposed decisions, deferred rows, typo fixes). Only an explicit reply from the user in the chat counts as approval. A tier is lowered only by a new decision. | 0028 (new) |
| **Bootstrap workflow.** `docs/tasks/task-list.md` is the task list. There's one review note per task in `docs/reviews/`, and the review queue is every `⏸` task, checked at the start of each session. | 0029 (new) |
| **M1 feature types:** prompt feature, markdown data, script. Python 3.11+ (standalone install, per-project virtual environment), a casing convention, and a `docs/dependencies.md` register. | 0030 (new) |
| **Review format:** a fixed template with eight sections, from "What changed" to "Outcome", and a header that gives the commits and tier. | 0031 (new) |
| **Style framework v0:** every feature is an Agent Skills folder, `features/<name>/SKILL.md`. Its metadata includes the approval tier and model needs, never model names. | 0032 (new) |
| **A feature's tier is set when the user accepts the feature**, so no separate decision is needed. Kinds of change that aren't features still need a decision. | 0033 (Proposed; supersedes 0028 rule 5 for features only) |

**Working rules set in reviews, not as numbered decisions:**
- **Two commits per task:** the work, then a closing commit (D07 interim; M0 review).
- **No tests before T08**, unless a task's done-when list asks for one (`AGENTS.md`; 0012).
- **T08 moved to after T12**, and the test items for T09–T11 moved into it (T07 review).
- **Decisions have a `Rejected` status** (T09 review; `docs/decisions/README.md`).
- **Closed loop records go to `docs/history/decision-loops/`** (T09 review).
- **The docs call the owner "the user"** (M0 review).

**Features built:**
- `review-queue`: active, tier 1 (0029, 0031, 0032).
- `decision-loop`: active, tier 1 (0019, 0026, 0028).
- `synthesis`: draft, tier 1 (0001, 0019).

## 2. The picture now

**The loop as it actually runs.** The self-improvement loop (0019, 0022) is now half built:
1. **Intake.** Input comes in through the chat, from the user working with an agent at the root (0026).
2. **Decision loop.** The `decision-loop` feature turns the input into a loop record and Proposed decisions, asks numbered questions, and closes only on the user's explicit acceptance (0019, 0028).
3. **Synthesis.** This feature summarizes a round and its knock-on effects (0001, 0019).
4. **Plan → task.** Still manual (T11). Tasks go into the markdown task list under 0029's rules.
5. **Execution.** Follows `AGENTS.md`, plan first and then the work. The formal workflow is T12 (0021).
6. **Review.** The work stops at `⏸` with a review note in 0031's format, and `review-queue` presents the queue at the start of the next session (0029).
7. **Commit.** Each task is committed straight to `main` in two commits (D07 interim; 0028 rule 2).

**Features have one shape** (0010, 0032). Prompt and script features are both Agent Skills folders. Each declares its type, approval tier (0028) and model needs (0020) in front matter. The format is an existing open standard (0023), so any agent that supports skills can find the features. Claude Code needs T18 before it can. Markdown data sets (decisions, tasks, reviews) each have a README and a template (0032).

**Approval is a single human gate, with a growing tier 1 band.** Every task is still tier 3 (0028). The three features so far all declare tier 1, because running them only drafts or reads. Accepting what they draft is still tier 3 (0028, 0033). Under 0028, a tier 1 feature would need its own tier decision, because that tier isn't on the tier 1 list. 0033 (Proposed) makes the user's acceptance of the feature, with its tier shown in the review (0031), the decision that sets the tier. That would confirm `review-queue` and `decision-loop` after the fact, and cover `synthesis`.

**Still missing:** tests (0012, 0013; T08), plan → task (T11) and the execution workflow (T12). Round 2's open items about sandboxing (D02) and self-restart (D01) are unchanged (0027).

## 3. Deferred changes

| Item | Change | Decision |
|---|---|---|
| D05 | Decided → 0028 (initial approval rules) | 0028 |
| D06 | Decided → 0029 (bootstrap workflow). D07 was split off. | 0029 |
| D07 | Updated: deferred to the end of M1 (T13), with an interim rule of two commits per task straight to `main`. With branches, the closing commit also squashes the branch. | 0029 (M0 review) |
| D10 | Annotated: building is Claude-only for now. Test `AGENTS.md` with a non-Claude agent when local models come in. | 0020 (M0 review) |
| D14 | Decided → 0031 (review format) | 0031 |
| D15 | Partly decided → 0030: Python 3.11+ for M1, and casing. Languages for services and apps are still open. | 0030 |
| D16 | Partly decided → 0030: prompt feature, markdown data and script. Service, app, hardware integration and MagicMirror module are still open. | 0030 |
| D17 | Annotated: rename runtime "skills" to **tools** when it's decided, because "skill" now means a feature folder. | 0032 |
| D37 | Added: visual style, the visual half of 0011. Revisit when the first UI is built. | 0011, 0032 |

D13–D36 were created when round 2 was applied to the docs. That was round 2's cascade, so they aren't counted here.

## 4. Knock-on effects and new questions

### 4.1 0033 is still Proposed, and this feature's tier depends on it
The loop for 0033 is open, with two round 1 questions unanswered: does lowering an accepted feature's tier count as a feature change, and must a review state the feature's tier? (0033) Until it closes, 0028 rule 5 still applies in full. So `synthesis`, which declares tier 1, has no valid tier yet. Neither do `review-queue` and `decision-loop`, strictly (0028). The T10 review will also need to state the tier under "Approval needed" (0031, 0033).
**Suggested action:** decision-loop: "Continue loop-2026-11-03-feature-tier-on-acceptance. Round 1 answers: 1 yes, 2 yes. Accept 0033."

### 4.2 There's no way to record a partial supersession
0033 adds a `Supersedes: 0028 rule 5, for features only` line. The decisions README only has a whole-decision `Superseded by NNNN` status, and the template has no Supersedes line (0001). Accepted decisions aren't edited (decisions README), so once 0033 is accepted, nothing in 0028 will point a reader of rule 5 to 0033 (0028, 0033).
**Suggested action:** decision-loop: "How is a partial supersession recorded? Suggestion: the new decision carries a `Supersedes: NNNN (part)` line, and the old decision gets a `Partly superseded by NNNN (rule N)` line, which counts as a tier 1 link fix. Add both to the template and the decisions README."

### 4.3 Some working rules exist only in reviews and `AGENTS.md`
The rules listed under "Working rules set in reviews" in section 1 were approved in reviews, and `AGENTS.md` changes are tier 3 (0028), so they're legitimate. But they can't be traced to a numbered decision (0001), and some of them change data formats (the `Rejected` status) or exceptions to standing decisions (no tests before T08 vs 0012).
**Suggested action:** decision-loop: "Do working rules approved in reviews need numbered decisions? They are: two commits per task, no tests before T08, the `Rejected` status, closed loops in `docs/history/decision-loops/`, and calling the owner 'the user'. If yes, draft them. If no, say where such rules live."

### 4.4 Tier 1 work done outside a task has no review note to land in
Tier 1 changes must be listed in "the next review note" (0028 rule 4), and review notes are per task (0029, 0031). `decision-loop` and `synthesis` are tier 1 (0033) and can be run from the chat with no task open, e.g. "what's changed". It's unclear which review note lists their output, and when it's committed under two commits per task (D07 interim).
**Suggested action:** decision-loop: "Where are tier 1 changes made outside a task listed, and when are they committed? Options: (a) the next task's review note and commit; (b) a running log in `docs/reviews/`, committed on its own."

### 4.5 What `draft`, `active` and `retired` mean is undefined
The style guide lists the three feature statuses but not what they mean or what moves a feature between them (0032). `review-queue` and `decision-loop` went `active` on acceptance, with no tests (T07 and T09 reviews), while 0012 says to test everything and the test items now sit in T08 (0013). Nothing says whether `active` gates anything, e.g. whether `AGENTS.md` may point only to active features.
**Suggested action:** decision-loop: "Define the feature statuses: what draft, active and retired mean, who moves a feature between them and at what tier, and whether passing its T08 test is required for active."

### 4.6 Rounds now continue after planning
0001 describes rounds that run "until the foundation is solid enough to build on". `AGENTS.md` and `README.md` say planning is complete, but `decision-loop` and `synthesis` make rounds an ongoing part of building (0019, 0024). The planning README's cascade step still says to revise decisions with a `Revised` line. That conflicts with the decisions README ("after planning, supersede") and with `synthesis` ("don't edit decisions"). When to run a round isn't set either. `decision-loop` step 8 only says "if several decisions changed".
**Suggested action:** decision-loop: "Rounds continue during building, driven by decision-loop and synthesis. After planning, accepted decisions are only superseded, never revised. Does 0001 need superseding to say so, and when should a synthesis round run?"

### 4.7 Priority review isn't covered
0025 says "some [features] may be prioritized for review". 0028, 0031 and `review-queue` don't cover it: the queue is simply oldest task first (0029).
**Suggested action:** defer: revisit when the review queue regularly holds more than a few items, or with task system design (T14, D13).

### 4.8 T08's decision-loop replay test has no raw input to replay
T08 says to replay "one of my original planning paragraphs from `docs/history/planning/`" through `decision-loop`. That folder only holds the round 1 and round 2 summaries, not the user's raw paragraphs (0012). Loop records now keep raw input word for word (0019), but rounds 1–2 predate them.
**Suggested action:** plan → task (T11): amend T08's done-when so the replay test uses either an original paragraph the user supplies as a fixture, or the input of a closed loop record.

### 4.9 Docs have fallen behind M0 and M1
Several docs still describe the system as it was at the end of round 2 (0028–0032). See section 5.
**Suggested action:** plan → task (T11): a doc-sync task to run after 4.1–4.3 are settled, covering the docs in section 5, so it's only done once.

## 5. Docs that no longer match

Round 2's list has been resolved:
- The rename is applied. The remaining "Lulu" references are intended (0003).
- `roadmap.md`, `models.md` and `privacy-security.md` have been rewritten.
- The `0009` links have been fixed.

`architecture.md` is only partly current (see below).

| Doc | Conflict |
|---|---|
| `README.md` | Says "Building starts with milestone M0", but M0 is done and M1 is under way. Lists the decisions as "0001–0027" (now 0001–0033). Describes `history/` as planning rounds only (now also decision loops, per the T09 review). Uses the first person ("my", "me"), but the docs call the owner "the user" (M0 review). |
| `docs/README.md` | Lists the decisions as "0001–0027". Describes `history/` as planning round summaries only. |
| `AGENTS.md` | The map row for Reviews still says "format in T06". It's 0031 now. History is described as "archived planning rounds" only. The Approval section doesn't mention 0033 yet (expected on acceptance, 0033). |
| `docs/architecture.md` | In the components table, "Review and approval" is still "To be designed" (0021, 0025, D05, D06, D14), but its bootstrap form is decided (0028, 0029, 0031). The task system has a bootstrap (0029). It still says "There will be a style framework", but v0 exists (0032). It doesn't mention `features/` or the decision-loop feature. The diagram says "questions to me". |
| `docs/roadmap.md` | Phase 0 lists "0001–0027". Phase 2 has "a first review interface beyond markdown and pull requests (0021, D06)", but D06 is decided and pull requests aren't used while work goes straight to `main` (0029). |
| `docs/configuration.md` | "initial rules pending, D05": D05 is decided (0028). Feature tiers live in `SKILL.md` metadata, not configuration (0032, 0033). Uses "my approval". |
| `docs/decisions/planning/README.md` | Step 3 says to revise decisions with a `Revised` line, which conflicts with "after planning, supersede" (decisions README) and with `synthesis` rules. Its status only covers rounds 1–2. It doesn't mention the synthesis feature (expected once T10 is accepted). See 4.6. |
| `docs/decisions/README.md`, `0000-template.md` | Neither has a partial supersession or a `Supersedes` line, which 0033 uses. See 4.2. |
| `docs/decisions/0028-initial-approval-rules.md` | Rule 5 doesn't point to 0033. Pending 0033's acceptance and 4.2. |
| `docs/standards/style-guide.md` | The `approval_tier` comment cites only 0028. 0033 says it should point to 0033 (pending acceptance). Feature statuses aren't defined (4.5). |
| `docs/decisions/deferred.md` | The intro says "D13 onward came from the docs", but D37 came from 0032 (T07). |
| `docs/skills.md` | Uses "skills" for runtime tools, which conflicts with "skill" meaning a feature folder (0032). Known, and waiting on D17. |

## 6. Decision map

The structure changed: there's a new branch of working rules under approval and style. New decisions are marked `*`, and Proposed ones `(P)`.

```
0021 Human in the loop ──► 0025 Approval tiers ──► 0028 Initial approval rules*
                                                     ├─► 0029 Bootstrap workflow*  ◄── 0016, 0022
                                                     │      └─► 0031 Review format*
                                                     └─► 0033 Tier set on acceptance* (P)  ◄── 0031, 0032
                                                            (supersedes 0028 rule 5 for features)

0010 Style ──► 0011 Style framework ──┬─► 0030 Feature types & conventions*  ◄── 0007, 0027
                                      └─► 0032 Style framework v0 (Agent Skills)*  ◄── 0020, 0023, 0028, 0030
                                             └─► 0013 Testing framework (T08 tests features in this layout)
```
