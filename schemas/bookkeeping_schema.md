schemas/bookkeeping_schema.md

Purpose

Handles expense tracking, income logs, receipt uploads, and category tagging for small businesses or freelancers.
Acts as Riclivo’s “micro-accounting” system — connected to the tax and reclaim modules.


---

Table: bookkeeping

Column	Type	Description	Example

id	String	Unique bookkeeping record ID	bk_1
user_id	String	Linked user	u_1
date	Date	Transaction or entry date	2025-09-01
entry_type	Enum	income, expense, liability, asset	expense
category	String	Category of entry	Office Supplies
description	String	Details of the expense/income	Printer paper and ink
amount	Float	Value	8000
currency	String	Currency	NGN
receipt_url	String	Uploaded proof of purchase	https://drive.google.com/.../receipt123.jpg
reference_id	String	Optional link to a bank transaction	txn_hash_001
tax_deductible	Boolean	Is it tax deductible?	TRUE
created_at	Date	Date record created	2025-09-02
updated_at	Date	Date updated	2025-09-05



---

Relationships

1 → Many (Users)

Many → 1 (Transactions)

Many → 1 (Tax Reports)



---

📗 schemas/tax_reports_schema.md

Purpose

Generates automatic or manual tax summaries based on bookkeeping + transaction data, localized per country tax laws.


---

Table: tax_reports

Column	Type	Description	Example

id	String	Unique tax report ID	txr_1
user_id	String	Owner	u_1
report_period_start	Date	Start date	2025-01-01
report_period_end	Date	End date	2025-12-31
total_income	Float	Calculated income	4500000
total_expenses	Float	Total deductible expenses	900000
taxable_amount	Float	Income - deductible	3600000
tax_due	Float	Computed tax	360000
tax_law_reference	String	Pulled from localization	Finance Act 2020
submission_status	Enum	draft, submitted, approved	draft
submission_date	Date	Date filed	2025-02-01
authority_submitted_to	String	e.g., FIRS, HMRC	FIRS
proof_url	String	Uploaded tax certificate	https://drive.google.com/.../proof123.pdf
created_at	Date	Created	2025-02-01



---

Relationships

Many → 1 (Users)

Aggregates data from Bookkeeping & Transactions.



---

📙 schemas/reclaims_schema.md

Purpose

Handles refund/reversal processing, from detection → verification → API submission to banks.


---

Table: reclaims

Column	Type	Description	Example

id	String	Unique reclaim ID	r_1
user_id	String	Owner	u_1
transaction_id	String	Related transaction	t_1
bank_provider	String	Which API provider handled it	Nordigen
account_id	String	Linked bank	a_1
reclaim_reason	String	Why it’s being reclaimed	wrong bank fee
reclaim_amount	Float	Amount user expects	1200
commission_pct	Float	% based on tier	20
commission_amount	Float	Computed deduction	240
status	Enum	pending, sent_to_bank, approved, paid, failed	sent_to_bank
bank_response	String	Summary of feedback	Refund approved
legal_clause_ref	String	Pulled from localization sheet	Section 24 – Consumer Banking Act
proof_of_submission_url	String	File link for verification	https://drive.google.com/.../reclaim_form.pdf
created_at	Date	Created	2025-10-02
updated_at	Date	Updated	2025-10-05



---

Relationships

1 → 1 (Transaction)

1 → 1 (User)

Uses localization → for legal law & reclaim note attachment.

Triggered via APIRequests sheet (Nordigen/Flutterwave).



---

📒 schemas/ai_chat_schema.md

Purpose

Stores prompts, responses, and context of Riclivo AI Assistant for bookkeeping, reclaim advice, and coaching.


---

Table: ai_chat

Column	Type	Description	Example

id	String	Unique chat ID	c_1
user_id	String	Linked user	u_1
prompt	String	What user asked	"How do I record VAT?"
role	String	Who sent it (user or assistant)	user
response	String	AI reply	"Record VAT under expense → tax category."
model_used	String	Which AI model	gpt-4-mini
related_context	String	e.g., bookkeeping, reclaim, tax	bookkeeping
timestamp	Date	Message date	2025-10-02



---

Relationships

1 → Many (Users)

Optionally links to Bookkeeping or Reclaim context.
