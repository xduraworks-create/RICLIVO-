# RICLIVO-
# Riclivo 🌍  
**AI-Powered Refund and Bookkeeping Assistant**

Riclivo is an intelligent financial assistant designed to help users automatically **track charges**, **reclaim wrongful bank fees**, and **manage their bookkeeping** — all powered by **AI, Open Banking, and secure payment APIs**.

---

## 🚀 Vision
To make global banking fairer and smarter — by enabling individuals and businesses to **reclaim what’s rightfully theirs** while simplifying financial management with AI automation.

---

## 🧠 Core Features
- **Open Banking Integration:** Connects securely to bank data via [Nordigen](https://nordigen.com/) and other API providers.  
- **AI-Assisted Reclaim:** Automatically identifies refund-eligible fees and generates legally backed reclaim requests.  
- **Smart Bookkeeping:** Auto-categorizes transactions, tax reports, and reconciliations.  
- **Multi-Language & Multi-Currency Support:** Auto-detects user location and applies country-specific tax and refund laws.  
- **Secure Payments:** Powered by **Flutterwave**, **Paystack**, and other regional processors.  
- **AI Chat Assistant:** Users can ask accounting or refund-related questions directly in-app.  

---

## 🧩 Architecture
- **Frontend:** Built with [Glide Apps](https://www.glideapps.com/) connected to Google Sheets.  
- **Backend:** Uses API integrations (Nordigen, Flutterwave, OpenAI).  
- **Database:** Google Sheets acting as dynamic data source.  
- **AI Models:** GPT-3.5-Turbo and GPT-4-Mini for reasoning, classification, and chat support.  

---

## 📊 Google Sheets Structure
Main sheets include:
- `users`
- `accounts`
- `transactions`
- `book_keeping`
- `reclaims`
- `api_requests`
- `config_sheet`
- `payments`
- `aichat`
- `localisation`
- `tax_reports`
- `ledger`
- `notifications`
- `integrations`
- `analytics_summary`
- `business_ideas`

Each sheet is structured with specific columns for secure data mapping between Glide and APIs.

---

## ⚙️ Config Highlights
| Setting | Default | Description |
|----------|----------|-------------|
| `commission_freemium` | 20% | Commission for free users |
| `commission_premium` | 10% | Commission for premium users |
| `commission_business` | 5% | Commission for business users |
| `freemium_switch_days` | 60 | Days between free account switches |
| `powered_by` | Nordigen, Flutterwave, Open Banking | Partner stack |

---

## 🔐 Security Notes
- User data is stored only temporarily and processed in compliance with **GDPR** and **Open Banking regulations**.  
- Sensitive API keys should never be shared publicly or stored directly in Glide sheets.  
- Always use environment variables (`.env`) or private Glide columns for API credentials.  

---

## 🧰 Tech Stack
- Glide + Google Sheets  
- Open Banking APIs (Nordigen, etc.)  
- Flutterwave / Paystack  
- OpenAI API (Chat + Classification)  
- GitHub for version control  

---

## 🧩 Upcoming Features
- 🧾 Reclaim tracking dashboard  
- 🌍 Country-level tax and legal intelligence  
- 🤝 Business partner portal  
- 💬 Multilingual AI chat  

---

## 📞 Contact
**Riclivo by Ndukwu Chukwukadibia Denis**  
📧 support@riclivo.com  
🌐 [www.riclivo.com](https://www.riclivo.com) *(coming soon)*  

---

### ⚖️ License
This project is licensed under the **MIT License** — see the LICENSE file for details.

---

### 💡 Note
This repository is for **project structure, configuration, and documentation**.  
Live backend APIs and secure data endpoints are hosted separately.
