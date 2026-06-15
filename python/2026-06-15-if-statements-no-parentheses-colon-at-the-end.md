> Today I Learned | Python
 
# if statements — no parentheses, colon at the end

Date: 2026/06/15

## Body

Same idea as C#, but Python drops the parentheses and uses a colon to open the block.
Indentation replaces braces.

```python
if score > 90:
    grade = "A"
elif score > 80:       # not "else if"
    grade = "B"
else:
    grade = "C"
```

Two things to note:

- The keyword is `elif`, not `else if`.

- There is no `switch` statement. Use `if/elif/else` or, since 3.10, `match/case`.

```python
match command:
    case "start":
        run()
    case "stop":
        halt()
    case _:            # default
        print("unknown")
```

`Truthy/falsy` values work like you'd expect — `0`, `""`, `[]`, `None` are **falsy**. No need to
write `if len(items) > 0:`; just `if items:`.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 