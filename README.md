# SQL Query commands

#### by David Murdoch

## Contents

## Queries

```sql
SELECT column_list 
FROM table_name
WHERE condition;
```
i.e.

```
SELECT * FROM customers
WHERE ID != 5;
```

```
SELECT column_name(s)
FROM table_name
WHERE column_name BETWEEN value1 AND value2;
```
```
SELECT * FROM customers 
WHERE ID BETWEEN 3 AND 7;
```