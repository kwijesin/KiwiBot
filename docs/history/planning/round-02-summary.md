# KiwiBot: Round 2 Synthesis

> **Archived.** This is an intermediate planning file, kept as history. Decisions may have changed since. See [decisions/](../../decisions/) for the current state and [deferred.md](../../decisions/deferred.md) for the live deferred register.

- **Round:** 2
- **Date:** 2026-11-02
- **Builds on:** [Round 1 synthesis](round-01-summary.md)
- **Covers:** Decisions 0001–0027, including 3 new decisions (0025–0027) and 5 revised ones.

Round 1 described what KiwiBot is and why. Round 2 worked through round 1's open questions. Most were **deferred** on purpose, a few became **decisions**, and the system got its name. This summary covers what changed, what was deferred, and the knock-on effects that should drive round 3.

---

## 1. What changed

| Change | Decisions |
|---|---|
| The system is now **KiwiBot**. "Lulu" may remain a wake word or interface name. | 0003 (revised) |
| The pipeline's decision step is now a **loop**: decisions are checked for consequences, the agent can ask me questions, and this repeats until the set of decisions is satisfactory. | 0019 (revised) |
| **Approval tiers:** more approval early, relaxed by later decisions, and considered for every new feature. | 0025 (new) |
| **Decision intake from any input:** phone, PC, voice, KiwiBot's own tasks, or me using Claude pointed at the root of the system. | 0026 (new) |
| **Early features are agent-driven.** Self-restart and sandboxing are research items for later. | 0027 (new) |
| **Frontier models for all core programming** for now. Escalation triggers are deferred. | 0005 (revised) |
| **No token or attention metering** for now. | 0015 (revised) |
| The **task system is fully custom.** | 0016 (revised) |

Process changes: decisions can now be **revised during planning**, marked with a `Revised` line, and the decisions README reflects that. The template includes the `Revised` line as an option.

---

## 2. The self-improvement loop, as it now stands

Putting 0019, 0021, 0022, 0025, 0026 and 0027 together gives a clearer picture of KiwiBot's early life:

1. **Intake (0026):** A decision comes in from any input. Early on, that realistically means **me using Claude pointed at the root of the system**, because the apps and voice input don't exist yet.
2. **Decision loop (0019):** The agent checks the decision for consequences, which may raise new decisions or questions back to me. This repeats until the set of decisions is satisfactory. It's the same process as these planning rounds.
3. **Plan → task (0019, 0016):** The decisions become a plan and then tasks in the custom task system.
4. **Execution (0005, 0027):** Tasks are carried out by **frontier models**. Early features are LLM-based and agent-driven, consistent with 0007's "LLMs are the growth tips".
5. **Review (0021, 0022, 0025):** Every task is reviewed daily, in the morning and again later in the day. Early on, **most things need approval**, because there's no sandbox yet to lean on.
6. **History (0006, 0017):** Changes land in git as small, well-bounded increments.

What the early loop **doesn't** have is a running system that restarts and rewires itself (0004's "improve itself while it runs"). That remains the goal, but self-restart is a research item within the initial self-improvement work (0027). Until then, "KiwiBot improving itself" in practice means **agent sessions working on KiwiBot's repository, reviewed by me**.

---

## 3. New decisions

### 0025: Approval tiers
How much approval a change needs varies and is expected to loosen over time. An **early decision** sets the initial approval rules, and **later decisions relax the automated tiers** as KiwiBot gains capabilities such as self-sandboxing. Approval tiers are considered **for every new feature**: some features need no approval, and some get priority review.

### 0026: Decision intake from any input
Decisions can arrive through the phone app, PC app, voice input, KiwiBot's own tasks ("make some decisions about xyz"), or me using Claude at the system root. The details are researched once the self-improvement loop is finished.

### 0027: Early features are agent-driven; self-restart and sandboxing come later
Early features will most likely all be LLM-based and driven through agentic, chatbot-style input. **Self-restart** is researched as part of the initial self-improvement work. **Sandboxing** is researched later.

---

## 4. Deferred register

Deferred items are kept here so they're not lost. Each has a rough trigger for when to revisit it.

| Item | From | Revisit when |
|---|---|---|
| **Self-restart / supervision** (how KiwiBot restarts and rolls back its own parts) | 0004, 0027 | During the initial self-improvement work |
| **Sandbox** for testing agent-based features | 0012, 0027 | After self-restart research; needed before approval can be relaxed much |
| **Decision intake details** | 0026 | Once the self-improvement loop is finished |
| **Escalation triggers** (what goes local vs frontier) | 0005 | When the first day-to-day runtime features exist that could run locally |
| **Resource metering** (token self-checks, attention metering) | 0015 | When efficiency becomes a priority; likely an early efficiency feature |
| **Working schedule** around the build model's usage window | 0022 | TBD |
| **Task structure** (how many lists, which ones) | 0016 | When designing the task system |
| **Where the daily review happens** | 0021, 0022 | Before the first daily review (see 5.2) |
| **What a review contains** | 0021 | With the review location |
| **Languages, runtimes, casing convention** | 0010 | Before the first code-based feature |
| **Feature types** for the style and testing frameworks | 0011, 0013 | Before the frameworks are designed |
| **Security baseline** (secrets, cloud data, remote access) | 0014 | Before remote access or sensitive data is involved |

---

## 5. Knock-on effects and new questions

These are prompts for round 3, not decisions.

### 5.1 The first approval decision is now on the critical path
0025 says an early decision sets the initial approval rules. Because 0022 needs daily reviews from the first day of building, this is probably one of the **first decisions round 3 needs**. What needs approval at the start, and what form does approval take?

### 5.2 Bootstrapping: what exists before KiwiBot exists?
Several parts of the loop depend on things that are themselves early tasks:
- **The task list.** 0022 requires a task list at the end of planning, but the task system is custom (0016) and not built yet. Where does the **first** task list live until the real system replaces it, e.g. a markdown file in the repo?
- **The review.** Daily reviews need somewhere to happen before any KiwiBot app exists. Git pull requests fit naturally with 0006 and 0017, but that's an open choice.
- **Intake.** "Claude pointed at the root" is the only realistic intake at first (0026).

A short "bootstrap" decision covering these three would let building start cleanly.

### 5.3 The system root has to be agent-readable
If one intake route is "an agent pointed at the root of the system" (0026), and agents must be model-agnostic (0020), the repository root needs an **entry point any agent can read**: what KiwiBot is, where the decisions, tasks and conventions live, and how to work in the repo. This overlaps with the style framework (0011), and could be one of its first parts.

### 5.4 What "local-first" means for now
With frontier models doing all core programming (0005, revised) and early features being agent-driven (0027), **very little runs locally at the start**. A reasonable reading is that local-first applies to KiwiBot's day-to-day **runtime** features as they appear, while **building** uses frontier models. Worth confirming.

### 5.5 Testing without a sandbox
Without a sandbox (0027), early testing (0012) is limited to ordinary code tests plus human review. Tests that watch an agent at work wait for the sandbox, so **human approval carries more weight early**, which is consistent with 0025.

### 5.6 Efficiency without measurement
0022 wants efficient use of the build model's usage window, but 0015 now defers metering. Early efficiency will be judged **by feel**, from how much gets done per review cycle. That's fine for now, but it's a reason to move metering up if usage limits start to bite.

### 5.7 Leftover naming
The rename is done in `decisions/`, but **"Lulu" still refers to the system** in:
- the project folder `LuluAgent`;
- the root `README.md` and the other docs (architecture, hardware, models, etc.); and
- the MagicMirror module `MMM-Lulu`, which can stay as an interface name per 0003.

These will be updated when the other docs are, after planning. One minor clarification: the intake list in 0026 says **voice input**. The round 2 notes called it the "TTS input method", but TTS is speech *output*. It's recorded as voice / speech-to-text input (0018).

---

## 6. Updated decision map

New and revised decisions are marked with an asterisk (*).

```
ROOTS
  0001 Decisions define KiwiBot ─────────────► (all)
  0002 Purpose ──┬─► 0008 Interfaces ──┬─► 0009 MagicMirror ◄── 0003 Name: KiwiBot*
                 │                     └─► 0018 Voice-to-text
                 ├─► 0016 Task system (custom)*
                 ├─► 0021 Human in the loop ──► 0025 Approval tiers*
                 └─► 0024 Building is using ──► 0004, 0019, 0022

CORE
  0004 Orchestration & self-improvement
     ├─► 0005 Local-first; frontier for core programming* ──► 0020 Model-agnostic
     ├─► 0006 Git / private ──► 0017 Small increments
     ├─► 0007 Grow code ──┬─► 0015 Resources (no metering yet)*
     │                    └─► 0027 Early features agent-driven*
     ├─► 0010 Style ──► 0011 Style framework ──┐
     ├─► 0012 Testing ─────────────────────────┴─► 0013 Testing framework
     ├─► 0014 Growth before hardening
     ├─► 0023 Open source vs custom
     └─► 0019 Self-improvement pipeline (decision loop)* ◄── 0026 Decision intake*

FIRST BUILD
  0016 + 0019 + 0020 + 0021 + 0025 + 0027 ──► 0022 First build priority
```

---

## 7. Existing docs that no longer match

Unchanged from round 1, plus the name:

| Doc | Conflict |
|---|---|
| **All docs and the root README** | Call the system **Lulu**. It's now **KiwiBot** (0003). |
| `roadmap.md` | Starts with assistant features. 0022 puts the self-improvement loop first. |
| `models.md` | Uses the old opt-in cloud policy. 0005 now uses frontier models for core programming, and 0020 makes everything model-agnostic. |
| `architecture.md` | Has no self-improvement loop, task system, approval tiers, review or testing. |
| `privacy-security.md` | Puts privacy first. 0014 defers hardening. |
| `hardware.md`, `magicmirror.md` | Link to the old `0002-…` filename, now `0009`. |

---

## Decision index

| # | Decision | Tags | Round 2 |
|---|---|---|---|
| 0001 | Decisions define KiwiBot | process, philosophy | |
| 0002 | Purpose: personal assistant, efficiency accelerator and interface | philosophy | |
| 0003 | Name: KiwiBot | identity | Revised |
| 0004 | An orchestration that improves itself | architecture, philosophy, features | |
| 0005 | Local-first, with frontier models for important tasks | architecture | Revised |
| 0006 | Git/GitHub for development history; private project | implementation | |
| 0007 | Grow code, not prompts | philosophy, architecture | |
| 0008 | Interfaces | features, hardware | |
| 0009 | MagicMirror on a converted Lululemon Mirror | features, hardware, implementation | |
| 0010 | Consistent style within and across feature systems | philosophy, standards | |
| 0011 | Style framework | architecture, standards | |
| 0012 | Test everything KiwiBot builds, including LLM processes | philosophy, standards | |
| 0013 | Testing framework | architecture, standards | |
| 0014 | Growth first, hardening later | philosophy, security | |
| 0015 | Resource efficiency and trade-offs | philosophy, architecture | Revised |
| 0016 | Task lists as a core system | features, architecture | Revised |
| 0017 | Build in small, well-bounded increments | process, implementation | |
| 0018 | Voice-to-text input is an early core feature | features | |
| 0019 | Self-improvement pipeline is an early core feature | features, architecture | Revised |
| 0020 | Model-agnostic LLM systems | architecture | |
| 0021 | Human in the loop: review and approval | philosophy, features | |
| 0022 | First build priority: a running self-improvement loop | roadmap, process | |
| 0023 | Open source vs custom | philosophy, architecture | |
| 0024 | Building is part of using | philosophy | |
| 0025 | Approval tiers | philosophy, features | New |
| 0026 | Decision intake from any input | features, process | New |
| 0027 | Early features are agent-driven; self-restart and sandboxing come later | roadmap, architecture | New |
