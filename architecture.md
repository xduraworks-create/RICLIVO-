architecture.md

Riclivo — System Architecture

Last updated: 2025-10-06
Purpose: high-level technical architecture for Riclivo — how components connect, data flows, security responsibilities, and deployment notes. This is written for founders, developers, and technical reviewers.


---

1 — Executive summary

Riclivo is an AI-powered financial assistant that:

securely connects to users’ bank accounts (read-only) using Open Banking providers,

analyses transactions to identify refund/reclaim opportunities,

generates and manages reclaim requests,

provides bookkeeping & tax-ready summaries,

offers an AI chat assistant for business/tax guidance.


Primary user interaction is a lightweight front-end (initially Glide) connected to Google Sheets as the data source. Production will evolve to a proper backend (FastAPI/Node) and a database (Postgres) as scale demands.


---

2 — Key components

1. Frontend

Glide App (MVP): UI, user auth, forms, buttons, scheduled notifications.

Future native: React Native or web frontend for store deployment.



2. Data Layer

Google Sheets (MVP): main dynamic datastore for prototyping.

Schemas: canonical sheet schemas live in /schemas.

Future: Postgres (primary), Redis (cache), object storage (S3) for receipts.



3. Backend / Orchestration

Small serverless functions or lightweight API (FastAPI/Node) to:

Receive webhooks (PSPs, bank providers).

Validate and parse incoming payloads.

Produce signed requests for reclaim letters/PDFs.

Handle asynchronous tasks (reclaim follow-ups).


Automations (Make.com / Zapier) for early integrations.



4. Open Banking & Payment Providers

Nordigen, Mono, Okra, Plaid (region-specific) — fetch transactions via OAuth/token flows.

Flutterwave, Paystack, Wise — payment and verification flows (card mandating, payouts).



5. AI / ML

OpenAI (GPT-3.5 / GPT-4-mini or project-branded wrappers) for:

Transaction classification

Reclaim justification text generation

Business idea generation tailored by localisation

Chat assistant


Lightweight rule-engine for deterministic checks (duplicate charge, fee thresholds) before calling LLM.



6. Security & Secrets

Secrets stored off-sheet (GitHub Secrets, vault, or server env vars).

Tokens and PII not persisted in Google Sheets (only masked identifiers).



7. Monitoring & Logging

API request logs (api_requests sheet / logs endpoint).

Error tracking (Sentry or similar) for backend and automations.

Audit trail for every reclaim (consent timestamps, mandate last4, request ids).





---

3 — Logical flow (high level)

User action → Glide front-end → Google Sheets (data) → Backend / Integrations → Open Banking / PSPs → Response → AI / Sheets update → User notified.

ASCII flow:

[User (Glide App)]
       ↓
[Google Sheets] <-> [Glide UI]
       ↓ (action: request transaction fetch, reclaim)
[Backend / Automation layer]
       ↓ (OAuth/token)
[Open Banking Providers (Nordigen/Mono/Okra/Plaid)]
       ↳ returns transactions (bank)
       ↓
[AI Module (OpenAI) & Rule Engine]  -> classify & decide
       ↓
[Reclaim Generator] -> PDF/email payload
       ↓
[PSP / Bank / Email API] -> send reclaim / track response
       ↓
[api_requests log] & [reclaims sheet] update
       ↓
[Glide: Notification to user]


---

4 — Detailed reclaim sequence (example)

1. User authorizes a bank connection via provider (Nordigen). Glide stores accounts metadata and token metadata (not raw token).


2. Glide triggers a fetch_transactions action (Make.com webhook or backend API).


3. Provider returns transactions; the system:

Runs deterministic checks (duplicate charge, merchant whitelists).

Sends candidate transactions to AI classifier for deeper analysis (LLM or cheaper classifier).



4. If candidate flagged, a reclaim row is created in sheet with status = draft and an estimated reclaim amount.


5. User is presented a reclaim popup (dynamic message referencing config.reclaim_popup_message). They confirm.


6. System generates the reclaim package (PDF + justification text referencing localisation legal note).


7. System sends reclaim to bank/merchant via supported channel (API/email/form) and logs the api_requests.


8. When bank confirms, user receives funds to their bank account. System calculates commission using config (20/10/5%), creates a payment record, and notifies the user.


9. All steps are auditable in api_requests, reclaims, and payments.




---

5 — Data model summary (high level)

Key sheets (MVP) — see /schemas for column details:

users

accounts

transactions

analytics_summary

reclaims

bookkeeping

ledger

ai_chat

notifications

api_requests

payments

tax_reports

integrations

localisation

config


Important principles

Sheets contain masked or aggregate data where legal risk exists.

PII minimal: keep email, phone, country, masked_account only.

Consent timestamps stored for audit.



---

6 — Security design and privacy controls

Authentication

Glide sign-in required (email / phone OTP).

Session tied to user_id and device_id.


Authorization

Row-level ownership in Glide (users only see rows where user_id matches).

Admin roles are separate (not stored in public sheet).


Secrets & Tokens

Do NOT store raw API keys or OAuth refresh tokens in Sheets.

Store only token metadata (expiry, scope) or token reference IDs.

Use a secrets manager (or GitHub Secrets) for API keys used by backend.


Data in transit & at rest

All provider calls via HTTPS/TLS.

Sheets remain private.

Future DB: AES-256 at rest.


Retention & deletion

Default retention policy: anonymized aggregates kept for 2 years (config).

Raw bank lines deleted / not stored; summaries kept for analytics.


Audit & Logging

Every external request logged with external_ref, timestamps, and latency.

User consent and mandate records kept for legal follow-up.



---

7 — Operational concerns & scaling

Early-stage (MVP)

Glide + Sheets + Make.com automations for quick iteration.

Sandbox mode for Nordigen/PSP using config.api_mode = sandbox.


Scale considerations

Move Sheets → Postgres when concurrent writes/reads increase.

Use background worker queue (Celery/FastAPI background tasks) for LLM calls and heavy processing to reduce frontend latency.

Add rate-limits & cost controls: batching transaction analysis, using cheaper models for routine tasks.


Costs

Monitor API calls (Nordigen), LLM tokens (OpenAI), and PSP charges (Flutterwave).

Implement model selection logic (small model for classification; bigger model for legal text generation).



---

8 — Deployment & environment

Environments

development (local / test Glide) — sandbox API keys

staging — limited pilot users

production — real API keys and PSP setup


CI/CD

GitHub Actions for infra and docs updates.

Keep secrets in GitHub Secrets; don’t commit .env to repo.


Backups

Periodic exports of critical sheets to an encrypted storage bucket.

Database snapshots (when migrated) every 24 hours.



---

9 — Files to add to repo now

Suggested initial docs to create under /docs and /schemas:

docs/architecture.md (this file)

docs/data_flow.md

docs/security_notes.md

docs/proof_of_concept.md

docs/compliance_summary.md

schemas/users_schema.csv, schemas/transactions_schema.csv, schemas/config_schema.csv (canonical headers)



---

10 — Next steps (developer checklist)

1. Add this architecture.md to /docs.


2. Create canonical CSVs for each sheet and upload to /schemas.


3. Implement config sheet in Google Sheets. Protect it.


4. Create GitHub repo folders (docs, schemas, integrations, ui, legal), add .gitkeep files.


5. Provision Wise Business or other multi-currency account for payouts.


6. Connect Glide to sheet and implement row-level security.


7. Start small pilot (5–50 users) and test reclaim flow end-to-end with sandbox APIs.
