> Today I Learned | Python
 
# zip and enumerate

Date: 2026/06/24

## Body

`enumerate` gives you index and value in one loop. `zip` walks two (or more) iterables in
parallel.

```python
fruits = ["apple", "banana", "cherry"]

for i, fruit in enumerate(fruits):
    print(i, fruit)              # 0 apple, 1 banana, 2 cherry

for i, fruit in enumerate(fruits, start=1):
    print(i, fruit)              # 1 apple, 2 banana, 3 cherry
```

```python
names = ["Iman", "Ali", "Sara"]
ages  = [30, 25, 28]

for name, age in zip(names, ages):
    print(f"{name} is {age}")
```

`zip` stops at the shortest input — extra items are silently dropped. If that's a
surprise, check lengths first or use `itertools.zip_longest`.

`zip` also transposes:

```python
pairs = [(1, "a"), (2, "b")]
nums, letters = zip(*pairs)      # (1, 2), ("a", "b")
```

This replaces most `for i in range(len(xs))` loops.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 