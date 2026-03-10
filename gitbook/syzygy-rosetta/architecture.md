# Architecture

## System Overview

Rosetta is a containerized, API-first governance middleware. Its architecture is designed around a single principle: **every AI input and output must pass through a structured evaluation pipeline before reaching production.**

```
┌─────────────────────────────────────────────┐
│              INPUT (Prompt / Output)         │
└───────────────────┬─────────────────────────┘
                    ↓
┌─────────────────────────────────────────────┐
│           SAFETY TAGGING LAYER              │
│   Pre-classification before evaluation      │
└───────────────────┬─────────────────────────┘
                    ↓
┌─────────────────────────────────────────────┐
│         POLICY ENGINE (Deterministic)       │
│   Rule-based enforcement + taxonomy         │
│   Violation classification                  │
│   Rewrite / escalation triggers             │
└───────────────────┬─────────────────────────┘
                    ↓
┌─────────────────────────────────────────────┐
│       ML RISK SCORING ENGINE                │
│   Probabilistic risk score (0.0 – 1.0)      │
│   Confidence scoring                        │
│   Failure / anomaly detection               │
└───────────────────┬─────────────────────────┘
                    ↓
┌─────────────────────────────────────────────┐
│           DECISION LAYER                    │
│   Combines deterministic + ML signals       │
│   Returns: allow / rewrite / escalate       │
└───────────────────┬─────────────────────────┘
                    ↓
┌─────────────────────────────────────────────┐
│         LOGGING & AUDIT SYSTEM              │
│   Full evaluation history                   │
│   Decision traceability                     │
│   Drift detection                           │
│   Compliance log export                     │
└───────────────────┬─────────────────────────┘
                    ↓
┌─────────────────────────────────────────────┐
│        STRUCTURED OUTPUT (JSON)             │
│   decision, risk_score, confidence,         │
│   violations, rewrite, metadata             │
└─────────────────────────────────────────────┘
```

---

## Core Components

### 1. Safety Tagging Layer

Before an input enters the main evaluation pipeline, it passes through a pre-classification layer that tags the content by risk category.

Tags include:
- `authority` — attempts to invoke false authority or override constraints
- `manipulation` — attempts to bypass governance logic through social engineering
- `dependency` — attempts to create unhealthy reliance patterns
- `escalation` — attempts to escalate privileges or scope beyond defined boundaries

Safety tags are **non-blocking** — they inform the evaluation pipeline without stopping execution. They feed directly into risk scoring.

---

### 2. Policy Engine (Deterministic Layer)

The policy engine is the rule enforcement core of Rosetta. It applies a defined violation taxonomy to every input and output.

**What it does:**
- Applies rule-based safety enforcement
- Classifies outputs against a violation taxonomy
- Triggers rewrite logic for soft violations
- Triggers escalation for hard violations

**Key properties:**
- Fully deterministic — same input always produces same policy outcome
- Configurable — rules can be adjusted per environment or industry context
- Taxonomy-driven — violations are classified and logged with structured categories

**Threshold logic:**

| Risk Score | Decision |
|---|---|
| `< 0.4` | `allow` |
| `0.4 – 0.7` | `rewrite` |
| `> 0.7` | `escalate` |

---

### 3. ML Risk Scoring Engine

The ML risk scoring module assigns probabilistic risk scores to inputs and outputs based on content classification, contextual metadata, and historical patterns.

**Outputs:**
- `risk_score` — float between 0.0 and 1.0
- `confidence` — float between 0.0 and 1.0 indicating scoring certainty

**Inputs considered:**
- Content classification from safety tags
- Industry context (`finance | healthcare | general`)
- Environment (`production | staging`)
- Historical evaluation patterns

The ML layer works in combination with the deterministic policy engine — it does not replace rule enforcement, it augments it with probabilistic context.

---

### 4. Decision Layer

The decision layer combines the outputs of the policy engine and the ML risk scoring module into a single structured decision.

**Decision logic:**

```python
def calculate_risk(tags, rewrite_flag):
    score = 0.0
    if rewrite_flag:
        score += 0.4
    if "authority" in tags:
        score += 0.3
    return score
```

The decision layer is the final arbiter. It produces the response returned by `POST /evaluate`.

---

### 5. Logging & Audit System

Every evaluation is logged to `logs/evaluations.json` with full metadata.

**Logged fields:**
- Timestamp (ISO8601)
- Input prompt or output
- Safety tags assigned
- Policy violations detected
- Risk score and confidence
- Decision made
- Rewrite flag status
- Environment and industry context

**Audit capabilities:**
- Full evaluation history
- Decision traceability
- Drift detection — confidence decay tracking over time
- Compliance log export (PDF/CSV — Phase 2)

---

### 6. Deployment Layer

Rosetta is Dockerized and infrastructure-agnostic.

```dockerfile
FROM python:3.11
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
EXPOSE 8000
CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000"]
```

It can be deployed on any cloud provider, on-premise environment, or local development setup without modification.

[Full deployment guide →](deployment-guide.md)

---

## Technology Stack

| Layer | Technology |
|---|---|
| API Framework | FastAPI |
| Runtime | Python 3.11 |
| Containerization | Docker |
| Server | Uvicorn |
| Logging | JSON file store (→ database in Phase 2) |
| ML Scoring | Rule-based (→ trained model in Phase 2) |

---

## Design Principles

**Middleware, not model** — Rosetta does not generate outputs. It evaluates them.

**Separation of concerns** — each component of the pipeline is independently replaceable.

**Fail-safe defaults** — if scoring is uncertain, escalate. Never allow by default in high-risk contexts.

**Minimal surface area** — one endpoint, one decision, one output schema. Simplicity is a security property.

[View the API documentation →](api-docs.md)
