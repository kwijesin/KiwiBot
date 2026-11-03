# Review: M0, bootstrap

- **Task:** M0 (T01–T05) · **Status:** ☑ Done · **Date:** 2026-11-03
- **Commits:** `bed2e36`…`63a886d` (T01–T05)
- **Tier:** 2 (result). There's no plan to approve: this is a review of work that has already been approved task by task.

## What changed
| Task | Result | Commits |
|---|---|---|
| T01 | Private repo `kwijesin/KiwiBot`, local folder renamed, `.gitignore` | `bed2e36`, `42c5027` (user), `a761fb7` |
| T02 | [AGENTS.md](../../AGENTS.md) entry point and a one-line `CLAUDE.md`; working rules moved out of the task list | `3b089c9`, `ecd29cb` |
| T03 | [0028](../decisions/0028-initial-approval-rules.md): approval tiers 0–3, everything starts at tier 3 with a small tier 1 list (resolves D05) | `33d1f13`, `e01d12a` |
| T04 | [0029](../decisions/0029-bootstrap-workflow.md): task list rules, review notes in `docs/reviews/`, review queue (resolves D06) | `7f27fa6`, `d95744c` |
| T05 | [0030](../decisions/0030-initial-feature-types-and-conventions.md): three feature types, Python 3.11+ (standalone install, per-project virtual environment), casing; [dependencies.md](../dependencies.md) register (partly resolves D15, D16) | `9e68dec`, `63a886d` |

**Decisions made in the chat along the way**, recorded but not as numbered decisions:
- D07 (git conventions) is deferred to the end of M1. Until then, everything goes to `main`, with a push after each task.
- No tests until T08 unless a task's done-when list asks for one. This is in `AGENTS.md` only, as a temporary rule.
- The docs refer to the owner as "the user" and never by name.

## Why
M0's goal was to bootstrap the repository and the rules of work, so that M1 can build the self-improvement loop (0022) under clear approval, task and review rules.

## Consequences
M1 inherits:
- the three feature types and casing rules, which T07 must apply;
- the approval-tier field that T07 must add to feature metadata;
- the Python test runner choice, which T08 makes;
- the review template, from T06.

Still open:
- D07, due at T13;
- D15 and D16, for later types;
- confirming that the entry point works for any model.

## Test results
- **T02 entry point (pass):** a fresh Claude subagent found the right task and rules from `AGENTS.md` alone, and held at the review gate.
- **Not tested:** whether `AGENTS.md` works with a non-Claude agent. No other agent CLI was installed.
- Nothing else was tested, under the T08 rule.

## Approval needed
- Tier 2: accept this M0 review, which closes the milestone.

## Done without approval (tier 1)
None.

## Open questions
1. **"One commit per task" has really been two:** one for the work at `⏸`, and one to close the task on approval. Should the rule say that, i.e. one commit for the work plus one closing commit? Or should the closing changes go into the next task's commit?
2. Should there be a task to test `AGENTS.md` with a non-Claude agent (e.g. a local model, once D10 is decided), or should it wait until T13's retrospective?

## Outcome
Approved by the user in the chat on 2026-11-03. M0 is complete. Answers to the open questions:
1. Two commits per task is fine for now. Once git uses branches (D07), the closing commit will also cover the merge and squash the branch into a single commit. This is recorded in `AGENTS.md` and in D07.
2. Building is Claude-only for a while, since the core is built on frontier models. Testing `AGENTS.md` with a non-Claude agent happens when local models come in, alongside the model-launching work (e.g. LM Studio). This is noted on D10.
