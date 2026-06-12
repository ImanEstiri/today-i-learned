> Today I Learned | Python
 
# The four collection types and when to use each

Date: 2026/06/12

## Body

Python has four built-in collections. Picking the right one is the first design decision
you make, and each has a clear job.

```python
# list — ordered, mutable, allows duplicates
fruits = ["apple", "banana", "apple"]
fruits.append("cherry")
fruits[0] = "pear"

# tuple — ordered, immutable, allows duplicates
point = (10, 20)
rgb = (255, 128, 0)

# set — unordered, mutable, no duplicates
tags = {"python", "csharp", "python"}   # {"python", "csharp"}
tags.add("sql")

# dict — key-value map, keys unique, ordered since 3.7
user = {"name": "Iman", "age": 30}
user["email"] = "iman@example.com"
```

How to choose:

- **list →** a sequence you'll change: rows, items, results.

- **tuple →** a fixed group: coordinates, RGB, a row from the database, returning multiple
values from a function.

- **set →** membership tests and uniqueness: tags, IDs already seen, "is this in the list?"

- **dict →** anything you'd look up by a key: config, JSON, caches, counting.

The syntax is worth memorizing because it's everywhere:

```python
empty_list  = []
empty_tuple = ()
empty_set   = set()    # NOT {} — that's an empty dict
empty_dict  = {}
```

That `{}` trap catches everyone once. `{}` is an empty dict, not an empty set.

A set is dramatically faster than a list for membership checks:

```python
big_list = list(range(1_000_000))
big_set  = set(big_list)

# 0.00001 seconds
999_999 in big_set

# 0.01 seconds — a thousand times slower
999_999 in big_list
```

Rule of thumb: if you find yourself writing `if x in some_list` in a loop, and the list is
big, switch to a set.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 