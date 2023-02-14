What are your risk areas? Identify and describe them.
1. It is a risk to assume *visitid* or fullvisitid is meant to be a **unique** identifier
2. It is a risk to assume the correct implementation of a query without using an alternative method/ source/ value to validate your results
3. It is a risk to use data without a dictionary that describes it

QA Process:
Describe your QA process and include the SQL queries used to execute it.

To address the first risk, questions were asked and used to explore what appeared to be intended as unique identifiers (These can be found in [Part 3: Starting with Data](starting_with_data.md)). It found that fullvisitorid was counterintuitively a worse identifier than visitid, and that visitid is an identifier, but not meant to be a unique one.

The second risk was addressed by testing queries on values with known output before attempting to use them for an unknown output. 
For example, when running a query to determine if a column is void of values:
```SQL
SELECT column 
FROM table
WHERE column
	IS NOT null
```
the query should first be run on a column known to have non-null values to check its validity, before being run on a column that may or may not have any non-null values.

The third risk is unavoidable if no dictionary is provided, meaning the best way to move forward is by making evidence based assumption. Question 5 in [Part 3: Starting with Data](starting_with_data.md) is an example of this, using the data from four different columns to make an assumption on what each row of the table is logging. 
