---
id: attack:jailbreak
type: attack
title: Jailbreak attacks
status: active
confidence: 0.7
sources:
  - raw/2026-05-16-jailbreakbench.md
  - raw/2026-05-16-anthropic-constitutional-ai.md
created: 2026-05-16
updated: 2026-05-16
updated_log:
  - 2026-05-16: created
tiers: semantic
half_life_days: 180
tags: [deck, attack, jailbreak]
---

# Jailbreak attacks

## Summary

A jailbreak coerces a *safety-trained* LLM to produce content that violates
its provider's policy (CSAM, weapons synthesis, etc.). Distinct from prompt
injection in that the target is the model's safety alignment, not the
surrounding application's logic. JailbreakBench standardises the benchmark
with 100 OpenAI-policy-aligned harmful behaviors and tracks both attacks and
defenses on a public leaderboard.

## Claims

- Jailbreak: "Jailbreak attacks cause large language models (LLMs) to generate
  harmful, unethical, or otherwise objectionable content."
  `[src: raw/2026-05-16-jailbreakbench.md] {conf: 0.9}`
- JailbreakBench v1.0 includes 100 behaviors aligned to OpenAI's policy and
  an Llama-3-70B jailbreak judge.
  `[src: raw/2026-05-16-jailbreakbench.md] {conf: 0.8}`
- Constitutional AI demonstrates an alternative defense path — harmlessness
  from AI feedback (RLAIF) using a constitution rather than human harm-labels.
  `[src: raw/2026-05-16-anthropic-constitutional-ai.md] {conf: 0.7}`

## Relationships

- alternative-to → [[attack:prompt-injection-direct]] `{conf: 0.5}` (overlap, distinct intent)
- detected-by → [[detector:lakera-guard]] `{conf: 0.6}` (`moderated_content/*`)
- mitigated-by → [[pattern:inline-blocking-guard]]

## Open questions

- [ ] Are detector taxonomies converging across vendors (Lakera, Aporia, Bedrock)?

## Changelog
- 2026-05-16 — created
