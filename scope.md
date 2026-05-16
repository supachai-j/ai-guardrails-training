# Scope — Production AI Guardrails

## Audience tier

**Expert.**

## Outcome

After this course, the reader will be able to **decompose** an agentic LLM
application's threat surface using formal threat modeling, **evaluate** inline
guardrail systems on FP/FN/latency/cost axes, **design** a detector stack
appropriate for their architecture (direct API, proxy, or hybrid), and
**operate** it with production telemetry — using
[`guard-demo-client`](https://github.com/supachai-j/guard-demo-client) and
Lakera Guard as the running case study.

## Audience profile

**Primary readers**

- ML / applied-AI engineers shipping LLM-backed products to production
- Security engineers covering the AI surface (AppSec, blue-team, red-team)
- Staff+ engineers making architecture decisions about agentic systems

**Assumed background**

- Fluent in LLM inference internals — tokenization, instruction-tuning, RLHF, decoding parameters
- Comfortable reading academic papers (arXiv, ACL, NeurIPS, USENIX, IEEE S&P)
- Threat-modeling fluency (STRIDE / LINDDUN or equivalent)
- Working knowledge of OpenAI / Anthropic tool-calling APIs, RAG architectures, MCP
- Python and TypeScript familiarity for hands-on labs
- Basic detector-evaluation literacy — precision, recall, AUC, base-rate fallacy

**NOT assumed**

- Specific Lakera-product experience (we'll cover what we use)
- Prior `guard-demo-client` exposure
- Generic AppSec primer (assumed)

## Format

- **`course-en.html`** — self-paced web (primary deliverable). Expected length
  25–30k words across 12 modules, ~2k words per module.
- **`slides/training-en.html`** — full-day workshop deck (6–8 hours with
  hands-on labs). Expected 80–100 slides at 1280×800.
- **`wiki/`** — claim-by-claim citations. Expected 20–30 wiki pages with 2+
  citations per non-trivial claim, ≥1 of which is primary literature.
- **`raw/`** — primary sources, captured verbatim. Expected 12–15 files
  (papers + vendor docs + production postmortems).
- **TH bilingual mirror** — deferred (Phase 8 skipped, EN-only fast path
  for the Expert tier).

## Time budget

Realistic against the SKILL.md time matrix for Expert × EN-only:
**~30–50 hours of authoring**, spread across:

| Phase | Estimated time |
|---|---|
| 2 — Research & capture | 8–12 h |
| 3 — Wiki schema | 1 h |
| 4 — Wiki ingest (20–30 pages) | 8–10 h |
| 5 — Outline | 2 h |
| 6 — Course pages (~25–30k words) | 15–20 h |
| 7 — Slide deck (~80 slides) | 6–8 h |
| 9 — Landing tuning | 1–2 h |
| 10 — Deploy | 0.5 h |
| 11 — Validate | 2 h |
| 12 — Promote | 1 h |
| **Total** | **~45–58 h** |

## Modules (12, full pipeline)

| # | Module | Why this depth |
|---|---|---|
| 1 | Why LLM apps fail differently | First-principles: instruction-following inductive bias, ICL hijack, sycophancy as a failure mode. References PromptBench / Wei et al. |
| 2 | Formal threat model for an agentic system | STRIDE × (input / output / tool / RAG / agent-loop) decomposition. Produces a reusable template. |
| 3 | `guard-demo-client` architecture walkthrough | ReAct loop, dual Lakera modes (direct API vs. LiteLLM-native guardrails), error→status extraction. Working code reference for the rest of the course. |
| 4 | Prompt injection | Direct / indirect / multi-turn / encoded / role-play. Why each works at the decoder level. Lakera prompt-attack detector internals. Defense layers. |
| 5 | PII & secret extraction | Direct ask, tool-output leak, agentic exfiltration. PII classifier coverage gaps. Canary-token strategy. |
| 6 | Tool & agent abuse | Confused deputy, prompt-injected tool output, tool-call argument tampering. MCP threat model. Sandboxing patterns. |
| 7 | RAG poisoning | Direct injection in retrieved docs, embedding-collision attacks, indirect injection via citations. Ingest-time vs. retrieve-time scanning. Chunking attacks. |
| 8 | Building a detector eval harness | Datasets (PromptBench, JailbreakBench, custom red-team). FP/FN cost framework. Latency budget. A/B-testing in production. |
| 9 | Observability & telemetry | What to log from monitor mode. Triaging flagged-but-allowed events. SIEM integration. Incident playbooks. |
| 10 | Deployment patterns | Direct API + inline guard (sync), proxy with native guardrails (LiteLLM), async post-hoc scanning. Latency / cost / coverage trade-offs. Multi-region. |
| 11 | Adversarial considerations | Robustness limits, attacker adaptivity, what defenders genuinely can't do today. |
| 12 | Open problems & reading list | Constitutional AI, agentic-safety frontier work, RFC-style open problems. ~30 cited papers. |

## Success criteria

After completing the course, a senior engineer can:

- Apply STRIDE-style decomposition to their own agentic system → enumerate every attack class
- Build an eval harness for guardrails and report FP / FN / latency per detector class
- Decide between inline vs. proxy vs. async deployment given latency / cost constraints
- Write a runbook for triaging monitor-mode events in production
- Cite ≥3 primary papers per topic area
- Explain ≥2 production guardrail-failure modes from real postmortems

## Out of scope

- Building a custom detector from scratch (we evaluate existing ones; references to the literature only)
- RLHF / Constitutional-AI fine-tuning defenses (mentioned in module 11, not taught)
- Generic AppSec primer (assumed background)
- TH bilingual version (deferred — Phase 8 skipped on the fast path)
- Vendor selection / pricing comparison (vendor-neutral framing)

## Sources baseline (Phase 2 will close gaps)

Phase 2 will capture these into `raw/` verbatim, with frontmatter:

1. `guard-demo-client` codebase + `designdocs/`
2. Lakera Guard documentation
3. OWASP LLM Top 10 + LLM AI Security & Governance Checklist
4. PromptBench (Zhu et al., 2023)
5. JailbreakBench (Chao et al., 2024)
6. Greshake et al. on indirect prompt injection (2023)
7. Anthropic safety research — prompt injection / Constitutional AI papers
8. Google "On the Difficulty of Defending Against Adversarial Prompts"
9. LiteLLM proxy guardrail documentation
10. MCP security model / threat-modeling docs
11. 3–5 production postmortems (Discord, Slack, GitHub, OpenAI plugin incidents, etc.)
12. NIST AI RMF generative-AI profile

## Repository

- **Slug:** `ai-guardrails-training`
- **Template origin:** `supachai-j/course-portal-template`
- **Worked example codebase:** `supachai-j/guard-demo-client`
- **Deploy target:** GitHub Pages at https://supachai-j.github.io/ai-guardrails-training/
