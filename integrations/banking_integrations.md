
# 🏦 banking_integration.md

Title: Banking Integration – Open Banking (Nordigen / GoCardless)


---

Purpose

Riclivo connects securely to users’ bank accounts using Nordigen (GoCardless) — an EU-regulated Open Banking API.
This enables:

Real-time transaction fetching

Balance verification

Refund source identification

Account linkage for reclaim and bookkeeping processes.



---

API Endpoints

Function	Endpoint	Method	Description

List institutions	/institutions/	GET	Fetch available banks for user’s region.
Create requisition	/requisitions/	POST	Generate consent link for user authorization.
Retrieve accounts	/accounts/	GET	Get authorized accounts under a requisition.
Fetch transactions	/accounts/{id}/transactions/	GET	Retrieve all recent transactions.
Fetch balances	/accounts/{id}/balances/	GET	Get account balance information.



---

Authentication

OAuth2-based system.

Each user consents once → Riclivo stores a refreshable access token.

Tokens are encrypted and stored in auth_keys table (Google Sheets / Firebase).

Tokens auto-renew using Nordigen’s refresh endpoint.



---

Flow Summary

1. User selects their bank and region (auto-detected from localization sheet).


2. Riclivo redirects to the Nordigen consent page for authentication.


3. Upon success, Riclivo stores:

institution_id

requisition_id

account_id



4. Background job (via Glide Action + Script) fetches:

Balances → accounts sheet

Transactions → transactions sheet



5. Riclivo automatically tags eligible failed or duplicate transactions for potential refund claims.




---

Error Handling

Code	Cause	Resolution

400	Invalid payload	Check user consent or expired session.
401	Token expired	Auto-refresh via stored refresh token.
404	Institution not supported	Fallback to manual import or CSV upload.
500	Bank server error	Retry after 10 mins (limit 3 retries).



---

Security Notes

All API keys stored in .env or Glide Config Sheet (hidden fields).

HTTPS enforced for every transaction.

Riclivo never stores user credentials — only access tokens post-consent.

Logs stored for 30 days for auditing, then anonymized.



---

Future Expansion

Add Plaid / Mono / Okra / Truelayer for region-specific support.

Enable instant refunds via bank rails where legally permitted.

Support multi-currency balance sync for cross-border users.
