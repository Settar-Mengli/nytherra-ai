# Nytherra AI

Nytherra AI is a self-hosted AI assistant deployed on a Linux VPS using OpenClaw, LiteLLM-compatible model routing, and the 4Geeks LLM gateway.

## Project Status

Core deployment is working.

- VPS access via SSH
- OpenClaw installed and configured
- Local OpenClaw gateway running on loopback
- LiteLLM provider route configured through 4Geeks
- Groq Llama 3.1 8B Instant model responding successfully
- Health check completed with no plugin errors
- Working configuration checkpoint created

## Architecture

Local machine → SSH → Linux VPS → OpenClaw runtime → Local gateway → 4Geeks LLM gateway → Groq/Llama model

## Security Notes

Secrets, API keys, gateway tokens, and live configuration files are excluded from this repository. Sanitized examples will be provided only when safe.

## Next Steps

- Add sanitized configuration examples
- Add architecture documentation
- Add safe screenshots
- Document troubleshooting and lessons learned
- Optionally add Telegram or external channel integration later
