# Nytherra AI

Nytherra AI is a self-hosted AI assistant deployed on a Linux VPS using OpenClaw, LiteLLM-compatible model routing, and the 4Geeks LLM gateway.

This repository is a sanitized documentation baseline for a private, self-hosted deployment. It intentionally excludes live runtime configuration, gateway tokens, API keys, VPS host details, credentials, checkpoints, and screenshots that could expose sensitive information.

## Project Status

Core deployment is working.

- VPS access via SSH
- OpenClaw installed and configured
- Local OpenClaw gateway running on loopback
- LiteLLM provider route configured through 4Geeks
- Groq Llama 3.1 8B Instant model responding successfully
- Health check completed with no plugin errors
- Working configuration checkpoint created

Validation evidence is documented privately for now. Sanitized screenshots may be added later after they are reviewed for secrets, host details, and private terminal history.

## Architecture

Local machine -> SSH -> Linux VPS -> OpenClaw runtime -> Local gateway -> 4Geeks LLM gateway -> Groq/Llama model

OpenClaw uses the LiteLLM-prefixed route internally:

```text
litellm/downtown-miami/groq/llama-3.1-8b-instant
```

The sanitized config example uses the underlying 4Geeks/Groq provider model id:

```text
downtown-miami/groq/llama-3.1-8b-instant
```

Both forms are expected because they refer to the same provider route from different configuration layers.

## Security Notes

Secrets, API keys, gateway tokens, and live configuration files are excluded from this repository. Public examples are sanitized and should not be used as live deployment files without replacing placeholders in a private environment.

## Documentation

- [Architecture](docs/architecture.md)
- [Security notes](docs/security.md)
- [Troubleshooting notes](docs/troubleshooting.md)
- [Sanitized OpenClaw config example](config-examples/openclaw.example.json)

## Next Steps

- Add safe screenshots
- Add deployment hardening notes
- Optionally add Telegram or external channel integration later
