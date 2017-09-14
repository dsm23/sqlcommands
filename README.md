# SQL Query commands

#### by David Murdoch

## Contents

1. *[Queries](#queries)*

1.1 *[WHERE](#where)*

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

```sql
SELECT * FROM customers 
WHERE City = 'New York' OR City = 'Chicago';
```