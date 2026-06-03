> Today I Learned | .NET
 
# IsNullOrEmpty vs IsNullOrWhiteSpace

Date: 2026/06/03

## Body

`string.IsNullOrEmpty` only checks if the string is `null` or `""`. But if the user enters
just spaces (`"   "`), it passes the check and can cause problems later.

`string.IsNullOrWhiteSpace` does the same but also treats spaces, tabs, and newlines as
empty. Almost always what you actually want.

```csharp
string input = "   ";

string.IsNullOrEmpty(input);      // false  ← trouble
string.IsNullOrWhiteSpace(input); // true   ← correct
```
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 