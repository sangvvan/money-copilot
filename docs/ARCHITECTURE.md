# Money Copilot Architecture

## Principle

**PostgreSQL is the financial source of truth. The LLM is never the ledger.**

Money, dates, transaction IDs, deduplication and totals are handled by deterministic application code. AI explains, queries and proposes classifications; it must not silently mutate canonical financial data.

## System

```text
Device biometric / PIN
        |
Passkey / WebAuthn
        |
   Next.js Web App
        |
      FastAPI
   /      |       \
 Auth   Finance   Ingestion
          |          |
      PostgreSQL  Gmail API (read-only)
          |
   Rules + Analytics
          |
      AI Copilot
```

## Stack

- Web: Next.js + TypeScript
- API: FastAPI + Python
- Database: PostgreSQL
- Local environment: Docker Compose
- Authentication: Passkeys / WebAuthn
- Bank-email ingestion: Gmail OAuth/API, read-only

## Core entities

User, WebAuthnCredential, Session, ConnectedAccount, Transaction, Category, CategorizationRule, TransactionOverride, ImportRun and AuditEvent.

## Transaction model

Canonical transactions contain amount as integer VND/minor units, currency, IN/OUT direction, transaction timestamp, bank/source, counterparty/merchant, category, source reference and a deterministic deduplication fingerprint.

Initial categories:

- FIXED_EXPENSE
- SPENDING
- GIFT
- LOAN
- TRANSFER
- UNCLASSIFIED

User overrides always win over automatic classification.

## Ingestion

Each bank gets an adapter. VCB is first. Email content is untrusted input. Parsers extract structured fields deterministically. Raw email should be processed ephemerally and not retained by default.

## AI boundary

Copilot uses constrained finance query APIs rather than unrestricted database access. Read-only is the default. Any future mutation must show a preview and require explicit user confirmation.

## MVP sequence

M1 Foundation + Security -> M2 Gmail/VCB -> M3 Finance Engine -> M4 Dashboard -> M5 AI Copilot -> M6 Statement Reconciliation.
