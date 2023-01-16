Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:
```SQL
--country query
WITH T1 AS (
SELECT country
	   ,SUM(totaltransactionrevenue) as sumTransaction
FROM all_sessions 
	WHERE country NOT LIKE '%not%'
GROUP BY country
ORDER BY country
   )

SELECT country
	  ,sumtransaction
FROM T1 
	WHERE sumtransaction IS NOT NULL 
GROUP BY country, sumtransaction 
ORDER BY country

WITH T1 AS (
SELECT city
	   ,SUM(totaltransactionrevenue) as sumTransaction
FROM all_sessions 
	WHERE city NOT LIKE '%not%'
GROUP BY city
ORDER BY city
   )

--city query
SELECT city
	  ,sumtransaction
FROM T1 
	WHERE sumtransaction IS NOT NULL 
GROUP BY city, sumtransaction 
ORDER BY sumtransaction DESC
```

Answer:
The country with the highest transaction revenue is USA with $13123.00 of revenue. The city with the highest transaction revenue is San Fransisco with $1561.00 of revenue. 



**Question 2: What is the average number of products ordered from visitors in each city and country?**

```SQL
--country query
WITH T1 AS (
SELECT  country
	   ,COUNT(productquantity) AS productCount
FROM all_sessions
	WHERE country NOT LIKE '%not%'
	GROUP BY country, productsku
	ORDER BY country
),

T2 AS  (
SELECT country
      ,productcount
FROM T1
	WHERE productcount  != 0
GROUP BY country, productcount
ORDER BY country
  )
  
SELECT country
	  ,ROUND(AVG(productcount), 2) AS avProductsOrdered 
FROM T2
GROUP BY country 
ORDER BY avProductsOrdered DESC

--city query
WITH T1 AS (
SELECT   city
		,productsku
	   ,COUNT(productQuantity) AS productCount
FROM all_sessions
	WHERE city NOT LIKE '%not%'
	GROUP BY city, productsku
	ORDER BY city
	),

T2 AS  (
SELECT city
      ,productcount
FROM T1
	WHERE productcount  != 0
GROUP BY city, productcount
ORDER BY city
  )
  
SELECT city
	  ,ROUND(AVG(productcount), 2) AS avProductsOrdered 
FROM T2
GROUP BY city 
ORDER BY avProductsOrdered DESC
```

Answer:
The average number of products ordered are 1 for Canada, Colombia, Finland,France, Argentina, Ireland, Mexico, Spain,India. The US is an average of 3 products ordered. 

The average number of products ordered for Mountain View and New York was 1.5. Everyother city had an average of 1.





**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**

```SQL
SQL Queries:
--city query
WITH T1 AS  (
SELECT city
      ,v2productcategory
      ,productquantity
FROM all_sessions 
	WHERE productquantity != 0
GROUP BY city, v2productcategory, productquantity
ORDER BY city
	  )

SELECT city
	  ,v2productcategory
FROM T1
	 WHERE NOT (city LIKE  '%not%'
	 OR v2productcategory LIKE '%not%')
GROUP BY city, v2productcategory
ORDER BY city, v2productcategory;	

--country query
WITH T1 AS  (
SELECT country
      ,v2productcategory
      ,productquantity
FROM all_sessions 
	WHERE productquantity != 0
GROUP BY country, v2productcategory, productquantity
ORDER BY country
	  )

SELECT country
	  ,v2productcategory
FROM T1
	 WHERE NOT (country LIKE  '%not%'
	 OR v2productcategory LIKE '%not%')
GROUP BY country, v2productcategory
ORDER BY country, v2productcategory;	
```

Answer:
There does not appear to be an obvious pattern of product types ordered from visitors in each country. There does seem to be a pattern with products ordered by city. Those cities within the Silicon Valley are ordering Home/Nest - examples: San Francisco, Palo Alto and San Jose.



**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**

```SQL
SQL Queries:
--country query
WITH T1 AS (
SELECT  country
	   ,v2productname
	   ,productsku
	   ,SUM(productquantity) AS productCount
FROM all_sessions
	WHERE country NOT LIKE '%not%'
	GROUP BY country, v2productname, productsku
	ORDER BY country
),

T2 AS (
SELECT country
	  ,v2productname
	  ,productsku
	  ,productcount
FROM T1 
	WHERE productcount != 0 
	)

SELECT country
	  ,v2productname
      ,MAX(productCount) AS maxProductCount
FROM T2
GROUP BY country, v2productname
ORDER BY country


--city query 
WITH T1 AS (
SELECT  city
	   ,v2productname
	   ,productsku
	   ,SUM(productquantity) AS productCount
FROM all_sessions
	WHERE city NOT LIKE '%not%'
	GROUP BY city, v2productname, productsku
	ORDER BY city
),

T2 AS (
SELECT city
	  ,v2productname
	  ,productsku
	  ,productcount
FROM T1 
	WHERE productcount != 0 
	)

SELECT city
	  ,v2productname
      ,MAX(productCount) AS maxProductCount
FROM T2
GROUP BY city, v2productname
ORDER BY city, maxProductCount DESC
```

Answer:
The top selling product in Spain is the Waze Dress socks and in the United States is the Leatherette Journal. For all other countries the quantity of the top selling product is 1. 

The top selling products in cities are (only given when the top selling product quantity is >1): 

	Atlanta        Reusable Shopping Bag

	Houston	        Google Sunglasses

	Madrid	        Waze Dress Socks

	Mountain View	Nest® Learning Thermostat 3rd Gen-USA - Stainless Steel

	New York	    Google Mens 100% Cotton Short Sleeve Hero Tee White and 
		            YouTube Mens Short Sleeve Hero Tee White

	Salem Red       Spiral Google Notebook



**Question 5: Can we summarize the impact of revenue generated from each city/country?**

```SQL
SQL Queries:
--country query
WITH T1 AS (
SELECT al.visitid
      ,country
	  ,revenue
FROM all_sessions al
LEFT JOIN analytics an
ON al.visitid = an.visitid
	WHERE revenue IS NOT NULL 
GROUP BY al. visitid, country, revenue
ORDER BY country
	)

SELECT country
       ,SUM(revenue) AS totalRevenue
FROM T1
GROUP BY country


--city query
WITH T1 AS (
SELECT al.visitid
      ,city
	  ,country
	  ,revenue
FROM all_sessions al 
LEFT JOIN analytics an
ON al.visitid = an.visitid
	WHERE revenue IS NOT NULL 
GROUP BY al. visitid, city, country, revenue
ORDER BY city
	)

SELECT city
	  ,country
      ,SUM(revenue) AS totalRevenue
FROM T1
WHERE city NOT LIKE '%not%'
GROUP BY city, country 
ORDER BY city
```

Answer:
What we can learn from total revenue generated is that  only 3 countries generated tangible revenue. Israel	$32, , Switzerland	$16 and United States	$4629. 

America's revenue is determined through the revenue of several cities, whereas there revenue in Tel Aviv-Yafo and Zurich are the only cities generating money for their country. 






