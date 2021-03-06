# SQL Query commands

#### by David Murdoch

## Contents

* [Basics](#basics)

* [Queries](#queries)

	* [WHERE](#where)

	* [BETWEEN](#between)

	* [Logical Operators](#logical-operators)

	* [OR](#or)

	* [CONCAT](#concat)

	* [Arithmetic Operators](#arithmetic-operators)

	* [UPPER and LOWER](#upper-and-lower)

	* [ORDER BY](#order-by)

	* [LIKE](#like)
	
* [Join](#join)

	* [INNER JOIN](#inner-join)
	
	* [LEFT JOIN](#left-join)
	
	* [RIGHT JOIN](#right-join)
	
	* [UNION](#union)
	
	* [FULL OUTER JOIN](#full-outer-join)
	
	* [Key](#key)

## Basics

SQL stands for Structured Query Language

SQL is used to access and manipulate a database

MS SQL Server is a program that understands SQL

SQL is not case sensitive

SQL can:

- insert, update, or delete records in a database

- create new databases, table, stored procedures, views

- retrieve data from a database, etc

##### Comments
```sql
/*
	This is a
	comment!
*/
```

## Queries

for a given table called employees

ID | FirstName |	LastName | City | Age | Salary
:---:|:---:|:---:|:---:|:---:|:---:
1 | John | Smith | New York | 35 | 2000
2 |	David | Williams | Los Angeles | 23 | 1500
3 |	Chloe | Anderson | Chicago | 27 | 3000
4 |	Emily | Adams | Houston | 34 | 4500
5 |	James | Roberts	| Philadelphia | 31 | 2000
6 |	Andrew | Thomas	| New York | 45 | 2500
7 |	Daniel | Harris	| New York | 30 | 3000
8 |	Charlotte | Walker | Chicago | 35 | 3500
9 |	Samuel | Clark | San Diego | 20 | 4000
10 | Anthony | Young | Los Angeles | 33 | 5000

#### WHERE

WHERE command syntax
```sql
SELECT column_list 
FROM table_name
WHERE condition;
```

numerical example (where employees is a generic table)
```sql
SELECT * FROM employees
WHERE ID != 5;
```

Result: 

ID | FirstName |	LastName | City | Age | Salary
:---:|:---:|:---:|:---:|:---:|:---:
1 | John | Smith | New York | 35 | 2000
2 |	David | Williams | Los Angeles | 23 | 1500
3 |	Chloe | Anderson | Chicago | 27 | 3000
4 |	Emily | Adams | Houston | 34 | 4500
6 |	Andrew | Thomas	| New York | 45 | 2500
7 |	Daniel | Harris	| New York | 30 | 3000
8 |	Charlotte | Walker | Chicago | 35 | 3500
9 |	Samuel | Clark | San Diego | 20 | 4000
10 | Anthony | Young | Los Angeles | 33 | 5000

#### BETWEEN

BETWEEN command syntax
```sql
SELECT column_name(s)
FROM table_name
WHERE column_name BETWEEN value1 AND value2;
```

numerical example
```sql
SELECT * FROM employees 
WHERE ID BETWEEN 3 AND 7;
```

Result:

ID | FirstName | LastName | City | Age | Salary
:---:|:---:|:---:|:---:|:---:|:---:
3 |	Chloe | Anderson | Chicago | 27 | 3000
4 |	Emily | Adams | Houston | 34 | 4500
5 |	James | Roberts	| Philadelphia | 31 | 2000
6 |	Andrew | Thomas	| New York | 45 | 2500
7 |	Daniel | Harris	| New York | 30 | 3000

text example
```sql
SELECT ID, FirstName, LastName, City 
FROM employees
WHERE City = 'New York';
```

Result:

ID | FirstName | LastName | City
:---:|:---:|:---:|:---:
1 | John | Smith | New York
6 |	Andrew | Thomas	| New York
7 |	Daniel | Harris	| New York


#### Logical Operators

| Operator  | Description |
| ------------- | ------------- |
| AND  | TRUE if *both* expressions are TRUE |
| OR  | TRUE if *either* expression is TRUE  |
| IN  | TRUE if the operand is equal to one of a list of expressions |
| NOT  | Returns TRUE if expression is not TRUE |

#### OR
```sql
SELECT * FROM employees 
WHERE City = 'New York' OR City = 'Chicago';
```

Result:

ID | FirstName | LastName | City | Age | Salary
:---:|:---:|:---:|:---:|:---:|:---:
1 | John | Smith | New York | 35 | 2000
3 |	Chloe | Anderson | Chicago | 27 | 3000
6 |	Andrew | Thomas	| New York | 45 | 2500
7 |	Daniel | Harris	| New York | 30 | 3000
8 |	Charlotte | Walker | Chicago | 35 | 3500

combine with AND
```sql
SELECT * FROM employees
WHERE City = 'New York'
AND (Age=30 OR Age=35);
```

Result:

ID | FirstName | LastName | City | Age | Salary
:---:|:---:|:---:|:---:|:---:|:---:
1 | John | Smith | New York | 35 | 2000
7 |	Daniel | Harris	| New York | 30 | 3000

IN (Multiple OR)
```sql
SELECT * FROM employees 
WHERE City IN ('New York', 'Los Angeles', 'Chicago');
```

Result:

ID | FirstName | LastName | City | Age | Salary
:---:|:---:|:---:|:---:|:---:|:---:
1 | John | Smith | New York | 35 | 2000
2 |	David | Williams | Los Angeles | 23 | 1500
3 |	Chloe | Anderson | Chicago | 27 | 3000
6 |	Andrew | Thomas	| New York | 45 | 2500
7 |	Daniel | Harris	| New York | 30 | 3000
8 |	Charlotte | Walker | Chicago | 35 | 3500
10 | Anthony | Young | Los Angeles | 33 | 5000

#### CONCAT
```sql
SELECT CONCAT(FirstName, ', ' , City) FROM employees;
```
Result:

| CONCAT(FirstName, ', ' , City) |
|:---:|
|John, New York|
|David, Los Angeles|
|Chloe, Chicago|
|Emily, Houston|
|James, Philadelphia|
|Andrew, New York|
|Daniel, New York|
|Charlotte, Chicago|
|Samuel, San Diego|
|Anthony, Los Angeles|

combine with AS
```sql
SELECT CONCAT(FirstName,', ', City) AS new_column 
FROM employees;
```

#### Arithmetic Operators
```sql
SELECT ID, FirstName, LastName, Salary+500 AS Salary
FROM employees;
```

Result:

ID | FirstName | LastName | Salary
:---:|:---:|:---:|:---:
1 | John | Smith | 2500
2 |	David | Williams | 2000
3 |	Chloe | Anderson | 3500
4 |	Emily | Adams | 5000
5 |	James | Roberts | 2500
6 |	Andrew | Thomas	| 3000
7 |	Daniel | Harris	| 3500
8 |	Charlotte | Walker | 4000
9 |	Samuel | Clark | 4500
10 | Anthony | Young | 5500

```sql
SELECT Salary, SQRT(Salary)
FROM employees;
```
Result:

Salary | SQRT(Salary)
:---:|:---:
2000 | 44.721359549995796
1500 | 38.72983346207417
3000 | 54.772255750516614
4500 | 67.08203932499369
2000 | 44.721359549995796
2500 | 50
3000 | 54.772255750516614
3500 | 59.16079783099616
4000 | 63.245553203367585
5000 | 70.71067811865476

```sql
SELECT AVG(Salary) FROM employees;
```
Result:

|AVG(Salary)|
|:---:|
|3100.0000|

```sql
SELECT SUM(Salary) FROM employees;
```
Result:

|SUM(Salary)|
|:---:|
|31000|

#### COUNT

```sql
SELECT COUNT (Salary)
FROM employees;
```
Result:

| COUNT(Salary) |
|:---:|
| 10 |

#### UPPER and LOWER
```sql
SELECT FirstName, UPPER(LastName) AS LastName 
FROM employees;
```

Result:

ID | FirstName | LastName 
:---:|:---:|:---:
1 | John | SMITH
2 |	David | WILLIAMS
3 |	Chloe | ANDERSON
4 |	Emily | ADAMS
5 |	James | ROBERTS
6 |	Andrew | THOMAS
7 |	Daniel | HARRIS
8 |	Charlotte | WALKER
9 |	Samuel | CLARK
10 | Anthony | YOUNG

The **UPPER** function converts all letters in the specified string to uppercase. 
The **LOWER** function converts the string to lowercase.

#### ORDER BY
```sql
SELECT FirstName, Salary FROM employees 
WHERE  Salary > 3100
ORDER BY Salary ASC;
```
Result:

ID | FirstName | Salary
:---:|:---:|:---:
8 |	Charlotte | Walker | Chicago | 35 | 3500
9 |	Samuel | Clark | San Diego | 20 | 4000
4 |	Emily | Adams | Houston | 34 | 4500
10 | Anthony | Young | Los Angeles | 33 | 5000

The **DESC** keyword sorts results in descending order. 
Similarly, **ASC** sorts the results in ascending order.

example
```sql
SELECT FirstName, Salary FROM employees 
WHERE  Salary > (SELECT AVG(Salary) FROM employees) 
ORDER BY Salary DESC;
```

Result:

FirstName | Salary
:---:|:---:
Charlotte | 3500
Samuel | 4000
Emily | 4500
Anthony | 5000

#### LIKE

LIKE syntax
```sql
SELECT * FROM employees 
WHERE FirstName LIKE 'A%';
```
Result:

ID | FirstName | LastName | City | Age | Salary
:---:|:---:|:---:|:---:|:---:|:---:
6 |	Andrew | Thomas	| New York | 45 | 2500
10 | Anthony | Young | Los Angeles | 33 | 5000

or

```sql
SELECT * FROM employees 
WHERE LastName LIKE '%s';
```
Result:

ID | FirstName | LastName | City | Age | Salary
:---:|:---:|:---:|:---:|:---:|:---:
2 |	David | Williams | Los Angeles | 23 | 1500
5 |	James | Roberts	| Philadelphia | 31 | 2000
6 |	Andrew | Thomas	| New York | 45 | 2500
7 |	Daniel | Harris	| New York | 30 | 3000

#### MIN
```sql
SELECT MIN(Salary) AS Salary FROM employees;
```
Result:

|Salary|
|:---:|
|1500|


## Join

#### Joining Tables
selecting from two different tables will create a temporary table containing the two
```sql
SELECT employees.ID, employees.Name, orders.Name, orders.Amount
FROM employees, orders
WHERE employees.ID=orders.Customer_ID
ORDER BY employees.ID;
```

Custom (shorter) table names can be achieved with AS
```sql
SELECT ct.ID, ct.Name, ord.Name, ord.Amount
FROM employees AS ct, orders AS ord
WHERE ct.ID=ord.Customer_ID
ORDER BY ct.ID;
```

#### INNER JOIN

```sql
SELECT column_name(s)
FROM table1 INNER JOIN table2 
ON table1.column_name=table2.column_name;
```

![INNER JOIN](innerjoin.png "INNER JOIN")

#### LEFT JOIN
```sql
SELECT table1.column1, table2.column2...
FROM table1 LEFT OUTER JOIN table2
ON table1.column_name = table2.column_name;

SELECT table1.column1, table2.column2...
FROM table1 LEFT OUTER JOIN table2
ON table1.column_name = table2.column_name
WHERE table2.column.name IS NULL;
```
The OUTER keyword is optional, and can be omitted.

![LEFT JOIN](leftjoin.png "LEFT JOIN")

#### RIGHT JOIN

```sql
SELECT table1.column1, table2.column2...
FROM table1 RIGHT OUTER JOIN table2
ON table1.column_name = table2.column_name;
```

![RIGHT JOIN](rightjoin.png "RIGHT JOIN")

#### FULL OUTER JOIN

```sql
SELECT table1.column1, table2.column2...
FROM table1 FULL OUTER JOIN table2
ON table1.column_name = table2.column_name;
```

#### UNION

```sql
SELECT column_name(s) FROM table1
UNION
SELECT column_name(s) FROM table2;

SELECT ID, FirstName, LastName, City FROM First
UNION ALL
SELECT ID, FirstName, LastName, City FROM Second;
```

#### Key
e.g.
```sql
SELECT <select_list> 
FROM Table_A A
INNER JOIN Table_B B
ON A.Key = B.Key
```


https://www.codeproject.com/Articles/33052/Visual-Representation-of-SQL-Joins
