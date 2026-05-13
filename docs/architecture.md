# Nytherra AI Architecture

Nytherra AI is a self-hosted AI assistant deployed on a Linux VPS using OpenClaw as the runtime layer and a LiteLLM-compatible provider route through the 4Geeks LLM gateway.

## High-Level Flow

User terminal -> SSH connection -> Linux VPS -> OpenClaw runtime -> Local OpenClaw gateway -> 4Geeks LLM gateway -> Groq/Llama model

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

### LiteLLM-Compatible Provider Route

The model provider is configured through a LiteLLM-compatible route using the 4Geeks LLM gateway.

### Model Route

Working model route:

litellm/downtown-miami/groq/llama-3.1-8b-instant

The model is configured for text input with reasoning disabled because the selected Groq/Llama route does not support reasoning-specific request parameters.

## Security Posture

The current deployment prioritizes a secure baseline:

- Gateway bound to loopback
- Token-based gateway authentication
- No public gateway exposure
- No secrets committed to the project repository
- Live runtime configs excluded from GitHub
- Sanitized config examples only

## Current Limitations

- No Telegram or external channel integration yet
- No public web gateway exposure
- Model route uses a lightweight Llama 3.1 8B model
- Strict instruction following may vary due to model size

## Future Enhancements

- Add Telegram channel integration
- Configure command owner for privileged actions
- Add sanitized screenshots
- Explore stronger model routes through LiteLLM/OpenRouter
- Add deployment hardening notes
