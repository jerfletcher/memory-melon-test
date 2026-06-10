---
key: IlTzLQPw
title: LiteLLM Model Registration via API
kind: reference
tags:
    - litellm
    - api
    - model
    - registration
    - coolify
created_at: "2026-06-10T20:07:36.84576167Z"
updated_at: "2026-06-10T20:07:36.84576167Z"
---
# LiteLLM Model Registration via API

## Endpoint

- **URL**: `https://llm.0mod.com/model/new`
- **Method**: `POST`
- **Auth**: `Authorization: Bearer <MASTER_KEY>`

## Example: Registering Speaches (Audio-Speech Model)

```bash
curl -X POST https://llm.0mod.com/model/new \
  -H "Authorization: Bearer dbfd4e99195c5b81406cece2ea3f8fe1e177d1e8c1b07ceb" \
  -H "Content-Type: application/json" \
  -d '{
    "model_name": "speaches",
    "litellm_params": {
      "model": "openai/speaches",
      "api_base": "http://192.168.8.130:11444",
      "api_key": "sk-speaches",
      "custom_llm_provider": "openai",
      "stream_timeout": 600
    },
    "model_info": {
      "model_name": "speaches",
      "mode": "audio-speech",
      "supports_audio_inputs": true,
      "supports_audio_outputs": true
    }
  }'
```

## Response Fields

- `model_id`: Unique identifier for the registered model
- `model_name`: Name of the model (e.g., "speaches")
- `litellm_params`: Encrypted configuration parameters
- `model_info`: Metadata including mode and capabilities

## Verification

```bash
# List registered models
curl -H "Authorization: Bearer <MASTER_KEY>" https://llm.0mod.com/v1/models

# Expected output includes:
{
  "id": "speaches",
  "object": "model",
  "created": 1677610602,
  "owned_by": "openai"
}
```

## Notes

- The LiteLLM proxy encrypts sensitive parameters (api_key, api_base) in the response
- Use `mode: "audio-speech"` for TTS/STT models
- Set `supports_audio_inputs` and `supports_audio_outputs` to `true` for audio models
- The `stream_timeout` can be adjusted based on model performance requirements
