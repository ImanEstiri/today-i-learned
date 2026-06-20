> Today I Learned | SQL Server
 
# EXISTS vs IN

Date: 2026/06/20

## Body

`IN` builds the full list of values first, then checks against it. `EXISTS` stops at the
first match. On large subqueries, `EXISTS` is usually faster.

```sql
-- IN — must produce every CustomerId first
SELECT * FROM Orders
WHERE CustomerId IN (SELECT Id FROM Customers WHERE IsActive = 1);

-- EXISTS — short-circuits on first match
SELECT * FROM Orders o
WHERE EXISTS (SELECT 1 FROM Customers c WHERE c.Id = o.CustomerId AND c.IsActive = 1);
```

`NOT IN` is the real trap: if the subquery returns a single `NULL`, the whole condition
becomes `NULL` and the query returns zero rows. Use `NOT EXISTS` instead.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 