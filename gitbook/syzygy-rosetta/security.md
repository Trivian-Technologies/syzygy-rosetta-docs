# Security

## Security Model

Rosetta is designed with a security-first architecture. As a governance middleware handling sensitive AI inputs and outputs — including content from healthcare, financial, and enterprise environments — security is not a Phase 3 consideration. It is a baseline requirement.

---

## Current Security Measures (MVP)

### Input Sanitization
All inputs passed to `POST /evaluate` are sanitized before entering the evaluation pipeline. Malformed inputs, injection attempts, and oversized payloads are rejected before processing begins.

### Secure Logging
Evaluation logs are written to structured JSON files with controlled access. Sensitive content in logs is handled according to the context metadata provided — healthcare and finance inputs receive additional handling consideration.

### Docker Isolation
Rosetta runs inside a Docker container. The containerized architecture ensures:
- Process isolation from the host system
- Defined network boundaries
- Reproducible, tamper-evident deployment environments
- No direct access to host filesystem or resources

### Access Control (Planned — Phase 3)
API key management, role-based access control, and authentication enforcement are Phase 3 deliverables. In MVP / local deployment, access control is the responsibility of the deploying organization's network configuration.

---

## Data Handling

### What Rosetta Processes
Rosetta evaluates the content of AI prompts and outputs. It does not store or transmit this content beyond the local logging system unless explicitly configured to do so.

### Log Storage
Evaluation logs are stored locally at `logs/evaluations.json`. In production deployments, log storage should be configured to comply with the data retention policies of the deploying organization.

### Data Minimization
Rosetta applies the principle of least data — it collects and retains only what is necessary for evaluation, decision-making, and audit purposes.

---

## Threat Model

Rosetta is designed to defend against the following threat categories in AI systems:

| Threat | How Rosetta Addresses It |
|---|---|
| Prompt injection | Safety tagging layer detects and flags injection patterns |
| Authority spoofing | `authority` tag classification flags false authority claims |
| Privilege escalation | `escalation` tag classification detects scope override attempts |
| Policy circumvention | Deterministic rule engine cannot be bypassed through prompt manipulation |
| Data extraction | Violation taxonomy includes data exfiltration patterns |
| Model manipulation | Rewrite and escalation logic intercepts manipulation attempts before output |

---

## Compliance Roadmap

Trivian Technologies is committed to formal compliance certification as the product scales.

### Phase 3 Targets

**SOC 2 Type II**
Service Organization Control 2 — security, availability, processing integrity, confidentiality, and privacy controls for service organizations.

**ISO 27001 (Planned)**
Information security management system standard — formal certification of Trivian's information security practices.

**Regional AI Regulatory Alignment**
As AI regulation frameworks mature globally (EU AI Act, US Executive Orders, UK AI Safety frameworks), Rosetta's governance logic will be updated to align with applicable requirements.

---

## Responsible Disclosure

If you identify a security vulnerability in Rosetta or Trivian Technologies infrastructure, please report it responsibly.

**Contact:** se@trivianinstitute.org

Include:
- Description of the vulnerability
- Steps to reproduce
- Potential impact assessment
- Your contact details

We commit to acknowledging reports within 72 hours and providing a remediation timeline within 14 days.

---

*Security documentation is updated as the product evolves. Last updated: March 2026.*
