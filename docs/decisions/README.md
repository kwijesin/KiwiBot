# Architecture Decision Records

Short records of significant decisions, so future-you knows *why*.

- Deferred decisions are tracked in [deferred.md](deferred.md). The planning process is described in [planning/](planning/).
- Copy `0000-template.md` to `NNNN-short-title.md` (next number).
- Status: `Proposed` → `Accepted` → (later) `Superseded by NNNN`.
- During planning, decisions can be revised. Add a `Revised` line when you do. After planning, supersede them with a new decision instead of editing.

| # | Title | Tags | Status |
|---|-------|------|--------|
| 0001 | [Decisions define KiwiBot](0001-decision-system.md) | process, philosophy | Accepted |
| 0002 | [Purpose: personal assistant, efficiency accelerator and interface](0002-purpose.md) | philosophy | Accepted |
| 0003 | [Name: KiwiBot](0003-name.md) | identity | Accepted |
| 0004 | [An orchestration that improves itself](0004-orchestration-and-self-improvement.md) | architecture, philosophy, features | Accepted |
| 0005 | [Local-first, with frontier models for important tasks](0005-local-first-with-cloud-escalation.md) | architecture | Accepted |
| 0006 | [Git/GitHub for development history; private project](0006-git-history-private.md) | implementation | Accepted |
| 0007 | [Grow code, not prompts](0007-grow-code-not-prompts.md) | philosophy, architecture | Accepted |
| 0008 | [Interfaces](0008-interfaces.md) | features, hardware | Accepted |
| 0009 | [MagicMirror on a converted Lululemon Mirror](0009-magicmirror-on-converted-lululemon-mirror.md) | features, hardware, implementation | Accepted |
| 0010 | [Consistent style within and across feature systems](0010-consistent-style.md) | philosophy, standards | Accepted |
| 0011 | [Style framework](0011-style-framework.md) | architecture, standards | Accepted |
| 0012 | [Test everything KiwiBot builds, including LLM processes](0012-test-everything.md) | philosophy, standards | Accepted |
| 0013 | [Testing framework](0013-testing-framework.md) | architecture, standards | Accepted |
| 0014 | [Growth first, hardening later](0014-growth-before-hardening.md) | philosophy, security | Accepted |
| 0015 | [Resource efficiency and trade-offs](0015-resource-efficiency.md) | philosophy, architecture | Accepted |
| 0016 | [Task lists as a core system](0016-task-system.md) | features, architecture | Accepted |
| 0017 | [Build in small, well-bounded increments](0017-small-increments.md) | process, implementation | Accepted |
| 0018 | [Voice-to-text input is an early core feature](0018-voice-to-text.md) | features | Accepted |
| 0019 | [Self-improvement pipeline is an early core feature](0019-self-improvement-pipeline.md) | features, architecture | Accepted |
| 0020 | [Model-agnostic LLM systems](0020-model-agnostic.md) | architecture | Accepted |
| 0021 | [Human in the loop: review and approval](0021-human-in-the-loop.md) | philosophy, features | Accepted |
| 0022 | [First build priority: a running self-improvement loop](0022-first-build-priority.md) | roadmap, process | Accepted |
| 0023 | [Open source vs custom](0023-open-source-vs-custom.md) | philosophy, architecture | Accepted |
| 0024 | [Building is part of using](0024-building-is-using.md) | philosophy | Accepted |
| 0025 | [Approval tiers](0025-approval-tiers.md) | philosophy, features | Accepted |
| 0026 | [Decision intake from any input](0026-decision-intake.md) | features, process | Accepted |
| 0027 | [Early features are agent-driven; self-restart and sandboxing come later](0027-early-features-agent-driven.md) | roadmap, architecture | Accepted |
| 0028 | [Initial approval rules](0028-initial-approval-rules.md) | process, features | Accepted |
| 0029 | [Bootstrap workflow: tasks and reviews](0029-bootstrap-workflow.md) | process | Accepted |
| 0030 | [Initial feature types and conventions](0030-initial-feature-types-and-conventions.md) | standards, architecture | Accepted |
| 0031 | [Review format](0031-review-format.md) | process | Accepted |
| 0032 | [Style framework v0: features as Agent Skills](0032-style-framework-v0.md) | standards, architecture | Proposed |

**Tags:** philosophy, features, architecture, implementation, plus process, identity, hardware, standards, security and roadmap so far. New tags are added as they come up.
