> Today I Learned | .NET
 
# Use var when the type is obvious, not when it hides it

Date: 2026/06/08

## Body

`var` is fine when the right-hand side makes the type clear. It's a problem when it
doesn't — the reader has to hunt for the type or open the method to find out.

```csharp
// clear — no doubt what these are
var name = "Iman";
var count = 42;
var order = new Order();
var items = new List<Order>();

// unclear — what type is this? What does the method return?
var x = GetSomething();
var result = Process(data);
var config = Load();
```

Rule of thumb: if the type isn't obvious from the right side, write it out. Your future
self (and reviewers) will thank you.

```
// better
OrderSummary result = Process(data);
AppConfig config = Load();
``` 

Nothing here is a compiler rule — it's a readability habit. The compiler doesn't care
either way.

---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 