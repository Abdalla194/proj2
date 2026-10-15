![jerry](Images/bd.jpg "A birthday card")
# ⚡ Git & GitHub — Repository Workflow

<p align="center">
  <img src="https://img.shields.io/badge/Git-Version_Control-F05032?style=for-the-badge&logo=git&logoColor=white" alt="Git Version Control" />
  <img src="https://img.shields.io/badge/GitHub-Remote_Repository-181717?style=for-the-badge&logo=github&logoColor=white" alt="GitHub Repository" />
  <img src="https://img.shields.io/badge/Status-Workflow_Documented-2ea44f?style=for-the-badge" alt="Workflow Documented" />
</p>

<p align="center">
  <b>From the first commit to branch management, merging, stashing, and version tagging.</b>
  <br />
  A hands-on journey through the essential Git commands used to manage and publish a repository.
</p>

---

## 🚀 About This Repository

This repository documents a practical Git and GitHub workflow, covering the process of initializing a repository, managing branches, merging changes, temporarily saving work, creating version tags, and publishing commits to a remote repository.

Instead of simply listing commands, this README follows the **actual order in which the commands were executed**, including failed attempts and corrections along the way.

### 🧭 Workflow Overview

| # | Task | What You'll Learn |
|---|---|---|
| 01 | 🏁 Repository Setup | Initialize Git and connect GitHub |
| 02 | 🌿 Branch Management | Create branches and publish commits |
| 03 | 🔀 Merging | Integrate feature branches into `main` |
| 04 | 📦 Stashing | Temporarily save and restore changes |
| 05 | 🧹 Branch Cleanup | Delete local and remote branches |
| 06 | 🏷️ Version Tagging | Create, publish, and remove tags |
| 07 | 📤 Publishing Updates | Commit project files and push changes |

---

## 🏁 01 — Initialize the Repository

**Goal:** Start tracking the project with Git and publish the first commit to GitHub.

Initialize the repository, connect it to the remote GitHub repository, rename the initial branch to `main`, and publish the first commit.

```bash
git init
git remote add origin git@github.com:Abdalla194/proj2.git
git branch -M main
git add .
git commit -m "commit 1"
git branch
git push -u origin main
```

**Key takeaway:** `git push -u origin main` publishes the branch and establishes upstream tracking, making future pushes simpler.

---

## 🌿 02 — Create and Publish Feature Branches

**Goal:** Separate development work into independent branches.

Create the `dev` and `test` branches, switch between them, create commits, and publish both branches to GitHub.

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

**Why it matters:** Branches let you work on separate features or experiments without making every change directly on `main`.

---

## 🔀 03 — Merge Changes into Main

**Goal:** Bring the work from both feature branches into the main branch.

```bash
git switch main
git merge dev
git merge test
git push -u origin main
```

After switching to `main`, merge `dev` and `test` sequentially, then push the updated branch to GitHub.

> 💡 **Remember:** A merge can produce conflicts when different changes affect the same parts of a file. Resolve those conflicts before completing the merge.

---

## 📦 04 — Stash and Restore Your Work

**Goal:** Temporarily put working changes aside so you can switch branches.

```bash
git switch dev
git stash
git switch test
git switch dev
git stash pop
```

Here's what happens:

- `git stash` — saves eligible uncommitted changes temporarily.
- `git switch test` — moves to the test branch.
- `git switch dev` — returns to development.
- `git stash pop` — reapplies the saved changes and removes that stash entry if the application succeeds.

**Pro tip:** Use `git stash list` to inspect your saved stashes before restoring them.

---

## 🧹 05 — Clean Up Merged Branches

**Goal:** Remove feature branches that are no longer needed.

First, return to `main` and delete the local branches. Then remove their remote counterparts.

```bash
git switch main
git branch -d dev
git branch -d test
git push --delete dev
git push origin --delete dev
git push origin --delete test
```

The first remote deletion attempt, `git push --delete dev`, was unsuccessful because it omitted the remote name. The corrected commands specify `origin`.

**Git distinction:**
- `git branch -d` deletes a local branch, provided Git considers it safely merged.
- `git push origin --delete dev` deletes the remote branch named `dev`.

---

## 🏷️ 06 — Create and Manage a Version Tag

**Goal:** Mark a specific point in the repository's history with a version identifier.

Create an annotated tag named `v1.7`, publish it, inspect the local tags, and then remove it locally and remotely.

```bash
git tag -a v1.7 -m "Version 1.7"
git push origin v1.7
git push origin --tags
git tag
git tag -d v1.7
git push origin --delete v1.7
```

**Why tags matter:** Tags identify important milestones, such as releases and stable versions, making them easier to locate later.

> ⚠️ The tag is deleted at the end of this sequence. If `v1.7` is intended to represent a permanent release, keep it instead of running the deletion commands.

---

## 📤 07 — Add Project Files and Publish Updates

**Goal:** Track changes to the project, create commits, and push them to GitHub.

### Commit 4

```bash
git add README.md images/bd.jpg
git commit -m "commit 4"
git push origin main
```

### Commit 5

```bash
git add .
git commit -m "commit 5"
git push origin main
```

### Commit 6 — First Attempt and Correction

```bash
git add README.md images/bd.jpg
git commit -m "commit 6"
git add .
git commit -m "commit 6"
git push origin main
```

The first attempt to create commit 6 did not have staged changes, so Git reported that there was nothing to commit. The subsequent `git add .` and commit command created the commit.

**Note:** Git does not create an empty commit by default. If there are no staged changes, `git commit` normally reports that there is nothing to commit.

### Commit 7

```bash
git add .
git commit -m "commit 7"
git push origin main
```

Each successful push publishes the latest commits on `main` to the remote repository.

---

## 🧠 Git Command Cheat Sheet

| Command | Purpose |
|---|---|
| `git init` | Initialize a repository |
| `git status` | Check the current working tree |
| `git add .` | Stage changes in the current directory |
| `git commit -m "message"` | Create a commit |
| `git branch` | List local branches |
| `git switch branch-name` | Switch branches |
| `git merge branch-name` | Merge another branch into the current branch |
| `git stash` | Temporarily save eligible uncommitted changes |
| `git stash pop` | Reapply and remove the latest stash entry when successful |
| `git branch -d branch-name` | Delete a local branch safely |
| `git push -u origin branch-name` | Push a branch and establish upstream tracking |
| `git tag -a v1.0 -m "message"` | Create an annotated tag |
| `git push origin --tags` | Push local tags to the remote |

---

## 🎯 Final Takeaway

This workflow demonstrates the core Git operations used in everyday development: **initialization, branching, committing, merging, stashing, cleanup, tagging, and remote synchronization.**

Understanding not just the commands, but also their effects on the working tree, commit history, local branches, and remote repository, is what makes Git a powerful version-control tool.

<p align="center">
  <b>Build. Commit. Merge. Ship. 🚀</b>
</p>

