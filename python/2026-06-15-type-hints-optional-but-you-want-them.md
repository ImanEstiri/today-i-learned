> Today I Learned | Python
 
# Type hints — optional, but you want them

Date: 2026/06/15

## Body

Python is dynamically typed, but since 3.5 you can annotate types. The interpreter ignores
them at runtime — they exist for tooling (`mypy`, `pyright`) and IDEs.

```python
def greet(name: str, greeting: str = "Hello") -> str:
    return f"{greeting}, {name}!"
```

The `->` is the return type. Nothing enforces it — calling `greet(42)` still runs.

A few built-in generics you'll use daily:

```python
names: list[str] = ["Iman", "Ali"]
ages: dict[str, int] = {"Iman": 30, "Ali": 25}
point: tuple[int, int] = (10, 20)
maybe: str | None = None      # optional, 3.10+
```

Older code uses `Optional[str]` and `List[str]` from `typing` — same meaning, more imports.

For a class or a type not yet defined, wrap it in quotes (forward reference):

```python
def clone(node: "Node") -> "Node":
    ...
```

Coming from C#, hints feel familiar but remember: they're documentation, not enforcement.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 