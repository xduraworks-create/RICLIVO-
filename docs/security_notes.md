# 🛡️ Riclivo Security Notes

Last updated: October 2025
Document Type: System Security Overview
Scope: Covers data protection, API key handling, authentication, and device security for Riclivo App (Glide + Google Sheets + Integrations).


---

1. Overview

Riclivo is designed on a privacy-first and minimal data retention model.
We operate under the principle:

> “Only store what’s necessary, and never store what can be fetched securely.”



All transactions, tokens, and user identities are protected through multi-layered encryption, and we comply with GDPR, PSD2, and Open Banking security frameworks.


---

2. Core Security Principles

Principle	Description

Least Data Storage	Riclivo only stores processed summaries, not raw transaction histories.
Temporary Access Tokens	Bank APIs use temporary access tokens (default expiry: 365 days).
User Consent First	No data access occurs without explicit user approval via consent pop-up.
Encrypted Storage	All stored data (IDs, hashes, logs) are encrypted at rest using AES-256.
One Device Binding	Each account is bound to a single device ID, verified via biometrics.
No Card Details Saved	Riclivo never stores or displays full bank/card numbers.
Independent Payment Processors	All card or payout activities occur within Flutterwave/Paystack secure gateways.



---

3. Authentication & Access Control

Layer	Mechanism

App Access	Secure login via verified email and phone OTP.
Device Verification	Each device gets a unique device_id bound to the user account.
Biometric Lock	Optional biometric unlock for premium/business users.
Session Control	Sessions auto-expire after 20 minutes of inactivity.
Role Access	Users are isolated — no shared or public data endpoints. Admin tools are separate.



---

4. API & Integration Security

🔗 Open Banking (Nordigen, Okra, Salt Edge)

OAuth 2.0 with read-transactions and read-accounts scope only.

Tokens refreshed securely via encrypted serverless function.

Riclivo never handles direct bank credentials.


💳 Flutterwave / Paystack

PCI-DSS Level 1 certified payment processors.

All card input occurs within hosted payment pages (not inside Riclivo).

Payment confirmation returned via secure webhooks → verified before any payout is initiated.


🤖 OpenAI (AI Chat Engine)

Chat requests are anonymized (no real user identifiers).

Each message processed transiently, no retention beyond inference session.

AI models are restricted to compliant versions (gpt-4-mini / gpt-3.5-turbo).



---

5. Encryption & Hashing

Data Type	Encryption Level	Example

Access Tokens	AES-256 + Base64	token_enc_4f92aX...
Device IDs	SHA-256 Hash	dev_hash_094f3b...
User IDs / Account IDs	UUID v4 + Salt	u_12b9d-e483...
Bank Accounts	Masked	****3456
Logs / Audit Data	Encrypted and automatically rotated every 30 days	-


Implementation Policy:

No unencrypted field should ever leave Glide or Sheets.

Any external API request must include a timestamp and HMAC signature (using Riclivo’s secret key).



---

6. Fraud Prevention

1. Device Binding:
Each account’s API connection is tied to a single verified device.

If detected on another device → triggers verification (email + biometric).

After verification → same API key is cloned, not reissued.



2. Account Verification via Card Match:
During reclaim, the card used must match the linked bank account.


3. Duplicate Use Prevention:
Riclivo blocks multiple devices trying to use the same reclaim key simultaneously.


4. Reclaim Confirmation Popup:
Before every payout:

> “By clicking confirm, you agree to Riclivo’s Terms and Conditions in line with your country’s financial law. Riclivo does not store your card details and only processes this transaction once.”






---

7. Data Retention & Deletion

Data Type	Retention	Deletion Trigger

API Tokens	365 days	Auto-expire after 365 days or manual revoke.
Reclaim Records	2 years	After 2 years → anonymized.
Bookkeeping / Tax Reports	2 years	Can be exported before auto-deletion.
User Profile	Until user deletion request	Handled within 30 days under GDPR.



---

8. Legal & Compliance Safeguards

GDPR and Open Banking compliant (EU).

CCPA (California) for U.S. users.

NDPR (Nigeria Data Protection Regulation).

PCI-DSS for all payment integrations.

Automated data export on user request.



---

9. Backup & Incident Management

Policy	Description

Automatic Backups	Google Drive + encrypted cloud redundancy every 24 hours.
Incident Alerts	Admins notified immediately on breach attempts or unauthorized API call.
Token Blacklisting	Compromised tokens immediately blacklisted in Sheets (token_status=revoke).
Audit Trails	Every API or reclaim event is logged for 30 days in api_requests.



---

10. Summary

Riclivo’s security architecture ensures:

Users remain in full control of their data.

Fraud is minimized via device-binding and card matching.

Sensitive info is encrypted and never stored in full form.

Regulatory compliance across multiple regions.


> “At Riclivo, trust and transparency are our real currency.”
