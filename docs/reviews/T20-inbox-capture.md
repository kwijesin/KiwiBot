# Review: T20, inbox-capture feature

- **Task:** T20 · **Status:** ⏸ Awaiting review · **Date:** 2026-11-03
- **Commits:** the T20 work commit
- **Tier:** 3 (plan + result). Trial: part of the T19–T22 set, reviewed together (T13, retrospective input 3).

## What changed
- [features/inbox-capture/SKILL.md](../../features/inbox-capture/SKILL.md): a prompt feature with status `draft`, **declared tier 0**, `model_class: any`, needing `file_write` and `shell`. Its steps:
  1. find the idea;
  2. copy it exactly;
  3. name the file `inbox/YYYY-MM-DD-HHMM-<slug>.md`;
  4. write the front matter (`captured`, `source`) and the body;
  5. commit by path (`git commit -m "inbox: <slug>" -- <file>`), so anything else that's staged stays out;
  6. push;
  7. reply in one or two lines.

  Its rules: never change the body, never capture the agent's own ideas, one idea per file, and no triage.
- [features/inbox-capture/tests/messy-idea.md](../../features/inbox-capture/tests/messy-idea.md): a prompt test case.

## Why
0034 (human-written, verbatim) and 0035 (the capture skill, plus committed `inbox: <slug>` commits). Built via T13.

## Consequences
- **This is the first tier 0 feature, and the first tier lowering under 0033.** The reason: it writes only the user's own words, only on request, and the result is shown in the chat, so a notice in a review note would add attention cost and no safety (0015).
- `inbox: <slug>` commits happen outside tasks. They're a D07 input (T13 retrospective input 1).
- `AGENTS.md` lists features under "How to work". inbox-capture is added there when it's accepted, as with earlier features.

## Test results
**messy-idea: PASS (7/7).** A fresh subagent ran it in a throwaway worktree, with `docs/setup.md` staged beforehand.
- The body was byte-identical (`od -c`), with the typos and ` ,` kept.
- The commit held only the inbox file, and `docs/setup.md` stayed staged.
- The reply didn't comment on the idea.

It also noted that a plain `git push` fails on a detached HEAD, which only happens in test worktrees.

## Approval needed
- Tier 3: accept `inbox-capture` at its **declared `approval_tier` of 0** (0033), and set its status to `active`.

## Done without approval (tier 1)
- T20 set to `◐`, then `⏸`.

## Open questions
None.

## Outcome
*(Filled in when the task is closed.)*
