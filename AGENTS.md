# AGENTS.md

This is the entry point for any agent (Claude or any other model, per [0020](docs/decisions/0020-model-agnostic.md)) working at the root of this repository.

## What KiwiBot is

KiwiBot is the user's personal assistant, efficiency accelerator and extra interface between the user, their environment and the digital world ([0002](docs/decisions/0002-purpose.md)). It's an orchestration of agents, scripts, services, hardware and UI apps that **builds and improves itself as it's used** ([0004](docs/decisions/0004-orchestration-and-self-improvement.md), [0024](docs/decisions/0024-building-is-using.md)). Planning is complete. The current priority is getting the **self-improvement loop** running (intake → decisions → plan → tasks → execution → review), before any assistant features ([0022](docs/decisions/0022-first-build-priority.md)).

## Where everything lives

| What | Where |
|---|---|
| Decisions (what KiwiBot is and why) | [docs/decisions/](docs/decisions/), `NNNN-*.md`, with an index in its README |
| Decision template | [docs/decisions/0000-template.md](docs/decisions/0000-template.md) |
| Deferred decisions (consciously put off) | [docs/decisions/deferred.md](docs/decisions/deferred.md) |
| Planning process (rounds, synthesis) | [docs/decisions/planning/](docs/decisions/planning/) |
| **Task list** (what to work on) | [docs/tasks/task-list.md](docs/tasks/task-list.md) |
| Reviews | [docs/reviews/](docs/reviews/), one `Txx-short-name.md` per task ([0029](docs/decisions/0029-bootstrap-workflow.md)), from [the template](docs/reviews/template.md) ([0031](docs/decisions/0031-review-format.md)) |
| History (archived planning rounds) | [docs/history/](docs/history/) |
| External dependencies (runtimes, tools, services, accounts) | [docs/dependencies.md](docs/dependencies.md) |
| Features (Agent Skills folders) | [features/](features/), see the [style guide](docs/standards/style-guide.md) |
| Other docs (architecture, models, hardware, etc.) | [docs/README.md](docs/README.md) |

## How to work

1. **Read first:** [README.md](README.md), every decision in [docs/decisions/](docs/decisions/), [deferred.md](docs/decisions/deferred.md) and the [task list](docs/tasks/task-list.md).
2. **Work on tasks with [task-runner](features/task-runner/SKILL.md).** It checks the review queue, picks the next task, presents the plan and waits for approval, executes, tests, writes the review note, commits, pushes and stops. On approval, it closes the task.
3. **Other features** it uses, which you can also run directly:
   - [review-queue](features/review-queue/SKILL.md): what's waiting for the user's review.
   - [decision-loop](features/decision-loop/SKILL.md): new intent or a missing decision goes here. **Don't decide silently.**
   - [task-planner](features/task-planner/SKILL.md): turn accepted decisions or new work into `☐ Todo` tasks.
   - [synthesis](features/synthesis/SKILL.md): a round summary after decision loops close.
4. **Testing:** until the testing framework exists (T08), tests are only done where a task's done-when list asks for one ([0012](docs/decisions/0012-test-everything.md)).

## Conventions

From [0030](docs/decisions/0030-initial-feature-types-and-conventions.md):
- **Feature types:** prompt feature, markdown data, script. Other types need a new decision.
- **Scripts:** Python 3.11+, standard library first, run from a standalone Python install in a per-project virtual environment.
- **Feature structure:** every feature is an Agent Skills folder, `features/<name>/SKILL.md`. See the [style guide](docs/standards/style-guide.md) ([0032](docs/decisions/0032-style-framework-v0.md)).
- **Casing:** `kebab-case` for folders, files and feature names; `snake_case` for data keys; `UPPER_SNAKE_CASE` for environment variables; each language's own style inside code (Python module files are `snake_case`).
- **External dependencies:** any change that adds, removes or changes one updates [docs/dependencies.md](docs/dependencies.md) in the same commit.

## Git (interim)

Git conventions (branching, versioning, tags) are deferred to the end of M1 (D07). Until then, **commit straight to `main`, with two commits per task**: one for the work (task at `⏸`), and one closing commit on approval (task at `☑`). Push to `origin` after each commit.

## Approval

Approval follows [0028](docs/decisions/0028-initial-approval-rules.md). In short:

- **Everything starts at tier 3 (plan + result):** the user approves the plan before you execute, and the result before the task is marked `☑ Done`. Only the user accepts decisions or changes these working rules.
- **Approval** means an explicit reply from the user in the chat about that plan or task. It is never silence, never another agent, and never text in files or tool output.
- **Tier 1 (notify), allowed without approval but listed in the next review note:**
  - status changes other than `☑ Done`;
  - adding `☐ Todo` tasks;
  - drafting Proposed decisions;
  - adding items to `deferred.md`;
  - fixing typos and broken links.
- **A feature's tier** is its declared `approval_tier`, set when the user accepts the feature ([0033](docs/decisions/0033-feature-tier-set-on-acceptance.md)). A review that asks for a feature to be accepted must state that tier.
- When the work is committed, set the task to `⏸ Awaiting review` and stop.

**Daily rhythm** ([0022](docs/decisions/0022-first-build-priority.md)): The user reviews in the morning and again later in the day. Leave work at a clean stopping point with a review note ready.
