> Today I Learned | SQL Server
 
# Implicit conversion can silently kill your index

Date: 2026/06/22

## Body

Comparing a `VARCHAR` column to an `NVARCHAR` value forces SQL Server to convert the
**column** to `NVARCHAR` on every row — so the index can't be used.

```sql
-- PhoneNumber is VARCHAR(20)
DECLARE @phone NVARCHAR(20) = N'0912...';

-- slow: index scan, converts every row
SELECT * FROM Users WHERE PhoneNumber = @phone;

-- fast: index seek
SELECT * FROM Users WHERE PhoneNumber = @phone COLLATE ...;
-- or declare the variable as VARCHAR
DECLARE @phone VARCHAR(20) = '0912...';
```

This usually shows up when parameters come from an ORM or from code that uses .NET
`string` (which maps to `NVARCHAR`). The fix is to align the types, or add
`CONVERT(VARCHAR(20), @phone)` on the value side — never on the column side.

Check the execution plan: an implicit `CONVERT_IMPLICIT` on the column's side of a
predicate is the tell.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 