# Governance Dashboard

The Governance Dashboard is a Phase 2 deliverable. This page documents the design specification for the dashboard — for product designers, frontend engineers, and stakeholders reviewing the product direction.

---

## Purpose

The Governance Dashboard provides a visual interface for teams using Rosetta in production. It surfaces evaluation data, risk patterns, policy violations, and compliance exports in a format that non-technical stakeholders — compliance officers, legal teams, operations managers — can use directly.

---

## Design Tone

The dashboard is enterprise-grade infrastructure software. It is not a consumer product.

- **Minimal** — no decorative elements, no unnecessary animations
- **Data-first** — every screen exists to surface information, not impress
- **High contrast** — clear visual hierarchy, readable at a glance
- **Neutral palette** — dark backgrounds, Trivian blue accents, status colors for decision states

---

## Core Sections

### 1. Overview

The landing screen. Provides a real-time summary of system state.

**Components:**
- Total evaluations counter (rolling 24h / 7d / 30d)
- Risk distribution chart — proportion of allow / rewrite / escalate decisions
- Violation heatmap — frequency of violation categories over time
- Confidence trend line — average confidence score over time
- Recent escalations feed — last 10 escalated evaluations with timestamps

---

### 2. Evaluation Logs

A searchable, filterable table of all evaluations processed by Rosetta.

**Table columns:**
- Timestamp
- Input preview (truncated)
- Decision (allow / rewrite / escalate)
- Risk score
- Confidence
- Violations detected
- Industry context
- Environment

**Filter options:**
- Date range
- Decision type
- Risk score threshold
- Industry
- Violation category

**Row detail view:**
Click any row to expand the full evaluation record — including full input, complete response JSON, reasoning, and field notes.

---

### 3. Policy Manager

A configuration interface for managing the rules that power the Policy Engine.

**Features:**
- View all active policy rules
- Enable / disable individual rules
- Edit rule parameters (threshold adjustments, scope)
- Add custom rules (Phase 3)
- View rule trigger frequency — which rules are firing most

**Rule display format:**
```
Rule ID       | Category      | Status   | Trigger Count
--------------+---------------+----------+--------------
auth_override | authority     | active   | 142
med_sys_int   | healthcare    | active   | 38
fin_coerce    | finance       | active   | 91
```

---

### 4. Drift Monitor

Tracks model behavior changes and confidence decay over time.

**Components:**
- Confidence decay chart — rolling average confidence score, flagged when it drops below threshold
- Risk score drift — weekly average risk score shift
- Alert flags — automated alerts when drift exceeds defined thresholds
- Drift event log — timestamped records of significant drift events

**Alert thresholds (configurable):**
- Confidence drops below 0.75 for more than 100 consecutive evaluations → alert
- Average risk score increases by more than 0.15 week-over-week → alert

---

### 5. Compliance Export

Generates audit-ready reports for compliance review, legal teams, or regulatory submissions.

**Export formats:**
- PDF — formatted compliance summary report
- CSV — raw evaluation data for external analysis

**Report contents:**
- Evaluation period summary
- Decision distribution breakdown
- Violation category analysis
- Escalation log
- Drift event record
- System configuration snapshot

---

## Status Colour System

Consistent color coding across all dashboard views:

| Decision | Color | Hex |
|---|---|---|
| `allow` | Green | `#16A34A` |
| `rewrite` | Amber | `#D97706` |
| `escalate` | Red | `#DC2626` |
| Neutral / info | Blue | `#1A6FC4` |

---

## Access & Permissions (Phase 3)

In Phase 3, the dashboard will support role-based access:

| Role | Access |
|---|---|
| Admin | Full access — all sections, policy editing, exports |
| Compliance Officer | Logs, drift monitor, exports — read only |
| Developer | Logs and API reference — read only |
| Observer | Overview only |

---

## Implementation Notes for Designers

- All data visualizations should use Trivian brand colours
- No pie charts — use bar charts or treemaps for distribution data
- Tables should support keyboard navigation and screen reader accessibility
- All screens should have a functional dark mode (primary) and light mode (secondary)
- Font: to be determined by brand type system (Chineme's deliverable)
- Reference the [Brand Brief](https://triviantech.com) for full visual direction

---

*Dashboard is a Phase 2 deliverable. Design work begins once MVP is stable. Last updated: March 2026.*
