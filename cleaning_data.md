What issues will you address by cleaning the data?
- Copy the tables to '_clean' tables to avoid unintentional data loss and clearly indicate cleaned data
- all_sessions
  - Change null values in 'productquantity' to '0'
  - Change default values ('(not set)', 'not available demo dataset') in 'country' and 'city' columns to null
  - Drop irrelevant empty columns (itemquantity, itemrevenue, searchkeyword)
  - Format monetary values (divide by 1\`000\`000)

Note: Hotkey cmd+option+f opens find and replace, which is the best way to quickly reuse generic queries (like the cleaning ones below)

Queries:
Below, provide the SQL queries you used to clean your data.
### Copying data to '_clean' tables
```
CREATE TABLE table_clean AS
TABLE table
```
### Set null values to 0
```
UPDATE table_clean
SET column = 0
WHERE column IS null
```
### Set default values to null
```
UPDATE table_clean
SET column = null
WHERE column = 'default value'
```
### Check for values in a column
```
SELECT column 
FROM table
WHERE column
	IS NOT null
```
### Drop a column
```
ALTER TABLE table_clean
DROP COLUMN column
```
### Format monetary values 
```
UPDATE all_sessions_clean
SET column = column/1000000
```