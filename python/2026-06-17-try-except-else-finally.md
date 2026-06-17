> Today I Learned | Python
 
# try / except / else / finally

Date: 2026/06/17

## Body

Same idea as C#'s `try/catch/finally`, but Python has an extra `else` block that runs only
if no exception was raised. Useful to keep the risky line and the follow-up line separate.

```python
try:
    value = int(user_input)
except ValueError:
    print("Not a number")
else:
    print(f"Got {value}")     # runs only if no exception
finally:
    print("Done")             # always runs
```

You can catch multiple types and inspect the exception:

```python
try:
    result = 10 / n
except (ZeroDivisionError, TypeError) as e:
    print(f"Failed: {e}")
```

Two rules that keep you out of trouble:

- Never use a bare `except:` — it also swallows `KeyboardInterrupt` and `SystemExit`.
Catch the specific type you expect.

- `finally` runs even if the `try` returns or raises. Use it for cleanup (closing files,
releasing locks).

```python
try:
    f = open("data.txt")
    ...
finally:
    f.close()       # always closes
```

Which is exactly why `with` is preferred — same guarantee, less code.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 