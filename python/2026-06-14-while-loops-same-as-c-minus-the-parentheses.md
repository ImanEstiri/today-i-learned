> Today I Learned | Python
 
# while loops — same as C#, minus the parentheses

Date: 2026/06/14

## Body

```python
n = 10
while n > 0:
    print(n)
    n -= 1
```

break and continue work like C#. Python also allows an `else` on the loop that runs
only if the loop finished without break:

```python
n = 10
while n > 0:
    if n == 3:
        break
    n -= 1
else:
    print("finished")   # does NOT run, the loop broke
```

In practice `for` is used far more than `while` in Python, because `for` can iterate over
anything — not just ranges. Reach for `while` only when the exit condition isn't tied to a
collection.

---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 