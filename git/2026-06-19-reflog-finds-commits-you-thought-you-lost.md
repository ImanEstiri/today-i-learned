> Today I Learned | Git
 
# reflog finds commits you thought you lost

Date: 2026/06/19

## Body

`git reflog` records every position `HEAD` has pointed to — including after a reset, a
rebase, or a deleted branch. It's the safety net for "I lost my commit."

```bash
git reflog
# a1b2c3d HEAD@{0}: reset: moving to HEAD~1
# f4e5d6c HEAD@{1}: commit: feat: the work I thought I lost
# 9a8b7c6 HEAD@{2}: checkout: moving from main to feature
```

To get that commit back, branch off it:

```bash
git branch rescue f4e5d6c
```

The reflog is local-only and expires after ~90 days by default. It's not a backup — it
only helps while the objects are still in `.git`. But for "oops, wrong reset" it's a
lifesaver.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 