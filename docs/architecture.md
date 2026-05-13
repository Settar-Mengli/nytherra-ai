# Nytherra AI Architecture

Nytherra AI is a self-hosted AI assistant deployed on a Linux VPS using OpenClaw as the runtime layer and a LiteLLM-compatible provider route through the 4Geeks LLM gateway.

## High-Level Flow

User terminal -> SSH connection -> Linux VPS -> OpenClaw runtime -> Local OpenClaw gateway -> 4Geeks LLM gateway -> Groq/Llama model

Telegram private chat -> Telegram Bot API -> OpenClaw Telegram channel polling -> OpenClaw runtime -> Local gateway -> 4Geeks/Groq model route

## Core Components

### Linux VPS

The VPS hosts the OpenClaw runtime and keeps the assistant available independently from the local machine.

### OpenClaw Runtime

OpenClaw provides the agent runtime, local gateway, session management, plugin system, and configuration layer.

### Local Gateway

The gateway is bound to loopback for safety.

- Port: 18789
- Bind mode: loopback
- Exposure: local only

This avoids exposing the gateway directly to the public internet during the initial deployment phase.

### Telegram Private Channel

Telegram Bot API integration has been configured and tested as a private OpenClaw channel using polling.

Access is protected through OpenClaw pairing and owner approval rather than open public DM access. The channel is documented as a tested private integration, not a public production bot.

### LiteLLM-Compatible Provider Route

The model provider is configured through a LiteLLM-compatible route using the 4Geeks LLM gateway.

### Model Route

OpenClaw uses the LiteLLM-prefixed route internally:

```text
litellm/downtown-miami/groq/llama-3.1-8b-instant
```

The sanitized config example uses the underlying 4Geeks/Groq provider model id:

```text
downtown-miami/groq/llama-3.1-8b-instant
```

Both forms may appear in this repository because they refer to the same provider route from different configuration layers.

The model is configured for text input with reasoning disabled because the selected Groq/Llama route does not support reasoning-specific request parameters.

## Security Posture

The current deployment prioritizes a secure baseline:

- Gateway bound to loopback
- Token-based gateway authentication
- Telegram private channel protected by pairing and owner approval
- No public gateway exposure
- No secrets committed to the project repository
- Live runtime configs excluded from GitHub
- Sanitized config examples only

## Current Limitations

- No public web gateway exposure
- Model route uses a lightweight Llama 3.1 8B model
- The lightweight Llama 3.1 8B route may occasionally need explicit identity/context prompts and may over-route or overuse internal message/session behavior on strict prompts. This is a model/tool-routing limitation, not a Telegram integration failure.

## Future Enhancements

- Continue hardening private channel permissions before enabling privileged commands
- Add additional sanitized evidence if useful
- Explore stronger model routes through LiteLLM/OpenRouter
- Add deployment hardening notes
