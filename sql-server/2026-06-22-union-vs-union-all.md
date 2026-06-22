> Today I Learned | SQL Server
 
# UNION vs UNION ALL

Date: 2026/06/22

## Body

`UNION` removes duplicate rows. `UNION ALL` keeps everything. Removing duplicates requires
a sort (or hash), which is expensive — so `UNION ALL` is much faster when you know the
sets don't overlap.

```sql
-- deduplicates, slower
SELECT Id FROM ActiveUsers
UNION
SELECT Id FROM InactiveUsers;

-- keeps all rows, faster
SELECT Id FROM ActiveUsers
UNION ALL
SELECT Id FROM InactiveUsers;
```

Rule: use `UNION ALL` by default. Switch to `UNION` only when you actually need
deduplication. Also note that `UNION` sorts by all columns unless you specify
`ORDER BY`, while `UNION ALL` preserves whatever order the branches produced.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 