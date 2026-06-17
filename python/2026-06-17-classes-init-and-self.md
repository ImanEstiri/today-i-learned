> Today I Learned | Python
 
# Classes: __init__ and self

Date: 2026/06/17

## Body

A Python class is closer to a C# class than you'd expect, but the syntax surprises on
first contact. The constructor is `__init__`, and every instance method takes `self` as
its first parameter — explicitly.

```python
class User:
    def __init__(self, name: str, age: int):
        self.name = name
        self.age = age

    def greet(self) -> str:
        return f"Hi, I'm {self.name}"

u = User("Iman", 30)
print(u.greet())          # Hi, I'm Iman
```

There's no `this` keyword — you pass `self` yourself. Python supplies it automatically when
you call the method on an instance, so `u.greet()` is really `User.greet(u)`.

`__init__` is not a constructor in the C# sense. The object is already created by the time
it runs; `__init__` just fills it in. (There's also `__new__` for the rare case you need to
control creation — almost never.)

Adding a readable string form is `__str__`:

```python
class User:
    def __init__(self, name): self.name = name
    def __str__(self): return f"User({self.name})"
```

Instance attributes don't need to be declared up front — assigning `self.x = ...` is
enough. But IDE and type checkers are happier if you annotate them:

```python
class User:
    name: str
    age: int
```

Two notes for C# devs:

- Python has no `private`/`public`. By convention, a leading underscore (`_name`) means
"internal use" — the language doesn't enforce it.

- There's no method overloading. Same name means the last definition wins.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 