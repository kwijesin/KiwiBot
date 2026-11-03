# Style Guide v0

How KiwiBot's features are structured ([0032](../decisions/0032-style-framework-v0.md)), covering the feature types in [0030](../decisions/0030-initial-feature-types-and-conventions.md). Casing rules are in 0030 and aren't repeated here. Visual style (0011) is deferred until there's a UI (D37).

## Features use the Agent Skills format

Every feature is a folder in the **[Agent Skills](https://agentskills.io/specification) format**, an open standard for packaging instructions, scripts and references so an agent can find and use them. The format is the same for both feature types:

- a **prompt feature** is a skill whose body is the instructions an agent follows;
- a **script feature** is a skill whose body explains how and when to run its script.

So any agent that supports skills can discover every feature, and any agent can run one by hand ("follow `features/<name>/SKILL.md`").

## Folder layout

```
features/<feature-name>/
├── SKILL.md          ← required: metadata + instructions (the entry point)
├── scripts/          ← script features: Python CLI entry point(s)
│   └── <feature_name>.py
├── references/       ← optional: supporting docs, examples, templates the instructions point to
└── tests/            ← tests (format defined by T08)
```

- A feature only has the folders it needs.
- A feature can be both types, e.g. instructions that call a script.
- `features/` is at the repo root. Each feature is one folder, never nested inside another feature.

## Naming

- **Feature names** are `kebab-case` noun phrases that say what the feature does: `review-queue`, `decision-loop`. Agent Skills requires lowercase letters, digits and hyphens (max 64 characters), and **the folder name must equal `name`**.
- **Script entry point:** `scripts/<feature_name>.py` (the feature name in `snake_case`). It runs as `python features/<name>/scripts/<feature_name>.py` and supports `--help`.
- **Supporting files** are `kebab-case.md` in `references/`.

## SKILL.md

YAML front matter, then the instructions in markdown.

```yaml
---
name: review-queue
description: >-
  What the feature does and when to use it, written so an agent can decide
  to load it. Max 1024 characters.
metadata:
  type: prompt                 # prompt | script | prompt+script
  status: draft                # draft | active | retired
  approval_tier: "3"           # 0028: 3 plan+result, 2 result, 1 notify, 0 none
  model_class: frontier        # 0020: frontier | local | any
  model_needs: file_read       # comma-separated: file_read, file_write, shell, tool_use, long_context
  decisions: "0029"            # comma-separated decisions it implements
  depends_on: ""               # comma-separated features it uses
---
```

- `name` and `description` are required by Agent Skills. Everything KiwiBot-specific goes under `metadata`.
- Agent Skills `metadata` values are strings, so numbers are quoted and lists are comma-separated.
- Model requirements describe **what the feature needs, never a model name** (0020).
- There's no version field yet. Versioning is part of D07.

### Body

These headings, in order:

1. **Purpose:** one short paragraph.
2. **Inputs:** what the feature reads, and anything it must be given.
3. **Steps:** numbered instructions. For a script feature, how to run it and how to read the output.
4. **Output:** what it produces and in what form.
5. **Rules:** constraints, e.g. what it must not change and its approval tier in practice.

Keep the body short. Detail goes in `references/` and is linked from the steps, so an agent only reads it when it needs to.

## Markdown data

Markdown data (decisions, tasks, reviews) isn't a feature folder. Each data set is a folder in `docs/` with:

- a `README.md` that describes the format, and
- a template to copy.

| Data set | Folder | Template |
|---|---|---|
| Decisions | [docs/decisions/](../decisions/) | [0000-template.md](../decisions/0000-template.md) (older name, kept) |
| Tasks | [docs/tasks/](../tasks/) | [template.md](../tasks/template.md) |
| Reviews | [docs/reviews/](../reviews/) | [template.md](../reviews/template.md) |

## Example

[features/review-queue/](../../features/review-queue/) is a small prompt feature that follows this guide.
