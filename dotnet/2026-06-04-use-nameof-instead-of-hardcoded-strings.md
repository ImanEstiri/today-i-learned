> Today I Learned | .NET
 
# Use nameof instead of hardcoded strings

Date: 2026/06/04

## Body

When you need the name of a variable, property, or type as a string, don't type it by hand.
Use `nameof`. If you rename the member later, the compiler updates the string for you, and
you also get compile-time checking plus IDE navigation (F12 works on it).

```csharp
// fragile — breaks silently after a rename
throw new ArgumentNullException("customerId");
logger.LogInformation("Customer {Id}", "customerId");

// safe — compiler keeps it in sync
throw new ArgumentNullException(nameof(customerId));
logger.LogInformation("Customer {Id}", nameof(customerId));
```

It works on properties, methods, types, and even fully-qualified members like `nameof(List<int>.Count)`.

---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 