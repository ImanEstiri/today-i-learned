> Today I Learned | SQL Server
 
# COUNT(*) vs COUNT(column)

Date: 2026/06/07

## Body

`COUNT(*)` counts all rows. `COUNT(column)` counts only rows where that column is not
`NULL`. They look similar but give different numbers the moment a column is nullable.

```sql
-- counts every row
SELECT COUNT(*) FROM Orders;

-- counts only orders that have a customer assigned
SELECT COUNT(CustomerId) FROM Orders;
```

Same trap with `COUNT(DISTINCT column)`: it ignores `NULL` too. If you want the real row
count, use `COUNT(*)`.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 