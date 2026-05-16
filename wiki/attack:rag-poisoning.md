---
id: attack:rag-poisoning
type: attack
title: RAG poisoning
status: active
confidence: 0.7
sources:
  - raw/2026-05-16-greshake-indirect-prompt-injection.md
  - raw/2026-05-16-guard-demo-client-design-overview.md
  - raw/2026-05-16-owasp-llm-top-10.md
created: 2026-05-16
updated: 2026-05-16
updated_log:
  - 2026-05-16: created
tiers: semantic
half_life_days: 180
tags: [deck, attack, rag]
---

# RAG poisoning

## Summary

A retrieval-augmented-generation system embeds a corpus and pulls top-k
chunks into the model's context. An attacker who controls *any* document
that may be retrieved can plant instructions that hijack the agent
(indirect prompt injection at the data layer). Defenses split into
**ingest-time** scanning (scan content before it enters the vector store)
and **retrieve-time** scanning (re-scan after retrieval, before the LLM
call) — the former catches the most material cheaply, but only the latter
catches embedding-collision and runtime-poisoning attacks.

## Claims

- guard-demo-client's RAG ingestion supports an optional "content scanning"
  toggle that scans each chunk during ingestion with a separate Lakera
  project ID (`rag_lakera_project_id`).
  `[src: raw/2026-05-16-guard-demo-client-design-overview.md] {conf: 0.8}`
- Indirect prompt injection via RAG is the practical instance of the
  Greshake taxonomy — "data theft" and "worming" are direct consequences.
  `[src: raw/2026-05-16-greshake-indirect-prompt-injection.md] {conf: 0.8}`
- OWASP LLM03 "Training Data Poisoning" is a related top-10 class targeting
  the training pipeline rather than the retrieval corpus.
  `[src: raw/2026-05-16-owasp-llm-top-10.md] {conf: 0.7}`

## Relationships

- extends → [[attack:prompt-injection-indirect]]
- mitigated-by → [[pattern:proxy-guardrail]] (retrieve-time)
- mitigated-by → [[pattern:inline-blocking-guard]] (ingest-time)
- depends-on → [[concept:agentic-threat-surface]]

## Open questions

- [ ] What's the latency cost of retrieve-time vs. ingest-time scanning at p99?

## Changelog
- 2026-05-16 — created
