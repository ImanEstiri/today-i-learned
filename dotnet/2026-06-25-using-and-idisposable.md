> Today I Learned | .NET
 
# using and IDisposable

Date: 2026/06/25

## Body

`using` guarantees `Dispose()` runs even if an exception is thrown — same idea as
`finally`, less noise.

```csharp
// statement form
using (var stream = File.OpenRead("data.bin"))
{
    // ...
}

// declaration form (C# 8+) — disposes at end of scope
using var stream = File.OpenRead("data.bin");
```

For async cleanup, use `await using` with `IAsyncDisposable`:

```csharp
await using var conn = new SqlConnection(cs);
await conn.OpenAsync();
```

Common mistake: `using` on something that isn't `IDisposable` won't compile, but wrapping
a class in `IDisposable` just because it has a `Close()` method isn't always right. If
disposal matters (files, sockets, DB connections), implement `IDisposable`; if not, leave
it alone — extra `IDisposable` types confuse garbage collection expectations and require
callers to `using` them for no reason.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 