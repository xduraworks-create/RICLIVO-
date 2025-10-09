#  🛡️ Riclivo Compliance Summary

Last Updated: October 2025
Document Type: Legal & Regulatory Compliance Overview


---

1. Purpose

This document summarizes the compliance standards, regulatory frameworks, and best practices observed by Riclivo, ensuring that all data, financial, and user-related activities are handled ethically, transparently, and securely.


---

2. Core Compliance Principles

Principle	Description

Transparency	Users always know what data is collected, how it is processed, and why.
Consent-Driven	Every connection (bank, API, or AI use) requires explicit user consent.
Data Minimization	Riclivo stores the least amount of personal data necessary to operate.
Right to Access & Erasure	Users can request their data export or deletion anytime.
Security-First Design	All data is encrypted both in transit and at rest.
Non-Custodial Operations	Riclivo doesn’t hold or store user funds — only metadata and API tokens.



---

3. Legal & Regulatory Frameworks

Region	Regulation	Riclivo Compliance Status

European Union	GDPR (General Data Protection Regulation)	Full alignment: consent logging, right-to-be-forgotten, encrypted data export
United Kingdom	UK-GDPR & Data Protection Act 2018	Mirrors EU compliance — user consent and retention limits respected
Nigeria	NDPR (Nigeria Data Protection Regulation)	Riclivo servers and partners adhere to NDPR’s consent and data portability requirements
United States	CCPA / CPRA (California)	Riclivo respects user opt-out and deletion requests
Canada	PIPEDA (Personal Information Protection and Electronic Documents Act)	Data use limited to stated purpose, retention policy = 2 years max
Global Payments	PCI-DSS Level 1	Flutterwave, Paystack, and other gateways used by Riclivo are fully certified
Open Banking	PSD2 / OBIE Standards	Riclivo relies on regulated partners (Nordigen, Okra, Salt Edge) for bank connections



---

4. Data Governance & Retention

Data Category	Retention Period	Storage Type	Encryption

User Profiles	2 years (auto-purge after inactivity)	Encrypted Sheets / Secure Cloud	AES-256
Bank Tokens	30 days (refreshed via Nordigen OAuth)	Secure Vault API	End-to-end
Transaction Logs	12 months	Sheets + Backup	AES-128
Analytics & AI Logs	90 days	Pseudonymized	Obfuscated storage
Audit & Legal	5 years (only if required)	Legal archive	AES-256



---

5. User Rights

Access & Portability: Users can download a copy of all their Riclivo data anytime.

Deletion & Revocation: Disconnecting a bank deletes associated tokens immediately.

Correction: Editable fields (currency, language, country) can be updated by user.

Consent Management: Explicit consent banners appear before connecting APIs.



---

6. Partner Compliance Summary

Partner	Role	Certification / Status

Nordigen (GoCardless)	Open Banking Data	PSD2 / GDPR Compliant
Flutterwave	Global Payments	PCI-DSS Level 1
Paystack	African Payments	PCI-DSS Level 1
OpenAI / Riclivo AI	Conversational Engine	GDPR Data Processing Addendum
Google Workspace	Sheets Backend	ISO/IEC 27001 Certified



---

7. Cross-Border Data Transfers

All cross-border transfers occur only through compliant cloud or partner APIs.

No personal or financial data is transferred outside verified infrastructure.

Data localization follows regional regulations (EU = EU servers, NG = NDPR zone).



---

8. Compliance Monitoring

Layer	Frequency	Responsible Unit

Internal Data Review	Quarterly	Data Officer
Partner API Audit	Bi-annual	Integration Lead
Security Pen-Testing	Yearly	External Vendor
Legal Policy Updates	Ongoing	Legal Advisor



---

9. Legal Safeguards

Riclivo provides data processing agreements (DPAs) with all API and AI providers.

Every API request is token-limited and logged in the api_requests sheet for traceability.

Reclaims processed through banks or payment partners carry legal footnotes based on the Localization sheet — ensuring each claim aligns with local refund and tax laws.



---

10. Summary

Riclivo’s compliance model ensures that:
✅ Users control their data.
✅ No funds are held directly by Riclivo.
✅ All integrations are globally certified.
✅ Regional data rules are respected by design.

> “Riclivo doesn’t just automate — it complies by architecture.”
