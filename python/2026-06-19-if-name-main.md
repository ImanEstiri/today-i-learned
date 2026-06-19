> Today I Learned | Python
 
# if __name__ == "__main__"

Date: 2026/06/19

## Body

Every Python file is a module. When you run a file directly, its `__name__` is
`"__main__"`. When the same file is imported by another file, `__name__` is the module's
name. This is how a file can be both importable and runnable.

```python
# greet.py
def hello(name):
    return f"Hello, {name}"

if __name__ == "__main__":
    print(hello("Iman"))
```

- `python greet.py` → prints `Hello, Iman`.

- `import greet` → the `print` does not run. You get the `hello` function only.

Without the guard, importing the module would execute everything at the top level. That
includes any side effect: file I/O, network calls, opening a window.

The C# equivalent is a file with a `Main` method. Python has no entry point by convention
— the entry point is just the file you run, and the guard keeps the rest importable.

A common pattern: keep the real work in functions, and put only the orchestration behind
the guard.

```python
def run():
    ...

if __name__ == "__main__":
    run()
```

This makes the module testable: tests import `run` without triggering it.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 