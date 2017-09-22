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

	* [Arithmetic Operators](arithmetic-operators)

	* [UPPER and LOWER](upper-and-lower)

	* [ORDER BY](order-by)

	* [LIKE](like)

## Basics

SQL stands for Structured Query Language

SQL is used to access and manipulate a database

MS SQL Server is a program that understands SQL

SQL is not case sensitive

SQL can:

- insert, update, or delete records in a database

- create new databases, table, stored procedures, views

- retrieve data from a database, etc

## Queries

#### WHERE

WHERE command syntax
```sql
SELECT column_list 
FROM table_name
WHERE condition;
```

numerical example (where customers is a generic table)
```sql
SELECT * FROM customers
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
SELECT * FROM customers 
WHERE ID BETWEEN 3 AND 7;
```

Result:

ID | FirstName |	LastName | City | Age | Salary
:---:|:---:|:---:|:---:|:---:|:---:
3 |	Chloe | Anderson | Chicago | 27 | 3000
4 |	Emily | Adams | Houston | 34 | 4500
5 |	James | Roberts	| Philadelphia | 31 | 2000
6 |	Andrew | Thomas	| New York | 45 | 2500
7 |	Daniel | Harris	| New York | 30 | 3000

text example
```sql
SELECT ID, FirstName, LastName, City 
FROM customers
WHERE City = 'New York';
```

Result:

ID | FirstName |	LastName | City | Age | Salary
:---:|:---:|:---:|:---:|:---:|:---:
1 | John | Smith | New York | 35 | 2000
6 |	Andrew | Thomas	| New York | 45 | 2500
7 |	Daniel | Harris	| New York | 30 | 3000


#### Logical Operators

| Operator  | Description |
| ------------- | ------------- |
| AND  | TRUE if *both* expressions are TRUE |
| OR  | TRUE if *either* expression is TRUE  |
| IN  | TRUE if the operand is equal to one of a list of expressions |
| NOT  | Returns TRUE if expression is not TRUE |

#### OR
```sql
SELECT * FROM customers 
WHERE City = 'New York' OR City = 'Chicago';
```

Result:

ID | FirstName |	LastName | City | Age | Salary
:---:|:---:|:---:|:---:|:---:|:---:
1 | John | Smith | New York | 35 | 2000
3 |	Chloe | Anderson | Chicago | 27 | 3000
6 |	Andrew | Thomas	| New York | 45 | 2500
7 |	Daniel | Harris	| New York | 30 | 3000
8 |	Charlotte | Walker | Chicago | 35 | 3500

combine with AND
```sql
SELECT * FROM customers
WHERE City = 'New York'
AND (Age=30 OR Age=35);
```

Result:

ID | FirstName |	LastName | City | Age | Salary
:---:|:---:|:---:|:---:|:---:|:---:
1 | John | Smith | New York | 35 | 2000
7 |	Daniel | Harris	| New York | 30 | 3000

IN (Multiple OR)
```sql
SELECT * FROM customers 
WHERE City IN ('New York', 'Los Angeles', 'Chicago');
```

Result:

ID | FirstName |	LastName | City | Age | Salary
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
SELECT CONCAT(FirstName, ', ' , City) FROM customers;
```

combine with AS
```sql
SELECT CONCAT(FirstName,', ', City) AS new_column 
FROM customers;
```

#### Arithmetic Operators
```sql
SELECT ID, FirstName, LastName, Salary+500 AS Salary
FROM employees;
```

Result:

ID | FirstName |	LastName | City | Age | Salary
:---:|:---:|:---:|:---:|:---:|:---:
1 | John | Smith | New York | 35 | 2500
2 |	David | Williams | Los Angeles | 23 | 2000
3 |	Chloe | Anderson | Chicago | 27 | 3500
4 |	Emily | Adams | Houston | 34 | 5000
5 |	James | Roberts	| Philadelphia | 31 | 2500
6 |	Andrew | Thomas	| New York | 45 | 3000
7 |	Daniel | Harris	| New York | 30 | 3500
8 |	Charlotte | Walker | Chicago | 35 | 4000
9 |	Samuel | Clark | San Diego | 20 | 4500
10 | Anthony | Young | Los Angeles | 33 | 5500

```sql
SELECT Salary, SQRT(Salary)
FROM employees;
```
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

#### UPPER and LOWER
```sql
SELECT FirstName, UPPER(LastName) AS LastName 
FROM employees;
```

Result:

ID | FirstName |	LastName | City | Age | Salary
:---:|:---:|:---:|:---:|:---:|:---:
1 | John | SMITH | New York | 35 | 2000
2 |	David | WILLIAMS | Los Angeles | 23 | 1500
3 |	Chloe | ANDERSON | Chicago | 27 | 3000
4 |	Emily | ADAMS | Houston | 34 | 4500
5 |	James | ROBERTS	| Philadelphia | 31 | 2000
6 |	Andrew | THOMAS	| New York | 45 | 2500
7 |	Daniel | HARRIS	| New York | 30 | 3000
8 |	Charlotte | WALKER | Chicago | 35 | 3500
9 |	Samuel | CLARK | San Diego | 20 | 4000
10 | Anthony | YOUNG | Los Angeles | 33 | 5000

The **UPPER** function converts all letters in the specified string to uppercase. 
The **LOWER** function converts the string to lowercase.

#### ORDER BY
```sql
SELECT FirstName, Salary FROM employees 
WHERE  Salary > 3100
ORDER BY Salary ASC;
```

Result:

ID | FirstName |	LastName | City | Age | Salary
:---:|:---:|:---:|:---:|:---:|:---:
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

ID | FirstName |	LastName | City | Age | Salary
:---:|:---:|:---:|:---:|:---:|:---:
8 |	Charlotte | Walker | Chicago | 35 | 3500
9 |	Samuel | Clark | San Diego | 20 | 4000
4 |	Emily | Adams | Houston | 34 | 4500
10 | Anthony | Young | Los Angeles | 33 | 5000

#### LIKE

LIKE syntax
```sql
SELECT * FROM employees 
WHERE FirstName LIKE 'A%';
```
Result:

ID | FirstName |	LastName | City | Age | Salary
:---:|:---:|:---:|:---:|:---:|:---:
6 |	Andrew | Thomas	| New York | 45 | 2500
10 | Anthony | Young | Los Angeles | 33 | 5000

or

```sql
SELECT * FROM employees 
WHERE LastName LIKE '%s';
```
Result:

ID | FirstName |	LastName | City | Age | Salary
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


#### Joining Tables
selecting from two different tables will create a temporary table containing the two
```sql
SELECT customers.ID, customers.Name, orders.Name, orders.Amount
FROM customers, orders
WHERE customers.ID=orders.Customer_ID
ORDER BY customers.ID;
```

Custom (shorter) table names can be achieved with AS
```sql
SELECT ct.ID, ct.Name, ord.Name, ord.Amount
FROM customers AS ct, orders AS ord
WHERE ct.ID=ord.Customer_ID
ORDER BY ct.ID;
```

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
