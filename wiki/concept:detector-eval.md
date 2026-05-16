---
id: concept:detector-eval
type: concept
title: Detector evaluation methodology
status: active
confidence: 0.7
sources:
  - raw/2026-05-16-jailbreakbench.md
  - raw/2026-05-16-promptbench-robustness.md
  - raw/2026-05-16-nist-ai-rmf.md
created: 2026-05-16
updated: 2026-05-16
updated_log:
  - 2026-05-16: created
tiers: semantic
half_life_days: 180
tags: [deck, eval, methodology]
---

# Detector evaluation methodology

## Summary

A guardrail vendor's marketing claims (e.g. "99% prompt-injection detection")
collapse into uselessness without **your** dataset, **your** cost matrix,
and **your** latency budget. The minimum viable eval harness has four pieces:
(1) a labelled dataset spanning realistic attacker payloads + benign edge
cases, (2) a scoring function that weighs FP and FN by their business cost,
(3) a latency budget gate, and (4) reproducible runs. PromptBench / PromptRobust
and JailbreakBench are useful starting datasets; your own production traffic
(sampled + labelled) is what makes the eval realistic.

## Claims

- JailbreakBench v1.0 ships 100 OpenAI-policy-aligned harmful behaviors and
  a Llama-3-70B jailbreak judge, with reproducible attack and defense
  leaderboards. `[src: raw/2026-05-16-jailbreakbench.md] {conf: 0.9}`
- PromptRobust generates 4,788 adversarial prompts across 8 tasks × 13
  datasets at character / word / sentence / semantic levels.
  `[src: raw/2026-05-16-promptbench-robustness.md] {conf: 0.9}`
- NIST AI RMF's "Measure" function frames eval as a continuous activity, not
  a one-time benchmark — i.e. test sets should rotate as the threat landscape
  shifts. `[src: raw/2026-05-16-nist-ai-rmf.md] {conf: 0.6}`

## Relationships

- composes → [[pattern:async-monitoring]] (feeds eval set from prod)
- evaluates → [[detector:lakera-guard]]
- uses → `source:jailbreakbench`
- uses → `source:promptbench`

## Open questions

- [ ] What's the right floor for "minimum prod sample size" to label per week?

## Changelog
- 2026-05-16 — created
