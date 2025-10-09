# payment_integration.md

File: /integrations/payment_integration.md


---

1. Purpose

To outline all supported and planned payment methods Riclivo integrates with — both for receiving user payments and processing refunds or reclaims.


---

2. Supported Payment Layers

Category	Provider	Purpose	Status

Card & Wallet Payments	Stripe	Card processing (Visa, MasterCard), Apple Pay, Google Pay	✅ Active
	Paystack	Local NGN / African payments	✅ Active
	Flutterwave	Alternative Africa-wide option	🔄 Optional
Bank Transfers (Wise)	Wise Business	Multi-currency account for global transfers and settlements	⚙️ Setup (Estonia preferred)
Crypto Payments	Binance Pay / Bybit API	Accept USDT, BTC, ETH	⚙️ Under Review
In-App Reclaim Engine	Riclivo AI Engine	Auto-detect wrong charges, initiate reclaim through linked bank API	🧠 In Development
Bookkeeping Sync	QuickBooks / Xero API (read-only)	Optional user sync for balance reconciliation	🧩 Planned



---

3. Payment Flow

User pays for Riclivo plan → Stripe/Paystack processes payment → Riclivo logs transaction
↓
Reclaim Engine monitors bank transactions via Open Banking API
↓
If wrongful deduction found → Auto-reclaim via bank API or generate refund task
↓
Refund approved → User wallet or bank account credited
↓
Riclivo collects 10–15% commission → Settled via Wise multi-currency account


---

4. Security & Compliance Notes

All payment data is tokenized (PCI-DSS Level 1 compliant processors only).

No raw card data is ever stored by Riclivo.

Bank connections use OAuth 2.0 + Open Banking PSD2 standards.

Refund & payout functions require user re-authentication.

Crypto transactions are processed with AML/KYC layers (via exchange API).



---

5. Future Integrations

Apple Pay + Google Pay full native integration

Automated invoice generation per transaction

Support for stablecoins (USDT, USDC) as primary cross-border option

Integration with Tax & Bookkeeping modules to record payments automatically



---

6. Notes for Developers

Use PAYMENT_GATEWAY_KEY from .env file (never commit keys)

Test environments: sandbox.stripe.com, sandbox.paystack.com

Crypto webhooks handled via /api/payments/crypto/listener

Refund verification logged to transactions sheet under refund_status
