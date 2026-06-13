> Today I Learned | Python
 
# Mutable vs immutable — the split that matters

Date: 2026/06/13

## Body

Every Python type is either mutable (you can change it in place) or immutable (you can't,
you can only rebind the name to a new object).

Immutable: `int`, `float`, `bool`, `str`, `tuple`, `frozenset`, `bytes`.
Mutable: `list`, `set`, `dict`, and most objects you define yourself.

```python
# strings are immutable — this creates a NEW string
s = "hello"
s = s.upper()      # "HELLO"
s[0] = "H"         # TypeError: 'str' object does not support item assignment

# lists are mutable — this changes the list in place
nums = [1, 2, 3]
nums.append(4)     # [1, 2, 3, 4]
nums[0] = 99       # [99, 2, 3, 4]
```

Why this matters — the classic trap:

```python
def add_tag(tag, tags=[]):    # DANGER: default argument is created once
    tags.append(tag)
    return tags

add_tag("a")    # ["a"]
add_tag("b")    # ["a", "b"]  ← surprise! The list persisted
```
The default `[]` is created when the function is defined, not each call. The fix is the
universal Python idiom:

```python
def add_tag(tag, tags=None):
    if tags is None:
        tags = []
    tags.append(tag)
    return tags
```

Use `None` as the default for anything mutable. It's a rule you'll see in every serious
Python codebase.

**Quick reference:**

| **Type**                | **Mutable** | **Can be a dict key?** |
|:------------------------|:------------|:-----------------------|
| `int`, `float`, `bool`  | No          | Yes                    |
| `str`                   | No          | Yes                    |
| `tuple` (of immutables) | No          | Yes                    |
| `frozenset`             | No          | Yes                    |
| `list`                  | Yes         | No                     |
| `set`                   | Yes         | No                     |
| `dict`                  | Yes         | No                     |

Dictionary keys must be hashable, and hashable means immutable in practice. That's why a
`list` can't be a key but a `tuple` can.

---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 