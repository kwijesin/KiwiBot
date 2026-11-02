# 0007. Grow code, not prompts

- **Status:** Accepted
- **Date:** 2026-11-02
- **Tags:** philosophy, architecture

## Decision
For repeated, common tasks, KiwiBot should prefer **using tools, writing scripts or building whole new features of itself** over handling them manually with an LLM each time.

Think of a growing tree or web: LLMs are the growing stem tips, and they leave behind a strong branch of ordinary code.

## Related decisions
- Depends on: 0004
- Affects: 0005 (less work needs a model at all)
