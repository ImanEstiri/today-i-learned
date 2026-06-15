> Today I Learned | Python
 
# venv and pip — project isolation from day one

Date: 2026/06/15

## Body

Unlike .NET, Python doesn't ship with a project-level package manager built in. The
standard workflow is `venv` (virtual environment) plus `pip`.

A venv is a folder that holds its own Python and its own packages. Activating it means
`pip install` only touches that folder — the global Python stays clean.

```bash
# create once per project
python -m venv .venv

# activate
# Windows (PowerShell)
.venv\Scripts\Activate.ps1
# Windows (cmd)
.venv\Scripts\activate.bat
# macOS / Linux
source .venv/bin/activate
```

Once activated, the prompt shows `(.venv)` and `pip` points inside the venv.

```bash
pip install requests
pip freeze > requirements.txt      # pin current versions
pip install -r requirements.txt    # recreate from the file
```

Two habits worth adopting immediately:

- Always create a venv per project. Mixing global packages leads to version conflicts
you can't reproduce.

- Add `.venv/` to `.gitignore`. Never commit the folder — commit `requirements.txt`
instead.

Unlike NuGet's `packages.config`, Python has no single canonical project file. `venv` +
`requirements.txt` is the portable baseline everyone recognizes.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 