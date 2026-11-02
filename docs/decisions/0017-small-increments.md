# 0017. Build in small, well-bounded increments

- **Status:** Accepted
- **Date:** 2026-11-02
- **Tags:** process, implementation

## Decision
As KiwiBot builds itself, features and changes are organized into **good stopping points**: major and minor versions, milestones and natural points for git merges.

Ideally, a single pull or merge shouldn't contain a huge number of added lines.

## Related decisions
- Depends on: 0004, 0006
- Affects: 0019
