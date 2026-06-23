> Today I Learned | .NET
 
# yield return builds a lazy sequence

Date: 2026/06/23

## Body

`yield return` lets a method produce items one at a time instead of building a list. The
caller gets each item as it's produced, and memory stays flat.

```csharp
IEnumerable<int> Evens(int max)
{
    for (int i = 0; i <= max; i += 2)
        yield return i;
}
```

Nothing runs until the caller iterates. `Evens(1_000_000).First()` produces one number
and stops — no list of a million ints is ever built.

```csharp
foreach (var n in Evens(10))
    Console.WriteLine(n);   // 0, 2, 4, 6, 8, 10
```

The same laziness trap as LINQ applies: the method body re-runs on every enumeration. If
that matters, materialize with `.ToList()`.

`yield break` exits early — handy for "stop after N items" or "stop on first match".

```csharp
IEnumerable<string> TakeUntilError(IEnumerable<string> lines)
{
    foreach (var line in lines)
    {
        if (line.StartsWith("ERROR")) yield break;
        yield return line;
    }
}
```

---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 