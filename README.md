# Repository Reset Guide

This documentation outlines the process for **purging all commit history** from a Git repository and starting fresh with a single "Initial commit."

> [!CAUTION]
> **WARNING:** This action is destructive and irreversible. It permanently deletes your entire commit history. If you are working in a shared repository, this will break the local history for all collaborators. **Back up your data before proceeding.**

## Prerequisites

* Access to a terminal with Git installed.
* Ensure you are in the root directory of the local repository you wish to reset.
* Verify that you have the necessary permissions to force-push to the remote repository (`origin`).

---

## Step-by-Step Instructions

Follow these commands in order to reset your history:

### 1. Create a New Orphan Branch

Create a temporary branch that carries no history from the previous branch.

```bash
git checkout --orphan temp-branch

```

### 2. Clear the Index

Remove all tracked files from the Git index while keeping the actual files on your hard drive.

```bash
git rm -rf --cached .

```

### 3. Stage and Commit

Add your current files back to the index and create your new starting point.

```bash
git add .
git commit -m "Initial commit"

```

### 4. Replace the Old Branch

Delete the old history-heavy branch (usually `main` or `master`) and rename your current branch to take its place.

```bash
git branch -D main
git branch -m main

```

### 5. Update the Remote

Force-push the new, single-commit history to your remote server.

```bash
git push --force origin main

```

---

## Summary Table

| Action | Command | Purpose |
| --- | --- | --- |
| **Isolate** | `git checkout --orphan` | Starts a fresh timeline. |
| **Reset** | `git rm -rf --cached .` | Unstages all files without deleting them. |
| **Start** | `git commit -m` | Creates the new "Version 1.0." |
| **Overwrite** | `git push --force` | Syncs the fresh start to GitHub/GitLab. |

