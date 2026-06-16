# Merge Basics

A merge is the process of combining changes from one branch into another.

Merging is one of the most common operations in Git because developers usually work on separate branches and later integrate their changes into a main branch.

## What is a merge?

A merge takes the changes from one branch and applies them to another branch.

Example:

```txt
feature/remote-repositories → main
```

This means the work created in `feature/remote-repositories` will be integrated into `main`.

## Why merging is useful

Merging allows teams to:

- Combine completed work.
- Integrate feature branches.
- Keep the main branch updated.
- Bring changes from `main` into a feature branch.
- Collaborate without working directly on the same branch.
- Preserve the history of how work was integrated.

## Basic merge syntax

```bash
git merge branch-name
```

Important:

```txt
Git merges the specified branch into your current branch.
```

So before merging, always check which branch you are currently on.

## Check current branch before merging

```bash
git branch
```

Example:

```txt
* main
  feature/remote-repositories
```

The `*` means you are currently on `main`.

If you run:

```bash
git merge feature/remote-repositories
```

Git will merge `feature/remote-repositories` into `main`.

## Basic merge example

```bash
git switch main
git merge feature/remote-repositories
```

This means:

```txt
Move to main.
Merge feature/remote-repositories into main.
```

## Common feature branch merge workflow

```bash
git switch main
git status
git merge feature/remote-repositories
```

After the merge:

```bash
git status
git log --oneline --graph --decorate --all
```

## Merge direction matters

This command:

```bash
git switch main
git merge feature/remote-repositories
```

means:

```txt
Merge feature/remote-repositories into main.
```

But this command:

```bash
git switch feature/remote-repositories
git merge main
```

means:

```txt
Merge main into feature/remote-repositories.
```

Both are valid, but they are used for different purposes.

## Merge feature branch into main

Use this when your feature is complete.

```bash
git switch main
git merge feature/remote-repositories
```

## Merge main into feature branch

Use this when you want to update your feature branch with the latest changes from `main`.

```bash
git switch feature/remote-repositories
git merge main
```

## Fast-forward merge

A fast-forward merge happens when the target branch has not changed since the feature branch was created.

Example before merge:

```txt
A---B main
     \
      C---D feature
```

If `main` has no new commits after `B`, Git can move `main` forward to `D`.

After fast-forward merge:

```txt
A---B---C---D main
```

Command:

```bash
git switch main
git merge feature
```

## Merge commit

A merge commit happens when both branches have new commits.

Example before merge:

```txt
A---B---C main
     \
      D---E feature
```

After merge:

```txt
A---B---C------M main
     \        /
      D---E feature
```

`M` is the merge commit.

## Fast-forward vs merge commit

| Type | What happens |
|---|---|
| Fast-forward merge | Git moves the branch pointer forward |
| Merge commit | Git creates a new commit that combines two histories |

## Force a merge commit

Sometimes teams prefer to always create a merge commit to preserve branch history.

Use:

```bash
git merge --no-ff branch-name
```

Example:

```bash
git switch main
git merge --no-ff feature/remote-repositories
```

The `--no-ff` option means:

```txt
Do not fast-forward. Create a merge commit even if fast-forward is possible.
```

## Only allow fast-forward merge

If you only want to merge when a fast-forward is possible:

```bash
git merge --ff-only branch-name
```

Example:

```bash
git merge --ff-only feature/remote-repositories
```

If Git cannot fast-forward, the merge will fail.

## Merge with a commit message

You can provide a merge commit message:

```bash
git merge --no-ff feature/remote-repositories -m "Merge remote repositories guide"
```

This is useful when you want a clear merge history.

## Check merge result

After merging, check:

```bash
git status
```

You should see something like:

```txt
On branch main
nothing to commit, working tree clean
```

Then check history:

```bash
git log --oneline --graph --decorate --all
```

## Push after merging

If you are working with a remote repository, push the updated branch.

Example:

```bash
git push origin main
```

If you have not pushed yet and everything is local, you can wait until your project is ready.

## Delete branch after merge

After a branch is merged and no longer needed, you can delete it locally.

```bash
git branch -d feature/remote-repositories
```

Use `-d` because it is safer. Git will prevent deletion if the branch has not been merged.

## Merge workflow for this repository

Example:

```bash
git switch main
git status
git merge feature/remote-repositories
git log --oneline --graph --decorate --all
git branch -d feature/remote-repositories
```

If you are not ready to delete the branch, you can keep it.

## Common merge commands

| Command | Purpose |
|---|---|
| `git merge branch-name` | Merges a branch into the current branch |
| `git merge --no-ff branch-name` | Forces a merge commit |
| `git merge --ff-only branch-name` | Allows only fast-forward merge |
| `git status` | Checks merge state |
| `git log --oneline --graph --decorate --all` | Shows branch and merge history |
| `git branch -d branch-name` | Deletes a merged local branch |

## Common mistakes

### Mistake 1: Merging from the wrong branch

Always check your current branch:

```bash
git branch
```

If you want to merge into `main`, first switch to `main`:

```bash
git switch main
```

### Mistake 2: Forgetting that merge direction matters

This:

```bash
git merge feature
```

merges `feature` into your current branch.

It does not automatically mean the feature is going into `main`.

### Mistake 3: Merging with uncommitted changes

Before merging:

```bash
git status
```

If you have uncommitted changes, commit or stash them first.

### Mistake 4: Deleting a branch before confirming the merge

Before deleting a branch, confirm the merge:

```bash
git branch --merged
```

Then delete it safely:

```bash
git branch -d branch-name
```

## Best practices

- Always check your current branch before merging.
- Make sure your working tree is clean.
- Merge completed and reviewed work.
- Use clear branch names.
- Review history after merging.
- Delete merged branches when they are no longer needed.
- Use pull requests in team environments.
- Avoid merging incomplete work into `main`.

## Professional recommendation

Before merging into `main`, run:

```bash
git switch main
git status
git log --oneline --graph --decorate --all
```

Then merge:

```bash
git merge feature/branch-name
```

After merging:

```bash
git status
git log --oneline --graph --decorate --all
```

## Summary

A merge combines changes from one branch into another.

Basic merge:

```bash
git switch main
git merge feature/branch-name
```

Remember:

```txt
The branch you name is merged into your current branch.
```

Merging is essential for integrating work from feature branches into stable branches like `main`.

## Recommended next topic

Continue with:

```txt
docs/04-merges-and-conflicts/conflict-resolution.md
```