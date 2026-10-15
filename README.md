# Git Workflow

![jerry](Images/bd.jpg "A birthday card")

This README documents the Git commands used in this repository, organized by the
task each group of commands performed. The commands are kept in the order they
were run.

## 1. Initialize the repository and publish `main`

Create the local repository, connect it to GitHub, rename the initial branch to
`main`, and make and publish the first commit.

```bash
git init
git remote add origin git@github.com:Abdalla194/proj2.git
git branch -M main
git add .
git commit -m "commit 1"
git branch
git push -u origin main
```

## 2. Create feature branches and publish their commits

Create the `dev` and `test` branches, make one commit on each, then push both
branches to the remote repository and set up upstream tracking.

```bash
git branch dev
git branch test
git switch dev
git add .
git commit -m "commit 2"
git switch test
git add .
git commit -m "commit 3"
git switch main
git push -u origin dev
git push -u origin test
```

## 3. Merge the feature branches into `main`

Switch to `main`, merge in the work from both branches, and push the updated
branch to GitHub.

```bash
git switch main
git merge dev
git merge test
git push -u origin main
```

## 4. Temporarily save and restore work with stash

Stash the working changes on `dev` so branches can be switched, then apply the
stashed changes back on `dev`.

```bash
git switch dev
git stash
git switch test
git switch dev
git stash pop
```

## 5. Delete the feature branches

Switch back to `main` and delete the merged local branches. The first remote
deletion command was attempted without naming the remote and failed; the next
two commands correctly delete the remote branches from `origin`.

```bash
git switch main
git branch -d dev
git branch -d test
git push --delete dev
git push origin --delete dev
git push origin --delete test
```

## 6. Create, publish, and delete a version tag

Create the annotated `v1.7` tag, push it to GitHub, list local tags, then remove
the tag locally and from the remote.

```bash
git tag -a v1.7 -m "Version 1.7"
git push origin v1.7
git push origin --tags
git tag
git tag -d v1.7
git push origin --delete v1.7
```

## 7. Add project files and publish later commits

Stage project changes, create commits 4 through 7, and push the commits on
`main`. The first attempt to create commit 6 had no staged changes, so Git
reported that there was nothing to commit; the next staging and commit commands
created it.

```bash
git add README.md images/bd.jpg
git commit -m "commit 4"
git push origin main
git add .
git commit -m "commit 5"
git push origin main
git add README.md images/bd.jpg
git commit -m "commit 6"
git add .
git commit -m "commit 6"
git push origin main
git add .
git commit -m "commit 7"
git push origin main
```
