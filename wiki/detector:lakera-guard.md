---
id: detector:lakera-guard
type: detector
title: Lakera Guard detector classes
status: active
confidence: 0.8
sources:
  - raw/2026-05-16-guard-demo-client-lakera-mapping.md
  - raw/2026-05-16-litellm-proxy-guardrails.md
created: 2026-05-16
updated: 2026-05-16
updated_log:
  - 2026-05-16: created
tiers: semantic
half_life_days: 180
tags: [deck, detector, lakera]
---

# Lakera Guard detector classes

## Summary

Lakera Guard exposes a single REST endpoint (`POST /v2/guard`) that returns a
per-detector breakdown rather than a single yes/no. Detectors fall into four
families: `prompt_attack`, `moderated_content/*` (crime, hate, profanity,
sexual, violence, weapons), `pii/*` (address, credit_card, iban_code,
ip_address, us_social_security_number), and `unknown_links`. The `flagged`
top-level boolean is the union of all per-detector signals; production code
should usually consume the breakdown directly.

## Claims

- The Lakera v2 request shape is `{messages, project_id, metadata, breakdown,
  payload, dev_info}` where `messages` is the full conversational turn under
  evaluation (system + user, or system + user + assistant for post-checks).
  `[src: raw/2026-05-16-guard-demo-client-lakera-mapping.md] {conf: 0.9}`
- The response includes `breakdown[]`, each entry carrying
  `{project_id, policy_id, detector_id, detector_type, detected, message_id}`
  — `detector_type` is the dimension to read for category-level metrics.
  `[src: raw/2026-05-16-guard-demo-client-lakera-mapping.md] {conf: 0.9}`
- Detector categories present in guard-demo-client's UI mapping:
  `prompt_attack`, `unknown_links`, `moderated_content/{crime,hate,profanity,sexual,violence,weapons}`,
  `pii/{address,credit_card,iban_code,ip_address,us_social_security_number}`.
  `[src: raw/2026-05-16-guard-demo-client-lakera-mapping.md] {conf: 0.9}`
- Lakera is one of LiteLLM's supported guardrail providers and can run in
  any of `pre_call / during_call / post_call / logging_only` modes from
  the proxy. `[src: raw/2026-05-16-litellm-proxy-guardrails.md] {conf: 0.8}`

## Relationships

- detects → [[attack:prompt-injection-direct]]
- detects → [[attack:pii-extraction]] (`pii/*`)
- detects → [[attack:jailbreak]] (`moderated_content/*`)
- detects → [[attack:data-exfiltration]] (`unknown_links`, partial)
- composes → [[pattern:inline-blocking-guard]]

## Open questions

- [ ] What's the latency p99 of `/v2/guard` for a single message-turn?

## Changelog
- 2026-05-16 — created
