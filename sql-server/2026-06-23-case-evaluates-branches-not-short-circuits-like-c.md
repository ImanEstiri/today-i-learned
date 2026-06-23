> Today I Learned | SQL Server
 
# CASE evaluates branches, not short-circuits like C#

Date: 2026/06/23

## Body

In C#, `a != 0 && 10 / a > 1` short-circuits — if `a` is 0, the right side never runs.
SQL's `CASE` **evaluates every branch's expression**, even the ones whose condition is
false. Division by zero still fires.

```sql
-- fails if any row has Quantity = 0
SELECT
    CASE WHEN Quantity = 0 THEN 0
         ELSE Total / Quantity
    END
FROM Orders;
```

The fix is `NULLIF` — turn the divisor into `NULL` before the division, so the branch
becomes `NULL` instead of throwing:

```sql
SELECT
    Total / NULLIF(Quantity, 0) AS UnitPrice
FROM Orders;
```

Same trap with `CASE` around `CONVERT`/`CAST` — a value that can't be converted causes the
whole query to fail even if that row's condition is false. Guard with `TRY_CAST` or
`TRY_CONVERT`.


 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 