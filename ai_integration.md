ai_integration.md

Title: AI Integration – Riclivo Smart Assistant & Automation Engine


---

Purpose

Riclivo’s AI layer powers:

Personalized chat and support (via GPT models)

Automated bookkeeping and tax estimation

Refund and reclaim classification

Smart reminders and financial insights


The AI system connects to OpenAI models and optionally other LLM APIs for fallback and load balancing.


---

Architecture Overview

Layer	Function	Technology

AI Gateway	Routes user prompts to AI provider (OpenAI, Anthropic, local model)	API proxy
Context Memory	Saves user interactions and context across sessions	Glide Sheets / Firestore
NLP Analysis	Detects intent (refund, tax, claim, or bookkeeping)	GPT model fine-tuned with Riclivo schema
Action Trigger	Executes related task (update sheet, flag reclaim, generate note)	Automation scripts or Zapier



---

Model Configuration

Plan	Model Used	Primary Function

Freemium	gpt-3.5-turbo	Chat and simple bookkeeping
Premium	gpt-4-mini	Smart insights, refund logic, auto-flag
Business	gpt-4o or custom-model	AI-powered analytics, auto tax prep, multilingual support


> All AI calls pass through Riclivo’s proxy endpoint to protect API keys.




---

AI Endpoints

Function	Endpoint	Method	Description

/ai/chat	POST	Handle chat messages and return AI response	
/ai/classify	POST	Classify transactions for tax/bookkeeping	
/ai/reclaim_suggest	POST	Suggest reclaim actions or verify eligibility	
/ai/summary	GET	Generate a summary of a user’s month/quarter performance	



---

Data Flow

1. User Prompt:
User sends a message (e.g., “Why did my bank charge ₦1,200?”)


2. Intent Detection:
AI identifies it as a fee-related reclaim query.


3. Context Fetch:
Pulls relevant data from transactions and accounts sheets.


4. Response Generation:
AI generates a reply:
“That’s a monthly service fee by FirstBank. You may reclaim ₦1,200 under CBN Refund Section 24.”


5. Action:
User can click “Proceed to Reclaim” → triggers reclaim API.




---

Automation Examples

Trigger	AI Action	Result

New transaction imported	Auto-classify type and category	“Bank Fee” tagged
Reclaim submitted	Generate legal summary	Pulls legal note from localization
User inactivity (14 days)	Send smart reminder	“Hey Ada, you have 2 reclaimable charges pending.”
Language change	Adjust prompt language	Returns localized responses



---

Security & Privacy

No banking or personal data sent to AI providers.

Only anonymized transaction context and intent are transmitted.

Users can opt-out of AI storage in config.allow_user_override.

All conversations logged in aichat sheet with unique session IDs.



---

Multilingual Support

Riclivo AI dynamically detects the user’s preferred or system language from the localization sheet.

Supported languages include:

English 🇬🇧

French 🇫🇷

German 🇩🇪

Spanish 🇪🇸

Hindi 🇮🇳

Arabic 🇸🇦

Swahili 🇰🇪

Portuguese 🇧🇷



---

AI Personalization Engine

Feature	Description

Contextual replies	AI remembers last 10 user interactions
Localized legal base	Fetches country’s tax and banking act
Adaptive tone	Formal for business users, friendly for freemium
Smart tagging	Flags expenses or recurring payments automatically



---

Future Plans

Introduce offline AI caching (for low-data regions)

Add voice assistant mode (“Hey Riclivo…”)

Launch Smart TaxBot that pre-fills forms using bank data

Develop LLM evaluation dashboard for compliance audits
