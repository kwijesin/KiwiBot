# Deferred Decisions

This is the live register of decisions that have been **consciously put off**. Each one has a source and a trigger for when to revisit it.

- When a deferred item is decided, record it as a normal decision (`NNNN-*.md`) and mark the row **Decided → NNNN**.
- **Candidates / notes** keeps earlier draft thinking (much of it from the pre-planning docs) so it isn't lost. **None of it is decided.**
- Items D01–D12 came from planning rounds 1 and 2 ([history](../history/planning/)). D13 onward came from the docs when the decisions were applied to them.

## Self-improvement and process

| ID | Item | Source | Candidates / notes | Revisit when |
|---|---|---|---|---|
| D01 | **Self-restart / supervision:** how KiwiBot restarts and rolls back its own parts | 0004, 0027 | Something must supervise the other parts and be able to roll back a bad change. | During the initial self-improvement work |
| D02 | **Sandbox** for testing agent-based features | 0012, 0027 | What it contains (real data or fixtures, real devices or mocks) and how it stays in sync. | After D01; needed before approval can be relaxed much |
| D03 | **Decision intake details** | 0026 | Any input method; early on, an agent pointed at the repo root. | Once the self-improvement loop is finished |
| D04 | **Working schedule** around the build model's usage window | 0022 | Overnight runs, scheduled bursts, etc. | TBD |
| D05 | **Initial approval rules** (the "early decision" in 0025) | 0025 | What needs approval at the start and what form approval takes. | **Decided → [0028](0028-initial-approval-rules.md)** |
| D06 | **Bootstrap workflow:** where tasks and reviews live before KiwiBot's own systems exist | 0016, 0021, 0022 | Markdown task list in the repo (in use now: [tasks/task-list.md](../tasks/task-list.md)); reviews as GitHub pull requests and/or markdown review notes. | **Decided → [0029](0029-bootstrap-workflow.md)** (D07 split off, deferred to end of M1) |
| D07 | **Branching, versioning and merge conventions** | 0006, 0017 | Branch per task, semantic versioning, milestone tags. **Interim (until decided):** commit straight to `main`, two commits per task (the work, then a closing commit on approval). **Direction from the user:** with branches, the closing commit also covers the merge and squashes the branch into a single commit. | End of M1 (task list T13) |

## Models

| ID | Item | Source | Candidates / notes | Revisit when |
|---|---|---|---|---|
| D08 | **Escalation triggers and routing modes:** what runs locally vs on frontier models | 0005, 0020 | Earlier draft modes: `local_only`, `local_first`, `auto`, `cloud_preferred`. Earlier draft triggers: explicit request, task type on an allow-list, context larger than the local window, repeated tool-call failures. | When the first runtime feature could run locally |
| D09 | **What "local-first" means for now** | 0005, 0027 | Likely reading: local-first applies to day-to-day **runtime** features, and **building** uses frontier models. Needs confirming. | With D08 |
| D10 | **Local model choices and serving runtime** | 0005, 0020 | Roles: main tool-use LLM, small fast LLM, embeddings. Runtimes: Ollama, llama.cpp, vLLM, LM Studio (an OpenAI-compatible endpoint keeps routing simple). Building is Claude-only until then; when local models come in, also test that `AGENTS.md` works with a non-Claude agent (open since T02). | With D08 and host hardware (D24) |
| D11 | **Resource metering:** token self-checks, attention metering, cloud call logging | 0015 | Earlier draft: log each cloud call with timestamp, provider, model, token count and reason, but not prompt content. | When efficiency becomes a priority |
| D12 | **Model evaluation suite** | 0012, 0013 | Earlier draft: a set of household requests (timers, device control, Q&A, multi-step) to compare models and tune routing. | With D08 |

## Tasks, review and standards

| ID | Item | Source | Candidates / notes | Revisit when |
|---|---|---|---|---|
| D13 | **Task system structure:** which lists, fields, format | 0016 | At least "my tasks" and "KiwiBot's tasks". Fully custom. | When designing the task system (T14) |
| D14 | **What a review contains** | 0021 | What changed, why, consequences, test results, approvals needed, questions. | **Decided → [0031](0031-review-format.md)** |
| D15 | **Languages, runtimes and casing convention** | 0010 | **Partly decided → [0030](0030-initial-feature-types-and-conventions.md):** Python 3.11+ for M1 scripts, casing convention. Still open: languages/runtimes for services and apps. | When the first service or app is built |
| D16 | **Feature types** for the style and testing frameworks | 0011, 0013 | **Partly decided → [0030](0030-initial-feature-types-and-conventions.md):** prompt feature, markdown data, script. Still open: service, app, hardware integration, MagicMirror module. | When each later type is first needed |
| D17 | **Skill / tool format** | 0011, 0025 | Earlier draft: a decorator declaring name, description, input schema, `confirm` and `cloud_ok`. Skills should be idempotent and return a short, speakable result. Approval flags overlap with 0025. | When the first runtime skill is built |
| D18 | **Configuration format and location**, including how models are connected (0020) | 0020 | Earlier draft: `config/*.yaml` for settings and `.env` for secrets, with example files committed and real ones git-ignored. | Before the first configurable component |

## Runtime assistant

| ID | Item | Source | Candidates / notes | Revisit when |
|---|---|---|---|---|
| D19 | **Runtime assistant pipeline** | 0004, 0008 | Earlier draft: input → wake word → STT → orchestrator (sessions, prompt assembly, tool loop) → TTS → output, with display events to the mirror. | When runtime assistant features begin |
| D20 | **Deployment model** | 0004 | Earlier draft: Docker Compose (one container per service) vs a single process with plugins. | With D01 (supervision shapes this) |
| D21 | **Speech-to-text engine** | 0018, 0023 | faster-whisper / Whisper, Vosk. Open source per 0023. | When voice-to-text (0018) is built |
| D22 | **Wake word:** engine and word | 0003, 0008 | openWakeWord, Porcupine. "Lulu" is a candidate wake word (0003). | With D21 |
| D23 | **Text-to-speech engine and voice** | 0008, 0023 | Piper, Kokoro, Coqui XTTS. Open source per 0023. | When audio output is built |
| D24 | **Memory design** | 0004 | Earlier draft: short-term rolling conversation context; long-term facts and preferences in local storage (e.g. SQLite + vector index); configurable retention. | When the assistant needs memory |
| D25 | **Home automation approach** | 0002, 0008 | Earlier draft: integrate with a hub (e.g. Home Assistant) through its API rather than controlling devices directly. | When home control is first wanted |
| D26 | **Latency targets** | 0008 | Earlier draft: end of speech → first audio < 2 s (wake → STT < 200 ms, STT < 500 ms, LLM first token < 700 ms, TTS first audio < 300 ms). | With D19 |
| D27 | **Physical-world safety:** confirmations for locks, doors, alarms and other safety actions; voice ID or PIN | 0014, 0025 | Earlier draft: confirmation always required for these. | Before any physical-world control |

## Hardware and interfaces

| ID | Item | Source | Candidates / notes | Revisit when |
|---|---|---|---|---|
| D28 | **Main host hardware:** CPU, RAM, GPU, storage, OS | 0005 | VRAM is the main limit on local model size. See [hardware.md](../hardware.md). | With D10 |
| D29 | **Voice satellites** | 0008, 0018 | Raspberry Pi + mic HAT, ESP32-S3 voice kits, reused tablets or phones. | After voice-to-text works on one device |
| D30 | **Mirror build choices:** SBC, mic, camera, audio routing | 0009 | Raspberry Pi 5 or x86 mini PC; USB mic array; optional USB camera. | When the mirror conversion starts |
| D31 | **Is the mirror the *primary* interface?** | 0008, 0009 | 0009's title says "primary"; 0008 lists several equal interfaces (apps, audiovisual, hardware). | When interfaces are prioritized |
| D32 | **Avatar rendering** | 0009 | 2D sprite or Lottie, Live2D, or 3D VRM via three.js. | When the mirror UI is built |
| D33 | **Power and reliability:** UPS, behaviour when the host is down | 0004 | | When KiwiBot runs always-on |

## Security baseline

| ID | Item | Source | Candidates / notes | Revisit when |
|---|---|---|---|---|
| D34 | **Security baseline** (cheap early protections despite 0014) | 0014 | Secrets out of git (`.env`, git-ignored); what data may go to cloud models (earlier draft: never raw audio, private memory, credentials, network details or camera feeds); least privilege. | Before sensitive data or credentials are involved |
| D35 | **Network and remote access** | 0008, 0014 | Earlier draft: services bound to LAN or localhost, no inbound ports, remote access only via VPN (WireGuard or Tailscale), IoT VLAN. | Before the phone app is used outside the home |
| D36 | **Kill switches and privacy controls** | 0014 | Earlier draft: a `local_only` hard switch, and a mute/privacy button on satellites. | With D34 |
