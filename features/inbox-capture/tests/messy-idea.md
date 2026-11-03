# Test: inbox-capture / messy-idea

- **Feature:** [inbox-capture](../SKILL.md) · **Kind:** prompt
- **What it checks:** a rough idea with typos is captured byte for byte into a correctly named inbox file, committed alone even when something else is staged, and nothing else changes.

## Fixture
The prompt given to the fresh agent, word for word:

> You are an agent at the root of the repository <worktree>. Follow features/inbox-capture/SKILL.md. The user's message, from Claude Code, is: "capture: maybe kiwibot shuold remind me to water the plants when its hot out , idk could use a weather api??". This is a test worktree: do not run `git push`. Instead, end your reply with the exact push command you would have run.

## Setup
1. Commit the standard setup (tests folders removed) in the worktree.
2. **After** that commit, append the line `test: staged but unrelated` to `docs/setup.md` and run `git -C <worktree> add docs/setup.md`. Don't commit it: it must be staged but uncommitted when the agent starts.

## Checklist
1. Exactly one new file exists in `inbox/`, named `YYYY-MM-DD-HHMM-<slug>.md` with a `kebab-case` slug of 2–5 words from the idea.
2. Its front matter has `captured:` (a date and time) and `source:` naming Claude Code or chat.
3. Its body, after the front matter, is **exactly** `maybe kiwibot shuold remind me to water the plants when its hot out , idk could use a weather api??`, with the typos, the space before the comma and both question marks kept, and nothing added.
4. The newest commit's message is `inbox: <slug>`, matching the file name's slug.
5. The newest commit contains **only** the new inbox file (`git show --stat HEAD`).
6. `docs/setup.md` is still staged and uncommitted (`git status --short` shows `M  docs/setup.md`), and no other file changed.
7. The reply doesn't comment on or triage the idea, and ends with a push command (e.g. `git push`).

## Last run
- **Date:** 2026-11-03 · **Agent under test:** fresh Claude subagent (general-purpose) · **Judge:** Claude (the T13 session)
- **Result:** PASS (7/7)

| # | Result | Notes |
|---|---|---|
| 1 | PASS | `inbox/2026-11-03-0118-water-plants-when-hot.md` |
| 2 | PASS | `captured: 2026-11-03T01:18`, `source: chat (Claude Code)` |
| 3 | PASS | Byte-identical (checked with `od -c`), typos and ` ,` kept |
| 4 | PASS | `inbox: water-plants-when-hot` |
| 5 | PASS | `git show --stat HEAD`: 1 file |
| 6 | PASS | `M  docs/setup.md` still staged |
| 7 | PASS | No comment on the idea; ended with `git push` |

**Note (not a failure):** the agent pointed out that a plain `git push` fails on a detached HEAD. That only happens in test worktrees, since real captures run on `main`.
