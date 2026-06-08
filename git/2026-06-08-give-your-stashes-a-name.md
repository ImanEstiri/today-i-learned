> Today I Learned | Git
 
# Give your stashes a name

Date: 2026/06/08

## Body

`git stash` saves work-in-progress so you can switch branches. But after a few stashes you
end up with `stash@{0}` through `stash@{7}` and no idea what's in each one.

Add `-m` (or `save`) with a message and the list becomes readable:

```bash
git stash push -m "wip: half-done login form"
git stash list
# stash@{0}: On main: wip: half-done login form
# stash@{1}: On main: wip: css grid experiment
```

To apply a specific one without popping it:

```
git stash apply stash@{1}
```
 
Also useful: `git stash -u` includes untracked files (new files Git doesn't know about
yet), which are skipped by default and are easy to forget.

---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 