# Safe Rebase Workflow

Rebase is powerful, but it must be used carefully.

A safe rebase workflow helps you keep a clean history while avoiding accidental loss of work or problems with shared branches.

## Main goal

The goal of a safe rebase workflow is to update your feature branch with the latest changes from `main` without creating unnecessary merge commits.

## Golden rule

```txt
Do not rebase public/shared branches unless your team agreed to it.
```

A shared branch is a branch that other people may have already pulled or used as a base for their own work.

## Safe rebase scenario

A safe scenario is:

```txt
You are working on your own feature branch.
Nobody else is using that branch.
You want to update it with the latest main.
```

Example branch:

```txt
feature/rebase-guide
```

## Unsafe rebase scenario

An unsafe scenario is:

```txt
You rebase main.
You rebase a shared team branch.
You rebase commits that other people already pulled.
You force push without checking.
```

## Before rebasing

Always check your current branch:

```bash
git branch
```

Check your working tree:

```bash
git status
```

Recommended clean state:

```txt
nothing to commit, working tree clean
```

If you have changes, commit or stash them before rebasing.

## Option 1: Commit changes before rebase

```bash
git add .
git commit -m "Save current work"
```

Then rebase.

## Option 2: Stash changes before rebase

```bash
git stash
```

Then rebase.

After rebase:

```bash
git stash pop
```

## Step-by-step safe rebase workflow

### Step 1: Go to main

```bash
git switch main
```

### Step 2: Update main

If you are working with GitHub:

```bash
git pull origin main
```

If you are working only locally and have not pushed anything yet, make sure your local `main` already has the latest merged work.

### Step 3: Go to your feature branch

```bash
git switch feature/rebase-guide
```

### Step 4: Rebase onto main

```bash
git rebase main
```

### Step 5: Resolve conflicts if needed

If conflicts happen:

```bash
git status
```

Resolve the files manually.

Then:

```bash
git add .
git rebase --continue
```

Repeat until the rebase completes.

### Step 6: Review history

```bash
git log --oneline --graph --decorate --all
```

### Step 7: Merge into main

If the rebase completed successfully:

```bash
git switch main
git merge --ff-only feature/rebase-guide
```

This keeps a linear history.

## Full safe workflow example

```bash
git switch main
git pull origin main
git switch feature/rebase-guide
git status
git rebase main
git log --oneline --graph --decorate --all
git switch main
git merge --ff-only feature/rebase-guide
```

If you are not using GitHub yet:

```bash
git switch main
git switch feature/rebase-guide
git status
git rebase main
git log --oneline --graph --decorate --all
git switch main
git merge --ff-only feature/rebase-guide
```

## Safe rebase with conflicts

Start rebase:

```bash
git rebase main
```

Conflict appears:

```txt
CONFLICT (content): Merge conflict in README.md
error: could not apply a1b2c3d... Add README update
```

Check status:

```bash
git status
```

Resolve the file manually.

Stage resolved files:

```bash
git add README.md
```

Continue:

```bash
git rebase --continue
```

If more conflicts appear, repeat the process.

## Abort if something feels wrong

If you are unsure:

```bash
git rebase --abort
```

This returns your branch to the state before the rebase started.

Then check:

```bash
git status
git log --oneline --graph --decorate --all
```

## Safe force push

If your feature branch was already pushed before rebase, a normal push may fail.

Use:

```bash
git push --force-with-lease
```

This is safer than:

```bash
git push --force
```

because it checks whether the remote branch changed unexpectedly.

## When force push is needed

Force push may be needed after rebase because the commit hashes changed.

Before rebase:

```txt
D---E feature
```

After rebase:

```txt
D'---E' feature
```

Since Git sees rewritten commits, the remote history may need to be updated.

## Avoid force push on main

Never force push to `main` unless you are completely sure and your team has a specific reason.

Usually, protected branches like `main` should not allow force push.

## Recommended workflow for personal feature branches

```bash
git switch main
git pull origin main
git switch feature/my-topic
git rebase main
git push --force-with-lease
```

Use this only if the branch was already pushed and needs to be updated remotely.

## Recommended workflow before merging locally

If everything is local:

```bash
git switch main
git switch feature/my-topic
git rebase main
git switch main
git merge --ff-only feature/my-topic
```

Then delete the branch if no longer needed:

```bash
git branch -d feature/my-topic
```

## Safe branch cleanup after rebase and merge

After successful merge:

```bash
git branch -d feature/rebase-guide
```

If the branch exists on GitHub:

```bash
git push origin --delete feature/rebase-guide
```

If deleted remote branches still appear locally:

```bash
git fetch --prune
```

## Checklist before rebase

```txt
Am I on the correct feature branch?
Is my working tree clean?
Is this branch only used by me?
Do I understand which branch I am rebasing onto?
Can I abort if something goes wrong?
```

## Checklist after rebase

```txt
Did the rebase finish successfully?
Did I resolve all conflicts?
Did I check git status?
Did I review git log?
Do I need to force push with --force-with-lease?
Is the branch ready to merge?
```

## Common safe commands

| Command | Purpose |
|---|---|
| `git status` | Check working tree state |
| `git branch` | Check current branch |
| `git rebase main` | Rebase current branch onto `main` |
| `git rebase --continue` | Continue after resolving conflicts |
| `git rebase --abort` | Cancel rebase |
| `git log --oneline --graph --decorate --all` | Review history |
| `git merge --ff-only branch-name` | Merge only if fast-forward is possible |
| `git push --force-with-lease` | Safer force push after rewritten history |

## Common mistakes

### Mistake 1: Rebasing with uncommitted changes

Before rebasing:

```bash
git status
```

If you have changes, commit or stash them first.

### Mistake 2: Rebasing the wrong branch

Always check:

```bash
git branch
```

before running:

```bash
git rebase main
```

### Mistake 3: Rebasing main

Usually avoid:

```bash
git switch main
git rebase feature/my-topic
```

This is not the normal feature branch workflow.

### Mistake 4: Force pushing without checking

Prefer:

```bash
git push --force-with-lease
```

Avoid:

```bash
git push --force
```

### Mistake 5: Continuing after a bad conflict resolution

If the conflict resolution feels wrong, you can abort:

```bash
git rebase --abort
```

Then try again more carefully.

## Best practices

- Rebase only your own feature branches.
- Start from a clean working tree.
- Keep feature branches short-lived.
- Use `git status` often.
- Use `git rebase --abort` when unsure.
- Prefer `--force-with-lease` over `--force`.
- Do not force push to protected branches.
- Review history after rebasing.
- Follow team rules.

## Recommended workflow for this repository

For your documentation project, you can use this flow for each topic branch:

```bash
git switch main
git switch -c feature/rebase-guide
# create or update documentation files
git add docs/05-rebase/
git commit -m "Add rebase documentation"
git switch main
git merge --ff-only feature/rebase-guide
git branch -d feature/rebase-guide
```

If `main` changed before merging:

```bash
git switch feature/rebase-guide
git rebase main
git switch main
git merge --ff-only feature/rebase-guide
```

## Summary

A safe rebase workflow helps keep history clean without risking shared work.

Basic safe flow:

```bash
git switch feature/my-branch
git status
git rebase main
git switch main
git merge --ff-only feature/my-branch
```

If conflicts happen:

```bash
git status
git add .
git rebase --continue
```

If something goes wrong:

```bash
git rebase --abort
```

Golden rule:

```txt
Rebase your own branches. Do not rebase shared branches unless your team agreed.
```

## Recommended next topic

Continue with:

```txt
docs/06-undoing-changes/restore.md
```