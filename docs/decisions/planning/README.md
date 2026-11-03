# Planning

The process for shaping KiwiBot's core decisions in rounds, before (and later alongside) building.

## How it works

1. **Decide:** record decisions in `docs/decisions/` as they're made.
2. **Summarize:** write a synthesis of the round.
3. **Cascade:** follow each decision through to its knock-on effects on other decisions, open questions and the docs. Revise decisions (with a `Revised` line), add new ones, and put consciously postponed items in the [deferred register](../deferred.md).
4. **Repeat** until the foundation is solid enough to build on.

This is the same shape as the self-improvement pipeline's decision loop (0019). This manual process is effectively its first run.

## Status

- **Rounds 1–2:** complete (2026-11-02). Their summaries are archived in [docs/history/planning/](../../history/planning/).
- The outcomes have been applied to the rest of `docs/`, and the [first task list](../../tasks/task-list.md) has been written.

Future rounds write their working summaries here, and the summaries are archived to `docs/history/planning/` once the round is applied.

The [decision-loop](../../../features/decision-loop/SKILL.md) feature automates steps 1 and 3 for one input at a time. Each run keeps a **loop record** here, `loop-YYYY-MM-DD-<slug>.md`.
