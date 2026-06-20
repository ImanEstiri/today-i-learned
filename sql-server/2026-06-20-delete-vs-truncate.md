> Today I Learned | SQL Server
 
# DELETE vs TRUNCATE

Date: 2026/06/20

## Body

Both remove rows, but they're not the same.

`DELETE` is logged row by row, can have a `WHERE`, fires triggers, and can be rolled back.

`TRUNCATE` deallocates whole pages, resets `IDENTITY`, can't have a `WHERE`, and doesn't
fire triggers. Much faster on large tables.

```sql
DELETE FROM Logs WHERE CreatedAt < '2026-01-01';   -- partial

TRUNCATE TABLE Logs;                                -- everything, fast
```

`TRUNCATE` fails if the table is referenced by a foreign key. In that case, use `DELETE`.


---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 