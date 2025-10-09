# 📘 schemas/users_schema.md

Purpose

Defines how user identity, preferences, and localization data are stored and linked to other sheets (accounts, transactions, AI chat, etc.).


---

Table: users

Column	Type	Description	Example

id	String	Unique user ID	u_1
email	String	User’s registered email	ada@example.com
name	String	Full name	Ada Ndukwu
phone	String	User’s phone number	2348012345678
country_code	String	2-letter ISO country code	NG
location_detected	String	Country detected automatically	Nigeria
preferred_language	String	User’s preferred language	English
preferred_currency	String	Display and reclaim currency	NGN
tier	Enum	Subscription plan (Freemium, Premium, Business)	Freemium
device_id	String	Auto-generated device identifier	dev_001
signup_date	Date	Date of registration	2025-10-01
last_seen	Date	Last active date	2025-10-05
user_status	Enum	Current status (active, inactive, banned)	active
legal_note	String	Regional legal clause from Localization	Refunds covered under NDPR 2020...
tax_law_ref	String	Country’s tax reference	Finance Act 2020



---

Relationships

1 → Many → Accounts: A user can connect multiple bank accounts.

1 → Many → Transactions: All transactions trace back to user_id.

1 → Many → Reclaims: Reclaims are generated per transaction by user.

1 → 1 → Localization: Country, currency, and language are linked automatically.



---{
  "user_id": "uuid",
  "full_name": "string",
  "email": "string",
  "phone_number": "string",
  "country": "string",
  "preferred_currency": "string",
  "linked_accounts": {
    "bank": ["Mono", "Plaid"],
    "crypto": ["Binance", "Bybit"]
  },
  "verification": {
    "kyc_status": "pending | verified | rejected",
    "last_verified": "datetime"
  },
  "user_role": "user | admin | accountant",
  "created_at": "datetime",
  "updated_at": "datetime",
  "ai_profile_notes": "string",
  "purpose": "Stores all user-related data including personal info, KYC status, linked accounts, and AI assistant context."
}




🏦 schemas/accounts_schema.md

Purpose

Defines how user bank accounts and tokens are handled via Nordigen, Flutterwave, or Paystack.


---

Table: accounts

Column	Type	Description	Example

id	String	Unique account ID	a_1
user_id	String	Linked user	u_1
bank_name	String	Display name of bank	FirstBank
bank_provider	Enum	API provider	Nordigen
masked_account	String	Partially hidden number	****2345
account_owner_name	String	Name on bank account	Ada Ndukwu
account_hash	String	Hashed identifier for security	acct_hash_001
account_currency	String	Currency used by the bank	NGN
connected_date	Date	Date account was linked	2025-09-20
token_status	Enum	Active, expired, revoked	active
token_expires	Date	Expiry of Open Banking token	2025-11-20
token_scope	String	Data access permission	transactions:read
device_binding	String	Linked device id	dev_001
switch_allowed_from	Date	When user can switch bank	2025-12-20



---

Relationships

Many → 1 (Users)

1 → Many (Transactions)

1 → Many (API Requests)



---

💸 schemas/transactions_schema.md

Purpose

Holds all user transaction data fetched from connected banks or entered manually.

