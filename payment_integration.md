payment_integration.md

Title: Payment Integration – Flutterwave / Paystack / Stripe


---

Purpose

Riclivo uses secure payment gateways to:

Collect subscription fees (Freemium → Premium → Business)

Process commission payments for successful refunds

Support multi-currency receipts and global scalability


Supported gateways are region-based:

Region	Provider	Notes

Africa	Flutterwave, Paystack	Local cards, bank transfer, and mobile money
Europe / UK	Stripe, GoCardless	SEPA, Visa, Mastercard
North America	Stripe	ACH and credit cards
Asia	Razorpay (future)	INR and regional wallets



---

API Endpoints

Function	Endpoint	Method	Description

Create payment link	/payments/create	POST	Generate payment link for subscription or refund commission
Verify payment	/payments/verify/:id	GET	Confirm transaction status
List transactions	/payments/history	GET	Retrieve all user payments
Refund payment	/payments/refund/:id	POST	Process refund reversal where applicable



---

Payment Flow

1. User selects a subscription plan (Freemium / Premium / Business) in the app.


2. Riclivo generates a checkout session with the active payment provider.


3. Upon successful payment:

Provider sends a webhook → /webhook/payment_success

Riclivo updates users and transactions sheets.



4. For refund reclaims:

The refund commission is auto-calculated (reclaim_amount_estimate × commission_pct)

Payment confirmation triggers the “release refund” workflow.





---

Commission and Plans

Plan	Duration	Commission	Billing Cycle

Freemium	60 days	20%	Free
Premium	6 months	10%	$60/year
Business	1 year	5%	$100/year or $270/3 years



---

Security Standards

All transactions go through SSL 256-bit encryption.

PCI-DSS Level 1 compliance enforced (Stripe / Flutterwave).

No card data is stored on Riclivo servers or Sheets.

Webhooks are verified via HMAC signature (secret keys in .env).

Fraud detection via gateway’s native risk API.



---

Webhook Handling

Event	Source	Action

payment_success	All	Update user tier and active subscription
payment_failed	All	Notify user and retry (max 3)
refund_processed	Stripe / Flutterwave	Update bookkeeping + transaction sheet
subscription_expired	Riclivo internal	Notify user and downgrade to Freemium



---

Multi-Currency Support

Handled dynamically via Localization Sheet:

Detect user region → match currency (₦, $, €, £, etc)

Payment API auto-converts or routes to correct provider

Currency stored in transactions.currency



---

Future Additions

Add crypto-based payout layer (USDT/BTC) for users in restricted payment regions

Introduce Riclivo Wallet (virtual escrow) for faster refund credits

Integrate Apple Pay / Google Pay for in-app payment flow
