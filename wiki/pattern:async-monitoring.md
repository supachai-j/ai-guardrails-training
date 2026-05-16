---
id: pattern:async-monitoring
type: pattern
title: Async monitoring (post-hoc scanning)
status: active
confidence: 0.6
sources:
  - raw/2026-05-16-guard-demo-client-lakera-mapping.md
  - raw/2026-05-16-litellm-proxy-guardrails.md
  - raw/2026-05-16-nist-ai-rmf.md
created: 2026-05-16
updated: 2026-05-16
updated_log:
  - 2026-05-16: created
tiers: procedural
half_life_days: 180
tags: [deck, pattern, deployment, observability]
---

# Async monitoring (post-hoc scanning)

## Summary

When latency budget is tight or coverage of high-recall detectors would push
SLA off-cliff, run the guardrail *after* the response has shipped — typically
as a side-effect on a queue. You can't block individual responses but you can
build a near-real-time feed of flagged events for SecOps review, retroactively
suspend the offending session, and feed labelled events into your detector
eval set. LiteLLM's `logging_only` mode is exactly this pattern.

## Claims

- LiteLLM's `logging_only` mode "Masks content in logs without blocking
  requests" — the canonical async path.
  `[src: raw/2026-05-16-litellm-proxy-guardrails.md] {conf: 0.9}`
- guard-demo-client's "monitoring mode" (`lakera_blocking_mode = false`) is
  the inline analog: still synchronous, still inserts the result into the UI,
  but does not refuse the response.
  `[src: raw/2026-05-16-guard-demo-client-lakera-mapping.md] {conf: 0.8}`
- NIST AI RMF's "Measure" and "Manage" functions explicitly call out
  ongoing measurement of risk and operational management — i.e. monitoring
  is a first-class part of the framework, not an afterthought.
  `[src: raw/2026-05-16-nist-ai-rmf.md] {conf: 0.6}`

## Relationships

- alternative-to → [[pattern:inline-blocking-guard]]
- composes → [[concept:detector-eval]]
- uses → [[detector:lakera-guard]]

## Open questions

- [ ] What's the right SLO for time-to-flag in monitoring mode?

## Changelog
- 2026-05-16 — created
