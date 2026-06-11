> Today I Learned | Python
 
# Indentation is syntax, not style

Date: 2026/06/11

## Body

In most languages, indentation is just for humans — the compiler ignores it and braces
(`{}`) define blocks. In Python, indentation **is** the block. Wrong spacing doesn't just
look bad, it changes what the program does.

```python
# correct — the print is inside the if
if score > 10:
    print("You win")
    print("Nice job")

# still runs, but the second print is now outside the if
if score > 10:
    print("You win")
print("Nice job")   # always runs
```

Rules that matter:

- **Use 4 spaces per level (PEP 8).** Don’t mix tabs and spaces. Python 3 refuses to run files that mix them.
- **A colon (`:`)** at the end of `if`, `for`, `while`, `def`, and `class` opens a new block.
- **Consistent indentation:** Every line inside the block must be indented by the same amount.

If you get `IndentationError: unexpected indent`, the fix is almost always a stray space
or a tab that looks like spaces.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 