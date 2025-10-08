🧭 Riclivo — UI Flow Document

Purpose:

This file maps the full user journey inside the Riclivo app — from onboarding to reclaims, bookkeeping, and AI assistance. It helps developers (or Glide builders) understand what each screen does, what data it touches in Google Sheets, and what triggers or conditions apply.


---

1️⃣ Splash & Onboarding

Screen: SplashScreen

Displays Riclivo logo & tagline:

> “Smart Refunds. Smarter Finances.”



Shows Powered by Nordigen | Flutterwave | OpenAI

Button: Continue


→ Leads to: Welcome / Sign Up


---

2️⃣ Welcome / Sign Up

Screen: AuthScreen

Options:

“Create Account” → /auth/signup

“Login” → /auth/login

“Continue as Guest” (limited demo)


User inputs: email, phone, password

Auto-detect country and currency via localisation sheet.

Checkbox: ✅ “I agree to Terms and Conditions.”


→ On success: redirect to Setup Bank


---

3️⃣ Setup Bank Connection

Screen: ConnectBankScreen

Title: “Link your bank or card”

Message:

> “Riclivo connects safely through Open Banking. Your details are never stored.”



Choose provider:

Nordigen (Europe)

Paystack / Flutterwave (Africa)

Plaid (optional for US/Canada)


After successful link → creates account entry in accounts sheet.


→ Next: Dashboard


---

4️⃣ Dashboard (Home)

Screen: DashboardScreen

Displays:

Account balance summary

Recent transactions (from transactions sheet)

Reclaimable estimate (AI summary)

Quick buttons:

🧾 Scan for Refunds

📊 Bookkeeping

💬 Ask Riclivo AI

💼 Business Tools



If user is freemium → banner:

> “Upgrade to Premium for faster scans and lower commission!”




→ Next possible actions: Reclaim | AI Chat | Bookkeeping | Business Panel


---

5️⃣ Reclaim Flow

Screen 1: ReclaimScan

Action: “Scan Account for Refunds”

Triggers /reclaim/scan endpoint (AI + API call).

Shows list:

Transaction Description

Bank Name

Date

“Possible Refund: ₦1,200”



Screen 2: ReclaimConfirm

Message:

> “@20% of ##,###.## can be reclaimed and paid to your bank account. Click Confirm to proceed.”



Terms checkbox (legal note auto-fills from localisation).

Card verification (via Flutterwave or Paystack).



Screen 3: ReclaimStatus

Shows:

Submitted claim

Date sent

Expected timeline

“Track Status” button



→ Data linked: reclaims, transactions, notifications, api_requests


---

6️⃣ Bookkeeping & Tax

Screen: BookkeepingDashboard

Tabs:

“Add Transaction”

“View Reports”

“Export Data”


Fields: amount, type, category, date, receipt upload

Auto-suggest categories using Riclivo AI.

Option: “Generate Tax Summary”
→ Creates tax report PDF from localisation tax law and sends to tax_reports.


→ Linked Sheets: book_keeping, tax_reports, users


---

7️⃣ AI Chat Assistant

Screen: AIChatScreen

Floating AI chat bubble on every main screen.

Prompts: “How do I record VAT?” or “What’s my reclaim total?”

Response from /ai/chat endpoint (GPT-3.5 or GPT-4-mini).

Context-aware: can pull data from current user, account, or transaction.


→ Linked Sheets: aichat, users, analytics_summary


---

8️⃣ Business Tools

Screen: BusinessPanel

For premium/business tiers only.

Tools:

“Reclaim Across Multiple Accounts”

“Smart Expense Classifier”

“3-Year Subscription Offer (-10%)”

“AI Business Coach” (chat specialized for SME guidance)


Uses same /ai/chat engine but with business context.

Shows analytics graphs from analytics_summary.


→ Linked Sheets: users, transactions, analytics_summary


---

9️⃣ Settings & Account Switch

Screen: SettingsScreen

Sections:

Profile & Subscription

Switch Account (button grayed until cooldown expires)

Language & Currency Preference (auto-detect but editable)

Legal Documents (view Terms, Privacy, Refund Policy)


App will notify user automatically when switch period is due (via notifications sheet).


→ Linked Sheets: users, config_sheet, notifications


---

🔟 Notifications & Alerts

Screen: NotificationsScreen

Displays reclaim updates, switch reminders, subscription renewal alerts.

Sources:

Automated from notifications sheet.

Realtime if possible via Glide “trigger actions”.




---

🧾 UI Navigation Overview

Section	Description	From	To	Data Source

Splash → Auth	App intro	App launch	Signup/Login	Static
Auth → Setup Bank	After signup	Bank setup	users, accounts	
Dashboard	Central hub	Any screen	All	transactions, reclaims
Reclaim Flow	Refund scan & status	Dashboard	Reclaim pages	reclaims
Bookkeeping	Finance management	Dashboard	Bookkeeping	book_keeping
AI Chat	Context help	Any screen	Chat	aichat
Business Tools	Advanced analytics	Dashboard	BusinessPanel	analytics_summary
Settings	Profile, plan	Dashboard	Settings	users, config
Notifications	Alerts	Dashboard	Notifications	notifications



---

🔒 Security Logic (UI-level)

All sensitive screens (Reclaim, Payment, Settings) require verified session token.

Device binding used to prevent multiple logins for freemium tier.

User confirmation popups before every reclaim and payment.
