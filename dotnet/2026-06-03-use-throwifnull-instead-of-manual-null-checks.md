> Today I Learned | .NET

# Use ThrowIfNull instead of manual null checks

Date: 2026/06/03

## Body

Since .NET 6, the exception types themselves expose static guard helpers, so the classic
`if (x is null) throw new ArgumentNullException(nameof(x));` boilerplate is no longer
needed. `ArgumentNullException.ThrowIfNull` does the same job, and because it is marked
with `[DoesNotReturnIf]`, the compiler flow-analysis still treats the argument as non-null
after the call — no `!` needed.

The same family covers most common argument validation: `ThrowIfNullOrEmpty`,
`ThrowIfNullOrWhiteSpace`, `ThrowIfNegative`, `ThrowIfNegativeOrZero`, `ThrowIfZero`,
`ThrowIfGreaterThan`, and more. They are also annotated with `[CallerArgumentExpression]`,
so the parameter name in the exception message is filled in automatically — you don't
even pass `nameof`.

```csharp
public void Process(string name, int count, IEnumerable<int> items)
{
    ArgumentNullException.ThrowIfNull(name);
    ArgumentException.ThrowIfNullOrWhiteSpace(name);
    ArgumentNullException.ThrowIfNull(items);
    ArgumentOutOfRangeException.ThrowIfNegativeOrZero(count);

    // ...
}
```
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 