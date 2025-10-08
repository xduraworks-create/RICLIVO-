
📄 bank_integration.md

🔹 Purpose

This document explains how Riclivo connects to traditional banks across regions to fetch transactions, verify accounts, and initiate reclaim payouts securely using compliant open-banking APIs.


---

⚙️ Core Banking Partners

Region	Provider	Purpose	Notes

🇪🇺 Europe	Nordigen (GoCardless)	PSD2 Open Banking	Free access to EU banks (over 2,000 supported).
🌍 Africa	Flutterwave	Account verification, payouts, transaction sync	Works with major banks in Nigeria, Ghana, Kenya, South Africa, etc.
🇺🇸 USA	Plaid / Finicity	Open banking API	Used for transaction sync and balance verification.
🇬🇧 UK	TrueLayer	FCA-compliant banking API	Covers UK banks for direct data and reclaim payouts.
🌏 Asia	SaltEdge / Brankas	Bank API aggregation	Supports India, Singapore, Philippines, and more.



---

🧩 Integration Flow

1. User Connects Bank

Riclivo uses secure OAuth or API token-based connection.

The user selects their bank → redirected to provider (e.g., Nordigen or Flutterwave) → logs in securely.

Riclivo never stores bank credentials directly.



2. Token Retrieval

After authentication, the provider returns an access token and refresh token stored in the encrypted database (config + users sheets).

Access tokens expire after a set period (e.g., 30–90 days).



3. Transaction Sync

Using /transactions/fetch endpoint, Riclivo pulls the last 90 days of data.

The data is stored in transactions and bookkeeping sheets automatically.



4. Fee Flagging

AI engine analyzes transactions for refund-eligible charges (bank_fee, failed_payment, duplicate_charge).

Automatically marks flagged_for_reclaim = TRUE.



5. Payouts / Reclaims

After verification, Riclivo triggers payout via Flutterwave or TrueLayer Pay.

Payout transactions are recorded in the bookkeeping sheet with status = completed.



6. Refresh Cycle

Tokens are automatically refreshed every 24–48 hours.

If expired, users receive a notification to reconnect their bank.





---

🔐 Security Protocols

All connections use OAuth2.0 + TLS 1.3 encryption.

Sensitive tokens are hashed using AES-256 and stored in a secure config sheet or encrypted field.

Riclivo follows Open Banking PSD2 and GDPR data processing standards.

Users can disconnect their bank anytime under Account → Security.



---

🧠 Automation + AI Layer

Auto-detects and classifies transactions using OpenAI model (e.g., gpt-4-mini).

Flags potential reclaim transactions automatically.

Calculates reclaimable amount based on config commission tiers.



---

⚙️ Fallback Option

If no open banking provider is available:

Users can upload their bank statement (CSV or PDF).

Riclivo parses it automatically and extracts transactions using OCR + AI.

All extracted data is stored in the transactions sheet with a tag source_bank = manual_upload.



---

🧾 Example API Setup (Nordigen)

POST /api/v1/bank/connect
Authorization: Bearer {user_token}
Body:
{
  "provider": "Nordigen",
  "institution_id": "SANDBOX_FINBANK_NG",
  "redirect_url": "https://riclivo.com/auth/callback"
}

Response:

{
  "link": "https://ob.nordigen.com/authorize?token=xxxx",
  "status": "pending",
  "expires_in": 300
}


---

✅ Success Indicator

Once a connection is successful:

The user sees “Bank Connected ✅”

Riclivo shows “Last Synced: [timestamp]”

A notification confirms the bank is eligible for reclaim automation.
