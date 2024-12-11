# SQLite_tutorials

## GROUP BY
#### The SQL GROUP BY clause is used in conjuction with the SELECT statement to arrange identical data into groups specifying FROM which table data to group.
#### The GROUP BY clause is typically used with aggregate functions such as SUM(), COUNT(), AVG(), MAX() or MIN().
>Basic syntax
```
SELECT column_name(s)
FROM table_name
GROUP BY column_name(s)
```

>For example, if you have a table named SALES_DATA containing the sales data with the columns YEAR, PRODUCT and SALES. To calculate the total sales in a year, the GROUP BY clause can be used to group the records in this table based on the year and calculate the sum of sales in each group using the SUM() function.

>Basic syntax
```
SELECT YEAR, SUM(SALES) AS TOTAL_SALES
FROM SALES_DATA
GROUP BY YEAR;
```

## DISTINCT
#### DISTINCT keyword is used in conjuction with the SELECT statement to fetch unique records from a table.
#### These used when there is a need to avoid duplicate values present in any specific columns/tables. When we use DISTINCT keyword, SELECT statement returns only the unique records available in the table.
>Basic syntax
```
SELECT DISTINCT column1, column2,....columnn
FROM table_name
```

## ORDER BY
#### The ORDER BY clause is used to sort data in either ascending(ASC) or descending(DESC) order, based on one or more columns. This clause can sort data by a single column or by multiple columns. Sorting of multiple columns can be helpful when you need to sort data hierarchically, such as sorting by state, city, and then by person`s name.
>Basic syntax
```
SELECT
   select_list
FROM
   table
ORDER BY
    column_1 ASC,
    column_2 DESC;
```

## WHERE
#### The WHERE clause is an optional clause of the SELECT statement. It appears after the FROM clause as the following statement.
>Basic syntax
```
SELECT
  column_list
FROM
  TABLE
WHERE
  search_condition;
```

## AND Operator
#### In SQLite, the AND operator allows you to combine two conditions in a WHERE clause to filter rows if all conditions are true.
>Basic syntax
```
SELECT
  BillingAddress,BillingCity,Total
FROM
  invoices
WHERE
  BillingCity = 'New York'
  AND Total > 5
ORDER BY
  Total;
```

## OR Operator
#### In SQLite, the OR operator allows you to combine multiple conditions in a WHERE clause to filter rows based on at least one condition being true.
>Basic syntax
```
SELECT
  BillingAddress,BillingCity,Total
FROM
  invoices
WHERE
  BillingCity = 'New York'
  OR BillingCity = 'Chicago'
ORDER BY 
  BillingCity;
```

## LIMIT
#### The LIMIT clause is an optional part of the  SELECT statement. You use the LIMIT clause to constrain the number of rows returned by the query.
#### For example, a SELECT statement may return one million rows. However, if you just need the first 10 rows in the result set, you can add the LIMIT clause to the SELECT statement to retrieve 10 rows
>Basic syntax
```
SELECT
	column_list
FROM
	table
LIMIT row_count;
```

>Syntax for the example
```
SELECT
	trackId,name
FROM
	tracks
LIMIT 10;
```

## BETWEEN Operator
#### The BETWEEN operator is a logical operator that tests whether a value is in range of values. If the value is in the specified range, the BETWEEN operator returns true.
#### The following statement finds invoices whose total is between 14.96 and 18.86:
>Basic syntax
```
SELECT
    InvoiceId,BillingAddress,Total
FROM
    invoices
WHERE
    Total BETWEEN 14.91 and 18.86    
ORDER BY
    Total;
```

## IN Operator 
#### The SQLite IN operator determines whether a value matches any value in a list or a subquery. 
>Basic syntax
```
SELECT
	TrackId,Name,Mediatypeid
FROM
	Tracks
WHERE
	MediaTypeId IN (1, 2)
ORDER BY
	Name ASC;
```

## JOIN
#### In this tutorial, you will learn about various kinds of SQLite joins to query data from two or more tables.
#### To query data from both artists and albums tables, you can use an INNER JOIN, LEFT JOIN, or CROSS JOIN clause. Each join clause determines how SQLite uses data from one table to match with rows in another table.

### INNER JOIN
#### This type of join returns rows when there is a match in both tables. The rows are combined based on the specified condition in the ON clause.
#### Taking into an example the following statement returns the album titles and the corresponding artist names:
>Basic syntax
```
SELECT
  Title,Name
FROM
  albums
INNER JOIN artists ON artists.ArtistId = albums.ArtistId;
```

### LEFT JOIN
#### Similar to the INNER JOIN clause, the LEFT JOIN clause is an optional clause of the SELECT statement. You use the LEFT JOIN clause to query data from multiple related tables.
#### Suppose we have two tables: A and B. In fact A has m and f columns and B has n and f columns.
#### To perform join between A and B using LEFT JOIN clause, you use the following statement:
>Basic syntax
```
SELECT
	a,
	b
FROM
	A
LEFT JOIN B ON A.f = B.f
WHERE search_condition;
```

### RIGHT JOIN
#### In SQLite, the RIGHT JOIN clause allows you to combine rows from two tables based on a related column between them.
#### The RIGHT JOIN clause returns all rows from the right table and matching rows from the left table. For non-matching rows in the left table, it uses NULL values.
>Basic syntax
```
SELECT
  select_list
FROM
  table1
  RIGHT JOIN table2 ON table1.column_name1 = table2.column_name2;
```
>If table1 and table2 have the same column_name, you can use the USING syntax
```
SELECT
  select_list
FROM
  table1
  RIGHT JOIN table2 USING (column_name);
```

### CROSS JOIN
#### A CROSS JOIN produces a Cartesian product of the two tables. This means that each row in the first table is paired with each row in the second table.
#### For example, The number of rows in the result set will be the product of the number of rows in the members table and the number of rows in the dates table.
#### If members has 10 rows and dates has 5 rows, the result will have 10 * 5 = 50 rows.
#### CROSS JOIN doesn't require a ON condition like other joins (e.g., INNER JOIN, LEFT JOIN).
>Basic syntax
```
SELECT
  name,
  date
FROM
  members
  CROSS JOIN dates;
```

## INSERT
### Inserting a single row in a table
#### To insert a single row into a table, you use the following form of the INSERT statement:
>Basic syntax
```
INSERT INTO table (column1,column2 ,..)
VALUES( value1,	value2 ,...);
```

### Inserting multiple rows in a table
#### To insert multiple rows into a table, you use the following form of the INSERT statement:
>Basic syntax
```
INSERT INTO table1 (column1,column2 ,..)
VALUES 
   (value1,value2 ,...),
   (value1,value2 ,...),
    ...
   (value1,value2 ,...);
```

## UPDATE
#### To update existing data in a table, you use SQLite UPDATE statement. 
>Basic syntax
```
UPDATE table
SET column_1 = new_value_1,
    column_2 = new_value_2
WHERE
    search_condition
```

## DELETE
#### Sometimes, you need to remove rows from a table. In this case, you use SQLite DELETE statement.
#### The SQLite DELETE statement allows you to delete one row, multiple rows, and all rows in a table. 
>Basic syntax
```
DELETE FROM table
WHERE search_condition;
```

## REPLACE
#### The idea of the REPLACE statement is that when a UNIQUE or PRIMARY KEY constraint violation occurs, it does the following:
#### First, delete the existing row that causes a constraint violation.Second, insert a new row.
#### In the second step, if any constraint violation e.g., NOT NULL constraint occurs, the REPLACE statement will abort the action and roll back the transaction.
>Basic syntax
```
REPLACE INTO table(column_list)
VALUES(value_list);
```

## COUNT() FUNCTION
#### The function COUNT() is an aggregate function that returns the number of items in a group.
>Basic syntax #Count all rows
```
SELECT COUNT(*)
FROM table_name
WHERE search_condition;
```
>Basic syntax #Count non-null values in a specific column
```
SELECT COUNT(column_name)
FROM table_name
WHERE search_condition;
```
>Basic syntax #Count distinct values
```
SELECT COUNT(DISTINCT column_name)
FROM table_name
WHERE search_condition;
```

## AVG() FUNCTION
#### The AVG function is an aggregate function that calculates the average value of all non-NULL values within a group.
>Basic syntax
```
SELECT AVG(column_name)
FROM table_name
WHERE search_condition;
```

>Basic syntax #Average for distinct values 
``` 
SELECT AVG(DISTINCT column_name)
FROM table_name 
WHERE search_condition;
```

## MAX() FUNCTION
#### The SQLite MAX function is an aggregate function that returns the maximum value of all values in a group. You can use the MAX function to accomplish a lot of things
>Basic syntax
```
SELECT MAX(column_name)
FROM table_name 
WHERE search_condition;
```

>Basic syntax #Maximum values for distinct values
```
SELECT MAX(DISTINCT column_name)
FROM table_name 
WHERE search_condition;
```

## MIN() FUNCTION
#### The SQLite MAX function is an aggregate function that returns the minimum value of all values in a group. You can use the MAX function to accomplish a lot of things
>Basic syntax
```
SELECT MIN(column_name)
FROM table_name 
WHERE search_condition;
```

>Basic syntax #Minimum values for distinct values
```
SELECT MIN(DISTINCT column_name)
FROM table_name 
WHERE search_condition;
```

## SUM() FUNCTION
#### The SUM function is an aggregate function that returns the sum the non-NULL values or only the distinct values in a group.
>Basic syntax
```
SELECT SUM(column_name)
FROM table_name 
WHERE search_condition;
```

>Basic syntax #Sum values for distinct values
```
SELECT SUM(DISTINCT column_name)
FROM table_name 
WHERE search_condition;
```

