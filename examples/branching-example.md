# Branching Example

This example shows how to create a branch, work on it, commit changes, merge it into `main`, and delete the branch after merging.

## Scenario

You are working on the repository:

```txt
git-commands-guide
```

You want to add documentation about branches.

Instead of working directly on `main`, you will create a feature branch.

## Goal

The goal is to practice this workflow:

```txt
Start from main → Create branch → Make changes → Commit → Merge into main → Delete branch
```

## Step 1: Go to main

```bash
git switch main
```

Example output:

```txt
Switched to branch 'main'
```

## Step 2: Check status

```bash
git status
```

Expected output:

```txt
On branch main
nothing to commit, working tree clean
```

This confirms that `main` is clean before creating a new branch.

## Step 3: Create a new branch

```bash
git switch -c feature/branches
```

Example output:

```txt
Switched to a new branch 'feature/branches'
```

## Step 4: Confirm current branch

```bash
git branch
```

Example output:

```txt
* feature/branches
  main
```

The `*` shows that you are currently on:

```txt
feature/branches
```

## Step 5: Create or edit files

Example files:

```txt
docs/02-branches/branch-basics.md
docs/02-branches/switch-and-checkout.md
docs/02-branches/branch-naming.md
docs/02-branches/delete-and-rename-branches.md
```

## Step 6: Check status

```bash
git status
```

Example output:

```txt
On branch feature/branches

Untracked files:
  docs/02-branches/branch-basics.md
  docs/02-branches/switch-and-checkout.md
  docs/02-branches/branch-naming.md
  docs/02-branches/delete-and-rename-branches.md
```

## Step 7: Stage changes

```bash
git add docs/02-branches/
```

## Step 8: Commit changes

```bash
git commit -m "Add branch management documentation"
```

Example output:

```txt
[feature/branches a1b2c3d] Add branch management documentation
 4 files changed, 500 insertions(+)
```

## Step 9: Review history

```bash
git log --oneline --graph --decorate --all
```

Example output:

```txt
* a1b2c3d (HEAD -> feature/branches) Add branch management documentation
* e4f5g6h (main) Add basic Git commands documentation
```

## Step 10: Switch back to main

```bash
git switch main
```

## Step 11: Merge the feature branch

```bash
git merge feature/branches
```

Example output:

```txt
Updating e4f5g6h..a1b2c3d
Fast-forward
 docs/02-branches/branch-basics.md              | 120 ++++++
 docs/02-branches/switch-and-checkout.md        | 120 ++++++
 docs/02-branches/branch-naming.md              | 120 ++++++
 docs/02-branches/delete-and-rename-branches.md | 140 +++++++
```

## Step 12: Confirm merge

```bash
git log --oneline --graph --decorate --all
```

Example output:

```txt
* a1b2c3d (HEAD -> main, feature/branches) Add branch management documentation
* e4f5g6h Add basic Git commands documentation
```

This means `main` now contains the branch changes.

## Step 13: Delete merged branch

```bash
git branch -d feature/branches
```

Example output:

```txt
Deleted branch feature/branches (was a1b2c3d).
```

## Step 14: Confirm branch was deleted

```bash
git branch
```

Example output:

```txt
* main
```

## Full local branch workflow

```bash
git switch main
git status
git switch -c feature/branches

# create or edit files

git status
git add docs/02-branches/
git commit -m "Add branch management documentation"

git switch main
git merge feature/branches
git branch -d feature/branches
```

## Workflow with GitHub

If you are using GitHub, after committing on your feature branch:

```bash
git push -u origin feature/branches
```

Then create a pull request.

After the pull request is merged:

```bash
git switch main
git pull origin main
git branch -d feature/branches
```

If the remote branch still exists:

```bash
git push origin --delete feature/branches
```

## Common mistake: merging in the wrong direction

This command:

```bash
git merge feature/branches
```

merges `feature/branches` into the current branch.

So if you want to merge into `main`, you must be on `main` first:

```bash
git switch main
git merge feature/branches
```

## Common mistake: deleting a branch too early

Before deleting, check if it was merged:

```bash
git branch --merged
```

Then delete safely:

```bash
git branch -d feature/branches
```

## Common mistake: unclear branch names

Avoid:

```txt
test
update
branch1
changes
```

Use:

```txt
feature/branches
feature/remote-repositories
docs/update-readme
bugfix/fix-broken-link
```

## Summary

Feature branch workflow:

```txt
main → feature branch → commit → main → merge → delete branch
```

Basic commands:

```bash
git switch main
git switch -c feature/my-topic
git add .
git commit -m "Add my topic"
git switch main
git merge feature/my-topic
git branch -d feature/my-topic
```

This keeps your work organized and keeps `main` stable.