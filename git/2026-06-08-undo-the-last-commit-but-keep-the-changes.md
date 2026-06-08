> Today I Learned | Git
 
# Undo the last commit but keep the changes

Date: 2026/06/08

## Body

If you committed too early (wrong message, forgot a file), don't panic and don't reach for
`git reset --hard`. Use `--soft` and the commit disappears while the changes stay staged,
ready to commit again.

```bash
git reset --soft HEAD~1
```
Your files are untouched. `git status` shows them as staged, and you can fix whatever was
wrong and commit again.

A quick map of the three modes:

| **Command**                | **Commit** | **Staging area** | **Working files** |
|:---------------------------|:-----------|:-----------------|:------------------|
| `git reset --soft HEAD~1`  | gone       | kept             | kept              |
| `git reset --mixed HEAD~1` | gone       | cleared          | kept              |
| `git reset --hard HEAD~1`  | gone       | cleared          | **lost**          |

`--hard` throws away uncommitted work with no warning. Only use it when you're sure.
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 