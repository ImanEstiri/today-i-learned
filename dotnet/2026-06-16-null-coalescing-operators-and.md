> Today I Learned | .NET
 
# Null-coalescing operators ?? and ??=

Date: 2026/06/16

## Body

`??` returns the left side if it isn't null, otherwise the right side. It's a shorter
ternary and it evaluates the left side only once.

```csharp
string name = input ?? "guest";

// equivalent to
string name = input is not null ? input : "guest";
```

`??=` assigns only when the target is null. Handy for lazy initialization.

```csharp
_cache ??= BuildCache();

// equivalent to
if (_cache is null)
    _cache = BuildCache();
```

You can chain `??` — the first non-null wins:

```csharp
string display = nickname ?? username ?? "anonymous";
```

A common pitfall: `??` only triggers on `null`, not on empty strings or whitespace. For
that, use `string.IsNullOrWhiteSpace`:

```csharp
string name = string.IsNullOrWhiteSpace(input) ? "guest" : input;
```

For type checks, `as` pairs well with `??`:

```csharp
var button = sender as Button ?? throw new InvalidOperationException();
```
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 