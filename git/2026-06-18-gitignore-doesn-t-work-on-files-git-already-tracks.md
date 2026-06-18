> Today I Learned | Git
 
# .gitignore doesn't work on files Git already tracks

Date: 2026/06/18

## Body

Adding a file to `.gitignore` does nothing if it's already tracked. Git keeps tracking it
because the ignore rules only apply to untracked files.

The symptom: you add `appsettings.Development.json` to `.gitignore`, run `git status`, and
it still shows as modified.

The fix is to remove it from the index while keeping the local file:

```bash
git rm --cached appsettings.Development.json
```

Then commit. The file stays on disk, but Git stops tracking it — and from now on the
`.gitignore` rule applies.

For a whole folder:

```bash
git rm -r --cached bin/ obj/
```

To check whether a file is ignored, without guessing:

```bash
git check-ignore -v appsettings.Development.json
```

The `-v` flag tells you which `.gitignore` line matched, which is handy when you have
nested `.gitignore` files and can't tell who's in charge.
 
---
*Iman Estiri | https://github.com/ImanEstiri/today-i-learned*
 