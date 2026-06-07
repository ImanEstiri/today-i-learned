> Today I Learned | SQL Server
 
# WHERE filters rows, HAVING filters groups

Date: 2026/06/07

## Body

`WHERE` runs before `GROUP BY`, so it filters individual rows. `HAVING` runs after, so it
filters the grouped result. You can't use an aggregate like `SUM` or `COUNT` in `WHERE` —
that's exactly what `HAVING` is for.

```sql
SELECT CustomerId, COUNT(*) AS OrderCount
FROM Orders
WHERE Status = 'Paid'          -- filters rows before grouping
GROUP BY CustomerId
HAVING COUNT(*) > 5;           -- filters groups after grouping
```

Rule of thumb: filter on columns in `WHERE`, filter on aggregates in `HAVING`. Putting
row-level filters in `HAVING` still works but is slower, because the grouping runs first.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 