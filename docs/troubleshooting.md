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

litellm/downtown-miami/groq/llama-3.1-8b-instant

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

The agent model file was recreated at:

~/.openclaw/agents/main/agent.models.json

and configured with reasoning disabled for the active model route.

## Final Working State

The final working deployment uses:

- OpenClaw running on a Linux VPS
- Local gateway bound to loopback
- Token-based gateway authentication
- 4Geeks LLM gateway
- Groq Llama 3.1 8B Instant model route
- Text-only input
- Reasoning-specific parameters disabled for provider compatibility
