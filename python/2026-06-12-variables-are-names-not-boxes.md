> Today I Learned | Python
 
# Variables are names, not boxes

Date: 2026/06/12

## Body

In C#, `int x = 5;` creates a slot that holds the value 5. In Python, `x = 5` binds the
name `x` to an object. The object lives on its own; the name just points to it.

This sounds like a small detail, but it explains almost every "weird" Python behavior.

```python
a = [1, 2, 3]
b = a            # b is another name for the SAME list
b.append(4)
print(a)         # [1, 2, 3, 4] — a changed too
```

To actually copy, you ask for a copy:

```python
b = a.copy()     # shallow copy
b = list(a)      # same thing
b = a[:]         # also the same
```

The same idea applies to function arguments. Python passes references to objects, not
copies. If you mutate the object inside the function, the caller sees it:

```python
def add_item(items):
    items.append("new")

my_list = []
add_item(my_list)
print(my_list)   # ["new"]
```

But if you rebind the name, the caller doesn't see anything:

```python
def replace(items):
    items = ["replaced"]   # new local name, no effect outside

my_list = [1, 2]
replace(my_list)
print(my_list)   # [1, 2]
```

Rule of thumb: assignment never copies. It only makes another name for the same object.
This is one of the biggest mental shifts coming from C#.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 