> Today I Learned | SQL Server
 
# OFFSET/FETCH for paging, not TOP

Date: 2026/06/16

## Body

`TOP` only limits the first N rows — it can't skip. For paging, SQL Server has
`OFFSET ... FETCH`, which needs an `ORDER BY` (you can't page without a stable order).

```sql
SELECT Id, Name
FROM Customers
ORDER BY Id
OFFSET 20 ROWS
FETCH NEXT 10 ROWS ONLY;
```

Page 1 is `OFFSET 0`, page 2 is `OFFSET 10` (if page size is 10), and so on. The formula
is `(page - 1) * size`.

Be aware that large offsets get slow — the engine still has to walk past every skipped
row. For deep paging on big tables, use keyset pagination instead:

```sql
SELECT TOP (10) Id, Name
FROM Customers
WHERE Id > @lastSeenId
ORDER BY Id;
```

Keyset paging stays fast regardless of page number, but only works when the user moves
forward, not to an arbitrary page.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 