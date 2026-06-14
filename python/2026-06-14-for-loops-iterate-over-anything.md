> Today I Learned | Python
 
# for loops iterate over anything

Date: 2026/06/14

## Body

Python has only one loop for iteration, and it works on any iterable — not just numbers.

```python
for fruit in ["apple", "banana"]:
    print(fruit)

for ch in "hello":
    print(ch)              # h, e, l, l, o

for key, value in {"a": 1, "b": 2}.items():
    print(key, value)      # a 1, b 2
```

If you need the index, use enumerate. Never for i in range(len(xs)):

```python
for i, fruit in enumerate(["apple", "banana"]):
    print(i, fruit)        # 0 apple, 1 banana
```

range produces numbers on demand — it doesn't build a list, so it's cheap even for huge
counts. Stop is exclusive:

```python
range(5)          # 0, 1, 2, 3, 4
range(2, 5)       # 2, 3, 4
range(0, 10, 2)   # 0, 2, 4, 6, 8
```

A loop can have an else that runs only if it finished without hitting break:

```python
for n in range(2, 10):
    if n % 7 == 0:
        print(f"Found: {n}")
        break
else:
    print("No multiple of 7 found")
```
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 