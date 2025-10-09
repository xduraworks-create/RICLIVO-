

# 🧩 api_endpoints.md


---

Purpose

This document lists all planned API endpoints that Riclivo will expose (directly or via Glide logic) for internal operations, partner APIs, and automation.
It also defines how the app communicates securely between modules.


---

1. Authentication & User Management

Endpoint	Method	Description	Input	Output	Notes

/auth/signup	POST	Registers a new user	{email, password, country_code}	{user_id, tier, token}	Validates email via OTP
/auth/login	POST	Logs user in	{email, password}	{token}	Token expires in 30 days
/auth/logout	POST	Ends session	{token}	{success}	Clears Glide session
/user/profile	GET	Fetches user profile	{token}	{user_id, name, plan, country}	Auto pulls from Google Sheets “users”



---

2. Accounts & Bank Connections

Endpoint	Method	Description	Input	Output	Notes

/accounts/connect	POST	Connects bank via Nordigen	{user_id, bank_code}	{account_id, status}	Uses OAuth2
/accounts/list	GET	Lists connected accounts	{user_id}	[{account_id, bank_name, balance}]	
/accounts/disconnect	DELETE	Disconnects bank	{account_id}	{success}	Updates token_status



---

3. Transactions & Reclaims

Endpoint	Method	Description	Input	Output	Notes

/transactions/fetch	GET	Fetches latest transactions	{account_id}	[{txn_id, desc, amount, date}]	Mapped from Nordigen or Crypto APIs
/reclaim/scan	POST	Runs AI scan for reclaimable fees	{user_id}	{count, estimate, reclaim_list}	Uses GPT-4-mini
/reclaim/submit	POST	Sends reclaim to provider	{txn_id}	{status, ref_id}	Generates proof letter or API claim
/reclaim/status	GET	Check status of ongoing reclaim	{ref_id}	{status, update}	Pulls from reclaims sheet



---

4. Bookkeeping & Tax Reports

Endpoint	Method	Description	Input	Output	Notes

/bookkeeping/add	POST	Add an expense/income manually	{user_id, desc, amount, type}	{entry_id}	Linked to Google Sheets bookkeeping tab
/bookkeeping/generate-tax	POST	Create automated tax report	{user_id, period}	{report_url}	Based on localisation tax law
/reports/download	GET	Download tax or reclaim report	{report_id}	.pdf or .csv	Optional on paid tiers



---

5. AI Chat & Assistant

Endpoint	Method	Description	Input	Output	Notes

/ai/chat	POST	Send message to Riclivo AI	{user_id, message}	{reply}	GPT-3.5 or GPT-4-mini
/ai/suggest	GET	Retrieve smart suggestions	{context}	{recommendations}	Used for reclaim tips and saving alerts



---

6. Payments

Endpoint	Method	Description	Input	Output	Notes

/payment/initiate	POST	Starts payment via Flutterwave/Paystack	{user_id, amount, currency, purpose}	{checkout_url}	Redirects user to gateway
/payment/verify	GET	Confirms completed payment	{tx_ref}	{status}	Updates subscription status
/subscription/change	POST	Upgrades or downgrades user tier	{user_id, plan}	{new_status}	Enforces cooldown period (30/180/365 days)



---

7. System & Config

Endpoint	Method	Description	Input	Output	Notes

/config/get	GET	Retrieve config constants	—	{config_object}	Used on app load
/notifications/list	GET	Show app notifications	{user_id}	[notification_id, type, date]	From notification sheet
/analytics/summary	GET	Retrieve usage & reclaim analytics	{user_id}	{summary}	Visible to user and admin



---

8. Admin / Monitoring

Endpoint	Method	Description	Input	Output	Notes

/admin/users	GET	List all users	{admin_token}	{user_data}	Restricted
/admin/logs	GET	Access API call logs	{admin_token}	{logs}	Read-only
/admin/config/update	POST	Change app settings	{key, value}	{success}	For developers only



---

🔒 Security

All endpoints are HTTPS-only.

Token-based authentication (JWT).

Role-based access control (user/admin).

Logs saved in api_requests sheet for transparency.
