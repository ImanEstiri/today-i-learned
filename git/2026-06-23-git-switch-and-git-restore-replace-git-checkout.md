> Today I Learned | Git
 
# git switch and git restore replace git checkout

Date: 2026/06/23

## Body

`git checkout` does too many things — switch branches, restore files, detach HEAD. Since
Git 2.23 there are two focused commands that are easier to read and safer to type.

```bash
# switch branches
git switch main
git switch -c feature/login      # create + switch (was checkout -b)

# restore a file to the last committed version
git restore appsettings.json

# unstage a file, keep the changes
git restore --staged appsettings.json
```

Why it matters: `git checkout -- file` silently discards local changes. `git restore`
makes the intent explicit, and `git switch` can't accidentally wipe a file because it only
moves branches.

`git checkout` still works — it's not deprecated — but `switch`/`restore` is what
`git help` shows first now, and what you'll see in modern guides.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 