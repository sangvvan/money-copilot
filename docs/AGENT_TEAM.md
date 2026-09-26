# Agent Team v1

## Operating model

The owner and reviewer are the final approval gate. Agents may design, implement, test and review, but **must never merge to main**.

### Lead / Orchestrator
- Read AGENTS.md and active milestone.
- Break work into bounded tasks.
- Delegate independent workstreams to specialist subagents when multi-agent execution is available.
- Avoid concurrent edits to the same files.
- Collect specialist results and prepare a reviewable PR.
- Stop at the human approval gate.

### Architecture Agent
Owns boundaries, data model, API contracts and architecture consistency. It does not weaken security requirements for convenience.

### Backend Agent
Owns FastAPI, persistence, migrations, deterministic finance services and server-side tests.

### Frontend Agent
Owns Next.js UI, WebAuthn client flows, accessibility and safe display/masking of sensitive values.

### Security Agent
Acts as an independent reviewer. Checks authentication, authorization, session handling, OAuth/token storage, logging/redaction, input trust boundaries and repository secret safety. Security findings marked blocking must be resolved before PR-ready status.

### QA Agent
Builds/runs acceptance, unit and integration tests. Maps results to milestone acceptance criteria. A failing required test blocks PR-ready status.

### Review Agent
Reviews the integrated diff after Security and QA. Checks scope, maintainability, architecture and evidence. It cannot approve/merge on behalf of the owner.

## Workflow

Requirement -> Lead planning -> parallel specialist work where safe -> integration -> Security review -> QA -> Review -> PR -> HUMAN APPROVAL -> merge.

## Human-only actions

- Merge to main.
- Approve security exceptions.
- Provide production credentials/secrets.
- Connect real Gmail/bank data.
- Authorize production deployment or destructive production changes.

## M1 team assignment

Architecture: verify implementation follows docs/ARCHITECTURE.md.
Backend: FastAPI/PostgreSQL/session/WebAuthn server foundation.
Frontend: Next.js shell and passkey client UX.
Security: threat-model verification and auth abuse cases.
QA: M1 acceptance criteria and CI evidence.
Review: final integrated PR report.

M2 work is forbidden until M1 receives human approval.
