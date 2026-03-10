# Use Cases

Rosetta is designed for any environment where AI outputs carry real consequences. Below are the primary use cases for the current MVP.

---

## 1. Enterprise AI Deployment

**The scenario:** An enterprise deploys an internal AI assistant for operations, HR, or customer service. The model is capable but uncontrolled — it can produce outputs that violate internal policy, expose sensitive information, or give incorrect guidance.

**How Rosetta helps:**
Every prompt and response passes through `POST /evaluate` before reaching the end user. Policy violations are caught before they surface. Risk is scored continuously. Every decision is logged for internal audit.

**Result:** AI deployment that legal, compliance, and operations teams can sign off on.

---

## 2. Financial Services

**The scenario:** A fintech company deploys an AI assistant for investment guidance, portfolio analysis, or customer financial advice. Regulatory frameworks (MiFID, SEC, FCA) require demonstrable compliance. Unsafe financial advice or coercive instructions carry direct legal exposure.

**How Rosetta helps:**
- Flags coercive financial instructions (`rewrite` or `escalate`)
- Detects regulatory violation patterns in AI-generated advice
- Produces audit logs suitable for compliance reporting
- Industry context (`"industry": "finance"`) activates finance-specific policy rules

**Result:** Compliant AI-assisted financial services with full audit capability.

---

## 3. Healthcare

**The scenario:** A healthcare provider or medical AI company deploys AI for patient triage, clinical documentation, or medical information retrieval. Non-compliant outputs can cause direct patient harm. HIPAA and clinical governance requirements demand auditability.

**How Rosetta helps:**
- Blocks outputs that attempt to override clinical safety protocols
- Flags non-compliant medical guidance
- Detects attempts to extract sensitive patient data
- Industry context (`"industry": "healthcare"`) activates healthcare-specific enforcement rules

**Result:** AI-assisted healthcare tools that meet clinical governance and regulatory requirements.

---

## 4. AI Agent Coordination

**The scenario:** A company deploys a multi-agent AI system where autonomous agents communicate with each other and take actions. Without governance, agents can drift — making decisions outside their defined scope, escalating their own privileges, or acting in ways that conflict with intended behavior.

**How Rosetta helps:**
- Acts as the governance layer between agents — every agent-to-agent instruction passes through `/evaluate`
- Detects escalation attempts and privilege override patterns
- Enforces boundaries on agent scope and authority
- Logs the full chain of agent decisions for traceability

**Result:** Multi-agent systems that stay within defined operational boundaries.

---

## 5. Regulated SaaS Platforms

**The scenario:** A SaaS company building on top of an LLM (GPT, Claude, Gemini, etc.) needs to ensure their AI features are compliant for enterprise customers. Enterprise buyers require compliance guarantees before signing contracts.

**How Rosetta helps:**
- Acts as a middleware layer between the SaaS platform and the underlying LLM
- Provides the compliance and audit infrastructure the SaaS company needs to sell to enterprise
- Returns structured decisions that can be surfaced to enterprise customers as compliance evidence

**Result:** LLM-powered SaaS products that can be sold into regulated enterprise environments.

---

## 6. Developer Testing & AI Safety Research

**The scenario:** An AI engineer or researcher needs to test how AI models behave under different prompt conditions — specifically around boundary violations, manipulation attempts, and policy edge cases.

**How Rosetta helps:**
- Provides a structured evaluation environment for testing prompt behavior
- Returns risk scores and confidence levels that quantify boundary proximity
- Logs all evaluations for analysis
- The sandbox environment (`syzygy-rosetta-sandbox`) is specifically designed for this use case

**Result:** A structured testing environment for AI safety research and red-teaming.

---

## Coming in Later Phases

- **Government and public sector deployment** — compliance-grade governance for public AI systems
- **Legal and professional services** — policy enforcement for AI-generated legal and professional advice
- **Education platforms** — content governance for AI tutoring and educational AI systems

[View the full roadmap →](roadmap.md)
