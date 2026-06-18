> Today I Learned | Git
 
# Fix the last commit message without touching the files

Date: 2026/06/18

## Body

Typo in your last commit message? `--amend` reopens it without changing anything else.

```bash
git commit --amend -m "correct message"
```

If you don't pass `-m`, Git opens the editor with the old message so you can edit it. No
files are re-added — only the message and committer date change.

Since amend rewrites the commit, the hash changes. That's fine locally, but if you already
pushed, you need to force:

```bash
git push --force-with-lease
```

Never amend a commit others have pulled. On a shared branch, prefer a new commit like
`fix: correct typo in previous message`. Rewriting public history forces everyone to
re-sync and can lose their work.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 