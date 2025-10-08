# Riclivo Component Mapping

This document outlines all core components of the Riclivo app — both frontend and backend — and how they interact to form a unified user experience.

---

## 1. Overview

Riclivo is structured as a modular financial ecosystem, allowing flexibility across web and mobile. Each module connects through a common API gateway and central database layer.

---

## 2. Component Hierarchy

### 🧩 Frontend Components (Glide / Web Interface)

| Component | Purpose | Data Source | Dependencies |
|------------|----------|--------------|---------------|
| **Dashboard** | Displays user balance, transactions, and insights | `/api/user/data` | Auth & Transaction API |
| **Smart Wallet** | Handles deposits, withdrawals, and transfers | `/api/wallet/*` | Banking Integration |
| **Expense Tracker** | Logs, categorizes, and analyzes spending | `/api/expenses` | ML Engine (for auto categorization) |
| **AI Chat Assistant** | Guides users in finance, tax, and reclaim features | `/api/ai/chat` | OpenAI or internal NLP model |
| **Bookkeeping Panel** | Auto-syncs with invoices and receipts | `/api/bookkeeping` | OCR Engine, Accounting Engine |
| **Crypto Option (optional)** | Allows users to hold/send USDT & BTC | `/api/crypto/*` | Binance/Bybit APIs |
| **Notifications Center** | Alerts for payments, refunds, compliance | `/api/notifications` | All connected services |
| **Settings / Profile** | Manages user preferences & KYC | `/api/user/settings` | Auth & KYC service |

---

## 3. Backend Components

| Component | Description | Example Endpoints |
|------------|--------------|-------------------|
| **Authentication Service** | Manages sign-in, KYC, MFA | `/auth/login`, `/auth/verify` |
| **Transaction Engine** | Records and reconciles all wallet operations | `/wallet/transaction` |
| **Refund Engine** | Handles refund & reclaim automation | `/refunds/submit`, `/refunds/status` |
| **Tax & Compliance Engine** | Classifies transactions for tax reporting | `/compliance/check` |
| **AI Advisor Engine** | Provides personalized financial advice | `/ai/advisor` |
| **Notification System** | Sends updates via email/push | `/notify/send` |
| **Analytics Engine** | Tracks spending habits & performance | `/analytics/*` |

---

## 4. External Integrations

| Service | Purpose | Type |
|----------|----------|------|
| **Bank APIs** | Real-time sync with supported banks | Open Banking / PSD2 |
| **Payment Gateways** | Handles card & transfer payments | Flutterwave, Paystack |
| **Crypto Exchanges** | Optional trading & transfers | Binance, Bybit |
| **AI Provider** | NLP & AI chat interface | OpenAI API |
| **Accounting Sync** | Optional export to Xero / QuickBooks | API webhook |

---

## 5. Component Relationship Flow

```plaintext
User → Frontend UI → API Gateway → Core Services → Database
                ↓
             Integrations (Banking, AI, Crypto)
