---
source_type: web
source_url: https://docs.litellm.ai/docs/proxy/guardrails/quick_start
ingested_at: 2026-05-16
title: LiteLLM Proxy Guardrails Quick Start
---

# LiteLLM Proxy Guardrails Quick Start

## Configuration Structure

Guardrails are defined in the `config.yaml` file under a dedicated `guardrails` section. Each guardrail entry requires:

- **guardrail_name**: Identifier for the guardrail
- **litellm_params**: Configuration including the guardrail type, execution mode, and API credentials
- **guardrail_info** (optional): Metadata describing parameters and capabilities

## Supported Guardrail Providers

The documentation references these providers:
- Aporia
- Lakera
- AWS Bedrock Guardrails
- Presidio (PII detection)
- AIM
- Generic Guardrail API
- OpenAI Moderation
- Azure Content Safety
- Guardrails AI
- DynamoAI, Javelin, Lasso, Pangea, Model Armor

## Execution Modes

The `mode` parameter controls when guardrails execute:

- **pre_call**: "Run **before** LLM call, on **input**"
- **post_call**: "Run **after** LLM call, on **input & output**"
- **during_call**: Runs in parallel with the LLM call
- **logging_only**: Masks content in logs without blocking requests

Modes can be a single value or a list for multiple execution points.

## YAML Configuration Example

```yaml
guardrails:
  - guardrail_name: general-guard
    litellm_params:
      guardrail: aim
      mode: [pre_call, post_call]
      api_key: os.environ/AIM_API_KEY
      api_base: os.environ/AIM_API_BASE
      default_on: true

  - guardrail_name: presidio-pii
    litellm_params:
      guardrail: presidio
      mode: pre_call
      presidio_language: en
      pii_entities_config:
        CREDIT_CARD: MASK
        EMAIL_ADDRESS: MASK
        US_SSN: MASK
      presidio_score_thresholds:
        CREDIT_CARD: 0.8
        EMAIL_ADDRESS: 0.6
```

## Request Flow

### Successful Request
When a request passes guardrail checks, it proceeds to the LLM with a response header:
```
x-litellm-applied-guardrails: guardrail-name
```

### Blocked Request
When a guardrail blocks content, the response returns a 400 error:

```json
{
  "error": {
    "message": {
      "error": "Violated guardrail policy",
      "aporia_ai_response": {
        "action": "block",
        "revised_prompt": null,
        "revised_response": "Aporia detected and blocked PII",
        "explain_log": null
      }
    },
    "type": "None",
    "param": "None",
    "code": "400"
  }
}
```

## Client-Side Usage

### Simple Format
```json
{
  "model": "gpt-3.5-turbo",
  "messages": [{"role": "user", "content": "hi what is the weather"}],
  "guardrails": ["aporia-pre-guard", "aporia-post-guard"]
}
```

### Advanced Format (Enterprise)
```json
{
  "guardrails": {
    "aporia-pre-guard": {
      "extra_body": {
        "success_threshold": 0.9
      }
    }
  }
}
```

## Key Features

**Default On Guardrails**: Set `default_on: true` to apply automatically without client specification.

**Skip System Messages**: Control whether system role messages are evaluated by setting `skip_system_message_in_guardrail: true` globally or per-guardrail.

**Model-Level Guardrails** (Enterprise): Apply guardrails to specific models by adding the `guardrails` list to individual model configurations.

**Per-API-Key Controls** (Enterprise): Restrict which guardrails teams can enable/disable through the `/key/generate` endpoint.
