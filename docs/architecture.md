# Nytherra AI Architecture

Nytherra AI is a self-hosted Telegram assistant that runs on OpenClaw and connects to Google Workspace through Composio MCP / mcporter. The current model route uses DeepSeek as the primary model and Groq Llama 3.1 8B Instant as the fallback.

## High-Level Flow

```text
Owner in Telegram
  -> Telegram Bot API
  -> OpenClaw Telegram channel polling
  -> OpenClaw runtime on Linux VPS
  -> LiteLLM-compatible model routing
  -> DeepSeek primary, Llama fallback
  -> Composio MCP / mcporter tools
  -> Gmail, Calendar, Docs, and Drive
```

## Core Components

### Linux VPS

The VPS hosts the OpenClaw runtime so the assistant can stay available independently from the local development machine.

### OpenClaw Runtime

OpenClaw provides the agent runtime, local gateway, Telegram channel polling, session handling, skill/plugin layer, and configuration boundary.

### Local Gateway

The gateway is bound to loopback for safety.

- Port: 18789
- Bind mode: loopback
- Exposure: local only

This avoids exposing the OpenClaw gateway directly to the public internet during the current deployment phase.

### Telegram Private Channel

Telegram Bot API integration is configured as a private OpenClaw channel using polling. Access is protected through OpenClaw pairing and owner approval rather than public DM access.

Telegram acts as the control surface for Google automation requests and status responses.

### Model Routing

Nytherra uses LiteLLM-compatible routing through the configured gateway provider.

- Primary model: DeepSeek V3.2 through the OpenRouter route.
- Fallback model: Groq Llama 3.1 8B Instant.
- The Llama fallback is also aliased for compatibility with older OpenClaw prompts and troubleshooting notes.

Sanitized model route examples:

```text
litellm/downtown-miami/openrouter/deepseek/deepseek-v3.2
litellm/downtown-miami/groq/llama-3.1-8b-instant
```

### Composio MCP / mcporter

Composio MCP / mcporter provides the bridge from OpenClaw to external Google tools. Nytherra uses it to discover tools, confirm active connections, and execute scoped Google Workspace actions.

The public documentation avoids raw tool responses, private resource URLs, document IDs, event IDs, draft IDs, message IDs, and account identifiers.

### Google Workspace Tools

- Gmail: creates draft messages only. Sending remains a manual user action.
- Google Calendar: creates explicit events from Telegram instructions.
- Google Docs: creates owner-requested documents.
- Google Drive: stores created Docs and exposes them through the owner's Drive.

## Security Posture

The current deployment prioritizes a secure baseline:

- Gateway bound to loopback.
- Token-based gateway authentication.
- Telegram private channel protected by pairing and owner approval.
- No public gateway exposure.
- No live secrets committed to the project repository.
- Live OpenClaw runtime state excluded from Git.
- Sanitized config examples only.
- Redacted screenshots only.
- Gmail automation limited to draft creation.

## Current Limitations

- No public web gateway exposure.
- Google tool execution depends on active Composio-authenticated accounts.
- Public docs intentionally omit raw provider responses, private URLs, and resource IDs.
- The Llama fallback may occasionally need more explicit prompts than the DeepSeek primary model.

## Future Enhancements

- Continue hardening private channel permissions before enabling any privileged commands.
- Add least-privilege Google scopes where feasible.
- Add more sanitized evidence for tool workflows as the project evolves.
- Document deployment hardening after private validation.
