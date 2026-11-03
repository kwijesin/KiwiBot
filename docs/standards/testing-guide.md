# Testing Guide v0

How KiwiBot's features are tested ([0012](../decisions/0012-test-everything.md), [0013](../decisions/0013-testing-framework.md)). There's no real sandbox yet (D02, [0027](../decisions/0027-early-features-agent-driven.md)), so prompt tests run in a throwaway git worktree.

## Where tests live

```
features/<feature-name>/tests/
├── <case-name>.md          ← prompt test case (one per case)
├── fixtures/<case-name>/   ← optional: files copied into the worktree, at the same paths as in the repo
└── test_<thing>.py         ← script tests (unittest)
```

## Prompt feature tests

Each case is a markdown file copied from [test-case-template.md](test-case-template.md). It has:

| Section | What it holds |
|---|---|
| **Fixture** | What the agent under test is given: the prompt, plus any fixture files. |
| **Setup** | How to prepare the worktree: files to replace or remove, and fixtures to copy. |
| **Checklist** | Numbered, observable pass/fail items: what the output says, which files change, which don't. |
| **Last run** | Date, who ran it and who judged it, pass/fail per item, the overall result, and feedback for each failure. |

### Running a case
Use the [feature-test](../../features/feature-test/SKILL.md) feature. In short:

1. **Worktree.** Run `git worktree add --detach <temp-dir> HEAD` with a temp directory outside the repo. Use a different commit instead of HEAD if the case's Setup names one, e.g. to replay a decision from before it existed. The agent under test can write there without touching `main`.
2. **Setup.** Apply the case's Setup in the worktree, then **delete every `features/*/tests/` folder** so the agent can't see checklists. Commit there (`git -C <temp-dir> commit -am "fixture"`). After the run, `git status` then shows only what the agent changed.
3. **Run.** Start a **fresh agent session** with no other context. Give it only the case's Fixture prompt, with the worktree as its working directory. For example: a Claude subagent, or `claude -p` run inside the worktree; any agent works (0020).
4. **Judge** each checklist item against the agent's reply and `git -C <temp-dir> status` / `diff`. The judge can be the user or a second agent. Human-judged pass/fail is allowed for now (T08).
5. **Record** the result in the case's **Last run** section. Git history keeps earlier runs.
6. **Clean up:** `git worktree remove --force <temp-dir>`.

A case **passes** only if every checklist item passes.

### Feedback for agents (0012)
Every failed item records four things, so the next agent can fix it without re-running the test to understand it:

- **Expected:** the checklist item.
- **Observed:** what actually happened.
- **Evidence:** a quote from the reply, or a file and line from the diff.
- **Likely cause:** which step or rule in `SKILL.md` (or which fixture) led to it, and a suggested fix.

## Script tests

- Python standard library **`unittest`**: no extra dependency (0030).
- Files are `features/<name>/tests/test_*.py`.
- Run with `python -m unittest discover -s features/<name>/tests -t .`, from a per-project virtual environment (0030).
- Test names say what they check (`test_skips_tasks_without_review_note`), and assertion messages say what was expected and why, so a failure reads as feedback.

No script features exist yet. T18 will be the first.

## When tests are required

- **Until T13:** only where a task's done-when list asks for one (the interim rule in `AGENTS.md`).
- **From T13 on**, as the default: a new or changed feature comes with at least one test case, and the review note's Test results gives the case's Last run.
