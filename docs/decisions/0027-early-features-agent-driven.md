# 0027. Early features are agent-driven; self-restart and sandboxing come later

- **Status:** Accepted
- **Date:** 2026-11-02
- **Tags:** roadmap, architecture

## Decision
**Early features will most likely all be LLM-based** (the growth zones of 0007), driven through **agentic, chatbot-style input**.

So two capabilities aren't needed at the start, and are **research items** for later:
- **Self-restart:** KiwiBot restarting its own services and apps (0004) will be researched **as part of the initial self-improvement work**. It's a few features away.
- **Sandboxing:** the sandbox-like version of the system for testing (0012) will be researched **later**, like self-restart.

## Related decisions
- Depends on: 0007, 0022
- Affects: 0004, 0012, 0025
