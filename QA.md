What are your risk areas? Identify and describe them.

A risk area is that data is constantly coming into the database as time goes on, there are new views to the web page/more purchases are made. So we want to ensure that the data is updated in regular intervals, that these intervals are set. We also want to know that there are no issues with the incoming data. 

We want to ensure that the data we have coming in is as accurate as possible as business decisions are made from this data. We don't want to be making business decisions with innaccurate data as it could cost the company money




A Process:
Describe your QA process and include the SQL queries used to execute it.

Implement a upload date column of data, so that it is known when the new data is added to the database. With this information we can confirm data accuracy by performing different queries to make sure the data is as we are expecting. Some examples of what we could be looking for in the queries are counts and averages to compare against the data we already have. If these are not what we're expeccting it would be a good indication to look more deeply into the data.  



Data Assertion: We can perform queries that look for problems in data set, such as missing values in columns that should not have any. Example: in our sales_report table all sales should have sku's and we could perform the below query to ensure they did:

```SQL
--exmaple data assertion query - determining whether there are any missing values 

SELECT productsku 
FROM sales_report
WHERE productsku IS NULL
```

Data Validation: We can perform this to ensure that data is as it is expected to be. That there are no duplicate values and that it is consistent with the data type we expect (example dates, or number of decimals)

```sql
--Data Validation - determining if there are any duplicate values  
SELECT productsku 
	  ,count(productsku) AS productSkuCount
FROM sales_report 
GROUP BY productsku
HAVING count(productsku) >1;
```
