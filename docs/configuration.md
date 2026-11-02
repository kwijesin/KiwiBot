# Configuration

> **Placeholder.** The configuration format and location haven't been decided (deferred: [D18](decisions/deferred.md)). An earlier draft schema (YAML settings and a `.env` for secrets) is kept as a candidate there.

## What configuration must cover (from decisions)

- **Model connections:** every LLM-based part is model-agnostic, and models are connected through configuration (0020).
- **Model use:** which work goes to frontier models and which runs locally (0005; triggers deferred, D08).
- **Approval tiers:** what needs my approval (0025; initial rules pending, D05).

## Secrets

Secrets handling is part of the deferred security baseline (D34). Until that's decided, keep API keys and tokens **out of git**.
