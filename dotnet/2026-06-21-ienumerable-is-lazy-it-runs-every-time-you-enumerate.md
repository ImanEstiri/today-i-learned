> Today I Learned | .NET
 
# IEnumerable is lazy — it runs every time you enumerate

Date: 2026/06/21

## Body

LINQ queries don't execute when you build them. They run each time you iterate. So
enumerating twice means running twice.

```csharp
var query = db.Users.Where(u => u.IsActive);   // nothing hits the DB yet

var count = query.Count();        // DB call #1
var list = query.ToList();        // DB call #2
```

Fix: materialize once with `ToList()` / `ToArray()`, then reuse.

```csharp
var users = db.Users.Where(u => u.IsActive).ToList();
var count = users.Count;
```

Same trap with side effects inside `.Select()` — they run on every enumeration. If the
query is expensive or non-deterministic, materialize it.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 