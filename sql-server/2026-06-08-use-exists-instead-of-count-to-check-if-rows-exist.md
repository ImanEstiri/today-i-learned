> Today I Learned | SQL Server
 
# Use EXISTS instead of COUNT(*) to check if rows exist

Date: 2026/06/08

## Body

When you only want to know "does anything match?", don't count — check.

```sql
-- slow: counts every matching row
IF (SELECT COUNT(*) FROM Orders WHERE CustomerId = @id) > 0
    ...

-- fast: stops at the first matching row
IF EXISTS (SELECT 1 FROM Orders WHERE CustomerId = @id)
    ...
```
 
`COUNT(*)` has to scan every matching row to produce a number. `EXISTS` stops the moment
it finds one match, which on a large table is dramatically faster.

The same idea for "get the first match":
```
SELECT TOP (1) * FROM Orders WHERE CustomerId = @id;
```

Don't sort by the primary key just to grab the first row — you're making SQL Server do
work you don't need.

---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 