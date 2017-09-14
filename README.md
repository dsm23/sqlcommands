# SQL Query commands

#### by David Murdoch

## Contents

1. *[Queries](#queries)*

1.1 *[WHERE](#where)*

1.2 *[BETWEEN](#between)*

1.3 *[Logical Operators](#logical-operators)*

1.3.1 *[OR](#or)*

## Queries

#### WHERE

WHERE command syntax
```sql
SELECT column_list 
FROM table_name
WHERE condition;
```

numerical example
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

combining
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

#### Concat
```sql
SELECT CONCAT(FirstName, ', ' , City) FROM customers;
```