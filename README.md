<h1><a name="return-to-toc"><div style="color:darkorange;">SQL NOTES</div></a></h1>

- sql statements are not case sensitive
- so they are same as `select` and `SELECT`
- Table of contents

	|KEYWORD                                 |USE                                                       |
	|----------------------------------------|----------------------------------------------------------|
	|**[SELECT](#select)**                   | to select / display data                                 |
	|**[WHERE](#where)**                     | for conditions                                           |
	|**[ORDER](#order)**                     | to order data ASC or DESC                                |
	|**[INSERT INTO](#insert-into)**         | to insert data                                           |
	|**[NULL](#null)**                       | to reference a `null` field                              |
	|**[UPDATE](#update)**                   | to update a data                                         |
	|**[DELETE](#delete)**                   | to delete data                                           |
	|**[LIMIT](#limit)**                     | to limit the output in `select`                          |
	|**[MIN - MAX](#min-max)**               | aggregate function to for minimum or maximum of a colunmn|
	|**[COUNT - AVG - SUM](#count-avg-sum)** | aggregate function for count, average or sum of a column |
	|**[LIKE](#like)**                       | for pattern finding                                      |
	|**[IN](#in)**                           | for multiple values condition in `where`                 |
	|**[BETWEEN](#between)**                 | to refer range of data                                   |
	|**[Aliases](#aliases)**                 | alias for variables / column names                       |

```sql
show databases;
```
```sql
use database_name;
```
```sql
show tables;
```
Some common commands in MYSQL : -
- `SELECT` - extracts data from a database
- `UPDATE` - updates data in a database
- `DELETE` - deletes data from a database
- `INSERT INTO` - inserts new data into a database
- `CREATE DATABASE` - creates a new database
- `ALTER DATABASE` - modifies a database
- `CREATE TABLE` - creates a new table
- `ALTER TABLE` - modifies a table
- `DROP TABLE` - deletes a table
- `CREATE INDEX` - creates an index (search key)

- `DROP INDEX` - deletes an index

<hr style="border-width : 3px; background-color : magenta"></hr>

<h1><a name="select"><div style="color:green;">SELECT</div></a></h1>

```sql
select * from table_name;
```
- selects everything from table to display
```sql
select column_name_1, column_name_2, ... from table_name;   
```
- displays specified columns from table

**[RETURN TO TOC](#return-to-toc)**


<hr style="border-width : 3px; background-color : magenta"></hr>

<h1><a name="where"><div style="color:green;">WHERE</div></a></h1>

```sql
select * 
from table_name
where condition_1;
```
- `=` - Equal	
- `>` - Greater than	
- `<` - Less than	
- `>=` - Greater than or equal	
- `<=` - Less than or equal	
- `<>` - Not equal. Note: In some versions of SQL this operator may be written as `!=`	
- `BETWEEN` - Between a certain range	
- `LIKE`- Search for a pattern	
- `IN` - To specify multiple possible values for a column

- `and`, `or`, `not` used for multiple conditons

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition1 AND condition2 AND condition3 ...;
```
```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition1 OR condition2 OR condition3 ...;
```
```sql
SELECT column1, column2, ...
FROM table_name
WHERE NOT condition1;
```
**[RETURN TO TOC](#return-to-toc)**

<hr style="border-width : 3px; background-color : magenta"></hr>
<h1><a name="order"><div style="color:green;">ORDER</div></a></h1>

```sql
SELECT column1, column2, ...
FROM table_name
ORDER BY column1, column2, ... ASC|DESC;
```
Examples
```sql
SELECT * FROM Customers
ORDER BY Country DESC;
```
```sql
SELECT * FROM Customers
ORDER BY Country, CustomerName;
```
```sql
SELECT * FROM Customers
ORDER BY Country ASC, CustomerName DESC;
```
**[RETURN TO TOC](#return-to-toc)**

<hr style="border-width : 3px; background-color : magenta"></hr>

<h1><a name="insert-into"><div style="color:green;">INSERT INTO</div></a></h1>
	
```sql
insert into table_name (column_name_1, column_name_2,...) values
(value_1, value_2,...),
(value_1, value_2,...),
... ;
```
- for specific columns
```sql
insert into table_name values
(value1, value_2, ...);
```
- use above if want to insert into every column
- beware that every value should be in order
**[RETURN TO TOC](#return-to-toc)**

<hr style="border-width : 3px; background-color : magenta"></hr>

<h1><a name="null"><div style="color:green;">NULL</div></a></h1>

- if a field is `null` it's not possible to use `<`, `>`, `=` in conditions
- use `is null` or `not null`
```sql
SELECT column_names
FROM table_name
WHERE column_name IS NULL;
```
```sql
SELECT column_names
FROM table_name
WHERE column_name IS NOT NULL;
```
**[RETURN TO TOC](#return-to-toc)**

<hr style="border-width : 3px; background-color : magenta"></hr>

<h1><a name="update"><div style="color:green;">UPDATE</div></a></h1>

- `update` used when any value is to be modified in table
```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```
<h3 style="background-color: red; color: black; width:600px"> If where statement doesn't exists then every row will be updated</h3>
**[RETURN TO TOC](#return-to-toc)**

<hr style="border-width : 3px; background-color : magenta"></hr>

<h1><a name="delete"><div style="color:green;">DELETE</div></a></h1>

```sql
DELETE FROM table_name WHERE condition;
```
<h3 style="background-color: red; color: black; ">If where condition is omitted every record in table gets deleted without deleting the table</h3>

```sql
delete from table_name;
```
**[RETURN TO TOC](#return-to-toc)**

<hr style="border-width : 3px; background-color : magenta"></hr>

<h1><a name="limit"><div style="color:green;">LIMIT</div></a></h1>

- The LIMIT clause is used to specify the number of records to return.
- The LIMIT clause is useful on large tables with thousands of records. Returning a large number of records can impact performance.
```sql
SELECT column_name(s)
FROM table_name
WHERE condition
LIMIT number;
```
- What if we want to select records 4 - 6 (inclusive)?
- MySQL provides a way to handle this: by using OFFSET.
- The SQL query below says "return only 3 records, start on record 4 (OFFSET 3)":
```sql
SELECT * FROM Customers
LIMIT 3 OFFSET 3;
```
**[RETURN TO TOC](#return-to-toc)**

<hr style="border-width : 3px; background-color : magenta"></hr>

<h1><a name="min-max"><div style="color:green;">MIN MAX</div></a></h1>

- The `MIN()` function returns the smallest value of the selected column.
- The `MAX()` function returns the largest value of the selected column.
```sql
SELECT MIN(column_name) AS another_name
FROM table_name
WHERE condition;
```
```sql
SELECT MAX(column_name) AS another_name
FROM table_name
WHERE condition;
```
**[RETURN TO TOC](#return-to-toc)**

<hr style="border-width : 3px; background-color : magenta"></hr>

<h1><a name="count-avg-sum"><div style="color:green;">COUNT AVG SUM</div></a></h1>

- The `COUNT()` function returns the number of rows that matches a specified criterion.
```sql
SELECT COUNT(column_name)
FROM table_name
WHERE condition;
```
- The `AVG()` function returns the average value of a numeric column. 
```sql
SELECT AVG(column_name)
FROM table_name
WHERE condition;
```
- The `SUM()` function returns the total sum of a numeric column. 
```sql
SELECT SUM(column_name)
FROM table_name
WHERE condition;
```
**[RETURN TO TOC](#return-to-toc)**

<hr style="border-width : 3px; background-color : magenta"></hr>

<h1><a name="like"><div style="color:green;">LIKE</div></a></h1>

- The LIKE operator is used in a WHERE clause to search for a specified pattern in a column.
- There are two wildcards often used in conjunction with the LIKE operator:
- The percent sign ( `%` ) represents zero, one, or multiple no. characters
- The underscore sign ( `_` ) represents one, single character

```sql
SELECT column1, column2, ...
FROM table_name
WHERE columnN LIKE pattern;
```
<h3 style="background-color: green; color: black; ">and , or operators can also be used for multiple conditions</h3>


| **Condition**                                      | **Description**                                                  |
|----------------------------------------------------|------------------------------------------------------------------|
| WHERE CustomerName LIKE `'a%'`                     | Finds any values that start with "a".                            |
| WHERE CustomerName LIKE `'%a'`                     | Finds any values that end with "a".                              |
| WHERE CustomerName LIKE `'%or%'`                   | Finds any values that have "or" in any position.                 |
| WHERE CustomerName LIKE `'_r%'`                    | Finds any values that have "r" in the second position.           |
| WHERE CustomerName LIKE `'a_%'`                    | Finds any values that start with "a" and are at least 2 characters in length. |
| WHERE CustomerName LIKE `'a__%'`                   | Finds any values that start with "a" and are at least 3 characters in length. |
| WHERE ContactName LIKE `'a%o'`                     | Finds any values that start with "a" and end with "o".           |

- demo example where customer name with start with `a` and atleast of length `3` and more 
```sql
SELECT * FROM Customers
WHERE CustomerName LIKE 'a__%';
```
**[RETURN TO TOC](#return-to-toc)**

<hr style="border-width : 3px; background-color : magenta"></hr>

<h1><a name="in"><div style="color:green;">IN</div></a></h1>

- The IN operator allows you to specify multiple values in a WHERE clause.
- The IN operator is a shorthand for multiple OR conditions.
```sql
SELECT column_name(s)
FROM table_name
WHERE column_name IN (value1, value2, ...);
```
```sql
SELECT column_name(s)
FROM table_name
WHERE column_name IN (SELECT STATEMENT);
```
**[RETURN TO TOC](#return-to-toc)**

<hr style="border-width : 3px; background-color : magenta"></hr>

<h1><a name="between"><div style="color:green;">BETWEEN</div></a></h1>

- The BETWEEN operator selects values within a given range. The values can be numbers, text, or dates.
- The BETWEEN operator is inclusive: begin and end values are included.
```sql
SELECT column_name(s)
FROM table_name
WHERE column_name BETWEEN value1 AND value2;
```	
- `ORDER BY` , `AND`, `OR` , `IN` , `NOT` can be used with it
**[RETURN TO TOC](#return-to-toc)**

<hr style="border-width : 3px; background-color : magenta"></hr>

<h1><a name="aliases"><div style="color:green;">Aliases</div></a></h1>

- Aliases are used to give a table, or a column in a table, a temporary name.
- Aliases are often used to make column names more readable.
- An alias only exists for the duration of that query.
- An alias is created with the `AS` keyword.
```sql
SELECT column_name AS alias_name         //column syntax
FROM table_name;
```
```sql
SELECT column_name(s)                    //table syntax
FROM table_name AS alias_name;
```
**[RETURN TO TOC](#return-to-toc)**
