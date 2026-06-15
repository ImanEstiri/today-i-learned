> Today I Learned | Python
 
# *args and **kwargs

Date: 2026/06/15

## Body

`*args` collects extra positional arguments into a tuple. `**kwargs` collects extra keyword
arguments into a dict. The names are convention — the `*` is what matters.

```python
def total(*numbers):
    return sum(numbers)

total(1, 2, 3)          # 6
total(1, 2, 3, 4, 5)    # 15
python
def describe(**info):
    for key, value in info.items():
        print(f"{key} = {value}")

describe(name="Iman", age=30)
# name = Iman
# age = 30
```

Order in the signature: positional, *args, keyword-only, **kwargs.

```python
def log(level, *messages, sep=" | ", **context):
    text = sep.join(str(m) for m in messages)
    print(f"[{level}] {text}", context)
```

The same `*` and `**` also work when calling — unpacking a list or dict into arguments:

```python
nums = [1, 2, 3]
total(*nums)              # same as total(1, 2, 3)

data = {"name": "Iman", "age": 30}
describe(**data)          # same as describe(name="Iman", age=30)
```

This is how you forward arguments from one function to another without spelling them out.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 