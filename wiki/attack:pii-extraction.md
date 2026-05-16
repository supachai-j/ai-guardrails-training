---
id: attack:pii-extraction
type: attack
title: PII and secret extraction
status: active
confidence: 0.7
sources:
  - raw/2026-05-16-owasp-llm-top-10.md
  - raw/2026-05-16-guard-demo-client-lakera-mapping.md
  - raw/2026-05-16-litellm-proxy-guardrails.md
created: 2026-05-16
updated: 2026-05-16
updated_log:
  - 2026-05-16: created
tiers: semantic
half_life_days: 180
tags: [deck, attack, pii]
---

# PII and secret extraction

## Summary

The attacker tries to coerce the model into revealing sensitive information —
either training-data PII, secrets in the system prompt (API keys, instructions),
or other customers' data accessible via RAG / tool outputs. Detection happens
at *both* sides: input ("show me all SSNs") and output ("here is the SSN list…").
Lakera maps PII into a dedicated detector class (`pii/credit_card`, `pii/iban_code`,
`pii/us_social_security_number`, etc.); Presidio offers a deterministic
alternative for regulated environments.

## Claims

- OWASP LLM06 "Sensitive Information Disclosure" identifies output-side
  leakage as a top-10 risk class.
  `[src: raw/2026-05-16-owasp-llm-top-10.md] {conf: 0.9}`
- Lakera defines PII as its own detector subtree with named subtypes:
  `pii/address`, `pii/credit_card`, `pii/iban_code`, `pii/ip_address`,
  `pii/us_social_security_number`.
  `[src: raw/2026-05-16-guard-demo-client-lakera-mapping.md] {conf: 0.9}`
- Presidio (open-source) lets you map PII entities to actions per type
  (e.g. `CREDIT_CARD: MASK`, `US_SSN: MASK`) with per-entity score thresholds.
  `[src: raw/2026-05-16-litellm-proxy-guardrails.md] {conf: 0.8}`

## Relationships

- detected-by → [[detector:lakera-guard]] (`pii/*` family)
- alternative → [[tool:presidio]]
- mitigated-by → [[pattern:inline-blocking-guard]]

## Open questions

- [ ] What is the false-positive rate of Lakera `pii/credit_card` on test-credit-card patterns in dev environments?

## Changelog
- 2026-05-16 — created
