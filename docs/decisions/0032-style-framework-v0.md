# 0032. Style framework v0: features as Agent Skills

- **Status:** Accepted
- **Date:** 2026-11-03
- **Tags:** standards, architecture

## Decision
The first version of the style framework (0011) is [docs/standards/style-guide.md](../standards/style-guide.md). Its structural choices:

1. **Features live in `features/<feature-name>/`** at the repo root, one folder per feature.
2. **Every feature uses the [Agent Skills](https://agentskills.io/specification) format.** This is an existing open standard for building repeatable prompt-based tasks and features (0023):
   - `SKILL.md` is the entry point;
   - `scripts/`, `references/` and `tests/` are optional folders.

   This applies to both prompt and script features, so every feature has the same shape (0010).
3. **Feature metadata** goes in the `SKILL.md` front matter. KiwiBot-specific fields go under `metadata`:
   - type and status;
   - **approval tier** (0028);
   - **model requirements** as needs, never model names (0020);
   - the decisions it implements, and the features it depends on.
4. **Markdown data sets** (decisions, tasks, reviews) stay in `docs/`, each with a README that describes its format and a template.

Changes to the style guide are tier 3 (0028).

## Related decisions
- Depends on: 0010, 0011, 0020, 0023, 0028, 0030
- Affects: 0013 (the testing framework tests features in this layout), 0019

---

## Optional sections

### Options considered *(optional)*
1. **A neutral `prompt.md`, with a thin skill wrapper where wanted.** This is more neutral, but it means two files per feature that must stay in sync.
2. **Agent Skills as the native format.** It's an open format supported by several agents, so it still fits 0020, and features can be discovered and triggered automatically. Chosen.

### Consequences *(optional)*
- Claude Code only discovers skills in `.claude/skills/`, so `features/` needs exposing there. This is a new task (T18).
- In [docs/skills.md](../skills.md) and D17, "skills" means runtime tools for the assistant. That should be renamed to "tools" when D17 is decided, so "skill" means only one thing.
- Visual style (0011) is deferred to D37.
