Question 1: 
How many fullvisitorid are duplicates?
SQL Queries:
```SQL
SELECT DISTINCT fullvisitorid FROM all_Sessions_clean
```
Answer: 
The query reduces the total 15'134 rows down to 14'223 rows, meaning there were 911 duplicates present in fullvisitorid.

Question 2: 
How do the duplicates in visitid compare to the duplicates in fullvisitorid?
SQL Queries:
```SQL
SELECT DISTINCT visitid FROM all_Sessions_clean
```
Answer:
The query returned 14'556 rows, meaning there are 578 duplicates, which is 333 less than full visitor id. This indicates that visitid may be a more unique column to choose if we were looking for an identifier.


Question 3: 
What year saw the most purchases?
SQL Queries:
SELECT 
```SQL
	CAST(LEFT(date, 4) AS SMALLINT) AS year,
	count(transactions)
FROM all_Sessions_clean
WHERE transactions is not null
GROUP BY year
```
Answer:
2017 saw 56 transaction (thus far) compared to 25 in 2016.

Question 4: 
Which year saw the most revenue? How does this compare to transactions?
SQL Queries:
```SQL
SELECT 
	CAST(LEFT(date, 4) AS SMALLINT) AS year,
	SUM(totaltransactionrevenue)
FROM all_Sessions_clean
WHERE transactions is not null
GROUP BY year
```
Answer:
2017 saw more revenue, $9849.64 compared to $4431.67 in 2016. In reference to total transactions 2017 averaged $175.89 per transaction, which is actually slightly lower than 2016 at $177.27.


Question 5: 
Are the duplicate visitid values duplicate across rows?
SQL Queries:
### To Identify duplicates and their degree:
```SQL
WITH duplicates AS (
	SELECT *,
		ROW_NUMBER() OVER(
			PARTITION BY visitid
		) AS duplicate
	FROM all_sessions_clean
)
SELECT visitid, duplicate
FROM duplicates
WHERE duplicate > 1
ORDER BY duplicate DESC
```
### And modifying to explore rows with duplicate ids:
```SQL
SELECT *
FROM all_sessions_clean
WHERE visitid IN (
	WITH duplicates AS (
	SELECT *,
		ROW_NUMBER() OVER(
			PARTITION BY visitid
		) AS duplicate
	FROM all_sessions_clean
	)
	SELECT visitid
	FROM duplicates
	WHERE duplicate > 1
	ORDER BY
		duplicate DESC)
```
### Exploring a specific fourth degree duplicate
```SQL
SELECT * FROM all_sessions_clean
WHERE visitid = '1474392675'
```
Answer:
After exploring the data across rows of what appear to be duplicate visitid values, observation in the productprice, productsku, and v2productname columns can be used to detemrine an assumption. This assumption is that the rows are not supposed to be logs of individual visits, but rather each interaction with a product. 

If an analyst wanted to accept this assumption, it would open the gateway to answering questions regarding the webpage engagement.
