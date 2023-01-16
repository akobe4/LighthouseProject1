Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:



Answer:




**Question 2: What is the average number of products ordered from visitors in each city and country?**

```sql
SQL Queries:
WITH T1 AS (
SELECT  country
	   ,productsku
	   ,count(productsku) AS productCount
FROM all_sessions
	WHERE country NOT LIKE '%not%'
	GROUP BY country, v2productname, productsku
	ORDER BY country
)

SELECT country
	   ,ROUND(AVG(productcount), 2) AS avProductCount 
FROM T1
GROUP BY country
ORDER BY country


WITH T1 AS (
SELECT  city
	   ,productsku
	   ,count(productsku) AS productCount
FROM all_sessions
	WHERE city NOT LIKE '%not%'
	GROUP BY city, v2productname, productsku
	ORDER BY city
)

SELECT city
	   ,ROUND(AVG(productcount), 2) AS avProductsOrdered 
FROM T1
GROUP BY city
ORDER BY city


Answer:
results of first 20 shown below
        Country
country	        avProductsOrdered 
Albania	                1.00
Algeria	                1.00
Argentina	            1.16
Armenia	                1.00
Australia	            1.74
Austria	                1.11    
Bahamas	                1.00
Bahrain	                1.00
Bangladesh	            1.14
Barbados	            1.00
Belarus	                1.00
Belgium	                1.26
Belize	                1.00
Bolivia	                1.00
Bosnia & Herzegovina	1.00
Botswana	            1.00
Brazil	                1.52
Brunei	                1.00
Bulgaria	            1.00
Cambodia	            1.00

    City
city	avproductsOrdered
Adelaide	1.00
Ahmedabad	1.00
Akron	    1.00
Alexandria	1.00
Amã	        1.00
Amsterdam	1.00
Ann Arbor	1.06
Antalya	    1.00
Antwerp	    1.00
Appleton	1.00
Ashburn	    1.00
Asuncion	1.00
Athens	    1.00
Atlanta	    1.27
Auckland	1.00
Austin	    1.27
Avon	    1.00
Bandung	    1.00
Bangkok	    1.03







**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:
```SQL
SELECT city
	  ,v2productcategory
	 FROM all_sessions a
	 WHERE NOT (city LIKE  '%not%'
	 OR v2productcategory LIKE '%not%')
GROUP BY city, v2productcategory
ORDER BY city, v2productcategory;	

SELECT country
	  ,v2productcategory
	 FROM all_sessions 
	 WHERE NOT (country LIKE  '%not%' 
	 OR v2productcategory LIKE '%not%')
GROUP BY country, v2productcategory
ORDER BY country, v2productcategory;




Answer:
There doesn't appear to be an obvious pattern of product types ordered from visitors in each country. There is some pattern of product types ordered by city. Some cities have more home type products ordered such as accessories and electronics, while other cities seem to have more apparal orders. 




**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:
```SQL
WITH T1 AS (
SELECT  country
	   ,v2productname
	   ,count(v2productname) AS productCount
FROM all_sessions
	WHERE country NOT LIKE '%not%'
	GROUP BY country, v2productname
	ORDER BY country
)

SELECT country
	   ,MAX(productCount) AS maxProductCount
FROM T1
GROUP BY country
ORDER BY country

```sql 
WITH T1 AS (
SELECT  city
	   ,v2productname
	   ,productsku
	   ,count(v2productname) AS productCount
FROM all_sessions
	WHERE city NOT LIKE '%not%'
	GROUP BY city, v2productname, productsku
	ORDER BY city
)

SELECT city
	   ,MAX(productCount) AS maxProductCount
FROM T1
GROUP BY city
ORDER BY city

Answer:





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:



Answer:







