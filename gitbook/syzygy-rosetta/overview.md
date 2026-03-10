# Syzygy Rosetta — Overview

## What Is Syzygy Rosetta?

Syzygy Rosetta is an API-first AI governance middleware built by Trivian Technologies.

It sits between users or applications and the AI models they rely on — evaluating every prompt and response before it reaches production systems.

Rosetta is:

- **Not a chatbot**
- **Not a UI layer**
- **Not a foundation model**
- **Not a monitoring tool**

**It is a decision engine.**

---

## What It Does

Rosetta evaluates AI inputs and outputs through three layers:

1. **Deterministic policy rules** — hard enforcement of defined constraints
2. **ML-based risk scoring** — probabilistic assessment of risk and confidence
3. **Structured decision logic** — combines both signals into a single, auditable output

Every evaluation returns one of three decisions:

| Decision | Meaning |
|---|---|
| `allow` | Input/output is within acceptable parameters — proceed |
| `rewrite` | Input/output violates soft constraints — modify before proceeding |
| `escalate` | Input/output violates hard constraints — route to human review |

---

## The Core Endpoint

All interactions with Rosetta happen through a single endpoint:

```
POST /evaluate
```

Send a prompt or AI output. Receive a structured governance decision.

```json
{
  "decision": "allow",
  "risk_score": 0.12,
  "confidence": 0.91,
  "violations": [],
  "rewrite": null,
  "timestamp": "2026-03-10T00:00:00Z"
}
```

[Full API documentation →](api-docs.md)

---

## Where Rosetta Sits

```
[ User / Application ]
        ↓
[ Syzygy Rosetta — POST /evaluate ]
        ↓
[ AI Model / LLM ]
        ↓
[ Rosetta evaluates response ]
        ↓
[ allow / rewrite / escalate ]
        ↓
[ Production System ]
```

Rosetta does not replace the model. It governs it.

---

## Key Properties

**API-first** — integrate with any stack via a single REST endpoint. No SDK required to get started.

**Dockerized** — deploy anywhere. Infrastructure-agnostic. Runs in any containerized environment.

**Deterministic + ML hybrid** — rule-based enforcement combined with probabilistic risk scoring gives you both precision and adaptability.

**Fully auditable** — every evaluation is logged with full metadata, decision traceability, and compliance export support.

**Industry-aware** — context-sensitive evaluation for finance, healthcare, and general enterprise environments.

---

## Current Status

Syzygy Rosetta is in active MVP development. The core `POST /evaluate` endpoint is functional. Codebase refactor and ML layer integration are in progress.

[View the roadmap →](roadmap.md)

---

## Next Steps

- [Understand the problem Rosetta solves →](problem.md)
- [Explore the architecture →](architecture.md)
- [Read the API documentation →](api-docs.md)
- [Deploy Rosetta locally →](deployment-guide.md)
