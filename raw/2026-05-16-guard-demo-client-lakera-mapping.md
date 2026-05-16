---
source_type: doc
source_url: https://github.com/supachai-j/guard-demo-client/blob/main/designdocs/LAKERA_MAPPING.md
ingested_at: 2026-05-16
title: LAKERA_MAPPING (guard-demo-client design docs)
---

# LAKERA_MAPPING.md
_Last updated: 2025-08-29_

This doc defines the request/response schema and the UI mapping for the Lakera Guard integration (Task 2).

## Endpoint
`POST https://api.lakera.ai/v2/guard`

## Request Shape (JSON)
```jsonc
{
  "messages": [
    {"role": "system", "content": "You are a helpful AI assistant for healthcare inquiries."},
    {"role": "user", "content": "Is it safe to brush my teeth 8 times a day"},
    {"role": "assistant", "content": "That might be a bit overkill"}
  ],
  "project_id": "project-8541012967",
  "metadata": {
    "user_id": "",
    "ip_address": "123.222.121.009",
    "session_id": "randomuuid"
  },
  "breakdown": true,
  "payload": true,
  "dev_info": true
}
```

### Notes
- `messages` should contain the **full turn** we want to evaluate (system + user + assistant). For pre-response checks, send system + user; for post-response checks, include assistant content.
- Include `project_id` if available; otherwise omit or use a default from config.
- `metadata` can be enriched with your session/user identifiers.
- Set `breakdown=true` to get detector-by-detector results and `payload=true` to include category payloads (if any).

## Response Shape (example, abridged)
```jsonc
{
  "payload": [],
  "flagged": true,
  "dev_info": {
    "git_revision": "e421af45",
    "git_timestamp": "2025-08-27T15:20:16+00:00",
    "model_version": "lakera-guard-1",
    "version": "2.0.242"
  },
  "metadata": {
    "request_uuid": "ce50530c-315c-47db-aba3-35244f0f8a1b"
  },
  "breakdown": [
    {
      "project_id": "project-7539648934",
      "policy_id": "policy-lakera-public",
      "detector_id": "detector-lakera-public-moderated-content",
      "detector_type": "moderated_content/crime",
      "detected": false,
      "message_id": 1
    },
    { "... many more detector results ..." }
  ]
}
```

## Detector → UX Label Map (example)
```ts
export const DETECTOR_LABELS: Record<string, string> = {
  "prompt_attack": "Prompt Attack",
  "unknown_links": "Unknown Links",
  "moderated_content/crime": "Crime",
  "moderated_content/hate": "Hate",
  "moderated_content/profanity": "Profanity",
  "moderated_content/sexual": "Sexual Content",
  "moderated_content/violence": "Violence",
  "moderated_content/weapons": "Weapons",
  "pii/address": "PII: Address",
  "pii/credit_card": "PII: Credit Card",
  "pii/iban_code": "PII: IBAN",
  "pii/ip_address": "PII: IP Address",
  "pii/us_social_security_number": "PII: SSN"
};
```

## Privacy & Safety
- Do not send secrets or file contents unnecessarily. Send only what Lakera needs to assess safety.
- For RAG, consider sending only the **user prompt** + any **assistant draft** (not the whole retrieved context) if you want to minimize data exposure.
- Redact obvious PII in `metadata` unless required for policy.

## UI Mapping (Overlay)
- **Overall Status Pill**:
  - `OK` if `flagged == false` and no `detected == true` in `breakdown`
  - `WARN` if `flagged == true` but only low-risk detector types
  - `BLOCK` if specific high-risk detector types are `detected` (policy up to you)
- **Guardrails List**: `detector_type` → `detected` (True/False); group by category: `prompt_attack`, `unknown_links`, `moderated_content/*`, `pii/*`.
- **Raw JSON Accordion**: pretty-print the whole response.
- **Meta Footer**: show `metadata.request_uuid` and `dev_info.version` if present.
