# Syzygy Rosetta — Documentation

> **Official Technical Documentation for Syzygy Rosetta and Trivian Technologies**

[![GitBook](https://img.shields.io/badge/Docs-GitBook-blue.svg)]()
[![Status: Active](https://img.shields.io/badge/Status-Active-green.svg)]()

---

## Overview

This repository contains the source markdown files for the official Syzygy Rosetta and Trivian Technologies documentation, published via GitBook.

---

## Documentation Structure

```
syzygy-rosetta-docs/
│
├── README.md                          ← GitBook landing page
├── SUMMARY.md                         ← GitBook navigation
│
├── trivian-technologies/
│   ├── introduction.md                ← About Trivian Technologies
│   ├── vision-and-mission.md          ← Mission, vision, principles
│   ├── team.md                        ← Team structure
│   └── governance-philosophy.md       ← Core governance principles
│
└── rosetta/
    ├── overview.md                    ← What Rosetta is
    ├── problem.md                     ← Problem statement
    ├── architecture.md                ← System architecture
    ├── api-docs.md                    ← POST /evaluate reference
    ├── use-cases.md                   ← Deployment use cases
    ├── roadmap.md                     ← Phase 1–4 roadmap
    ├── governance-dashboard.md        ← Dashboard spec (Phase 2)
    ├── security.md                    ← Security model
    ├── deployment-guide.md            ← Docker deployment guide
    ├── contributing.md                ← Contribution guidelines
    └── contact.md                     ← Contact and partnerships
```

---

## API Reference — Quick Summary

The primary endpoint is `POST /evaluate`. Full reference is in `rosetta/api-docs.md`.

**Request:**

```json
{
  "input": "string",
  "context": {
    "user_id": "string (optional)",
    "environment": "production | staging",
    "industry": "finance | healthcare | general"
  }
}
```

**Response — 8 fields, always:**

```json
{
  "decision": "allow | rewrite | escalate",
  "risk_score": 0.12,
  "confidence": 0.91,
  "violations": [],
  "rewrite": null,
  "reasoning": "string",
  "field_notes": [],
  "timestamp": "2026-03-21T14:32:00Z"
}
```

---

## Reading the Docs

The documentation is published via GitBook. For the full rendered documentation, visit the GitBook link above.

If you are contributing to the documentation, work directly with the markdown files in this repository.

---

## Contributing to Documentation

Documentation contributions are welcome. If you find an error, a gap, or something that needs updating:

1. Fork this repository
2. Make your changes in the relevant markdown file
3. Open a pull request with a clear description of what you changed and why

**Keep it accurate.** Do not add content that describes features or capabilities not yet built. Mark planned features clearly with their roadmap phase.

---

## Markdown Conventions

- Use `#` for page titles — one per page
- Use `##` for major sections
- Use `###` for subsections
- Code blocks use triple backticks with language identifiers
- Tables use standard GitHub markdown table syntax
- Internal links use relative paths: `[Architecture](rosetta/architecture.md)`

---

## Related Repositories

| Repository | Role |
|---|---|
| [syzygy-rosetta-originbase](https://github.com/Trivian-Technologies/syzygy-rosetta-originbase) | Core governance engine |
| [syzygy-rosetta-sandbox](https://github.com/Trivian-Technologies/syzygy-rosetta-sandbox) | Testing and simulation |
| [syzygy-rosetta-sdk](https://github.com/Trivian-Technologies/syzygy-rosetta-sdk) | SDK (planned — Phase 4) |

---

## Organization

Part of the [Trivian Technologies](https://github.com/Trivian-Technologies) organization.

**Website:** [triviantech.com](https://triviantech.com) | **X:** [@TrivianOS](https://x.com/TrivianOS) | **LinkedIn:** [Trivian Technologies](https://www.linkedin.com/company/awakening-the-architect) | **Contact:** se@trivianinstitute.org
