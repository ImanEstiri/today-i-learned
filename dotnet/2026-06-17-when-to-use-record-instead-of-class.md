> Today I Learned | .NET
 
# When to use record instead of class

Date: 2026/06/17

## Body

A `record` is a class with value-based equality and a few conveniences baked in. Use it
when the type's job is to **carry data**, not to have behavior with identity.

```csharp
public record Person(string Name, int Age);

var a = new Person("Iman", 30);
var b = new Person("Iman", 30);
Console.WriteLine(a == b);          // True — value equality
Console.WriteLine(a);               // Person { Name = Iman, Age = 30 }
```

What you get for free:

- Value equality — two records with the same data are equal.

- `ToString()` that prints the properties.

- Deconstruction — `var (name, age) = a;`

- `with` expressions for non-destructive updates.

```csharp
var older = a with { Age = 31 };
```

A regular `class` gives reference equality (`a == b` is false unless same instance) and no
generated `ToString`. So the rule is:

record — DTOs, API responses, events, configs, "this is data".

class — services, controllers, anything with behavior and identity.

`record struct` gives you value-type semantics with the same conveniences — good for small
value objects that get copied a lot.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 