# SQL Query commands

#### by David Murdoch

## Contents

1. *[Basics](#basics)*

1. *[Queries](#queries)*

1.1 *[WHERE](#where)*

1.2 *[BETWEEN](#between)*

1.3 *[Logical Operators](#logical-operators)*

1.3.1 *[OR](#or)*

1.4 *[CONCAT](#concat)*

1.5 *[Arithmetic Operators](arithmetic-operators)*

1.6 *[UPPER and LOWER](upper-and-lower)*

1.7 *[ORDER BY](order-by)*

1.8 *[LIKE](like)*

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

text example
```sql
SELECT ID, FirstName, LastName, City 
FROM customers
WHERE City = 'New York';
```

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

combine with AND
```sql
SELECT * FROM customers
WHERE City = 'New York'
AND (Age=30 OR Age=35);
```

IN (Multiple OR)
```sql
SELECT * FROM customers 
WHERE City IN ('New York', 'Los Angeles', 'Chicago');
```

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
```sql
SELECT Salary, SQRT(Salary)
FROM employees;
```
```sql
SELECT AVG(Salary) FROM employees;
```
```sql
SELECT SUM(Salary) FROM employees;
```

#### UPPER and LOWER
```sql
SELECT FirstName, UPPER(LastName) AS LastName 
FROM employees;
```

The *UPPER* function converts all letters in the specified string to uppercase. 
The *LOWER* function converts the string to lowercase.

#### ORDER BY
```sql
SELECT FirstName, Salary FROM employees 
WHERE  Salary > 3100
ORDER BY Salary ASC;
```
The **DESC** keyword sorts results in descending order. 
Similarly, **ASC** sorts the results in ascending order.

example
```sql
SELECT FirstName, Salary FROM employees 
WHERE  Salary > (SELECT AVG(Salary) FROM employees) 
ORDER BY Salary DESC;
```

#### LIKE

LIKE syntax
```sql
SELECT * FROM employees 
WHERE FirstName LIKE 'A%';
```
or
```sql
SELECT * FROM employees 
WHERE LastName LIKE '%s';
```

#### MIN
```sql
SELECT MIN(Salary) AS Salary FROM employees;
```

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