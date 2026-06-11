> Today I Learned | Python
 
# Lists are mutable, tuples are not

Date: 2026/06/11

## Body

Both hold a sequence of items, but a list `[...]` can change and a tuple `(...)` cannot.
Pick based on whether the data is meant to change.

```python
colors = ["red", "green", "blue"]   # list
colors.append("yellow")             # ok
colors[0] = "pink"                  # ok

point = (10, 20)                    # tuple
point[0] = 15                       # TypeError
```

A few things follow from that:

- Tuples are slightly faster and use less memory.

- Tuples can be used as dictionary keys or inside a set; lists cannot.

- Returning more than one value from a function actually returns a tuple.

```python
def min_max(values):
    return min(values), max(values)     # returns a tuple

lo, hi = min_max([3, 1, 4, 1, 5])       # unpacking
print(lo, hi)                            # 1 5
```

Rule of thumb: use a list when it **grows** or **changes**, a tuple when the values **belong
together** and stay put (coordinates, RGB, config pairs).
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 