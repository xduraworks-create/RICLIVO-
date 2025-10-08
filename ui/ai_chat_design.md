🤖 ai_chat_design.md

This document describes how Riclivo’s AI Assistant interface works — from layout and chat logic to model allocation per tier and feature permissions.
You’ll put this inside your GitHub folder:
📁 /ui/ai_chat_design.md


---

🧩 1️⃣ Overview

Riclivo AI Assistant is the interactive financial and tax companion built into the app.
It helps users:

Understand transactions

Get bookkeeping and reclaim guidance

Learn business & finance best practices

Communicate with support if needed


The assistant has three personalities — tuned to user tiers.

Tier	Model	Role	Limits

Freemium	gpt-3.5-turbo	Basic accounting + Reclaim help	10 chats/month
Premium	gpt-4-mini	Tax assistant + bookkeeping AI	50 chats/month
Business	gpt-4	Business coach + AI tax strategist	Unlimited chats



---

💬 2️⃣ Chat Layout

Section	Description

Header	“💬 Riclivo AI — Ask about your finance or reclaim” + Tier tag
Message Bubbles	Rounded, minimal look. Riclivo AI messages in green, user messages in grey.
Suggested Prompts	Below input box — e.g., “Track my expenses”, “Explain VAT”, “How much can I reclaim?”
Input Field	Smart text box with mic + send button (voice option to come later).
Attachment Icon	Allows upload of receipt / bank statement for analysis (future update).



---

⚙️ 3️⃣ Chat Logic Flow

1. User sends query →
message logged in /aichat sheet with timestamp.


2. Backend trigger (via Make.com):

Reads user tier → loads correct AI model.

Passes message + user data context (e.g., “last 10 transactions”).

AI generates a tailored financial response.



3. Response displayed in chat UI with “thinking…” animation for realism.


4. AI Suggests follow-up (“Would you like me to reclaim that charge?” or “Add to bookkeeping?”).




---

🧠 4️⃣ Context-Aware Prompts

The AI dynamically references user’s:

Last transaction summary (from /transactions)

Current reclaim count (from /reclaims)

Tax laws from /localisation

Active plan (from /users)


This makes answers specific per user & country.
Example:

> “Based on your location (NG), VAT is 7.5%. This purchase may be reclaimable under Section 24 of the Finance Act.”




---

🔐 5️⃣ Permissions & Privacy

All messages stored securely in /aichat sheet with timestamps.

User can delete entire chat history at any time (button: “Clear chat”).

No banking data is exposed — AI only reads tokens or IDs, not credentials.

Riclivo displays a reminder once per chat:

> “Riclivo AI provides financial guidance only. Always confirm with your tax authority.”





---

💎 6️⃣ Tier-Specific Features

Feature	Freemium	Premium	Business

Reclaim suggestions	✅	✅	✅ + Auto draft
Expense categorization	✅ Manual	✅ Auto	✅ Smart rules
Tax estimate	❌	✅	✅ Advanced
Bookkeeping entry	✅	✅	✅ + AI predictions
Business coach	❌	❌	✅
Chat history	30 days	6 months	Unlimited
Voice chat	❌	✅ (Beta)	✅



---

🧩 7️⃣ Future Enhancements

Multi-language support via /localisation

Voice-to-text and speech response

Export chat as PDF report

Connect AI advice directly to “Actions” (Reclaim / Bookkeeping / Tax)

“Ask Riclivo AI” floating button across app pages
