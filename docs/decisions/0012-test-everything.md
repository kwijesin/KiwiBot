# 0012. Test everything KiwiBot builds, including LLM processes

- **Status:** Accepted
- **Date:** 2026-11-02
- **Tags:** philosophy, standards

## Decision
Programs, tools and systems built by KiwiBot should be **tested whenever possible**. Tests should give **useful feedback to the agents working on the system**.

Processes that run through LLMs should be tested too. For example, if a system is a prompt file given to a new agent to carry out a task, the test could watch that agent do its job in a **sandbox-like version of the system** and distil the result into **pass/fail**.

## Related decisions
- Depends on: 0004, 0007
- Affects: 0013
