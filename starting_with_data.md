Question 1: Determine the average amount of time spent on site for those who made purchases and those who did not. 

SQL Queries:
```sql
--average amount  of time spent on site for transactions with a purchase vs withour a purchase 
WITH T1 AS (
SELECT timeonsite 
,CASE
	   	WHEN productquantity IS NULL THEN 'noPurchase'
		ELSE 'purchaseMade'
END AS ifPurchase
FROM all_sessions 
	),

--remove null values from time 
T2 AS (
SELECT ifpurchase
	   ,timeonsite
FROM T1
WHERE timeonsite IS NOT NULL
GROUP BY ifpurchase, timeonsite
	)

SELECT ifpurchase
      ,AVG(timeonsite) AS avgTimeOnSite
FROM T2
GROUP BY ifpurchase

```

Answer: 
Those who made a purchase spent an average of 6 minutes and 37 seconds, while those who did not make a purchase spent more than double that on the site - 13 minutess and 26 seconds. 


Question 2: 

SQL Queries:

Answer:



Question 3: 

SQL Queries:

Answer:



Question 4: 

SQL Queries:

Answer:



Question 5: 

SQL Queries:

Answer:
