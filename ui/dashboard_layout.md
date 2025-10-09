

# 🏠 Riclivo Dashboard Layout

1️⃣ Overview

The Riclivo dashboard is the main control panel for users after login.
It gives a quick summary of financial health, pending reclaims, bookkeeping overview, and AI guidance.


---

2️⃣ Layout Structure

Top Bar (Fixed):

Logo: Riclivo name + white icon version

Greeting: “Welcome back, {user_name}”

Quick buttons:

🔍 Search

🧠 AI Chat

⚙️ Settings




---

Main Sections:

Section	Visible to	Description	Dynamic Elements

Reclaim Summary	All tiers	Displays number of flagged transactions and potential reclaim value	“@{commission_pct}% of ##,###.## available for reclaim”
Bookkeeping Snapshot	Premium & Business	Auto-updated balance sheet summary	Chart of expenses vs income
Tax Overview	Premium & Business	Estimated taxes owed or reclaimable VAT	Links to “Tax Reports” tab
Smart Tips	All tiers	AI-generated personal finance or business insights	Updated weekly
AI Chat Widget	All tiers	Opens a side panel to chat with Riclivo AI	Pulls chat model per tier
Subscription Summary	All tiers	Shows current plan, renewal date, switch option	Dynamic button: “Upgrade / Renew”
Reward / Referral	All tiers	Displays referral count & bonus value	Connects to config.referral_bonus_pct



---

3️⃣ Navigation Menu (Bottom / Side)

Icon	Label	Action

💰	Reclaims	Opens Reclaim Management page
📊	Bookkeeping	Opens Transactions + Ledger summary
🧾	Tax	View tax records and submit VAT returns
🧠	AI	Opens AI assistant (floating chat window)
⚙️	Settings	Profile, subscriptions, notifications



---

4️⃣ Theme & UI Behaviour

Theme: White background + black logo (default), auto dark mode at night.

Primary Accent: Deep green (#00A67E) to indicate “verified / approved reclaim.”

Secondary Accent: Soft grey + teal for status indicators.

Responsive Design: Automatically fits both mobile (vertical) and tablet (horizontal) layouts.



---

5️⃣ Notifications

🔔 Top-right icon displays count of pending actions:

Reclaim awaiting verification

Subscription renewal

AI message or accounting tip

Referral payout available




---

6️⃣ Business Dashboard Additions

For Business Tier users only:

“Team Members” tab — manage accountant and staff access.

“Tax Filing Progress” — tracks monthly/quarterly tax report uploads.

“Business Coach AI” — premium chat option for strategic financial advice.



---

7️⃣ Future Enhancements

Drag-and-drop customizable widgets (e.g., move “Tax” before “Bookkeeping”)

Real-time notifications when API tokens expire.

Visual leaderboard for referral bonuses.

Personalized “Financial Goals” section.
