What issues will you address by cleaning the data?





Queries:
Table: all_sessions
```SQL
ALTER TABLE all_sessions
	DROP COLUMN totaltransactionrevenue, 
	DROP COLUMN transactions,
	DROP COLUMN	sessionqualitydim,
	DROP COLUMN	productrefundamount,
	DROP COLUMN productquantity,
	DROP COLUMN productrevenue,
	DROP COLUMN itemquantity,
	DROP COLUMN itemrevenue,
	DROP COLUMN	transactionrevenue,
	DROP COLUMN	transactionid,
	DROP COLUMN	searchkeyword,
	DROP COLUMN	ecommerceaction_option;
