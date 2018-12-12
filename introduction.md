>What data types do each of these values represent?

- "A Clockwork Orange"  - STRING
- 42 - INTEGER
- 09/02/1945 - DATE
- 98.7 - FLOAT
- $15.99 - FLOAT/NUMBER


> Explain when a database would be used. Explain when a text file would be used.

I would use a database to store a large amount of similar data. Like an address book or bank ledger.
I would use a text file to store presentatational or human readable information. Like a ltter to a friend or recipe.

>Describe one difference between SQL and other programming languages.

SQL is a declarative rather than a procedural language. We say what we want not how to do something.

>In your own words, explain how the pieces of a database system fit together at a high level.

A database is a collection of organized data. Unlike a text file the information is in non human readable form and can be thought of a collection of values. We query the collection using a declaritive language (ie SQL) to retrieve the specific information that we want. Data values are organized around datatypes in groups that reprsent a single entity or collection of entities. In the case of SQL databases the values/cells are collected in rows which are part of a table. And a group of tables would be a collection and one or more collections would be in a database. Tables also have columns to organize the datatypes found in each row.


>Explain the meaning of table, row, column, and value.

- __value__: an intersection of a column and row. represents a single cell or data point in a record.
- __Row__: reprsents a single record in a table. consists of one set of values/cells.
- __column__: is one catagory of data in a table. One tyoe of data used in a record.
- __table__:  a collection of data organized by colums (data types) and rows (data records/units)

>List three data types that can be used in a table.

integer, boolean, string(varchar)

>Given this payments table, provide an English description of the following queries and include their results:
```
     SELECT date, amount
     FROM payments;
```

Selct the `date` and `amount` fields from the payments database.
result:
date | amount
---- | -----
2016-05-01T00:00:00.000Z	| 1500.0000
2016-05-10T00:00:00.000Z	| 37.0000
2016-05-15T00:00:00.000Z | 124.9300
2016-05-23T00:00:00.000Z | 54.7200
```
     SELECT amount
     FROM payments
     WHERE amount > 500;
```
Select the `amount` field from the payments table for each record where `amount` is greater than 500.
result
amount |
------ |
1500.0000 |

```
     SELECT *
     FROM payments
     WHERE payee = 'Mega Foods';
```
select all payemnts from `Mega Foods` from database
result:
date	| payee | amount | memo
---- | ----- | ------ | ----
2016-05-15T00:00:00.000Z	| Mega Foods |	124.9300	| Groceries

>Given this users table, write SQL queries using the following criteria and include the output:

>The email and sign-up date for the user named DeAndre Data.
```
SELECT email,signup 
FROM users
WHERE name='DeAndre Data'
```
result:
email | signup
----- | ------
datad@comcast.net | 2008-01-20T00:00:00.000Z


>The user ID for the user with email 'aleesia.algorithm@uw.edu'.
```
SELECT userid
FROM users
WHERE email='aleesia.algorithm@uw.edu'
```
result:
userid |
------ |
1 |

>All the columns for the user ID equal to 4.
```
SELECT *
FROM users
WHERE userid=4
```
result:
userid | name | email | signup
------ | ---- | ----- | ------
4 | Brandy Boolean | bboolean@nasa.gov | 1999-10-15T00:00:00.000Z





First Header | Second Header
------------ | -------------
Content from cell 1 | Content from cell 2
Content in the first column | Content in the second column
