What issues will you address by cleaning the data?
In cleaning the data, columns were removed when they had no data/not enough data to provide meaningful results. 

Unit_price in the "analytics" table was divided by 1,000,000 and set to a number with two decimal points as standard for money. 




Queries:
```SQL
--cleaning all_sessions table 
ALTER TABLE all_sessions
	DROP COLUMN	sessionqualitydim,
	DROP COLUMN	productrefundamount,
	DROP COLUMN	searchkeyword,
	DROP COLUMN	ecommerceaction_option;
	
UPDATE all_sessions SET totaltransactionrevenue = totaltransactionrevenue/1000000

ALTER TABLE all_sessions
	ALTER COLUMN totaltransactionrevenue SET DATA TYPE DECIMAL(6,2);

 
--cleaning analytics table 
UPDATE analytics SET unit_price = unit_price/1000000

ALTER TABLE analytics
	ALTER COLUMN unit_price SET DATA TYPE DECIMAL(5,2);

UPDATE analytics SET revenue = revenue/1000000

```
