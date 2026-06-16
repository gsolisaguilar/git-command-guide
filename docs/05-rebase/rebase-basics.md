# Rebase Basics

`git rebase` is a Git command used to move or replay commits from one branch onto another base commit.

Rebase is commonly used to keep a branch updated, create a cleaner project history, and avoid unnecessary merge commits.

## What is rebase?

Rebase means changing the base of a branch.

In simple terms:

```txt
Rebase takes your commits and places them on top of another branch.
```

For example, if you are working on a feature branch and `main` has new commits, you can rebase your feature branch on top of the latest `main`.

## Basic rebase syntax

```bash
git rebase base-branch
```

Example:

```bash
git rebase main
```

This means:

```txt
Take the commits from the current branch and replay them on top of main.
```

## Important rule

Before running rebase, always check your current branch.

```bash
git branch
```

Example:

```txt
  main
* feature/rebase-guide
```

If you run:

```bash
git rebase main
```

while you are on `feature/rebase-guide`, Git will rebase `feature/rebase-guide` on top of `main`.

## Rebase example

Imagine this history:

```txt
A---B---C main
     \
      D---E feature/rebase-guide
```

The feature branch started from commit `B`.

Then `main` advanced to commit `C`.

If you run:

```bash
git switch feature/rebase-guide
git rebase main
```

The result will be:

```txt
A---B---C main
         \
          D'---E' feature/rebase-guide
```

The commits `D` and `E` are replayed on top of `C`.

They become new commits: `D'` and `E'`.

## Why commits change after rebase

Rebase creates new commits because it rewrites commit history.

Even if the changes look the same, the commit hashes are different.

Example before rebase:

```txt
D---E
```

Example after rebase:

```txt
D'---E'
```

This is important because rewriting history can affect other people if the branch was already shared.

## When to use rebase

Use rebase when:

- You want a cleaner linear history.
- You want to update your feature branch with the latest `main`.
- You want to avoid extra merge commits.
- You are working on a local branch.
- Your team uses a rebase-based workflow.

## When not to use rebase

Avoid rebase when:

- The branch is shared and other people are working on it.
- You do not understand the impact of rewriting history.
- The branch has already been merged.
- Your team prefers merge commits.
- You are working on protected branches like `main`.

## Golden rule of rebase

```txt
Do not rebase public/shared branches unless your team agreed to it.
```

A public branch is a branch that other people may have already pulled or based work on.

## Safe beginner use case

The safest way to practice rebase is on your own local feature branch.

Example:

```bash
git switch feature/rebase-guide
git rebase main
```

This is usually safe if nobody else is using that branch.

## Rebase current branch onto main

```bash
git switch feature/rebase-guide
git rebase main
```

This updates your feature branch so it starts from the latest commit on `main`.

## Rebase after updating main

A common workflow is:

```bash
git switch main
git pull origin main
git switch feature/rebase-guide
git rebase main
```

If you are working locally and have not pushed yet, you can use:

```bash
git switch main
git switch feature/rebase-guide
git rebase main
```

assuming your local `main` is already updated.

## Rebase with conflicts

Sometimes rebase causes conflicts.

Example:

```txt
CONFLICT (content): Merge conflict in README.md
error: could not apply a1b2c3d... Add README update
```

This means Git could not replay one of your commits automatically.

## Resolve conflicts during rebase

When a conflict happens:

```bash
git status
```

Open the conflicted files and resolve them.

Then stage the resolved files:

```bash
git add file-name
```

Continue the rebase:

```bash
git rebase --continue
```

## Rebase conflict workflow

```bash
git status
# resolve conflicts manually
git add .
git rebase --continue
```

Repeat this process until the rebase finishes.

## Abort a rebase

If you want to cancel the rebase:

```bash
git rebase --abort
```

This returns the branch to the state it had before the rebase started.

## Skip a commit during rebase

If a specific commit cannot be applied and you decide you do not need it:

```bash
git rebase --skip
```

Use this carefully because it removes that commit from the rebased result.

## Rebase commands

| Command | Purpose |
|---|---|
| `git rebase main` | Replays current branch commits on top of `main` |
| `git rebase --continue` | Continues rebase after resolving conflicts |
| `git rebase --abort` | Cancels the rebase |
| `git rebase --skip` | Skips the current commit being replayed |
| `git status` | Shows rebase state and conflicted files |

## Rebase vs pull --rebase

You can also update a branch using:

```bash
git pull --rebase
```

This means:

```txt
Fetch remote changes, then rebase local commits on top of them.
```

Example:

```bash
git pull --rebase origin main
```

Use this only when you understand that it rebases your local commits.

## Rebase and force push

Because rebase rewrites commit history, if the branch was already pushed, Git may reject a normal push.

You may see something like:

```txt
non-fast-forward
```

In that case, some workflows require:

```bash
git push --force-with-lease
```

Prefer:

```bash
git push --force-with-lease
```

instead of:

```bash
git push --force
```

because `--force-with-lease` is safer.

## Important warning about force push

Force push can overwrite remote history.

Use it only when:

- You understand why it is needed.
- You are working on your own branch.
- Nobody else depends on that branch.
- Your team allows it.

## Example workflow for this repository

If you are working on:

```txt
feature/rebase-guide
```

and want to update it with `main`:

```bash
git switch main
git status
git switch feature/rebase-guide
git rebase main
```

After rebase:

```bash
git status
git log --oneline --graph --decorate --all
```

## Rebase before merge

A common clean workflow is:

```bash
git switch feature/rebase-guide
git rebase main
git switch main
git merge --ff-only feature/rebase-guide
```

This creates a linear history.

## Common mistakes

### Mistake 1: Rebasing main onto a feature branch

Avoid accidentally doing this:

```bash
git switch main
git rebase feature/rebase-guide
```

This changes the base of `main`, which is usually not what you want.

### Mistake 2: Rebasing shared branches

Avoid rebasing branches that other people are already using.

### Mistake 3: Panicking during conflicts

Conflicts during rebase are normal.

Use:

```bash
git status
```

Resolve files, then:

```bash
git add .
git rebase --continue
```

### Mistake 4: Using force push without understanding

Avoid:

```bash
git push --force
```

Prefer:

```bash
git push --force-with-lease
```

and only when necessary.

## Best practices

- Rebase only when you understand the branch direction.
- Rebase your own local branches.
- Avoid rebasing shared branches.
- Check `git status` before rebasing.
- Review history after rebasing.
- Use `git rebase --abort` if something goes wrong.
- Prefer `--force-with-lease` over `--force` if force push is required.
- Communicate with your team before rewriting shared history.

## Summary

Rebase moves your branch commits onto a new base.

Basic command:

```bash
git switch feature/my-branch
git rebase main
```

Conflict resolution:

```bash
git status
git add .
git rebase --continue
```

Cancel rebase:

```bash
git rebase --abort
```

Golden rule:

```txt
Do not rebase public/shared branches unless your team agreed to it.
```

## Recommended next topic

Continue with:

```txt
docs/05-rebase/rebase-vs-merge.md
```