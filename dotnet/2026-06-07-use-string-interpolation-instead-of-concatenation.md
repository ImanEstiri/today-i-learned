> Today I Learned | .NET
 
# Use string interpolation instead of concatenation

Date: 2026/06/07

## Body

String interpolation (`$"..."`) is easier to read than gluing strings together with `+`,
and it's what most logging and formatting APIs expect. No more counting spaces or mixing
up commas.

```csharp
var name = "Iman";
var count = 3;

// hard to read
var msg1 = "Hello " + name + ", you have " + count + " new messages.";

// clear
var msg2 = $"Hello {name}, you have {count} new messages.";
```

Bonus: interpolated strings are `FormattableString` under the hood, so structured logging
can pick out the values instead of just the final text:

```csharp
logger.LogInformation("User {Name} has {Count} messages", name, count);
```

Always prefer the named-placeholder form in logs — it keeps the values searchable.

---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 