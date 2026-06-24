> Today I Learned | Python
 
# sorted() vs list.sort()

Date: 2026/06/24

## Body

`sorted()` returns a **new** list and works on any iterable. `list.sort()` sorts **in
place** and returns `None` — a classic gotcha.

```python
nums = [3, 1, 2]

# new list, original untouched
asc = sorted(nums)          # [1, 2, 3]
print(nums)                 # [3, 1, 2]

# in place, returns None
result = nums.sort()        # nums is now [1, 2, 3]
print(result)               # None  ← don't assign
```

Both accept `reverse=True` and `key=`:

```python
words = ["banana", "fig", "apple"]
sorted(words, key=len)                  # ["fig", "apple", "banana"]
sorted(words, key=str.lower, reverse=True)
```

`sorted()` works on tuples, sets, dicts, and generators. `list.sort()` only exists on
lists. Rule: `sorted()` when you want a new list, `.sort()` when you own the list and
want to save memory.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 