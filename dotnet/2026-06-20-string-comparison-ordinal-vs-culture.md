> Today I Learned | .NET
 
# String comparison: Ordinal vs culture

Date: 2026/06/20

## Body

`==` on strings is ordinal — it compares code points, no culture. That's what you want for
keys, IDs, and file paths.

For user-facing text, use `string.Equals` with a culture-aware mode:

```csharp
// exact, case-sensitive — for identifiers
if (a == b) { }

// case-insensitive — culture-invariant
if (string.Equals(a, b, StringComparison.OrdinalIgnoreCase)) { }

// user-visible sort/comparison
string.Compare(a, b, StringComparison.CurrentCultureIgnoreCase);
```

Avoid `ToLower()`/`ToUpper()` for comparison — it allocates and breaks on Turkish `i`.
Use `StringComparison` instead.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 