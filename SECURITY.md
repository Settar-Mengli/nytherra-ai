# Security Policy

Nytherra AI is published as a sanitized documentation baseline for a private, self-hosted deployment. Live runtime configuration, gateway tokens, API keys, VPS host details, credentials, checkpoints, and sensitive screenshots should not be committed to this repository.

For the detailed project security notes and pre-submission checklist, see [docs/security.md](docs/security.md).

## Reporting or Reviewing Security Issues

If you are reviewing this project and notice a possible secret, credential, private host detail, unsafe configuration, or misleading security claim, open a GitHub issue or contact the repository owner directly.

Please do not include live secrets, full tokens, private IP addresses, SSH host details, or sensitive screenshots in a public issue. Describe the affected file, line, and concern using redacted values where needed.

## Current Scope

- The OpenClaw gateway is documented as loopback-only.
- Public configuration is sanitized and example-only.
- Telegram is documented as a tested private channel integration protected through OpenClaw pairing and owner approval.
- Gmail automation is documented as draft-only.
- Google Docs, Drive, and Calendar evidence should avoid raw resource URLs and IDs.
- Future or additional screenshots should be added only after manual review and redaction.
