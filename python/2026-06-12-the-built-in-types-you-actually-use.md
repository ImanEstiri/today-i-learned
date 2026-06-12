> Today I Learned | Python
 
# The built-in types you actually use

Date: 2026/06/12

## Body

Coming from C#, the first thing to know is that Python has fewer types and they do more
work. There is no `int` vs `long` vs `short` — just `int`, and it grows as needed.

The types you'll touch every day:

| Python | Closest C# | Notes |
|---|---|---|
| `int` | `int` / `long` / `BigInteger` | One type, arbitrary precision |
| `float` | `double` | 64-bit, no `float`/`decimal` split |
| `bool` | `bool` | `True` / `False` (capitalized) |
| `str` | `string` | Immutable, Unicode by default |
| `bytes` | `byte[]` | Raw binary |
| `None` | `null` | A real object, not a keyword-only value |
| `list` | `List<T>` | Mutable, ordered |
| `tuple` | `(T1, T2, ...)` / `ValueTuple` | Immutable, ordered |
| `set` | `HashSet<T>` | Mutable, unordered, unique |
| `dict` | `Dictionary<K,V>` | Mutable key-value map |

A few things that trip up C# developers:

- There are no unsigned types. If you need bit-level control, use `bytes` or a library.
- `bool` is actually a subclass of `int` — `True == 1` and `False == 0`. Handy sometimes,
  surprising other times.
- `None` is a singleton object of type `NoneType`. `x is None` is the idiomatic check.
- Strings are Unicode. There's no `char` type — a single character is just a `str` of
  length 1.

To check a type at runtime:

```python
type(42)          # <class 'int'>
type("hello")     # <class 'str'>
isinstance(42, int)   # True — preferred over type() == for checks
```
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 