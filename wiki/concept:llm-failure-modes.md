---
id: concept:llm-failure-modes
type: concept
title: Why LLM apps fail differently
status: active
confidence: 0.7
sources:
  - raw/2026-05-16-owasp-llm-top-10.md
  - raw/2026-05-16-promptbench-robustness.md
  - raw/2026-05-16-anthropic-constitutional-ai.md
created: 2026-05-16
updated: 2026-05-16
updated_log:
  - 2026-05-16: created
tiers: semantic
half_life_days: 180
tags: [deck, foundations]
---

# Why LLM apps fail differently

## Summary

Classical web apps fail when validation is missing; LLM apps fail because the
underlying model is **trained** to follow instructions in its input — there's no
clean boundary between "data" and "instructions" once both are tokens in the
context window. Defense therefore moves from input validation to detector
stacks, monitoring, and architectural choices that bound damage.

## Claims

- LLMs blur the data/instruction boundary because both arrive as tokens in the
  same context window. `[src: raw/2026-05-16-greshake-indirect-prompt-injection.md] {conf: 0.7}`
- Instruction-tuning + RLHF creates a strong inductive bias toward following
  any text that looks like an instruction, even from untrusted sources.
  `[src: raw/2026-05-16-anthropic-constitutional-ai.md] {conf: 0.6}`
- The OWASP LLM Top 10 codifies 10 vulnerability classes including prompt
  injection (LLM01), insecure output handling (LLM02), excessive agency
  (LLM08), and overreliance (LLM09). `[src: raw/2026-05-16-owasp-llm-top-10.md] {conf: 0.8}`
- LLMs are *not* robust to adversarial prompts at the character, word,
  sentence, or semantic level — across 8 tasks and 13 datasets.
  `[src: raw/2026-05-16-promptbench-robustness.md] {conf: 0.7}`
- The "no robust defense" claim is the empirical baseline:
  "I have not yet seen a robust defense against this vulnerability which is
  guaranteed to work 100% of the time."
  `[src: raw/2026-05-16-simon-willison-prompt-injection-worst-case.md] {conf: 0.7}`

## Relationships

- composes → [[concept:agentic-threat-surface]] `{conf: 0.7}`
- cites → `source:owasp-llm-top-10`
- cites → `source:promptbench`

## Open questions

- [ ] Is there a meaningful gap between LLMs trained with Constitutional AI vs. pure RLHF in adversarial robustness?

## Changelog
- 2026-05-16 — created
