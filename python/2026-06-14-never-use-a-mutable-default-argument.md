> Today I Learned | Python
 
# Never use a mutable default argument

Date: 2026/06/14

## Body

Default values are evaluated **once**, when the function is defined — not on every call. So
a default like `[]` or `{}` is shared across all calls, and mutations stick around.

```python
def add_tag(tag, tags=[]):    # danger
    tags.append(tag)
    return tags

add_tag("a")    # ["a"]
add_tag("b")    # ["a", "b"]  ← surprise
```

The fix is the standard Python idiom — use `None` as the sentinel:

```python
def add_tag(tag, tags=None):
    if tags is None:
        tags = []
    tags.append(tag)
    return tags
```

This rule applies to every mutable default: `[]`, `{}`, `set()`, and any custom object.
Immutable defaults like `0`, `""`, `None`, and `tuples` are fine.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 