> Today I Learned | Python
 
# dict.get and dict.setdefault

Date: 2026/06/19

## Body

Indexing a missing key raises `KeyError`. `.get()` returns a default instead.

```python
user = {"name": "Iman"}

user["age"]              # KeyError
user.get("age")          # None
user.get("age", 0)       # 0
```

Use `.get()` when you expect the key might be missing and you have a sensible fallback.
Use `user["age"]` when the key is required — letting it crash is better than silently
carrying a `None` forward.

`.setdefault` is `.get` plus a write: it returns the value if present, otherwise inserts
the default and returns it.

```python
# counting without setdefault
counts = {}
for word in words:
    if word in counts:
        counts[word] += 1
    else:
        counts[word] = 1

# with setdefault
counts = {}
for word in words:
    counts[word] = counts.get(word, 0) + 1
```

For counting specifically, `collections.Counter` does it in one line:

```python
from collections import Counter
counts = Counter(words)
```

For grouping, `.setdefault` (or `defaultdict`) beats check-then-assign:

```python
by_first = {}
for name in names:
    by_first.setdefault(name[0], []).append(name)
```

`setdefault` evaluates its default argument every call, so for expensive defaults,
`defaultdict` is the better fit.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 