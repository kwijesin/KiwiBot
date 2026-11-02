# Models

KiwiBot is **model-agnostic** (0020). Every LLM-based part connects to models through configuration, and no part is tied to one provider.

- **Building:** frontier models do **all core programming**, including self-improvement (0005). Claude is the current build model. It's not a permanent choice.
- **Day-to-day operation:** **local-first** (0005). What that means in practice for now is deferred (D09).
- **Escalation:** what triggers escalation from local to frontier models is deferred (D08).

## Local models

Local model choices and the serving runtime are deferred (D10).

| Role | Candidate | Notes |
|------|-----------|-------|
| Main chat / tool-use LLM | TODO (e.g. Llama, Qwen, Mistral, Gemma families) | Needs reliable function/tool calling |
| Small fast LLM (optional) | TODO | Intent classification, routing, quick replies |
| Embeddings | TODO | For long-term memory retrieval (D24) |
| STT | Whisper / faster-whisper, Vosk | Deferred (D21) |
| TTS | Piper / Kokoro / XTTS | Deferred (D23) |

**Serving:** candidate runtimes include Ollama, llama.cpp server, vLLM and LM Studio. An OpenAI-compatible endpoint keeps model connections simple.

## Frontier models

| Provider | Models | Use for |
|----------|--------|---------|
| Anthropic | Claude family | Core programming and self-improvement (current build model) |
| OpenAI | GPT family | Same, when connected |
| Others | TODO | |

## Routing and escalation

**Deferred (D08).** The earlier draft routing modes and escalation triggers are kept as candidates in the [deferred register](decisions/deferred.md).

## Cloud data rules

**Deferred** as part of the security baseline (D34), consistent with growth first, hardening later (0014).

## Usage tracking

**Deferred (D11).** For now, KiwiBot runs without token or attention metering (0015).

## Evaluation

**Deferred (D12).** Model evaluation will follow the testing framework (0013).
