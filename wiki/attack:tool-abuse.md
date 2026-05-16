---
id: attack:tool-abuse
type: attack
title: Tool & agent abuse
status: active
confidence: 0.7
sources:
  - raw/2026-05-16-mcp-specification-2024-11-05.md
  - raw/2026-05-16-owasp-llm-top-10.md
  - raw/2026-05-16-guard-demo-client-orchestrator-seams.md
created: 2026-05-16
updated: 2026-05-16
updated_log:
  - 2026-05-16: created
tiers: semantic
half_life_days: 180
tags: [deck, attack, agentic, mcp]
---

# Tool & agent abuse

## Summary

Once the model can call tools, two new attack classes appear: **(a)** the
*confused-deputy* problem — the agent calls a tool with attacker-tampered
arguments, and the tool runs with the agent's higher privileges; and **(b)**
*prompt-injected tool output* — the tool returns content that contains
instructions, which the model then follows. MCP makes capability discovery
dynamic, so the same agent can talk to untrusted tools later in its
lifetime. The spec acknowledges tools "represent arbitrary code execution"
and requires explicit user consent.

## Claims

- OWASP LLM07 "Insecure Plugin Design" — "LLM plugins processing untrusted
  inputs and having insufficient access control risk severe exploits like
  remote code execution." `[src: raw/2026-05-16-owasp-llm-top-10.md] {conf: 0.9}`
- OWASP LLM08 "Excessive Agency" — granting LLMs unchecked autonomy
  is a recognised top-10 vulnerability.
  `[src: raw/2026-05-16-owasp-llm-top-10.md] {conf: 0.9}`
- The MCP spec says: "Tools represent arbitrary code execution and must
  be treated with appropriate caution. Hosts must obtain explicit user
  consent before invoking any tool."
  `[src: raw/2026-05-16-mcp-specification-2024-11-05.md] {conf: 0.9}`
- guard-demo-client's `toolhive.maybe_run_tool(message, enabled_tools)`
  pattern shows where to insert pre-execution argument-shape validation
  before each tool call. `[src: raw/2026-05-16-guard-demo-client-orchestrator-seams.md] {conf: 0.7}`

## Relationships

- composes → [[attack:data-exfiltration]] (tools enable exfiltration)
- mitigated-by → [[pattern:inline-blocking-guard]] (on tool args)
- depends-on → [[concept:agentic-threat-surface]]

## Open questions

- [ ] How does MCP's "user consent" rule map to non-interactive batch agents?

## Changelog
- 2026-05-16 — created
