# Riclivo Data Flow Documentation

Last updated: October 2025
Document type: System Architecture – Data Flow Overview
Purpose: To describe how user data, AI services, API connections, and business logic move through Riclivo for refunds (reclaims), bookkeeping, tax reporting, and AI chat.


---

1. Overview

Riclivo is a smart finance automation and refund assistant built around Open Banking APIs, Flutterwave/Paystack integrations, and AI automation.

It performs four key functions:

1. 🏦 Automatically identifies and reclaims wrongful bank charges (refund automation).


2. 📘 Records and categorizes financial activity for bookkeeping and self-employment.


3. 🧾 Generates tax summaries aligned with local tax laws using AI automation.


4. 🤖 Offers a built-in AI chat assistant for instant financial help and business coaching.




---

2. Core Components

Layer	Description

Glide Frontend (App UI)	The user-facing app, built in Glide and powered by Google Sheets. It handles all inputs, displays data, and connects with APIs securely.
Google Sheets Backend	Acts as Riclivo’s live database (users, transactions, reclaims, bookkeeping, localization, etc.).
API Integrations	Nordigen (Open Banking), Flutterwave/Paystack (Payments), and others connect to sync accounts and handle bank payouts.
Automation Layer (Serverless Logic)	Handles AI analysis, reclaim processing, bookkeeping categorization, and report generation.
AI Engine (OpenAI Models)	Powers chat, refund explanations, and smart insights using localized context.



---

3. Data Flow by Pipeline


---

3.1 — Onboarding & Authentication

Step	Source	Destination	Description

1	User	Glide (Users Sheet)	User signs up using email, name, and phone number.
2	Glide	Nordigen API	Riclivo initiates Open Banking connection.
3	Nordigen	Riclivo	Retrieves token + account metadata.
4	Riclivo	Sheets (accounts)	Saves basic account data (bank name, country, expiry date).
5	Sheets → Glide	User	Shows connected accounts and summary dashboard.


Automation: Users only re-verify banking connections when token_status=expired.


---

3.2 — Transaction Synchronization

Step	Source	Destination	Description

1	Nordigen	API Requests Sheet	Riclivo requests transactions using date filters.
2	API	Transactions Sheet	Each transaction (debit/credit) logged with metadata.
3	AI Logic	Transactions	AI flags potential reclaim candidates (fee_flag=TRUE).
4	Sheets	Analytics Summary	Used for monthly metrics and reports.



---

3.3 — Refund/Reclaim Pipeline

Step	Source	Destination	Description

1	Transactions	AI Engine	AI checks for wrongful or duplicate charges.
2	AI	Reclaims Sheet	Creates new reclaim entry with status="pending".
3	Riclivo	Bank API (Nordigen/Flutterwave)	Initiates reclaim to user’s linked bank card.
4	Bank API	Riclivo	Sends response (success/failure).
5	Riclivo	Reclaims Sheet	Updates status & sends user push notification.


Commission Logic:

Freemium = 20%

Premium = 10%

Business = 5%


Popup Example:

> “@20% of ##,###.## can be reclaimed and paid to your bank account. Click confirm to proceed.”
Note: Riclivo only charges from successful reclaims.




---

3.4 — Payments & Account Switching

Payouts are handled through Flutterwave (global) and Paystack (Africa).

Users can switch bank connections after:

Freemium → every 30 days

Premium → every 6 months

Business → every 12 months


Users receive automated reminders when a switch becomes available.



---

3.5 — Analytics & Reporting

Source	Output	Function

Transactions	Analytics Summary Sheet	Tracks monthly inflow/outflow, reclaim success rates, and AI accuracy.
Reclaims	Notification System	Sends updates and alerts to users.
API Logs	Security & Auditing	Verifies uptime, token validity, and API efficiency.



---

3.6 — Bookkeeping & Tax Automation Pipeline

Step	Source	Destination	Description

1	Transactions	Bookkeeping Sheet	Each verified transaction is mirrored and categorized.
2	Bookkeeping	AI Tax Classifier	AI assigns tax category (deductible, taxable, exempt).
3	AI Engine	Tax Reports Sheet	Summaries are generated monthly or quarterly.
4	Tax Reports	Glide	User sees tax dashboard and reports.
5	Localisation	Tax Logic	References correct tax laws for each country.


Example Record:

{
  "transaction_id": "t_2034",
  "category": "Software Subscription",
  "amount": -35,
  "currency": "USD",
  "deductible": true,
  "vat_applicable": true,
  "tax_code": "US-IRS-162",
  "receipt_url": "https://riclivo.com/docs/receipt_2034.pdf"
}

Purpose:
This feature turns Riclivo into a micro-accountant, helping users automate tax returns and financial management.


---

3.7 — AI Chat & Support Assistant

Step	Source	Destination	Description

1	User → Glide	OpenAI Model	User asks a question via chat (tax, business, refund, etc).
2	Glide	Sheets (Context Retrieval)	Pulls user’s region, data, and transaction history.
3	Sheets → AI Engine	Response Generation	AI forms a personalized answer or suggestion.
4	AI → Glide	Chat Response	User receives contextual response.
5	AI → Logs	Summary	Logs for analytics (not stored permanently).



---

3.8 — Combined System Overview

Users 
   │
   ▼
 Glide App (Frontend)
   │
   ▼
 Google Sheets (Backend)
   ├── Transactions
   ├── Reclaims
   ├── Bookkeeping
   ├── Tax Reports
   ├── AI Chat
   └── Localisation
   │
   ▼
 API Integrations
   ├── Nordigen (Bank Data)
   ├── Flutterwave / Paystack (Payments)
   └── OpenAI (AI Logic)
   │
   ▼
 Automation Layer
   ├── Reclaim Validation
   ├── Tax & Bookkeeping
   ├── Analytics + Notifications
   └── Legal Logic (Localization)


---

3.9 — Data Privacy & Security Notes (Summary)

Riclivo does not permanently store raw bank transaction data.

All API tokens are temporary (default 365 days) and encrypted.

Only computed results (reclaim summaries, analytics, tax reports) are stored in Sheets.

Each user’s data is segmented by user_id to ensure compliance with GDPR and Open Banking standards.



---

✅ Summary

Riclivo’s data flow ensures:

Full automation of financial reclaiming, bookkeeping, and tax management.

Localized compliance with each country’s refund and tax laws.

Privacy-first design — lightweight, serverless, secure.

AI-powered personalization — every user gets tailored insights, reports, and conversations.
