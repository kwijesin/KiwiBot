# KiwiBot: Round 1 Synthesis

> **Archived.** This is an intermediate planning file, kept as history. Decisions may have changed since. See [decisions/](../../decisions/) for the current state and [deferred.md](../../decisions/deferred.md) for the live deferred register.

- **Round:** 1
- **Date:** 2026-11-02
- **Covers:** Decisions [0001](../../decisions/0001-decision-system.md) to [0024](../../decisions/0024-building-is-using.md)
- **Purpose:** One readable picture of what KiwiBot is, why it exists and what has been decided so far, to prompt the next round of decisions.

Decision numbers are given in brackets, e.g. (0007), so any statement can be traced back to its record.

---

## 1. What KiwiBot is

KiwiBot is a personal system that acts as three things at once (0002):

- **A personal assistant:** it helps me with my own tasks and life.
- **An efficiency accelerator:** it makes the things I do faster and cheaper in time and attention.
- **An additional interface:** it sits between me, my physical environment and the digital world, and I can reach through it in either direction.

KiwiBot is **not a single program**. It's an orchestration of agents, scripts, services, hardware and UI apps (0004), built up over time, and many of its parts will be written by KiwiBot itself.

The system is named **KiwiBot**, after me (0003). It was originally called **Lulu**, after the Lululemon Mirror that started the idea, and **Lulu** may live on as a wake word or interface name. The mirror is also still part of the plan: converted, it becomes a MagicMirror² display and one of KiwiBot's interfaces (0009).

This set of decisions is itself the system that defines KiwiBot (0001). It records the core architecture, uses, philosophy and features, and it's refined in rounds: decide, summarize, cascade the knock-on effects, then decide again.

---

## 2. Motivation: building is part of using

The most important idea behind KiwiBot's shape is in **0024**.

The obvious approach is to build an assistant and then use it. In practice that becomes a loop. Every new use exposes a missing feature, so I'd go back to building mode, take the systems down, add the feature, set everything up again, use it for a day, and find the next gap. Building and using would take turns, and each switch has a cost.

KiwiBot avoids this by making **building a core part of using**. KiwiBot grows while it runs. Most of the other decisions follow from that:

- KiwiBot must be able to **improve itself while running**, including viewing, restarting and modifying its own services and apps (0004).
- A **self-improvement pipeline** is an early, core feature (0019).
- The **first thing built** is that pipeline, not the assistant features (0022).

The assistant features I actually want (voice, the mirror, task management, home control) are what the self-improvement loop will *produce*. They aren't something built by hand before the loop exists.

---

## 3. Core philosophy

### 3.1 Grow code, not prompts (0007)

For repeated, common tasks, KiwiBot prefers **tools, scripts and new features of itself** over handling the task with an LLM every time. The image is a growing tree: **LLMs are the growing stem tips**, exploring and doing new work, and they leave behind a **strong branch of ordinary code**.

Over time the share of KiwiBot's work that needs a model should shrink compared with the work it does. That makes KiwiBot cheaper (0015), easier to test (0012) and better suited to local models (0005), since the hard parts become code.

### 3.2 Self-improvement is the engine (0004, 0019)

KiwiBot changes itself as it runs. The pipeline that does this works in steps (0019):

1. A **decision** comes in.
2. It's **checked for consequences**, which may lead to new decisions. The improvement agent may need to ask me questions.

   Steps 1 and 2 repeat until there's a satisfactory set of decisions.

3. A **plan** is made.
4. The plan may become a **task**.
5. The task is **executed** later.

This is deliberately the same shape as the planning process we're using now (0001). The decide → summarize → cascade loop in this folder is effectively the first, manual run of KiwiBot's own pipeline.

### 3.3 A human stays in the loop (0021)

I stay in the loop most of the time, especially early on. KiwiBot needs a **review and approval system** that explains each change and its consequences and accepts my feedback.

The working model is the **5-80-15 split**: I give the first **5%** (the intent and instruction), an AI gets **80%** of the way to a finished feature, and it comes back to me for review before the last **15%**.

Review is also KiwiBot's main early safeguard (see 3.5), and it costs attention, one of the resources in 3.4.

### 3.4 Resources are finite and can be traded (0015)

KiwiBot consumes four resources:

| Resource | Notes |
|---|---|
| **Tokens** | Cloud and local model usage. |
| **Human attention** | Mine: reviews, approvals, feedback, setup. |
| **Local compute** | Home hardware running models and services. |
| **Cash** | Eventually, for hardware additions. |

KiwiBot is **partially** optimized for token efficiency. It isn't token-minimal at any cost, because some automations rightly trade tokens for attention and others the reverse. The daily review rhythm in 0022 is partly a token-efficiency strategy: it spreads work across the usage window of the current build model.

### 3.5 Growth first, hardening later (0014)

KiwiBot will **eventually** be privacy- and security-hardened. Early on, security **doesn't take priority over KiwiBot's ability to grow**. Speed of growth wins until the foundation exists. Human review (0021), a private repository (0006) and small, reviewable changes (0017) give some protection in the meantime, although none of them is a security measure in itself.

### 3.6 Open source when it's obvious, custom otherwise (0023)

- **Readily available and easy to integrate** (e.g. a TTS engine): use the open-source option.
- **A toss-up** (e.g. Obsidian as the markdown viewer vs our own): it gets its own decision.
- **Everything else:** custom by default.

MagicMirror² (0009) is an existing example of the first category.

---

## 4. Architecture

### 4.1 A mixed orchestration (0004)

KiwiBot's parts vary widely in form. A part can be a **compiled app**, a **service**, a **script**, a **hardware device** or simply a **prompt file in a folder** that an agent is given (0010). The architecture has to treat all of these as first-class parts of one system, which can be observed, restarted and changed by KiwiBot itself.

### 4.2 Models: local-first, escalate when it matters, never locked in

- **Local-first (0005):** Day-to-day operation uses **local agents**. Important work, especially **self-improvement**, uses **frontier cloud models**. An **escalation system** decides what goes where. This replaces the earlier decision, where the cloud was opt-in by policy with a hard `local_only` switch.
- **Model-agnostic (0020):** Most or all LLM-based systems are model-agnostic, and models are connected through **configuration**. This applies to the self-improvement pipeline too. **Claude is the current build model, not a permanent one.**

### 4.3 Tasks are a core system (0016)

KiwiBot needs several task lists: at least **my tasks** and **KiwiBot's tasks**. A **task program** will probably be the core system KiwiBot uses to organize itself. The pipeline's output (0019), the daily review loop (0022) and the assistant role (0002) all depend on it.

### 4.4 Development history and change size (0006, 0017)

- KiwiBot's core components use **git and GitHub** for their development history, including changes KiwiBot makes to itself. The project is **private** (0006).
- Changes are organized into **good stopping points**: major and minor versions, milestones and natural merge points. No single merge should contain a huge number of added lines (0017). Small changes keep reviews manageable (0021) and history useful.

---

## 5. Standards: style and testing

Because KiwiBot's parts take so many forms, consistency doesn't happen by accident.

### 5.1 Style (0010, 0011)

- **Within a system type:** Features built the same way look the same. Folder-based features match other folder-based features, and apps match other apps.
- **Across system types:** Some shared conventions apply everywhere, such as one casing convention (camelCase vs snake_case) across programming levels.
- **A style framework** will be developed covering both the **architecture of feature types** (how each kind of feature is structured) and **visual style** (how features look on KiwiBot's interfaces).

### 5.2 Testing (0012, 0013)

- Everything KiwiBot builds is **tested whenever possible**, and the tests are written to give **useful feedback to the agents** working on the system.
- **LLM-based processes are tested too.** If a feature is a prompt file given to a new agent, its test can be to run that agent in a **sandbox-like version of the system**, watch it work and reduce the result to **pass/fail**.
- **A testing framework** will be developed so each feature type has a consistent way of being tested.

Testing is what makes self-improvement trustworthy: it gives the agents an objective signal, so not every change needs my full attention.

---

## 6. Interfaces

KiwiBot is meant to become a new interface between me and the digital world (0002), so it reaches me through several channels (0008):

- an **application** for **PC and phone**;
- **audiovisual input and output**;
- **custom hardware**; and
- possibly **physical interfaces**.

Two interface decisions already exist:

- **Voice-to-text input** is an **early, core** feature (0018).
- The **converted Lululemon Mirror** running **MagicMirror²** is a display interface (0009). The earlier hardware notes in that decision still apply: it's an irreversible conversion, has no camera or microphone, uses a portrait 1080×1920 layout, and black areas read as mirror.

---

## 7. How building starts (0022)

The first order of business is to get the **self-improvement loop** running:

1. **Planning ends with a task list.** The rounds in this folder must produce one.
2. **An agent works through those tasks.**
3. **Every task is reviewed daily.** I wake up to a review, give feedback, and review again later in the day.

This puts the 5-80-15 model (0021), the task system (0016), the pipeline (0019) and small increments (0017) into practice from day one. It also uses tokens efficiently across the build model's usage window (0015), while respecting the fact that the build model itself can be swapped (0020).

---

## 8. Decision map

A simplified view of how the decisions depend on each other. Arrows point from a decision to the ones it shapes.

```
ROOTS
  0001 Decisions define KiwiBot ─────────────► (all)
  0002 Purpose ──┬─► 0008 Interfaces ──┬─► 0009 MagicMirror ◄── 0003 Name
                 │                     └─► 0018 Voice-to-text
                 ├─► 0016 Task system
                 ├─► 0021 Human in the loop
                 └─► 0024 Building is using ──► 0004, 0019, 0022

CORE
  0004 Orchestration & self-improvement
     ├─► 0005 Local-first + escalation ──► 0020 Model-agnostic
     ├─► 0006 Git / private ──► 0017 Small increments
     ├─► 0007 Grow code ──► 0015 Resources
     ├─► 0010 Style ──► 0011 Style framework ──┐
     ├─► 0012 Testing ─────────────────────────┴─► 0013 Testing framework
     ├─► 0014 Growth before hardening
     ├─► 0023 Open source vs custom
     └─► 0019 Self-improvement pipeline

FIRST BUILD
  0016 + 0019 + 0020 + 0021 ──► 0022 First build priority
```

---

## 9. Tensions and open questions

These came out of putting the decisions side by side. **They're prompts for round 2, not decisions.**

> **Round 2 outcome:** each question below is marked with what happened to it. See [round-02-summary.md](round-02-summary.md).

### Self-improvement mechanics
- **What can KiwiBot change without approval?** 0004 says it modifies itself while running, and 0021 says I stay in the loop. Where's the line: by risk, by feature type, by size of change? **→ Round 2:** Approval tiers ([0025](../../decisions/0025-approval-tiers.md)). More approval early, relaxed by later decisions.
- **How does KiwiBot restart itself safely?** Self-modification while running implies something that **supervises** the other parts and can roll back a bad change. What is it, and does it ever change itself? **→ Round 2:** Deferred. Researched as part of the initial self-improvement work ([0027](../../decisions/0027-early-features-agent-driven.md)).
- **Where do decisions come from?** 0019 begins with "a decision comes in". Is this `decisions/` folder the intake, and can KiwiBot propose decisions as well as receive them? **→ Round 2:** Any input method ([0026](../../decisions/0026-decision-intake.md)). Details researched once the loop is finished.

### The sandbox
- 0012 needs a **sandbox-like version of KiwiBot** for testing agent-based features. What does it contain (real data or fixtures, real devices or mocks), and how does it stay in sync with the real system? **→ Round 2:** Deferred. Researched later ([0027](../../decisions/0027-early-features-agent-driven.md)).

### Models and cost
- **What triggers escalation** to a frontier model (0005)? Task type, failure of a local attempt, a flag on the feature? **→ Round 2:** Deferred. Frontier models for all core programming for now ([0005](../../decisions/0005-local-first-with-cloud-escalation.md)).
- **How are resources measured** (0015)? Does KiwiBot track token spend and attention cost, and are there budgets? **→ Round 2:** Deferred. No metering for now ([0015](../../decisions/0015-resource-efficiency.md)).
- **How is work scheduled** around the build model's usage window (0022)? Overnight runs, scheduled bursts? **→ Round 2:** Deferred (TBD).

### Tasks and review
- **One task system or several?** Is it custom or an existing tool (a 0023 toss-up)? **→ Round 2:** Fully custom ([0016](../../decisions/0016-task-system.md)). The number of lists is deferred.
- **Where does the daily review happen?** On the PC app, the phone, the mirror, or GitHub pull requests? It's the first interface I'll use every day, so it may need to exist before the others. **→ Round 2:** Deferred.
- **What does a review contain?** Per 0021: what changed, why, the consequences and the test results. **→ Round 2:** Deferred.

### Standards
- **Which languages and runtimes** are used, and which casing convention wins (0010)? **→ Round 2:** Deferred.
- **Which feature types exist?** The style and testing frameworks (0011, 0013) both need a list, e.g. prompt file, script, service, app or hardware integration. **→ Round 2:** Deferred.

### Security baseline
- 0014 defers hardening, but some basics may be worth having from the start because they're cheap now and costly to add later: **secrets handling**, **what data may go to cloud models**, and **remote access** to the phone app from outside the home. **→ Round 2:** Deferred.

### Identity
- **Lulu or Kiwi?** (0003). **→ Round 2:** **KiwiBot** ([0003](../../decisions/0003-name.md)). Lulu may remain a wake word or interface name.

---

## 10. Existing docs that no longer match

Per the planning rules, these aren't being changed yet. They're listed so the cascade step can deal with them.

| Doc | Conflict |
|---|---|
| `roadmap.md` | Phases start with a text MVP, voice and home integration. 0022 puts the self-improvement loop first. |
| `models.md` | Built on the old opt-in cloud policy (old 0001). 0005 and 0020 change routing and escalation. |
| `architecture.md` | Describes an assistant pipeline (wake word → STT → LLM → TTS). It doesn't yet include self-improvement, the task system, review, testing or supervision. |
| `privacy-security.md` | Written with privacy as a principle from the start. 0014 defers hardening. |
| `hardware.md`, `magicmirror.md` | Link to the old `0002-…` filename, now `0009`. |

---

## Decision index

| # | Decision | Tags |
|---|---|---|
| 0001 | Decisions define KiwiBot | process, philosophy |
| 0002 | Purpose: personal assistant, efficiency accelerator and interface | philosophy |
| 0003 | Name: KiwiBot | identity |
| 0004 | An orchestration that improves itself | architecture, philosophy, features |
| 0005 | Local-first, with frontier models for important tasks | architecture |
| 0006 | Git/GitHub for development history; private project | implementation |
| 0007 | Grow code, not prompts | philosophy, architecture |
| 0008 | Interfaces | features, hardware |
| 0009 | MagicMirror on a converted Lululemon Mirror | features, hardware, implementation |
| 0010 | Consistent style within and across feature systems | philosophy, standards |
| 0011 | Style framework | architecture, standards |
| 0012 | Test everything KiwiBot builds, including LLM processes | philosophy, standards |
| 0013 | Testing framework | architecture, standards |
| 0014 | Growth first, hardening later | philosophy, security |
| 0015 | Resource efficiency and trade-offs | philosophy, architecture |
| 0016 | Task lists as a core system | features, architecture |
| 0017 | Build in small, well-bounded increments | process, implementation |
| 0018 | Voice-to-text input is an early core feature | features |
| 0019 | Self-improvement pipeline is an early core feature | features, architecture |
| 0020 | Model-agnostic LLM systems | architecture |
| 0021 | Human in the loop: review and approval | philosophy, features |
| 0022 | First build priority: a running self-improvement loop | roadmap, process |
| 0023 | Open source vs custom | philosophy, architecture |
| 0024 | Building is part of using | philosophy |
