---
id: pattern:proxy-guardrail
type: pattern
title: Proxy-native guardrail
status: active
confidence: 0.7
sources:
  - raw/2026-05-16-litellm-proxy-guardrails.md
  - raw/2026-05-16-guard-demo-client-lakera-mapping.md
created: 2026-05-16
updated: 2026-05-16
updated_log:
  - 2026-05-16: created
tiers: procedural
half_life_days: 180
tags: [deck, pattern, deployment, litellm]
---

# Proxy-native guardrail

## Summary

Instead of calling the guardrail from the app, host an OpenAI-compatible proxy
(LiteLLM, Portkey, etc.) and let it run the guardrail before/during/after the
upstream LLM call. The app code becomes vendor-agnostic — it just calls
`POST /v1/chat/completions` — and you can add or swap guardrails without
shipping new app code. Trade-off: the application loses fine-grained control
of *when* the guardrail runs (it follows the proxy's mode) and the proxy
becomes a load-bearing single point of failure.

## Claims

- LiteLLM proxy supports four execution modes per guardrail: `pre_call`,
  `during_call`, `post_call`, `logging_only`. Modes can be combined for the
  same guardrail. `[src: raw/2026-05-16-litellm-proxy-guardrails.md] {conf: 0.9}`
- A successful pass-through is observable via the response header
  `x-litellm-applied-guardrails: <guardrail-name>`.
  `[src: raw/2026-05-16-litellm-proxy-guardrails.md] {conf: 0.8}`
- A blocked request returns HTTP 400 with structured detail — the body
  contains `error.message.error: "Violated guardrail policy"` and a vendor
  payload (e.g. `aporia_ai_response` for Aporia).
  `[src: raw/2026-05-16-litellm-proxy-guardrails.md] {conf: 0.9}`
- guard-demo-client has explicit code to extract Lakera details from the
  LiteLLM 400 body (`_extract_litellm_guardrail_status`) and reshape it into
  the same UI status object used by the direct-API path — i.e. the same UI
  works in both deployment patterns.
  `[src: raw/2026-05-16-guard-demo-client-lakera-mapping.md] {conf: 0.7}`

## Relationships

- alternative-to → [[pattern:inline-blocking-guard]]
- uses → [[detector:lakera-guard]]
- uses → [[tool:litellm-proxy]]
- mitigates → [[attack:prompt-injection-direct]]

## Open questions

- [ ] How does `during_call` parallelism affect tail latency vs. `pre_call` + `post_call`?

## Changelog
- 2026-05-16 — created
