> Today I Learned | Git
 
# Cherry-pick a single commit from another branch

Date: 2026/06/17

## Body

When you want one commit from another branch but not the rest, cherry-pick copies it by
its hash.

```bash
git switch main
git cherry-pick a1b2c3d
```

Git applies that commit's changes on top of the current branch, creating a new commit with
the same message (new hash). The original branch is untouched.

Range works too:

```bash
# inclusive of both ends
git cherry-pick a1b2c3d..f4e5d6c
```

A few things to know:

- Conflicts are resolved like a merge. Use `git cherry-pick --continue` after fixing, or
`--abort` to bail out.

- If you don't want it to commit automatically, add `-n` — this stages the changes and
lets you combine them with others or edit the message.

- Cherry-picking duplicates the change. The same fix now lives on two branches with two
different hashes, and a later merge won't dedupe them. Use it deliberately, not as a
habit.

The common case: a hotfix on `release` that you also need on `main`, without dragging
along the rest of the release branch.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 