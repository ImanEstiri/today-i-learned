> Today I Learned | Blazor

# Razor code-behind classes cannot be internal

Date: 2026/06/01

## Body

The Razor SDK generates each component as a `public partial class`. If the code-behind
file (`Foo.razor.cs`) declares the same class as `internal partial`, the compiler fails with
CS0262: conflicting accessibility modifiers on the partial declarations.

The CA1515 analyzer ("make public types internal") still flags those classes in an app
project. Instead of fighting the generator, silence the rule only for code-behind files, so
services and data sources elsewhere are still reported.

```ini
# .editorconfig
[*.razor.cs]
dotnet_diagnostic.CA1515.severity = none
```

---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*