---
id: pattern:inline-blocking-guard
type: pattern
title: Inline blocking guardrail
status: active
confidence: 0.8
sources:
  - raw/2026-05-16-guard-demo-client-orchestrator-seams.md
  - raw/2026-05-16-guard-demo-client-lakera-mapping.md
created: 2026-05-16
updated: 2026-05-16
updated_log:
  - 2026-05-16: created
tiers: procedural
half_life_days: 180
tags: [deck, pattern, deployment]
---

# Inline blocking guardrail

## Summary

The simplest deployment pattern: the application calls the guardrail
*synchronously* before (input check) and after (output check) the LLM call,
and refuses to return any content that fails. Latency cost = 1-2 extra HTTP
RTTs per turn; coverage is highest because everything goes through the same
checkpoint. Two failure modes worth knowing: **(a)** the pre-check sees the
user message but not the system prompt, so context-dependent injections may
slip through; **(b)** the post-check sees the assistant draft but is often
called *before* tool invocation — tool-call args may need a separate
mid-flight guard.

## Claims

- guard-demo-client implements pre + post inline checks in `agent.run_agent`:
  pre-check on user input only, post-check on user + assistant turn.
  `[src: raw/2026-05-16-guard-demo-client-orchestrator-seams.md] {conf: 0.8}`
- Two-toggle UX: `lakera_enabled` and `lakera_blocking_mode`. Blocking mode
  refuses content; monitoring mode lets it through and records the result.
  `[src: raw/2026-05-16-guard-demo-client-lakera-mapping.md] {conf: 0.9}`
- The "Overall Status Pill" UX maps `flagged + detected[*]` into `OK / WARN /
  BLOCK` — a simple but expressive surface for live demos.
  `[src: raw/2026-05-16-guard-demo-client-lakera-mapping.md] {conf: 0.8}`

## Relationships

- uses → [[detector:lakera-guard]]
- mitigates → [[attack:prompt-injection-direct]]
- mitigates → [[attack:pii-extraction]]
- alternative-to → [[pattern:proxy-guardrail]]
- alternative-to → [[pattern:async-monitoring]]

## Open questions

- [ ] Where should the *tool-call argument* check live in this pattern?

## Changelog
- 2026-05-16 — created
