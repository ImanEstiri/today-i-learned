> Today I Learned | Python
 
# Read and write files with with

Date: 2026/06/16

## Body

`with` opens a file and closes it for you, even if an exception fires inside the block.
It's the same idea as C#'s `using`.

```python
with open("data.txt", "r", encoding="utf-8") as f:
    text = f.read()          # whole file as one string

with open("data.txt", "r", encoding="utf-8") as f:
    for line in f:           # line by line, memory-friendly
        print(line.rstrip())
```

The mode is the second argument:

- `"r"` — read (default)

- `"w"` — write, truncates the file

- `"a"` — append

- `"x"` — create, fails if it exists

- `"b"` — binary, combine with others (`"rb"`, `"wb"`)

Writing:

```python
with open("out.txt", "w", encoding="utf-8") as f:
    f.write("hello\n")
    f.writelines(["a\n", "b\n"])
```

Two habits worth adopting:

- Always pass `encoding="utf-8"`. The default depends on the OS and causes `UnicodeDecodeError`
on Windows with non-ASCII files.

- Use `pathlib.Path` for paths instead of string concatenation. `Path("dir") / "file.txt"`
handles separators for you.

```python
from pathlib import Path

path = Path("data") / "notes.txt"
text = path.read_text(encoding="utf-8")
path.write_text("hello\n", encoding="utf-8")
```

`Path.read_text` and `write_text` are shortcuts for the whole-file case — no `with` needed.


---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 