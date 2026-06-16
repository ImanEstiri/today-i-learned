> Today I Learned | SQL Server
 
# WHERE vs ON in a LEFT JOIN

Date: 2026/06/16

## Body

On an `INNER JOIN`, `WHERE` and `ON` behave the same. On a `LEFT JOIN`, they don't — and
the difference changes the result.

`ON` filters the right table **before** the join. Rows on the left are always kept.

```sql
-- all customers, with their paid orders (or NULLs if none)
SELECT c.Name, o.Id
FROM Customers c
LEFT JOIN Orders o ON o.CustomerId = c.Id AND o.Status = 'Paid';
```

`WHERE` filters after the join. Rows where the condition is false get dropped — which
turns a `LEFT JOIN` into an `INNER JOIN`.

```sql
-- only customers who have at least one paid order
SELECT c.Name, o.Id
FROM Customers c
LEFT JOIN Orders o ON o.CustomerId = c.Id
WHERE o.Status = 'Paid';
```

A useful pattern: to find customers with no matching rows, filter on a `NULL` column
from the right side:

```sql
SELECT c.Name
FROM Customers c
LEFT JOIN Orders o ON o.CustomerId = c.Id
WHERE o.Id IS NULL;
```

---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 