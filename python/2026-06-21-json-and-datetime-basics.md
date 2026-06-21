> Today I Learned | Python
 
# json and datetime basics

Date: 2026/06/21

## Body

`json` is in the standard library — no install needed.

```python
import json

data = {"name": "Iman", "age": 30, "tags": ["a", "b"]}

text = json.dumps(data)              # dict → string
back = json.loads(text)              # string → dict

# files
with open("data.json", "w", encoding="utf-8") as f:
    json.dump(data, f, indent=2)

with open("data.json", encoding="utf-8") as f:
    data = json.load(f)
```

`dumps`/`loads` for strings, `dump`/`load` for files (no `s`).

`datetime`:

```python
from datetime import datetime, date, timedelta

now = datetime.now()                          # naive, local
utc = datetime.now(timezone.utc)              # aware, UTC — prefer this
today = date.today()                          # date only

iso = now.isoformat()                         # "2026-06-21T14:30:00"
parsed = datetime.fromisoformat("2026-06-21T14:30:00")

later = now + timedelta(days=7)
```

For anything that crosses time zones or gets stored, use aware datetimes
(`timezone.utc`). Naive datetimes silently drift.

`json` can't `serialize` datetime directly — convert with `isoformat()` first.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 