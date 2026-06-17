# Rebase Workflow

The rebase workflow is used to keep a branch history clean and linear.

It is commonly used when you want to update a feature branch with the latest changes from `main` before merging.

## Goal

The goal of this workflow is to replay your branch commits on top of the latest `main`.

This creates a cleaner history and can allow a fast-forward merge.

## When to use this workflow

Use this workflow when:

- You want a linear history.
- You are working on your own feature branch.
- Your branch is not shared with other people.
- You understand that rebase rewrites commit hashes.
- Your team allows rebase.
- You want to merge with `--ff-only`.

## When not to use this workflow

Avoid this workflow when:

- The branch is shared with other people.
- You are not comfortable resolving rebase conflicts.
- Your team prefers merge commits.
- You are working directly on `main`.
- You already pushed the branch and others may have pulled it.

## Golden rule

```txt
Do not rebase public or shared branches unless your team agreed to it.
```

## Basic rebase workflow

```bash
git switch main
git pull origin main

git switch feature/my-topic
git rebase main

git switch main
git merge --ff-only feature/my-topic
```

## If you are working locally only

If you have not pushed anything to GitHub yet:

```bash
git switch main
git switch feature/my-topic
git rebase main
git switch main
git merge --ff-only feature/my-topic
```

## Step 1: Check your current work

Before rebasing:

```bash
git status
```

Recommended state:

```txt
nothing to commit, working tree clean
```

If you have changes, either commit or stash them.

## Step 2: Commit or stash unfinished work

Option 1: Commit changes.

```bash
git add .
git commit -m "Save current progress"
```

Option 2: Stash changes.

```bash
git stash push -m "Temporary changes before rebase"
```

## Step 3: Update main

```bash
git switch main
git pull origin main
```

If working locally only, this may not be necessary.

## Step 4: Switch to your feature branch

```bash
git switch feature/my-topic
```

Example:

```bash
git switch feature/workflows
```

## Step 5: Rebase onto main

```bash
git rebase main
```

This replays your feature branch commits on top of `main`.

## Step 6: Resolve conflicts if needed

If conflicts happen, Git pauses.

Check status:

```bash
git status
```

Open conflicted files and fix them.

Stage resolved files:

```bash
git add .
```

Continue rebase:

```bash
git rebase --continue
```

Repeat until the rebase finishes.

## Step 7: Abort if something goes wrong

If you are unsure:

```bash
git rebase --abort
```

This returns the branch to the state before the rebase started.

## Step 8: Review history

```bash
git log --oneline --graph --decorate --all
```

Check that your feature branch is now on top of `main`.

## Step 9: Merge with fast-forward

```bash
git switch main
git merge --ff-only feature/my-topic
```

This moves `main` forward without creating a merge commit.

## Step 10: Delete feature branch

After successful merge:

```bash
git branch -d feature/my-topic
```

## Full local rebase workflow

```bash
git switch main
git switch feature/my-topic
git status
git rebase main
git log --oneline --graph --decorate --all
git switch main
git merge --ff-only feature/my-topic
git branch -d feature/my-topic
```

## Full GitHub rebase workflow

```bash
git switch main
git pull origin main

git switch feature/my-topic
git status
git rebase main

git push --force-with-lease
```

Then open or update the pull request.

After merge:

```bash
git switch main
git pull origin main
git branch -d feature/my-topic
```

## Why force push may be needed

Rebase rewrites commit hashes.

If the branch was already pushed before rebasing, Git may reject a normal push.

Use:

```bash
git push --force-with-lease
```

Avoid:

```bash
git push --force
```

unless you fully understand the risk.

## Rebase conflict workflow

```bash
git status
# resolve files manually
git add .
git rebase --continue
```

Abort:

```bash
git rebase --abort
```

Skip current commit:

```bash
git rebase --skip
```

Use `--skip` carefully.

## Interactive rebase before merge

If you want to clean commits:

```bash
git rebase -i main
```

Or for the last 3 commits:

```bash
git rebase -i HEAD~3
```

Common actions:

```txt
pick
reword
squash
fixup
drop
```

## Example for this repository

```bash
git switch main
git switch -c feature/workflows

# create workflow files

git add workflows/
git commit -m "Add workflow documentation"

git switch main
git merge --ff-only feature/workflows
git branch -d feature/workflows
```

If `main` changed before merge:

```bash
git switch feature/workflows
git rebase main
git switch main
git merge --ff-only feature/workflows
```

## Checklist before rebase

```txt
Am I on my own feature branch?
Is the working tree clean?
Did I check git status?
Do I know which branch I am rebasing onto?
Is this branch safe to rewrite?
```

## Checklist after rebase

```txt
Did the rebase finish successfully?
Did I resolve all conflicts?
Did I review git log?
Do I need to force push with --force-with-lease?
Is the branch ready to merge?
```

## Common mistakes

### Mistake 1: Rebasing main

Avoid:

```bash
git switch main
git rebase feature/my-topic
```

Usually, you rebase the feature branch onto `main`, not the other way around.

### Mistake 2: Rebasing shared branches

Do not rewrite history that other people may depend on.

### Mistake 3: Force pushing carelessly

Prefer:

```bash
git push --force-with-lease
```

### Mistake 4: Continuing after bad conflict resolution

If unsure:

```bash
git rebase --abort
```

Then try again carefully.

## Best practices

- Rebase only your own feature branches.
- Start from a clean working tree.
- Use `git status` often.
- Abort if unsure.
- Prefer `--force-with-lease` over `--force`.
- Review history after rebase.
- Use fast-forward merge after successful rebase.
- Follow team rules.

## Summary

Rebase workflow:

```txt
Update main → Rebase feature branch → Resolve conflicts → Fast-forward merge
```

Basic commands:

```bash
git switch feature/my-topic
git rebase main
git switch main
git merge --ff-only feature/my-topic
```

Golden rule:

```txt
Rebase your own branches. Do not rebase shared history without agreement.
```