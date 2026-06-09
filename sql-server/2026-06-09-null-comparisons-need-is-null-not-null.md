> Today I Learned | SQL Server
 
# NULL comparisons need IS NULL, not = NULL

Date: 2026/06/09

## Body

In SQL, `NULL` means "unknown", not "empty". So comparing anything to `NULL` with `=`
gives `NULL` (which is treated as false in a `WHERE`), never `true`.

```sql
-- returns zero rows, even if Email is NULL
SELECT * FROM Users WHERE Email = NULL;

-- correct
SELECT * FROM Users WHERE Email IS NULL;

-- also correct
SELECT * FROM Users WHERE Email IS NOT NULL;
```

This also means `NOT IN` with a subquery that contains a single `NULL` returns zero rows.
If the subquery's result can be `NULL`, use `NOT EXISTS` instead.

```sql
-- safe
SELECT * FROM Orders o
WHERE NOT EXISTS (
    SELECT 1 FROM Cancelled c WHERE c.OrderId = o.Id
);
```

`ISNULL(col, '')` and `COALESCE(col, '')` are fine for display, but they don't fix the
comparison — they just replace the value. 

---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 