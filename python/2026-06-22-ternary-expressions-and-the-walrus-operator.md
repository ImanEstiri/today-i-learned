> Today I Learned | Python
 
# Ternary expressions and the walrus operator

Date: 2026/06/22

## Body

Python has a one-line `if/else`, same as C#'s ternary but reads in a different order:
`value_if_true if condition else value_if_false`.

```python
label = "adult" if age >= 18 else "minor"
```

No parentheses required, but use them when nesting — deeply nested ternaries are worse
than a plain `if`.

The walrus operator `:=` (Python 3.8+) assigns inside an expression. The classic use is
"compute once, use in the condition":

```python
# without walrus — call twice
while len(data := read_chunk()) > 0:
    process(data)

# or in a comprehension, to avoid computing twice
results = [y for x in xs if (y := transform(x)) is not None]
```

The name comes from the `:=` looking like a walrus. Use it sparingly — outside of these
patterns, an explicit assignment is clearer.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 