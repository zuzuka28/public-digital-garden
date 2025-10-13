---
{"dg-publish":true,"permalink":"/notes/organize-resource-it-clean-git-commits-history/","title":"Clean Git Commits History"}
---


1. Checkout/create orphan branch (this branch won't show in `git branch` command):

```bash
git checkout --orphan latest_branch
```

2. Add all the files to the newly created branch:

```bash
git add -A
```

2. Commit the changes:

```bash
git commit -am "commit message"
```

3. Delete `main` (default) branch (this step is permanent):

```bash
git branch -D main
```

4. Rename the current branch to `main`:

```bash
git branch -m main
```

5. Finally, all changes are completed on your local repository, and force update your remote repository:

```bash
git push -f origin main
```

6. Prune to repack unused objects:

```bash
git gc --aggressive --prune=all
```
