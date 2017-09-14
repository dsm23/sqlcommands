# SQL Query commands

#### by David Murdoch

## Contents

## Queries

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
| AND  | Content Cell  |
| OR  | Content Cell  |
| IN  | Content Cell  |
| NOT  | Content Cell  |