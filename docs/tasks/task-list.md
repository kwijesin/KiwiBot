# KiwiBot Task List

- **Version:** 1 (first task list, written at the end of planning, 2026-11-02)
- **Type:** Bootstrap. This markdown file is the task list until KiwiBot's own custom task system (0016) replaces it (T14, T15).

The goal of this list is **0022: get the self-improvement loop running.** M0 bootstraps the repository and the rules of work. M1 builds the loop. M2 is a rough outline of the first features the loop builds, and the loop will refine it.

---

## How to work this list

The working rules (how to pick, plan, test, review and approve tasks) live in [AGENTS.md](../../AGENTS.md) at the repo root.

**Status:** `☐ Todo` · `◐ In progress` · `⏸ Awaiting review` · `☑ Done` · `✕ Dropped`
**Size:** S (under an hour of agent work) · M (one session) · L (should probably be split)

---

## M0: Bootstrap

### T01: Initialize git and a private GitHub repository
- **Status:** ☑ Done · **Size:** S · **Depends on:** none
- **Decisions:** 0006, 0014 (D34: secrets out of git), 0017
- **Goal:** Put KiwiBot under version control from the start, privately.
- **Done when:**
  - [x] `git init` at the repo root, with a `.gitignore` covering `.env`, local config, `data/`, model files and OS/editor clutter.
  - [x] A **private** GitHub repository exists and the current docs are committed and pushed as the initial commit.
  - [x] The repository name is confirmed with me (`KiwiBot`?), and so is whether to rename the local `LuluAgent` folder. → `KiwiBot` (`kwijesin/KiwiBot`); local folder renamed to `KiwiBot`.
- **Notes:** Branching conventions are deferred (D07, end of M1). Commit directly to `main`.

### T02: Create an agent entry point at the repo root
- **Status:** ☑ Done · **Size:** S · **Depends on:** T01
- **Decisions:** 0020 (model-agnostic), 0026 (intake via an agent at the root), 0010, 0011
- **Goal:** Any agent, not just Claude, opened at the repo root knows what KiwiBot is, where everything lives and how to work.
- **Done when:**
  - [x] A model-agnostic entry file exists: `AGENTS.md`, plus a one-line `CLAUDE.md` (`@AGENTS.md`), confirmed with me. It covers a one-paragraph summary of KiwiBot, a map of where decisions, deferred items, tasks, reviews and history live, and the working rules (moved here from this file).
  - [x] **Test (0012):** a fresh agent session at the root, asked *"what should you work on next, and how?"*, names the right task and rules without extra guidance. Record the result.
- **Test result (2026-11-02): pass.** A fresh Claude subagent, given only that question, read `AGENTS.md`, found that T02 was awaiting review and that T03 depends on it, and held at the review gate instead of starting T03. It then described T03 correctly: draft 0028, plan first, one commit to `main`, a review note with the right headings, then update D05 and `AGENTS.md`. **Limitation:** no non-Claude agent CLI was installed, so the "model-agnostic" part is untested.

### T03: Decide the initial approval rules
- **Status:** ☑ Done · **Size:** S · **Depends on:** T02
- **Decisions:** 0021, 0025 → resolves **D05**
- **Goal:** Make the "early decision" that 0025 calls for.
- **Done when:**
  - [x] Decision 0028 is drafted (Proposed) and answers these questions:
    - What needs approval at the start (probably nearly everything)?
    - At what points: the plan, the merge, or both?
    - What counts as approval (a PR approval, a reply on the review note)?
    - What, if anything, may proceed without approval (e.g. task status updates, typo fixes)?
    - How do later decisions relax the tiers?
  - [x] I accept it. D05 is marked **Decided → 0028**, and the agent entry point is updated.

### T04: Decide the bootstrap workflow
- **Status:** ☑ Done · **Size:** M · **Depends on:** T03
- **Decisions:** 0006, 0016, 0017, 0021, 0022 → resolves **D06**
- **Goal:** Settle how work flows before KiwiBot's own systems exist.
- **Done when:**
  - [x] A decision is drafted and accepted (0029), covering:
    - **Tasks:** confirm this markdown file as the interim task list, and how tasks are added and updated.
    - **Reviews:** where they happen and how the morning and later-day reviews work in practice (0022). (No PRs while everything goes straight to `main`; see the note below.)
  - [x] D06 is marked decided, and the agent entry point is updated.
- **Notes:** Git conventions (**D07**: branching, versioning, tags, change size) are deferred to the end of M1 (T13). Until then: everything is committed straight to `main`, **one commit per task**.

### T05: Decide the initial feature types and coding conventions
- **Status:** ☑ Done · **Size:** S · **Depends on:** T04
- **Decisions:** 0007, 0010, 0011, 0013, 0027 → resolves **D15, D16** (only as far as M1 needs)
- **Goal:** Define just enough for M1. Early features are mostly prompt-based (0027), with some scripts.
- **Done when:**
  - [x] A decision is accepted (0030) listing the **initial feature types**, e.g. prompt/agent-instruction feature, markdown data, script, and later service, app and hardware integration.
  - [x] It picks a **scripting language/runtime** for M1 and a **casing convention** across levels (0010).
  - [x] D15 and D16 are updated (decided, or partially decided with the rest still deferred).

---

## M1: Self-improvement loop v0

### T06: Define the review format and write the first review
- **Status:** ☐ Todo · **Size:** S · **Depends on:** T03, T04
- **Decisions:** 0021, 0022, 0025 → resolves **D14**
- **Done when:**
  - [ ] A review template exists where T04 decided reviews live. It covers: what changed, why, consequences, test results, approval needed (per 0028), and questions for me.
  - [ ] A review of the M0 work is written using it.

### T07: Style framework v0
- **Status:** ☐ Todo · **Size:** M · **Depends on:** T05
- **Decisions:** 0010, 0011, 0020, 0025
- **Goal:** Consistent structure for the M1 feature types, mainly prompt-based features.
- **Done when:**
  - [ ] A style guide covers:
    - folder layout per feature (e.g. `features/<name>/` with its README, prompt files and tests);
    - naming;
    - feature metadata, including the **approval tier** (0025) and **model requirements** (0020).
  - [ ] The guide is shown applied to a small example feature.
- **Notes:** Visual style (0011) can wait until there's a UI. Add it to `deferred.md` if needed.

### T08: Testing framework v0
- **Status:** ☐ Todo · **Size:** M · **Depends on:** T05, T07
- **Decisions:** 0012, 0013, 0027 (no sandbox yet)
- **Done when:**
  - [ ] A testing guide exists:
    - **Prompt-based features:** fixture inputs, an expected-outcome checklist, an agent run, and a pass/fail result recorded. Human-judged pass/fail is allowed for now.
    - **Scripts:** standard unit tests in the language chosen in T05.
  - [ ] There's a test template and one example test that passes.
  - [ ] Test output is written to be useful feedback for an agent (0012).

### T09: Decision-loop feature (intake → decisions → consequences → questions)
- **Status:** ☐ Todo · **Size:** M · **Depends on:** T07, T08
- **Decisions:** 0019 (steps 1–2 and the loop), 0026, 0001
- **Goal:** Turn the manual planning process into a reusable feature. It takes raw input (a paragraph from me), checks it against the existing decisions and the deferred register, drafts or revises decisions, lists consequences and asks me questions, and repeats until the set is satisfactory.
- **Done when:**
  - [ ] The feature exists in the style framework format.
  - [ ] **Test:** replaying one of my original planning paragraphs from `docs/history/planning/` (e.g. the testing paragraph behind 0012) gives a decision equivalent to the recorded one, with sensible related decisions and questions.

### T10: Synthesis/cascade feature (round summaries)
- **Status:** ☐ Todo · **Size:** S · **Depends on:** T09
- **Decisions:** 0001, 0019; process in `docs/decisions/planning/README.md`
- **Goal:** Produce a round summary: what changed, knock-on effects, new questions and deferred items.
- **Done when:**
  - [ ] The feature exists.
  - [ ] **Test:** run over decisions 0025–0027, it surfaces the main knock-on effects found in the archived round 2 summary (approval decision on the critical path, bootstrap, agent-readable root).

### T11: Plan → task feature
- **Status:** ☐ Todo · **Size:** S · **Depends on:** T07, T08
- **Decisions:** 0019 (steps 3–4), 0016, 0017, 0025
- **Goal:** Turn accepted decisions into a plan and tasks in this file's format: goal, decisions, approval, size, dependencies and done-when.
- **Done when:**
  - [ ] The feature exists.
  - [ ] **Test:** it generates sensible, small tasks for one accepted decision, and I approve them.

### T12: Task-execution workflow
- **Status:** ☐ Todo · **Size:** S · **Depends on:** T06, T07, T08
- **Decisions:** 0019 (step 5), 0021 (5-80-15), 0017, 0012
- **Goal:** Formalize "How to work this list" as a feature or agent instruction set: pick a task, plan, get approval if required, execute in small increments, test, write the review note, and stop at about 80% for review.
- **Done when:**
  - [ ] The workflow exists and the agent entry point refers to it.
  - [ ] **Test:** the next task (T13) is carried out using it.

### T13: First end-to-end run of the loop
- **Status:** ☐ Todo · **Size:** M · **Depends on:** T09, T10, T11, T12
- **Decisions:** 0022, 0018
- **Goal:** Push one real item through the whole loop: intake → decision loop → plan → tasks → execution → review.
- **Suggested item:** **D21, the speech-to-text engine for voice-to-text input** (0018, an early core feature). It's small, real, and leads straight into M2.
- **Done when:**
  - [ ] The item has been through every stage, with reviews.
  - [ ] A short retrospective lists what to improve in the loop, and those improvements become new tasks (via T11).
  - [ ] **D07** (branching, commit style, versioning, milestone tags, change-size guideline) is decided, informed by how M1 went.
  - [ ] M1 is complete and tagged as a version (per D07).

---

## M2: First features built by the loop (rough, to be refined via T11)

### T14: Task system design
- **Status:** ☐ Todo · **Size:** M · **Depends on:** M1
- **Decisions:** 0016 (fully custom), 0023 → resolves **D13**
- **Goal:** Research and decide the structure of the custom task system: which lists (at least mine and KiwiBot's), fields, storage and interfaces.

### T15: Task system v1
- **Status:** ☐ Todo · **Size:** L (split via T11) · **Depends on:** T14
- **Goal:** Build it, migrate this file into it, and update the agent entry point.

### T16: Research self-restart and supervision
- **Status:** ☐ Todo · **Size:** M · **Depends on:** M1
- **Decisions:** 0004, 0027 → informs **D01**, and **D20** (deployment)
- **Goal:** Write a research note on how KiwiBot can view, restart and roll back its own parts, ending in a Proposed decision.

### T17: Voice-to-text input v0
- **Status:** ☐ Todo · **Size:** L (split via T11) · **Depends on:** T13
- **Decisions:** 0018, 0023, and the decision produced in T13
- **Goal:** The first working voice-to-text input, built from the tasks T13 produced.
