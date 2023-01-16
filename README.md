# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals
To gain a better understanding of SQL and to be able to manipulate and query in different ways.  


## Process
- created a query to set-up the table in postgres, then a query to add the data to the file

```sql 
--Examples with table analytics
--creating table 
CREATE TABLE analytics (
	 analyticsId SERIAL
	,visitNumber INT	
	,visitId INT	
	,visitStartTime INT 	
	,visitDate	DATE
	,fullvisitorId	VARCHAR(50)
	,userid	INT
	,channelGrouping VARCHAR(20)	
	,socialEngagementType	VARCHAR(50)
	,units_sold	INT
	,pageviews	INT
	,timeonsite	INT
	,bounces	INT
	,revenue	INT8
	,unit_price INT
	,PRIMARY KEY(analyticsId)  
)

--adding data 
COPY analytics(visitNumber,	visitId,	visitStartTime,	visitDate,	fullvisitorId,	userid,	channelGrouping,	socialEngagementType,	units_sold,	pageviews,	timeonsite,	bounces,	revenue,	unit_price)
FROM 'C:\Users\akobe\OneDrive\Desktop\Lighthouse\Project1\analytics.csv'
DELIMITER ','
CSV HEADER;
```

- cleaned the data, removing data not relevant for project and divided prices by 1,000,000
- created queries to answer questions about the data


## Results
Through the questions asked in the assignment I learned, which makes logical sense, that those living in the Silicon Valley purchase Nest products more frequently. The site is also making the most revenue off people living in this area - San Fransisco had the highest transaction revenue for cities. 

Through my own queries, I found that customers who buy products spend less time on the site than those who do not buy anything. Time spent on site is doubled when a purchase is not made - 13 min vs 6 min. 

Three different Nest products fell within the top 10 items purchased, the most purchased item was the Grip Highlighter Pen 3 Pack at 50 units. 

The months that generated the most revnue were in 2017, with July generating the most revenue $1348, closely followed by June $1343. 

## Challenges 
I did not completely understanding the data set when I first started to clean and query data. This casued me needing to re-upload the data multiple times as data important to the questions asked has been deleted. As a consequence of not really understanding the dataset properly it took me a long time to get my head around what data was appropriate to answer the assignment questions. 

I had lots of hiccups and troubleshooting while uploading the data into postres. It came with a lot of trial and error and trying to better understand the SQL datatypes. For example I kept getting an error while using INT for revenue in the analytics table, I finally realized that in order for me to import it as a number I needed to use INT8. 


## Future Goals
With more time I would understand the data set better. I would also do a more thorough data cleaning process as data cleaning was minimal. I did realize part way through that I should have done more, however I did not have the time to go back to it. Examples of what I would do in the future are  look for outliers, ensure all data types chosen for importing the data were correct once the data went it. 

A better overall understanding of the data going in would produce better data coming out. 

With more time/in the future I would have a specific goal in mind for the data and ask questions that fit the overall goal. In this assignment I just thought of random questions that I felt like could show different aspects of my SQL knowledge. 




