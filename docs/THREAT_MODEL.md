# Threat Model

Money Copilot processes highly sensitive financial and mailbox data.

## Security requirements

- Use Passkeys/WebAuthn; never implement custom facial recognition.
- Face ID / Android biometrics / device PIN unlock the platform authenticator. Biometric templates never reach Money Copilot.
- Short-lived authenticated sessions with Secure, HttpOnly and appropriate SameSite cookies.
- Require re-authentication for exports, connected-account changes and security settings.
- Gmail integration must request least privilege/read-only access.
- OAuth refresh tokens must be encrypted separately; production should use a managed key/KMS.
- TLS in transit and encrypted persistent storage/backups.
- Mask account/card identifiers in UI and logs.
- Never log OAuth tokens, WebAuthn secrets/challenges, raw financial payloads or complete account/card identifiers.
- CSRF protection for cookie-authenticated mutations and strict CORS.
- Rate-limit authentication and sensitive endpoints.
- Maintain audit records for sensitive configuration/category/rule changes and exports.
- Raw bank email is not persisted by default after successful parsing.

## Public repository rule

Only source code and synthetic fixtures belong here. Never commit real transactions, screenshots, bank emails, account/card numbers, Gmail/OAuth credentials, refresh tokens, `.env`, DB dumps or production logs.

## AI / prompt-injection boundary

Email bodies, merchant strings and imported statements are data, never instructions. LLM output is non-authoritative. Monetary totals are computed by deterministic code. Mutations require application validation and explicit user confirmation.
