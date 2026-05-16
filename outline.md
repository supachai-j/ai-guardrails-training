# Outline — Production AI Guardrails

12 modules, Expert tier. Every module cites ≥1 wiki page (Phase 5 quality gate).

| # | Module | Wiki pages cited |
|---|---|---|
| 1 | Why LLM apps fail differently | `concept:llm-failure-modes` |
| 2 | Threat model for an agentic system | `concept:agentic-threat-surface` |
| 3 | `guard-demo-client` architecture walkthrough | `concept:agentic-threat-surface`, `pattern:inline-blocking-guard` |
| 4 | Prompt injection — direct + indirect | `attack:prompt-injection-direct`, `attack:prompt-injection-indirect`, `detector:lakera-guard` |
| 5 | PII & secret extraction | `attack:pii-extraction`, `detector:lakera-guard` |
| 6 | Tool & agent abuse | `attack:tool-abuse`, `concept:agentic-threat-surface` |
| 7 | RAG poisoning | `attack:rag-poisoning`, `attack:prompt-injection-indirect` |
| 8 | Building a detector eval harness | `concept:detector-eval` |
| 9 | Observability & telemetry | `pattern:async-monitoring`, `concept:detector-eval` |
| 10 | Deployment patterns | `pattern:inline-blocking-guard`, `pattern:proxy-guardrail`, `pattern:async-monitoring` |
| 11 | Adversarial considerations & limits | `attack:jailbreak`, `concept:llm-failure-modes` |
| 12 | Open problems & reading list | (frontier — references all wiki pages) |

**Coverage check:** 14/14 wiki pages cited at least once. ✓
