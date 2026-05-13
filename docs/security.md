# Security Notes

Nytherra AI is configured with a security-first baseline for the initial deployment.

## Current Security Decisions

- The OpenClaw gateway is bound to loopback.
- The gateway is not exposed directly to the public internet.
- Token-based gateway authentication is enabled.
- Telegram access is protected through OpenClaw pairing and owner approval.
- Live runtime configuration files are excluded from the GitHub project.
- API keys, gateway tokens, and credentials are not committed.
- Public documentation uses sanitized configuration examples only.

## Secret Handling

The following should never be committed to GitHub:

- API keys
- Gateway tokens
- SSH keys
- Environment files
- Live OpenClaw configuration files
- Checkpoint backups
- Screenshots that reveal secrets

## Telegram Channel Security

Telegram Bot API integration has been tested as a private OpenClaw channel using polling.

The channel is protected through OpenClaw pairing and owner approval rather than open public DM access. It should be described as a tested private channel integration, not as a public production bot.

Privileged commands should remain disabled unless owner permissions, allowlists, and command boundaries are explicitly configured and reviewed.

## Screenshot Policy

Screenshots should be reviewed before being added to the repository. Any visible token, API key, host credential, or private terminal history should be blurred, cropped, or replaced with a clean screenshot.

![Repository hardening for runtime files, credentials, checkpoints, and local OpenClaw artifacts.](../screenshots/nytherra-security-gitignore-hardening.png)
*Repository hardening for runtime files, credentials, checkpoints, and local OpenClaw artifacts.*

## Pre-Submission Security Checklist

Before final portfolio submission:

- Confirm live credentials remain private and excluded from Git.
- Review screenshots for secrets.
- Confirm .gitignore is active.
- Confirm no live config files are staged in Git.
- Run a final security review.

## Future Hardening

Possible future hardening steps include:

- Keep Telegram limited to owner-approved private channel access.
- Configure command permissions before enabling privileged actions.
- Use least-privilege access for channels and tools.
- Avoid public gateway exposure unless secured behind an authenticated proxy.
- Keep model and provider credentials separate from the repository.
