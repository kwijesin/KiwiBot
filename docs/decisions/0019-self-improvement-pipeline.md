# 0019. Self-improvement pipeline is an early core feature

- **Status:** Accepted
- **Date:** 2026-11-02
- **Tags:** features, architecture
- **Revised:** 2026-11-02 (round 1 cascade)

## Decision
A **self-improvement pipeline** is an early, core feature:

1. A **decision** comes in.
2. It's **checked for consequences**, which may lead to new decisions. The improvement agent may need to ask me questions.

   Steps 1 and 2 repeat until there's a satisfactory set of decisions.

3. A **plan** is made.
4. The plan may be turned into a **task**.
5. The task is **executed** some time later.

## Related decisions
- Depends on: 0001 (mirrors the decision process), 0004, 0016, 0026 (decision intake)
- Affects: 0005 (escalation for self-improvement), 0012, 0017, 0025
