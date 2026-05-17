# Troubleshooting Notes

This document summarizes key issues encountered while deploying Nytherra AI and how they were resolved.

## Invalid Model Name

### Symptom

The agent returned an error similar to:

Invalid model name passed in model=claude-opus-4-6.

### Cause

OpenClaw initially selected a default LiteLLM model route that was not available through the configured 4Geeks LLM gateway.

### Resolution

The model route was updated to the available 4Geeks/Groq route:

```text
litellm/downtown-miami/groq/llama-3.1-8b-instant
```

OpenClaw uses this LiteLLM-prefixed route internally. The sanitized config example uses the underlying provider model id, `downtown-miami/groq/llama-3.1-8b-instant`, because that value is passed within the 4Geeks/Groq provider configuration.

## Provider Schema Rejection

### Symptom

The provider rejected the request schema or tool payload.

### Cause

The selected Groq/Llama route did not support some of the richer request capabilities that OpenClaw initially attempted to send.

### Resolution

The model configuration was simplified to text-only input.

## Unsupported Reasoning Parameter

### Symptom

The provider returned an error that Groq does not support reasoning_effort.

### Cause

The Groq/Llama route does not support reasoning-specific request parameters.

### Resolution

Reasoning was disabled for the active model route.

## Missing Agent Model Config

### Symptom

OpenClaw continued falling back to reasoning behavior even after the main config was updated.

### Cause

The agent-specific model configuration file was missing.

### Resolution

The agent-specific model file was recreated in the private OpenClaw runtime directory and configured with reasoning disabled for the active model route. The live path is intentionally omitted from this public checkpoint.

## Telegram Polling Test

### Symptom

Telegram needed to be verified as a private channel integration without publishing private setup details.

### Resolution

OpenClaw channel status confirmed Telegram was enabled, configured, running, connected, polling, and working.

Sanitized prompt test:

```text
Prompt: Plain text test. Say ONLINE.
Result: ONLINE
```

Telegram access is protected through OpenClaw pairing and owner approval rather than open public DM access.

## Current Model Routing

Nytherra now uses DeepSeek V3.2 as the primary model route and Groq Llama 3.1 8B Instant as the fallback route.

Sanitized route examples:

```text
litellm/downtown-miami/openrouter/deepseek/deepseek-v3.2
litellm/downtown-miami/groq/llama-3.1-8b-instant
```

## Current Model/Tool-Routing Limitation

The lightweight Llama 3.1 8B route may occasionally need explicit identity/context prompts and may over-route or overuse internal message/session behavior on strict prompts. This is a model/tool-routing limitation, not a Telegram integration failure.

## Final Working State

The final working deployment uses:

- OpenClaw running on a Linux VPS
- Local gateway bound to loopback
- Token-based gateway authentication
- 4Geeks LLM gateway
- DeepSeek V3.2 primary model route
- Groq Llama 3.1 8B Instant fallback model route
- Telegram Bot API private channel integration through OpenClaw polling
- Composio MCP / mcporter Google tools integration
- Gmail draft-only automation
- Google Calendar event creation
- Google Docs and Drive creation
- Text-only input
- Reasoning-specific parameters disabled for provider compatibility
