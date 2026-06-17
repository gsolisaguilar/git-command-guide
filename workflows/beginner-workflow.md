# Beginner Git Workflow

This workflow is for beginners who are learning how to use Git in a safe and simple way.

It focuses on the most common Git actions:

```txt
Edit files → Check status → Stage changes → Commit → Review history
```

## Goal

The goal of this workflow is to help you save your work correctly using Git.

You will learn how to:

- Check your current branch.
- Review file changes.
- Stage changes.
- Create a commit.
- Check commit history.
- Avoid common beginner mistakes.

## When to use this workflow

Use this workflow when:

- You are working on a small change.
- You are updating documentation.
- You are learning Git basics.
- You are working locally.
- You are not ready for advanced workflows yet.

## Basic workflow

```bash
git status
git diff
git add .
git diff --staged
git commit -m "Describe the change"
git log --oneline
```

## Step 1: Check your current status

Before making a commit, always run:

```bash
git status
```

This shows:

- Current branch.
- Modified files.
- Untracked files.
- Staged files.
- Whether there is anything to commit.

Example:

```txt
On branch feature/basic-git-commands

Changes not staged for commit:
  modified: README.md

Untracked files:
  docs/example.md
```

## Step 2: Review unstaged changes

Before staging files, review what changed:

```bash
git diff
```

This helps you avoid committing unwanted changes.

## Step 3: Stage changes

To stage all changes:

```bash
git add .
```

To stage only one file:

```bash
git add file-name
```

Example:

```bash
git add README.md
```

## Step 4: Review staged changes

Before creating the commit:

```bash
git diff --staged
```

This shows what will be included in the commit.

## Step 5: Create a commit

```bash
git commit -m "Add beginner Git workflow"
```

A good commit message should be clear and specific.

Good examples:

```txt
Add beginner Git workflow
Update README navigation
Fix typo in Git lifecycle guide
Create basic commands documentation
```

Bad examples:

```txt
update
fix
changes
final
stuff
```

## Step 6: Check commit history

After committing:

```bash
git log --oneline
```

Example:

```txt
a1b2c3d Add beginner Git workflow
e4f5g6h Add basic Git commands documentation
```

## Beginner workflow example

```bash
git status
git diff
git add .
git diff --staged
git commit -m "Add beginner Git workflow"
git log --oneline
```

## If you only want to commit one file

```bash
git status
git diff README.md
git add README.md
git diff --staged
git commit -m "Update README"
```

## If you staged the wrong file

Unstage it:

```bash
git restore --staged file-name
```

Example:

```bash
git restore --staged README.md
```

Your changes remain in the working directory.

## If you want to discard local changes

Discard one file:

```bash
git restore file-name
```

Example:

```bash
git restore README.md
```

Warning:

```txt
This removes local changes in that file.
Use it only when you are sure.
```

## If you created a file by mistake

Preview untracked files that would be removed:

```bash
git clean -n
```

Remove untracked files:

```bash
git clean -f
```

Warning:

```txt
git clean deletes untracked files.
Always preview with git clean -n first.
```

## Beginner checklist before commit

Before committing, ask:

```txt
Am I on the correct branch?
Did I run git status?
Did I review git diff?
Did I stage only the correct files?
Did I check git diff --staged?
Is my commit message clear?
```

## Common beginner mistakes

### Mistake 1: Not checking status

Always run:

```bash
git status
```

before committing.

### Mistake 2: Staging everything without reviewing

Avoid using this blindly:

```bash
git add .
```

Better:

```bash
git status
git diff
git add .
```

### Mistake 3: Writing vague commit messages

Avoid:

```bash
git commit -m "update"
```

Better:

```bash
git commit -m "Add beginner Git workflow"
```

### Mistake 4: Forgetting that commit is local

A commit saves changes locally.

If you are using GitHub, you still need:

```bash
git push
```

## Beginner safe commands

| Command | Purpose |
|---|---|
| `git status` | Check repository status |
| `git diff` | Review unstaged changes |
| `git add file-name` | Stage one file |
| `git add .` | Stage all changes |
| `git diff --staged` | Review staged changes |
| `git commit -m "Message"` | Save staged changes |
| `git log --oneline` | Check commit history |
| `git restore --staged file` | Unstage a file |
| `git restore file` | Discard local file changes |

## Recommended habit

Use this sequence often:

```bash
git status
git diff
git add .
git diff --staged
git commit -m "Clear message"
```

This habit prevents many beginner mistakes.

## Summary

The beginner Git workflow is:

```txt
Check → Review → Stage → Commit → Verify
```

Basic commands:

```bash
git status
git diff
git add .
git commit -m "Message"
git log --oneline
```

Golden rule:

```txt
Always check what you are committing before creating the commit.
```