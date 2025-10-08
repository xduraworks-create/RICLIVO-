# 🧩 Riclivo Compliance Summary

**Last Updated:** October 2025  
**Prepared By:** Riclivo Core Team  
**Applies To:** All Riclivo Platforms (App, API, and AI Assistant)

---

## 1. Overview
Riclivo operates as a **financial data management and refund automation platform**, connecting users’ bank data through **Open Banking APIs (Nordigen, Paystack, Flutterwave, and Binance Pay)** to help them:
- View transactions,
- Detect reclaimable fees or failed transactions,
- Automate refund requests,
- Simplify tax and bookkeeping operations.

We do **not hold user funds** or directly process financial transactions. All payment and data connections are handled through **licensed third-party providers**.

---

## 2. Regulatory Compliance

### a. **Open Banking (EU & UK)**
Riclivo uses **Nordigen (GoCardless)** for secure data aggregation under the **EU PSD2 and UK Open Banking Regulations**.  
All API connections are compliant with:
- **European Banking Authority (EBA) RTS standards**
- **Strong Customer Authentication (SCA)**
- **Account Information Service Provider (AISP)** rules

**We never store bank credentials or access tokens directly.**

---

### b. **Financial Data Compliance**
- All data is encrypted (AES-256 at rest, TLS 1.3 in transit).
- Riclivo does not modify or create synthetic financial records.
- Refund or reclaim requests are submitted through **user-consented endpoints** only.

---

### c. **Tax Compliance**
- Riclivo AI Tax Assist follows **jurisdiction-based tax laws** (from localization sheet).
- The system provides **AI guidance only** — users are advised to confirm filings with licensed accountants.
- Country references are mapped using `tax_law_reference` in the localization dataset.

---

### d. **Crypto Payout Compliance**
Riclivo integrates with **Binance Pay / BitPay / NOWPayments** for optional crypto withdrawals.  
Crypto functions are:
- Optional and disabled by default.
- Bound by user country’s crypto law (see `crypto_regulation_note` in Localization).
- Subject to **KYC verification** via third-party gateway before disbursement.

---

## 3. Privacy and Data Protection

- Riclivo complies with **GDPR (EU)**, **NDPR (Nigeria)**, **CCPA (California)**, and **PIPEDA (Canada)**.
- All personal data (email, phone, account details) are user-owned.
- Users can **export or delete** their data at any time via the app or email request.
- No personal data is sold, rented, or used for targeted advertising.

---

## 4. AI Model Compliance

AI responses are powered by **OpenAI models (GPT-4-mini, GPT-3.5-turbo)**.  
Riclivo AI:
- Provides explanations, not financial advice.
- Is limited to contextual data provided by the user.
- Logs are anonymized before model use.

---

## 5. Legal Frameworks & Disclaimers

Riclivo operates as a **Data Processing Platform**, not a financial institution.  
Users’ rights and obligations are governed by:
- `terms_and_conditions.md`
- `privacy_policy.md`
- `refund_policy.md`
- `open_banking_disclaimer.md`
- `crypto_disclaimer.md`
- `gdpr_notice.md`

All disclaimers are accessible from the “Legal” tab in the app.

---

## 6. Auditing and Record Retention

- Transaction logs are retained for **2 years** for compliance and traceability.
- All reclaim communications include an **audit hash** and **timestamp**.
- Users can view or download their reclaim audit reports.

---

## 7. Data Hosting and Security

Riclivo infrastructure is hosted on **Google Cloud** with:
- **ISO 27001** data centers,
- Daily encrypted backups,
- Role-based access control (RBAC),
- 2FA enforced on all admin panels.

---

## 8. Cross-Border Data Handling

- Data is processed within the **region of origin** whenever possible.
- Transfers outside EU/EEA follow **Standard Contractual Clauses (SCCs)**.
- Country mapping is handled dynamically by `localization` settings.

---

## 9. Compliance Contact

**Riclivo Compliance Office**  
📧 compliance@riclivo.com  
🌍 https://riclivo.com/legal  
🕒 Response Time: Within 72 hours  

---

> ⚖️ *Riclivo is committed to transparency, user empowerment, and full adherence to open banking and privacy laws across all jurisdictions.*
