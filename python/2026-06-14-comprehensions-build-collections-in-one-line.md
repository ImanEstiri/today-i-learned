> Today I Learned | Python
 
# Comprehensions build collections in one line

Date: 2026/06/14

## Body

A comprehension is the Pythonic way to build a collection from a loop.

```python
# loop way
squares = []
for n in range(10):
    squares.append(n * n)

# comprehension way
squares = [n * n for n in range(10)]
```

Add if at the end to filter:

```python
evens = [n for n in range(20) if n % 2 == 0]
```

`if/else` goes before the `for` — it transforms instead of filtering:

```python
labels = ["even" if n % 2 == 0 else "odd" for n in range(6)]
```

The same syntax works for dicts and sets:

```python
lengths = {w: len(w) for w in ["apple", "fig"]}   # {"apple": 5, "fig": 3}
initials = {w[0] for w in ["apple", "fig"]}       # {"a", "f"}
```

Use a generator expression `(...)` when you don't need the list — it yields items lazily:

```python
total = sum(n * n for n in range(1_000_000))
```

Rule of thumb: comprehension for building a collection, plain loop for side effects
(printing, writing, calling APIs).
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 