# Review: T07, style framework v0

- **Task:** T07 · **Status:** ☑ Done · **Date:** 2026-11-03
- **Commits:** `6e67943`, plus the closing commit
- **Tier:** 3 (plan + result)

## What changed
- [docs/standards/style-guide.md](../standards/style-guide.md): the style guide v0. It covers:
  - features as Agent Skills folders in `features/<name>/` (`SKILL.md`, plus `scripts/`, `references/` and `tests/`);
  - naming;
  - `SKILL.md` front matter, with KiwiBot metadata under `metadata` (type, status, `approval_tier`, `model_class`, `model_needs`, decisions, `depends_on`);
  - a fixed set of body headings (Purpose, Inputs, Steps, Output, Rules);
  - the rules for markdown data sets.
- Decision [0032](../decisions/0032-style-framework-v0.md), "Style framework v0: features as Agent Skills", **Proposed**.
- Example feature [features/review-queue/SKILL.md](../../features/review-queue/SKILL.md): a read-only prompt feature that lists the review queue.
- [docs/tasks/template.md](../tasks/template.md) and [docs/tasks/README.md](../tasks/README.md), so tasks follow the same markdown-data rule as decisions and reviews.
- Agent Skills added to [dependencies.md](../dependencies.md). D37 (visual style) added and D17 annotated in [deferred.md](../decisions/deferred.md). Both READMEs updated.
- New task **T18** (expose features as Claude Code skills) in M1.

## Why
T07 makes M1's features consistent (0010, 0011) before T09–T12 build them. You chose to use the Agent Skills format as the existing standard for prompt-based features (option A in the chat), so every feature has one shape and can be discovered by agents that support skills.

## Consequences
- **Script features are skills too.** Their `SKILL.md` explains when and how to run the script. This goes slightly beyond the chat, which only discussed prompt features. I did it so all features have the same shape; say if you'd rather scripts were plain folders.
- Agent Skills `metadata` values must be strings, so numbers are quoted (`"3"`) and lists are comma-separated strings. That's a little clunky, but it keeps the files valid against the spec.
- Claude Code won't discover `features/` until T18 is done. Until then, features are run by hand ("follow `features/x/SKILL.md`").
- T08 defines what goes in each feature's `tests/`.
- On acceptance, `AGENTS.md` gets a pointer to the style guide, and the review-queue feature is referenced from rule 2.

## Test results
None, under the T08 rule. **Demonstration** (not a test): a fresh agent, told only to follow `features/review-queue/SKILL.md`, produced:

```
### T07: Style framework v0
Review: docs/reviews/T07-style-framework.md
Approval needed:
- Tier 3: accept 0032 and the style guide.
- Tier 3: accept the `review-queue` example feature (status `draft`).
Open questions:
1. Are you happy for script features to also be `SKILL.md` folders (see Consequences)?
2. When 0032 is accepted, should `review-queue` go from `draft` to `active`, or stay `draft` until T08 tests it?
```

It found the one `⏸` task, matched its review note, quoted the note exactly, and changed no files.

## Approval needed
- Tier 3: accept 0032 and the style guide.
- Tier 3: accept the `review-queue` example feature (status `draft`).

## Done without approval (tier 1)
- Task status change (T07 → `⏸`).
- New task T18.
- New deferred item D37, and the "rename to tools" note on D17.

## Open questions
1. Are you happy for script features to also be `SKILL.md` folders (see Consequences)?
2. When 0032 is accepted, should `review-queue` go from `draft` to `active`, or stay `draft` until T08 tests it?

## Outcome
Approved by the user in the chat on 2026-11-03. 0032 accepted, `review-queue` set to `active`, and `AGENTS.md` updated: rule 2 uses `review-queue`, and the conventions point to the style guide.
1. Script features as skills: agreed. A script can still run another script directly, and a skill can also be run by an LLM with context.
2. `review-queue` activated.

**Follow-up (user's call):** T08 (testing) moves to after T12, just before T13, so T09–T12 aren't held up by test runs. T13 becomes the first task to use testing, and the T09–T11 test items move into T08. Task IDs are unchanged (0029).
