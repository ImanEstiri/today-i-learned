> Today I Learned | .NET
 
# Pattern matching works outside switch

Date: 2026/06/17

## Body

C# pattern matching isn't just for `switch`. You can use patterns in `if`, `is`, and even
in assignments, which removes a lot of casts and null checks.

```csharp
if (obj is string s && s.Length > 3)
    Console.WriteLine(s.ToUpper());

if (value is int n and > 0 and < 100)
    Console.WriteLine("in range");
```

The `is` pattern both tests and assigns in one step — no separate `as` and null check.

Common patterns worth knowing:

```csharp
// property pattern
if (order is { Total: > 100, Status: "Paid" })
    ...

// list pattern (C# 12+)
if (numbers is [1, 2, .. var rest])
    ...

// switch expression with patterns
string Describe(object o) => o switch
{
    int n when n < 0 => "negative",
    int n            => $"int {n}",
    string s         => $"string of length {s.Length}",
    null             => "null",
    _                => "other"
};
```

`not` negates a pattern, `and`/`or` combine, and `_` is the discard. This is C# 9+ mostly;
list patterns are C# 12.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 