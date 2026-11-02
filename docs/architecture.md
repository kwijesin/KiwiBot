# Architecture

> **Placeholder.** Most of KiwiBot's architecture will be designed by KiwiBot's own self-improvement loop (0019, 0022), one decision at a time. This page only records what's already decided. Earlier draft designs for the runtime assistant are kept as candidates in the [deferred register](decisions/deferred.md) (D19–D27).

## What's decided

**KiwiBot is an orchestration, not a single program (0004).** Its parts are agents, scripts, services, hardware and UI apps, ranging from compiled apps to prompt files in plain folders (0010). KiwiBot should eventually be able to view, restart and change its own parts while it runs.

**Building is part of using (0024).** The first system built is the **self-improvement loop** (0022), not the assistant features:

```
 intake (any input, 0026)
     │
     ▼
 decision loop ◄──── questions to me ────┐
 (check consequences, new decisions)     │   repeat until satisfactory (0019)
     │ ─────────────────────────────────►┘
     ▼
 plan ──► task (custom task system, 0016)
              │
              ▼
        execution by an agent (frontier models for core programming, 0005)
              │
              ▼
        review & approval (approval tiers, 0021, 0025) ── daily (0022)
              │
              ▼
        git history, small increments (0006, 0017)
```

**Grow code, not prompts (0007).** LLM-driven parts are the growing edge. Repeated work is turned into tools, scripts and features over time. Early features are expected to be LLM-based and agent-driven (0027).

**Models are pluggable (0020).** LLM-based parts are model-agnostic and connected through configuration. Day-to-day operation is local-first, and core programming uses frontier models (0005).

**Standards apply across parts.** There will be a style framework (0010, 0011) and a testing framework (0012, 0013) covering every feature type, LLM-based ones included.

**Interfaces (0008):** a PC and phone app, audiovisual input and output (voice-to-text first, 0018), custom hardware including the converted mirror (0009, [magicmirror.md](magicmirror.md)), and possibly physical interfaces.

## Components

**TODO (designed by the loop):** each component gets a section here once its decisions exist.

| Component | Status | Decisions |
|---|---|---|
| Self-improvement loop | First build priority | 0019, 0022, 0025, 0026, 0027 |
| Task system | Custom, to be designed | 0016, D13 |
| Review and approval | To be designed | 0021, 0025, D05, D06, D14 |
| Supervisor / self-restart | Research item | 0004, D01 |
| Sandbox | Research item | 0012, D02 |
| Model connections and routing | To be designed | 0005, 0020, D08–D10 |
| Voice-to-text input | Early core feature | 0018, D21 |
| Apps (PC, phone) | To be designed | 0008 |
| Mirror display | Hardware decided | 0009, D30–D32 |
| Runtime assistant (wake word, tools, memory, TTS, home control) | Deferred | D19–D27 |

## Deployment

**TODO:** deferred (D20). Shaped by how self-restart and supervision work (D01).
