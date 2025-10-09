

# 📄 crypto_integration.md

🔹 Purpose

This document describes how Riclivo connects with cryptocurrency exchanges and wallets (such as Binance and Bybit) to support:

Reclaim of network or platform fees,

Tracking of crypto transactions for bookkeeping, and

Optional payout in crypto (for supported regions).



---

⚙️ Supported Crypto Providers

Provider	Type	Supported Assets	Purpose	Notes

Binance API	Exchange	BTC, ETH, USDT	Transaction sync, reclaim of overpaid network fees	Global reach, strong API support
Bybit API	Exchange	BTC, ETH, USDT	Alternative to Binance; fast sync	Useful for margin traders
Coinbase API (optional)	Exchange/Wallet	BTC, ETH, USD Coin	Fiat-to-crypto conversion & user verification	GDPR-compliant
MetaMask / WalletConnect	Wallet	All EVM tokens	For wallet tracking or reclaim proof	Web3 ready



---

🧩 Integration Flow

1. User Connects Exchange or Wallet

The user chooses “Connect Crypto Account”.

Redirected to Binance/Bybit OAuth2 or enters an API key (securely encrypted).

Riclivo never stores private keys.



2. Wallet Verification

Riclivo requests read-only permissions:

wallet.balance.read

wallet.transaction.read


System confirms ownership via transaction signature or OAuth callback.



3. Transaction Import

Riclivo imports last 90 days of trades, deposits, withdrawals, and fees.

All imported data is saved in the transactions and bookkeeping sheets under source_bank = crypto.


Example entry in Google Sheets:

id: t_101
account_id: a_3
user_id: u_1
description: Binance trading fee
amount: -2.5
currency: USDT
type: fee
flagged_for_reclaim: TRUE
status: processing


4. Fee Reclaim Analysis

AI module analyzes transaction patterns.

Flags potential reclaimable items like:

Overcharged withdrawal fees

Failed transfers

Exchange downtime losses (optional)


Uses gpt-4-mini to classify and assign a refund probability score.



5. Reclaim Initiation

For compliant exchanges (e.g., Binance, Bybit):

Riclivo auto-fills a reclaim request via API or email template.

Exchange replies to user email directly (or via API ticket system).


For others: Riclivo prepares a downloadable proof file.





---

💱 Crypto-to-Fiat Conversion

Riclivo can automatically convert crypto refunds into USDT, USD, or NGN using supported providers:

Binance Convert API

Flutterwave Crypto Payment Gateway


Users can choose “Hold in Wallet” or “Withdraw to Bank”.



---

🔐 Security & Compliance

Area	Method

Encryption	AES-256 + SHA256 for stored credentials
Keys Storage	Encrypted field in config or Firebase secure vault
GDPR / AML	Riclivo never holds user funds; acts as data processor only
Audit Logs	Every connection and reclaim recorded in api_requests sheet
2FA Support	Exchange integrations require 2FA enabled by the user



---

🧠 AI Automation Layer

Auto Fee Detection: Identifies repeated small losses.

Reclaim Draft: Generates a pre-written claim referencing exchange policy.

Risk Scoring: Uses AI to assess reclaim success likelihood (Low, Medium, High).

User Prompt: “We found a reclaimable 2.5 USDT — proceed?”



---

🧾 Example API Request (Binance)

GET /api/v3/myTrades
Headers:
  X-MBX-APIKEY: {api_key}
Params:
  symbol: BTCUSDT
  startTime: 1698883200000
  endTime: 1701484800000

Response:

[
  {
    "symbol": "BTCUSDT",
    "commission": "2.5",
    "commissionAsset": "USDT",
    "time": 1701031200000,
    "isBuyer": false
  }
]

Riclivo interprets this as:

Transaction Fee → 2.5 USDT

Auto-tagged as reclaimable.



---

🌍 Fallback Option

If exchange APIs are blocked in a country:

Users can upload Binance Statement CSV.

Riclivo parses it using its AI engine.

Extracts trading fees, timestamps, and network charges for reclaim suggestions.



---

✅ Success Indicators

Once setup is complete:

“Wallet Connected ✅” appears under Integrations.

Riclivo shows total crypto holdings and reclaimable value estimate.

Notifications alert users of potential reclaims or sync issues.
