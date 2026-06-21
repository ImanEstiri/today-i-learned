> Today I Learned | .NET
 
# Use StringBuilder in loops, not string +=

Date: 2026/06/21

## Body

Strings are immutable — every `+=` allocates a new string and copies the old one. In a
loop, that's O(n²) work.

```csharp
// slow for large n
string result = "";
for (int i = 0; i < 10_000; i++)
    result += i;

// fast — one buffer, amortized append
var sb = new StringBuilder();
for (int i = 0; i < 10_000; i++)
    sb.Append(i);
string result = sb.ToString();
```

Use `+=` for one or two concatenations. For loops or unknown counts, `StringBuilder`.

Tip: `string.Join(",", items)` beats both when you have a collection.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 