> Today I Learned | Python
 
# f-strings are the default way to format text

Date: 2026/06/10

## Body

Since Python 3.6, f-strings are the cleanest way to put values inside a string. You prefix
the string with `f` and drop the variable inside `{}` — no `+`, no `.format()`, no `%`.

```python
name = "Iman"
count = 3

# old style
print("Hello " + name + ", you have " + str(count) + " messages")

# f-string
print(f"Hello {name}, you have {count} messages")
```

Anything inside `{}` is real Python, not just a variable name. You can call functions,
do math, format numbers, and access items:

```python
price = 1234.5678
print(f"Total: {price:.2f}")          # Total: 1234.57
print(f"Name: {name.upper()}")        # Name: IMAN
print(f"Double: {count * 2}")         # Double: 6
```

Use single or double quotes freely — the `f` prefix doesn't change anything about the
string itself.

---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 