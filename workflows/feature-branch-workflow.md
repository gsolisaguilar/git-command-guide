# Feature Branch Workflow

The feature branch workflow is one of the most common professional Git workflows.

It allows you to work on a specific task in a separate branch without affecting `main`.

## Goal

The goal of this workflow is to develop each change in its own branch and merge it into `main` when it is ready.

## When to use this workflow

Use this workflow when:

- You are adding a new feature.
- You are writing a new documentation section.
- You are fixing a specific issue.
- You want to keep `main` stable.
- You want each task separated.
- You are working with pull requests.
- You want a clean project history.

## Main idea

```txt
main stays stable.
Each task gets its own branch.
Completed branches are merged into main.
```

## Recommended branch name format

```txt
type/short-description
```

Examples:

```txt
feature/basic-git-commands
feature/branches
feature/remote-repositories
feature/merges-and-conflicts
feature/rebase-guide
docs/update-readme
bugfix/fix-broken-link
```

## Step 1: Start from main

```bash
git switch main
```

If working with GitHub:

```bash
git pull origin main
```

If you are working locally only and have not pushed yet, make sure your local `main` already has the latest merged work.

## Step 2: Create a feature branch

```bash
git switch -c feature/my-topic
```

Example:

```bash
git switch -c feature/professional-workflows
```

## Step 3: Make changes

Edit, create, or delete files related to the task.

Check status:

```bash
git status
```

## Step 4: Stage changes

```bash
git add .
```

Or stage specific files:

```bash
git add file-name
```

Example:

```bash
git add docs/10-professional-workflows/github-flow.md
```

## Step 5: Commit changes

```bash
git commit -m "Add professional workflows documentation"
```

Use a clear message that describes the task.

## Step 6: Review history

```bash
git log --oneline --graph --decorate --all
```

This helps verify where your branch is in the history.

## Step 7: Merge into main

Switch to `main`:

```bash
git switch main
```

Merge the feature branch:

```bash
git merge feature/my-topic
```

Example:

```bash
git merge feature/professional-workflows
```

## Step 8: Delete the branch after merge

After confirming the merge is correct:

```bash
git branch -d feature/my-topic
```

Example:

```bash
git branch -d feature/professional-workflows
```

Use `-d` because it is safer. Git will prevent deletion if the branch was not merged.

## Full local workflow

```bash
git switch main
git switch -c feature/my-topic

# make changes

git status
git add .
git commit -m "Add my topic documentation"

git switch main
git merge feature/my-topic
git branch -d feature/my-topic
```

## Full workflow with GitHub

```bash
git switch main
git pull origin main
git switch -c feature/my-topic

# make changes

git status
git add .
git commit -m "Add my topic documentation"
git push -u origin feature/my-topic
```

Then open a pull request on GitHub.

After the pull request is merged:

```bash
git switch main
git pull origin main
git branch -d feature/my-topic
```

If the remote branch still exists:

```bash
git push origin --delete feature/my-topic
```

## Merge options

### Normal merge

```bash
git switch main
git merge feature/my-topic
```

### No fast-forward merge

```bash
git switch main
git merge --no-ff feature/my-topic
```

Use this if you want to preserve visible branch history.

### Squash merge

```bash
git switch main
git merge --squash feature/my-topic
git commit -m "Add my topic documentation"
```

Use this if you want one clean commit per topic.

### Rebase then fast-forward

```bash
git switch feature/my-topic
git rebase main
git switch main
git merge --ff-only feature/my-topic
```

Use this if you want linear history and understand rebase.

## Recommended workflow for this repository

Since this repository is organized by topics, one branch per topic works well.

Example:

```bash
git switch main
git switch -c feature/workflows

# add workflow files

git add workflows/
git commit -m "Add Git workflow documentation"

git switch main
git merge feature/workflows
git branch -d feature/workflows
```

## If you are creating one branch per section

Example sequence:

```txt
feature/basic-git-commands
feature/branches
feature/remote-repositories
feature/merges-and-conflicts
feature/rebase-guide
feature/undoing-changes
feature/stash-guide
feature/tags-and-releases
feature/advanced-git
feature/professional-workflows
feature/workflows
```

## Checklist before merging

Before merging into `main`, check:

```txt
Am I on the correct feature branch?
Did I commit all intended changes?
Did I review git status?
Is the feature complete?
Is the commit message clear?
Did I switch back to main before merging?
```

Commands:

```bash
git status
git log --oneline --graph --decorate --all
```

## Checklist after merging

After merge, check:

```txt
Does main contain the changes?
Is the working tree clean?
Can I safely delete the feature branch?
```

Commands:

```bash
git status
git log --oneline --graph --decorate --all
git branch --merged
```

## Common mistakes

### Mistake 1: Creating the branch from the wrong base

Always start from `main`:

```bash
git switch main
git switch -c feature/my-topic
```

### Mistake 2: Merging while still on the feature branch

This command merges into the current branch:

```bash
git merge branch-name
```

If you want to merge into `main`, switch to `main` first.

### Mistake 3: Deleting a branch before merge

Use safe delete:

```bash
git branch -d feature/my-topic
```

Git will stop you if it is not merged.

### Mistake 4: Using unclear branch names

Avoid:

```txt
update
test
changes
my-branch
```

Use:

```txt
feature/workflows
docs/update-readme
bugfix/fix-link
```

## Best practices

- Use one branch per task.
- Keep branches focused.
- Keep branch names clear.
- Start from updated `main`.
- Commit small logical changes.
- Merge only completed work.
- Delete branches after merge.
- Use pull requests when collaborating.
- Keep `main` stable.

## Summary

Feature branch workflow:

```txt
Start from main → Create feature branch → Commit work → Merge into main → Delete branch
```

Basic local commands:

```bash
git switch main
git switch -c feature/my-topic
git add .
git commit -m "Add my topic"
git switch main
git merge feature/my-topic
git branch -d feature/my-topic
```

Golden rule:

```txt
Do not work directly on main when the change belongs in its own task branch.
```