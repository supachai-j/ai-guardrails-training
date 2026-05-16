# SCHEMA — Production AI Guardrails

> Constitution of this wiki. Every Ingest / Query / Lint operation reads this file.

## 1. Domain

A senior-engineer deep-dive into protecting agentic LLM applications — threat modeling, inline guardrail evaluation, and production deployment patterns — using the open-source guard-demo-client (FastAPI + React + Lakera Guard) as the running case study.

## 2. Entity catalogue

Edit this table to fit your domain. Keep the type set small and stable.

| type | id pattern | gets its own page? | notes |
|---|---|---|---|
| `concept` | `concept:<kebab>` | yes | core ideas, definitions, mental models |
| `attack` | `attack:<kebab>` | yes | named attack class (e.g. `attack:prompt-injection-direct`) — the unit threat models reason about |
| `detector` | `detector:<kebab>` | yes | a specific detector mechanism (e.g. `detector:lakera-prompt-attack`) |
| `pattern` | `pattern:<kebab>` | yes | reusable patterns (e.g. `pattern:inline-blocking-guard`) |
| `tool` | `tool:<name>` | yes | concrete tools / products (Lakera, LiteLLM, Presidio, etc.) |
| `decision` | `decision:<date>-<slug>` | yes | ADRs / authoritative decisions |
| `source` | `source:<kebab>` | no | reference only — links from raw/ |

## 3. Relation catalogue

- `uses` — A consumes B at runtime
- `depends-on` — A cannot function without B
- `composes` — A is built from / orchestrates B
- `alternative-to` — A and B solve overlapping problems
- `extends` — A is a specialisation of B
- `supersedes` — new claim/decision replaces older one (old stays, marked stale)
- `contradicts` — flagged for Lint to resolve
- `cites` — A draws evidence from source B
- `detects` — detector D detects attack A (typed: `detector → attack`)
- `mitigates` — pattern P mitigates attack A (typed: `pattern → attack`)
- `enables` — vector V enables attack A (e.g. unfurling enables exfil)

## 4. Page rules

- One concept per page.
- YAML frontmatter mandatory (see `wiki/_TEMPLATE.md`).
- Every claim has an inline source marker `[src: raw/...]`.
- Wikilinks use entity IDs: `[[concept:foo]]`, not `[[Foo]]`.
- Status: `active` (default), `stale`, `faded`, `orphan`.

## 5. Ingest rules

- Raw source → `raw/YYYY-MM-DD-<slug>.md` untouched.
- Entity extraction runs against §2.
- A new page is created when entity is "yes" in the catalogue _and_ ≥1 non-trivial claim exists.
- Existing page updates: reinforce matching claims (bump confidence), append new ones.

## 6. Confidence and decay

- First observation: `confidence: 0.5`
- Reinforcement (independent source): `conf ← 1 - (1 - conf) * 0.6`
- Decay half-life:
  - `decision`: 365 days
  - `concept`, `pattern`, `feature`, `tool`: 180 days
  - `source`: not applicable (raw is immutable)

## 7. Privacy and secrets

Never written to wiki/ or graph/, redacted in raw/ on detection:
- API keys, tokens, signed URLs
- Passwords, private keys, certificates
- PII beyond `person:` name

Replacement token: `<REDACTED:apikey|token|pii|secret|other>`.

## 8. Training-deck rules

This wiki feeds two HTML training decks (English + Thai) under `slides/`. When a wiki page is updated with a new "deck-worthy" claim, mark the claim with `tag: deck` so Crystallize can find it.
