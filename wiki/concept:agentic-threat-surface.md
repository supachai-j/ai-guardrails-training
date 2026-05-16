---
id: concept:agentic-threat-surface
type: concept
title: Threat surface of an agentic LLM system
status: active
confidence: 0.7
sources:
  - raw/2026-05-16-owasp-llm-top-10.md
  - raw/2026-05-16-mcp-specification-2024-11-05.md
  - raw/2026-05-16-guard-demo-client-orchestrator-seams.md
created: 2026-05-16
updated: 2026-05-16
updated_log:
  - 2026-05-16: created
tiers: semantic
half_life_days: 180
tags: [deck, foundations, threat-modeling]
---

# Threat surface of an agentic LLM system

## Summary

An agentic LLM system has five distinct attackable boundaries that classical
threat-modeling frameworks (STRIDE, LINDDUN) need to be re-mapped onto:
**input** (user prompt + system prompt), **output** (model response and
downstream rendering), **tool surface** (function calls and their arguments),
**RAG retrieval** (any retrieved-context channel), and **agent loop**
(multi-step planning that compounds errors and intent). A guardrail strategy
should explicitly own each axis.

## Claims

- The classical reactor "ReAct" loop (retrieve → tool? → LLM → respond →
  Lakera check) has at least 7 ordered stages, each a potential checkpoint.
  `[src: raw/2026-05-16-guard-demo-client-orchestrator-seams.md] {conf: 0.8}`
- MCP makes tool capability discovery dynamic and explicitly requires user
  consent before tool invocation because tools "represent arbitrary code
  execution". `[src: raw/2026-05-16-mcp-specification-2024-11-05.md] {conf: 0.8}`
- OWASP names "LLM08: Excessive Agency" as a top-10 risk, indicating that
  granting agentic autonomy without bounds is a recognised industry-level
  threat class. `[src: raw/2026-05-16-owasp-llm-top-10.md] {conf: 0.7}`
- "LLM07: Insecure Plugin Design" maps to tool-surface attacks — RCE-class
  exploits via insufficient access control on plugins.
  `[src: raw/2026-05-16-owasp-llm-top-10.md] {conf: 0.7}`

## Relationships

- composes → [[attack:prompt-injection-direct]]
- composes → [[attack:prompt-injection-indirect]]
- composes → [[attack:tool-abuse]]
- composes → [[attack:rag-poisoning]]
- composes → [[attack:data-exfiltration]]

## Open questions

- [ ] How should STRIDE categories map onto the 5-axis decomposition we use here?

## Changelog
- 2026-05-16 — created
