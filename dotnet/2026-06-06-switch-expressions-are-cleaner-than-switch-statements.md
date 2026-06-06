> Today I Learned | .NET
 
# Switch expressions are cleaner than switch statements

Date: 2026/06/06

## Body

Since C# 8, you can write a `switch` as an expression instead of a statement. No more
`break` on every case, no more awkward `default` blocks, and the whole thing fits on a few
lines. Pattern matching also works inside it, so you can match on types, ranges, and
`when` conditions in the same syntax.

```csharp
// old style
string Describe(int n)
{
    switch (n)
    {
        case 0: return "zero";
        case < 0: return "negative";
        case > 100: return "big";
        default: return "small";
    }
}

// new style
string Describe(int n) => n switch
{
    0 => "zero",
    < 0 => "negative",
    > 100 => "big",
    _ => "small"
};
```

The `_` is the discard pattern — it's the new `default`. Order matters: the first matching
arm wins, so put specific cases before general ones.

---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 