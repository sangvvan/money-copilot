# Codex instructions

Money Copilot is a security-sensitive financial application.

Before coding, read `docs/ARCHITECTURE.md`, `docs/THREAT_MODEL.md`, and the active milestone document.

Rules:
- Never add real financial data or credentials.
- Do not weaken authentication/security requirements to simplify implementation.
- Keep financial calculations deterministic; do not use an LLM for amounts, dates, transaction IDs, deduplication or totals.
- AI is read-only by default. Mutations require explicit user confirmation.
- Prefer small, reviewable changes with tests.
- M1 is a security gate; do not implement M2 features until M1 is approved.
