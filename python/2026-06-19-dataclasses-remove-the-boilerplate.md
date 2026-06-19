> Today I Learned | Python
 
# dataclasses remove the boilerplate

Date: 2026/06/19

## Body

The `@dataclass` decorator generates `__init__`, `__repr__`, and `__eq__` from annotated
attributes. It's the closest thing Python has to C# records.

```python
from dataclasses import dataclass

@dataclass
class Point:
    x: int
    y: int

p = Point(10, 20)
print(p)              # Point(x=10, y=20)
print(p == Point(10, 20))   # True
```

Without `@dataclass` you'd write the constructor, the string form, and equality by hand.

Defaults work, but like function arguments, never use a mutable one directly:

```python
from dataclasses import dataclass, field

@dataclass
class Order:
    id: int
    items: list[str] = field(default_factory=list)   # not []
    note: str = ""
```
`field(default_factory=...)` calls the factory per instance — the equivalent of the
`None` trick, but cleaner.

Useful options:

```python
@dataclass(frozen=True)     # immutable, hashable, can be a dict key
@dataclass(slots=True)      # smaller memory footprint, blocks new attributes
@dataclass(kw_only=True)    # all fields must be passed by name
```
`frozen=True` is the one to reach for when the object is really a value — coordinates,
IDs, configs. It pairs well with `slots=True` for small objects created in bulk.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 