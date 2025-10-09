# transactions schema

Column	Type	Description	Example

id	String	Unique transaction ID	t_1
account_id	String	Linked account	a_1
user_id	String	Owner	u_1
date	Date	Transaction date	2025-09-01
description	String	Transaction description	Monthly service fee
amount	Float	Debit or credit amount	-1200
currency	String	Transaction currency	NGN
type	Enum	credit or debit	debit
merchant	String	Vendor or source	FirstBank
category	String	Type of transaction	bank_fee, income
fee_flag	Boolean	Fee detected	TRUE
flagged_for_reclaim	Boolean	Eligible for refund	TRUE
reclaim_amount_estimate	Float	Estimated refund	1200
status	Enum	processing / approved / failed	processing
raw_notes	String	Extra description	monthly maintenance fee
transaction_hash	String	Unique checksum	txn_hash_001
reference_id	String	API reference	req_ref_001
source_bank	String	Original provider	ZenithBank
device_id	String	Source device	dev_001
created_at	Date	Record created	2025-09-31
updated_at	Date	Record updated	2025-10-05


