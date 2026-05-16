# Launching: Production AI Guardrails (Expert-tier, Bilingual)

**Date**: 2026-05-16
**Live site**: https://supachai-j.github.io/ai-guardrails-training/

---

## What this is

A full-day Expert-tier workshop and self-paced course on building, deploying, and
operating **guardrails for production agentic LLM apps**. Written for senior
engineers and security researchers who are already shipping AI features and now
need to put a security floor under them.

This is the sixth course in the bilingual Foundations / Production series after
*Agent Skills 101*, *Prompt Engineering 101*, *LLM Wiki 101*, *Oracle 101*, and
*Cybersec Skills 101* — same author, same teaching cadence, same EN-first +
canonical-TH-mirror discipline.

## What you get

| Deliverable | EN | TH |
|---|---|---|
| Self-paced course (12 modules, hands-on lab in every one) | `course-en.html` | `course-th.html` |
| Full-day workshop deck (72 slides, 7 inline labs) | `slides/training-en.html` | `slides/training-th.html` |
| Cited wiki (3 concepts + 7 attack pages + 1 detector + 3 patterns) | 14 pages | — (linked from TH course) |
| Primary sources captured verbatim | 14 raw files | — |

Every wiki page cites its source by file path and confidence rating; every slide
that makes a claim cites the primary literature it came from (NIST AI RMF,
OWASP LLM Top 10 2025, MITRE ATLAS, Greshake et al. 2023, Constitutional AI,
JailbreakBench, AdvBench, Embrace The Red, Simon Willison's prompt injection
post, MCP spec, LiteLLM proxy guardrails docs).

## Coverage

The 12-module course covers:

1. Why LLM apps fail differently from traditional software
2. Threat-modelling an agentic system (five-axis surface: input / output / RAG / tools / auth)
3. `guard-demo-client` architecture walkthrough (the companion reference codebase)
4. Prompt injection — direct and indirect (Greshake taxonomy)
5. PII & secret extraction (Lakera vs Presidio vs Azure Content Safety)
6. Tool & agent abuse (confused deputy [Hardy 1988] adapted to LLM tools)
7. RAG poisoning (index-time vs retrieval-time)
8. Building a detector eval harness (JailbreakBench, PromptBench, AdvBench)
9. Observability & telemetry (schemas, dashboards, alert routing)
10. Deployment patterns (inline blocking / async monitoring / proxy guardrail)
11. Adversarial considerations & limits (GCG, PAIR, Crescendo, RLHF limitations)
12. Open problems & a curated reading list

The deck adds five layers the course only summarises: **multimodal threats**
(image / document injection per OWASP LLM07 2025), **governance** (NIST AI RMF,
EU AI Act Article 6 / Annex III, SOC2 evidence), an **operational maturity model**
(Level 0–4 self-assessment), **future trends** (sandboxing, attestation, formal
verification), and a 7-step **capstone design review** at the end.

## Companion codebase: `guard-demo-client`

Every lab references the open-source companion repo
[`guard-demo-client`](https://github.com/supachai-j/guard-demo-client) — a
FastAPI + React demo with:

- **9 LLM providers** (OpenAI / Anthropic / Google / Mistral / Groq / Together / Ollama / LiteLLM proxy / Portkey)
- **6 Guardrail providers** (Lakera / OpenAI Moderation / AWS Bedrock / Azure AI Content Safety / Palo Alto AIRS / Cloudflare Firewall for AI)
- An **Admin → Threat Lab** tab with audit log + CSV export, guardrail compare matrix, OWASP LLM Top 10 playbook runner, and replayable recordings
- A side-by-side "Compare" landing modal that works for every guardrail provider
- Streaming chat (SSE) + multi-turn memory + image moderation

If you finish the course you will have:
- A reproducible eval harness against three guardrails of your choice
- A 10 × 3 OWASP Top 10 detection-rate matrix for your stack
- One concrete bypass you found and a write-up of which guardrail layer would catch it
- A wiki-shaped detector proposal for one open problem

## Built with the 12-phase pipeline

This course was scaffolded with the `scaffolding-course-portal` skill that
codifies the same 12-phase pipeline used by every previous course in the
series. The full process is documented at
[supachai-j.github.io/process.html](https://supachai-j.github.io/process.html).

## Audience

- Senior software engineers shipping LLM features to production
- AI / security red-team practitioners
- Staff+ engineers responsible for an org's AI risk posture
- Anyone preparing for a SOC2 / EU AI Act compliance review of an AI product

Not a beginner course. We assume you have shipped at least one LLM-powered
feature, can read Python or TypeScript, and are comfortable with HTTP +
sequence diagrams.

## Open source

All four deliverables (EN course + TH course + EN slides + TH slides) ship with
the wiki + primary sources under MIT in the same GitHub repo:
[`supachai-j/ai-guardrails-training`](https://github.com/supachai-j/ai-guardrails-training).

Issues and PRs welcome — especially: more attack-class wiki pages, additional
detector implementations, and translation polish for the Thai mirrors.
