# Security Notes

Nytherra AI is configured with a security-first baseline for a private, self-hosted deployment.

## Current Security Decisions

- The OpenClaw gateway is bound to loopback.
- The gateway is not exposed directly to the public internet.
- Token-based gateway authentication is enabled.
- Telegram access is protected through OpenClaw pairing and owner approval.
- Gmail automation is draft-only; Nytherra prepares messages but does not send them.
- Google Calendar, Docs, and Drive actions are initiated only from owner-controlled instructions.
- Live runtime configuration files are excluded from the GitHub project.
- API keys, gateway tokens, OAuth files, and credentials are not committed.
- Public documentation uses sanitized examples and redacted screenshots only.

## Secret Handling

The following should never be committed to GitHub:

- API keys
- Gateway tokens
- Telegram bot tokens or chat IDs
- Gmail draft IDs or message IDs
- Google Doc IDs
- Google Calendar event IDs
- OAuth client secrets or refresh tokens
- SSH keys
- Environment files
- Live OpenClaw configuration files
- Runtime checkpoints, sessions, logs, or database files
- Screenshots that reveal secrets, private URLs, account identifiers, host details, or raw tool output

## Telegram Channel Security

Telegram Bot API integration has been tested as a private OpenClaw channel using polling.

The channel is protected through OpenClaw pairing and owner approval rather than open public DM access. It should be described as a tested private channel integration, not as a public production bot.

Privileged commands should remain disabled unless owner permissions, allowlists, and command boundaries are explicitly configured and reviewed.

## Google Tool Safety

Nytherra uses Composio MCP / mcporter as the tool bridge for Google Workspace automation.

- Gmail: create drafts only; never auto-send.
- Calendar: create events only from explicit owner prompts.
- Docs and Drive: create documents without exposing raw document URLs or IDs in public docs.
- Tool responses: summarize outcomes instead of publishing raw tool JSON or private resource identifiers.

## Screenshot Policy

Screenshots should be reviewed before being added to the repository. Any visible token, API key, host credential, private terminal history, account identifier, raw URL, document ID, event ID, draft ID, message ID, or chat ID should be blurred, cropped, or replaced with a clean screenshot.

![Repository hardening for runtime files, credentials, checkpoints, and local OpenClaw artifacts.](../screenshots/nytherra-security-gitignore-hardening.png)
*Repository hardening for runtime files, credentials, checkpoints, and local OpenClaw artifacts.*

## Pre-Submission Security Checklist

Before final portfolio submission:

- Confirm live credentials remain private and excluded from Git.
- Review screenshots for secrets and private identifiers.
- Confirm `.gitignore` is active.
- Confirm no live config files are staged in Git.
- Run a final text audit for keys, tokens, emails, private URLs, IPs, chat IDs, message IDs, document IDs, event IDs, and raw logs.

## Future Hardening

Possible future hardening steps include:

- Keep Telegram limited to owner-approved private channel access.
- Configure command permissions before enabling privileged actions.
- Use least-privilege OAuth scopes for Google tools.
- Avoid public gateway exposure unless secured behind an authenticated proxy.
- Keep model and provider credentials separate from the repository.
