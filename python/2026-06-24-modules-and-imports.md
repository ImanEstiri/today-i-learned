> Today I Learned | Python
 
# Modules and imports

Date: 2026/06/24

## Body

Every `.py` file is a module. Importing it runs the file once, then caches it — the same
import later returns the cached version.

```python
import math                     # whole module
print(math.sqrt(16))

from math import sqrt, pi       # specific names
print(sqrt(16))

import numpy as np              # alias
from pathlib import Path as P
```

Three forms:

- `import x` — you call x.thing.

- `from x import y` — you call `y` directly.

- `import x as y` — alias.

`from x import *` (wildcard) is discouraged — it pollutes the namespace and hides where
names come from. Use explicit imports.

Packages are folders with `__init__.py`. The package name is the folder; imports use dots:

```python
from myapp.services import users
users.create("Iman")
```

Local imports resolve from the current working directory and from `sys.path`. That's
why running `python script.py` from a different folder can break imports — use a package
layout (`python -m myapp.script`) or an installed package to avoid it.

Standard library is huge — check `dir(module)` and `help(module.func)` before pulling a
dependency.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 