---
name: feature-test
description: >-
  Runs the test cases of a KiwiBot feature: prompt cases in a throwaway git
  worktree with a fresh agent and a judged checklist, and script tests with
  unittest. Records pass/fail and agent-useful feedback in each case's Last
  run section. Use when a feature is built or changed, or when asked to test
  a feature.
metadata:
  type: prompt
  status: active
  approval_tier: "1"
  model_class: frontier
  model_needs: file_read,file_write,shell
  decisions: "0012,0013,0027"
  depends_on: ""
---

# Feature test

## Purpose
Gives every feature an objective pass/fail signal, plus feedback a later agent can act on (0012, 0013). It works without a real sandbox (D02) by using a throwaway git worktree.

## Inputs
- The feature name, and optionally specific case names. By default, every case in `features/<name>/tests/`.
- [docs/standards/testing-guide.md](../../docs/standards/testing-guide.md)

## Steps
For each **prompt case** (`tests/<case-name>.md`):
1. **Worktree.** Run `git worktree add --detach <temp-dir> <base>`, where `<base>` is HEAD, or the commit the case's Setup names, and `<temp-dir>` is a new directory outside the repo (e.g. the system or session temp directory).
2. **Setup.** Apply the case's Setup steps in the worktree. Fixture files come from `features/<name>/tests/fixtures/<case-name>/` and are copied over the worktree root at the same paths. Then **delete every `features/*/tests/` folder in the worktree**, so the agent under test can't see any checklist. Then commit in the worktree (`git -C <temp-dir> add -A` and `git -C <temp-dir> commit -m fixture`).
3. **Run.** Start a **fresh agent session** with no context from this one. Give it only the case's Fixture prompt, with `<worktree>` replaced by the real path. Capture its full reply.
   - With Claude, use a subagent, or `claude -p` run inside the worktree.
   - With another agent, use its equivalent (0020).
4. **Judge** each checklist item against the reply, plus `git -C <temp-dir> status --short` and `git -C <temp-dir> diff`. Be strict: an item passes only if it's clearly met. If the user is judging, present the reply and the diff, then ask.
5. **Record** in the case file's **Last run**:
   - the date, the agent under test and the judge;
   - PASS or FAIL with the count, e.g. `FAIL (4/5)`;
   - a per-item table;
   - for every failed item: **Expected**, **Observed**, **Evidence** and **Likely cause**, with a suggested fix in `SKILL.md` or the fixture.
6. **Clean up:** `git worktree remove --force <temp-dir>`.

For **script tests**, run `python -m unittest discover -s features/<name>/tests -t .` and record the summary line, plus any failures, in the review note.

Finish with a short summary in the chat: each case's result, and the feedback for each failure.

## Output
- Updated **Last run** sections in the case files, and the script test summary.
- A chat summary of the results.

## Rules
- **Never fix the feature during a test run.** Report only. A fix is a separate change, made through the task that owns the feature.
- Never edit a case's Fixture or Checklist to make it pass. If the case itself is wrong, say so in the feedback.
- Always clean up the worktree, even when the run fails.
- The agent under test must not see the checklist.
