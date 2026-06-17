# Rebase Example

This example shows how to use `git rebase` to update a feature branch with the latest changes from `main`.

Rebase is useful when you want a clean, linear history.

## Scenario

You are working on this branch:

```txt
feature/rebase-guide
```

While you were working, `main` received new commits.

You want your feature branch to be based on the latest version of `main`.

## Goal

The goal is to practice this workflow:

```txt
Update main → Rebase feature branch onto main → Resolve conflicts if needed → Fast-forward merge
```

## Initial history

Before rebase, history may look like this:

```txt
A---B---C main
     \
      D---E feature/rebase-guide
```

The feature branch started from commit `B`.

Then `main` advanced to commit `C`.

## Desired result

After rebase:

```txt
A---B---C main
         \
          D'---E' feature/rebase-guide
```

The feature commits are replayed on top of the latest `main`.

## Step 1: Check status

```bash
git status
```

Recommended output:

```txt
nothing to commit, working tree clean
```

If you have uncommitted changes, commit or stash them before rebasing.

## Step 2: Go to main

```bash
git switch main
```

If using GitHub:

```bash
git pull origin main
```

If working locally only, make sure your local `main` already contains the latest merged work.

## Step 3: Switch to feature branch

```bash
git switch feature/rebase-guide
```

## Step 4: Rebase onto main

```bash
git rebase main
```

If there are no conflicts, Git completes the rebase.

Example output:

```txt
Successfully rebased and updated refs/heads/feature/rebase-guide.
```

## Step 5: Review history

```bash
git log --oneline --graph --decorate --all
```

Example output:

```txt
* e5f6g7h (HEAD -> feature/rebase-guide) Add safe rebase workflow
* d4e5f6g Add interactive rebase documentation
* c3d4e5f (main) Add merge conflict documentation
* b2c3d4e Add branch documentation
* a1b2c3d Add README
```

This shows the feature commits on top of `main`.

## Step 6: Merge into main with fast-forward

```bash
git switch main
git merge --ff-only feature/rebase-guide
```

Example output:

```txt
Updating c3d4e5f..e5f6g7h
Fast-forward
```

## Step 7: Delete branch after merge

```bash
git branch -d feature/rebase-guide
```

## Full successful rebase workflow

```bash
git status
git switch main
git pull origin main
git switch feature/rebase-guide
git rebase main
git log --oneline --graph --decorate --all
git switch main
git merge --ff-only feature/rebase-guide
git branch -d feature/rebase-guide
```

## Local-only version

If you have not pushed to GitHub yet:

```bash
git status
git switch main
git switch feature/rebase-guide
git rebase main
git switch main
git merge --ff-only feature/rebase-guide
git branch -d feature/rebase-guide
```

## Rebase with conflicts

Sometimes rebase causes conflicts.

Example output:

```txt
CONFLICT (content): Merge conflict in README.md
error: could not apply d4e5f6g... Add rebase documentation
```

## Step 1: Check status

```bash
git status
```

Example output:

```txt
interactive rebase in progress
Unmerged paths:
  both modified: README.md
```

## Step 2: Resolve the file

Open the conflicted file.

Example conflict:

```md
<<<<<<< HEAD
# Complete Git Commands Guide
=======
# Rebase Guide
>>>>>>> d4e5f6g
```

Edit it to the final version:

```md
# Complete Git Commands Guide

This section explains how to use rebase safely.
```

Remove all conflict markers.

## Step 3: Stage resolved file

```bash
git add README.md
```

## Step 4: Continue rebase

```bash
git rebase --continue
```

If another conflict appears, repeat:

```bash
git status
# resolve conflict
git add .
git rebase --continue
```

## Abort rebase

If something feels wrong:

```bash
git rebase --abort
```

This returns the branch to the state before the rebase started.

## Rebase conflict workflow

```bash
git rebase main
git status

# resolve conflicts manually

git add .
git rebase --continue
```

Abort:

```bash
git rebase --abort
```

## Force push after rebase

If the feature branch was already pushed before the rebase, a normal push may fail.

Use:

```bash
git push --force-with-lease
```

Avoid:

```bash
git push --force
```

unless you fully understand the risk.

## Important warning

Rebase rewrites commit history.

Do not rebase shared branches unless your team agreed to it.

Safe:

```txt
Rebasing your own local feature branch.
```

Risky:

```txt
Rebasing a branch other people are using.
```

## Common mistake: rebasing main

Avoid this:

```bash
git switch main
git rebase feature/rebase-guide
```

Usually, you want:

```bash
git switch feature/rebase-guide
git rebase main
```

## Common mistake: rebasing with uncommitted changes

Before rebase:

```bash
git status
```

If needed:

```bash
git stash push -m "Temporary changes before rebase"
```

After rebase:

```bash
git stash pop
```

## Common mistake: force pushing carelessly

Prefer:

```bash
git push --force-with-lease
```

This is safer than:

```bash
git push --force
```

## Rebase checklist

Before rebase:

```txt
Am I on the correct feature branch?
Is my working tree clean?
Is this branch only used by me?
Do I know which branch I am rebasing onto?
```

After rebase:

```txt
Did the rebase finish successfully?
Did I resolve all conflicts?
Did I review the history?
Do I need to force push safely?
Is the branch ready to merge?
```

## Summary

Basic rebase workflow:

```bash
git switch feature/my-topic
git rebase main
git switch main
git merge --ff-only feature/my-topic
```

If conflicts happen:

```bash
git status
git add .
git rebase --continue
```

Abort if needed:

```bash
git rebase --abort
```

Golden rule:

```txt
Rebase your own branches, not shared history.
```