# Basic Workflow Example

This example shows a basic Git workflow from editing a file to creating a commit.

It is designed for beginners who want to understand the daily Git process.

## Scenario

You are working on a repository called:

```txt
git-commands-guide
```

You want to update the `README.md` file and save the change with Git.

## Goal

The goal is to practice this workflow:

```txt
Check status → Edit file → Review changes → Stage changes → Commit changes → Review history
```

## Step 1: Check current branch

```bash
git branch
```

Example output:

```txt
* feature/basic-git-commands
  main
```

This means you are currently on:

```txt
feature/basic-git-commands
```

## Step 2: Check repository status

```bash
git status
```

Example output:

```txt
On branch feature/basic-git-commands
nothing to commit, working tree clean
```

This means there are no pending changes.

## Step 3: Edit a file

Open `README.md` and add a short description.

Example:

```md
# Git Commands Guide

A curated reference of essential Git commands and workflows used in professional software development.

## Purpose

This repository helps developers learn Git from basic commands to professional workflows.
```

## Step 4: Check status again

```bash
git status
```

Example output:

```txt
On branch feature/basic-git-commands

Changes not staged for commit:
  modified: README.md
```

This means Git detected a change in `README.md`, but it is not staged yet.

## Step 5: Review the change

```bash
git diff
```

Example output:

```diff
+## Purpose
+
+This repository helps developers learn Git from basic commands to professional workflows.
```

This shows what changed before staging.

## Step 6: Stage the file

```bash
git add README.md
```

## Step 7: Check status after staging

```bash
git status
```

Example output:

```txt
On branch feature/basic-git-commands

Changes to be committed:
  modified: README.md
```

This means the file is staged and ready to commit.

## Step 8: Review staged changes

```bash
git diff --staged
```

This shows exactly what will be included in the next commit.

## Step 9: Commit the change

```bash
git commit -m "Update README purpose section"
```

Example output:

```txt
[feature/basic-git-commands a1b2c3d] Update README purpose section
 1 file changed, 3 insertions(+)
```

## Step 10: Review commit history

```bash
git log --oneline
```

Example output:

```txt
a1b2c3d Update README purpose section
e4f5g6h Add basic Git commands documentation
```

## Full command sequence

```bash
git branch
git status
git diff
git add README.md
git status
git diff --staged
git commit -m "Update README purpose section"
git log --oneline
```

## Example with all files

If you changed multiple files and all belong to the same task:

```bash
git status
git diff
git add .
git diff --staged
git commit -m "Update basic Git documentation"
git log --oneline
```

## Example with one specific file

If you only want to commit one file:

```bash
git status
git diff README.md
git add README.md
git diff --staged
git commit -m "Update README"
```

## Common mistake: staging everything without checking

Avoid doing this without reviewing:

```bash
git add .
git commit -m "update"
```

Better workflow:

```bash
git status
git diff
git add .
git diff --staged
git commit -m "Clear commit message"
```

## Common mistake: forgetting to stage

If you run:

```bash
git commit -m "Update README"
```

without staging, Git may show:

```txt
no changes added to commit
```

Fix:

```bash
git add README.md
git commit -m "Update README"
```

## Common mistake: unclear commit message

Avoid:

```bash
git commit -m "changes"
```

Use:

```bash
git commit -m "Update README purpose section"
```

## Beginner checklist

Before committing:

```txt
Did I run git status?
Did I review git diff?
Did I stage the correct files?
Did I review git diff --staged?
Is my commit message clear?
```

## Summary

A basic Git workflow looks like this:

```bash
git status
git diff
git add .
git diff --staged
git commit -m "Describe the change"
git log --oneline
```

Use this workflow every time you want to save a clean and understandable change in Git.