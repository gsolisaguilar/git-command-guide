# Basic Git Workflow

The basic Git workflow is the daily process used to track changes in a project.

This workflow is essential for beginners and is also used constantly by professional developers.

## Basic workflow overview

The basic workflow is:

```txt
Modify files
Check status
Stage changes
Commit changes
Push changes
```

In Git commands:

```bash
git status
git add .
git commit -m "Describe the change"
git push
```

## Step 1: Modify files

First, you create, edit, or delete files in your project.

Examples:

```txt
README.md updated
index.html created
old-notes.txt deleted
```

At this point, the changes exist only in your working directory.

## Step 2: Check status

Use:

```bash
git status
```

This command shows:

- Current branch.
- Modified files.
- Untracked files.
- Staged files.
- Whether your branch is ahead or behind the remote branch.

Example output:

```txt
On branch feature/basic-git-commands

Changes not staged for commit:
  modified: README.md

Untracked files:
  docs/example.md
```

## Step 3: Review changes

Before staging, it is a good habit to review what changed.

```bash
git diff
```

This shows the difference between your working directory and the last commit.

Example:

```diff
- Old sentence
+ New sentence
```

## Step 4: Stage changes

To stage one file:

```bash
git add README.md
```

To stage all changes:

```bash
git add .
```

The staging area prepares changes for the next commit.

## Step 5: Check staged changes

After staging, check the status again:

```bash
git status
```

You can also review the staged changes:

```bash
git diff --staged
```

This shows exactly what will be included in the next commit.

## Step 6: Commit changes

Create a commit with:

```bash
git commit -m "Add basic workflow documentation"
```

A commit saves a snapshot of the staged changes in your local Git history.

## Step 7: Push changes

To upload your commits to the remote repository:

```bash
git push
```

If this is the first push of a new branch, use:

```bash
git push -u origin branch-name
```

Example:

```bash
git push -u origin feature/basic-git-commands
```

After the upstream is configured, you can usually use:

```bash
git push
```

## Full basic workflow example

```bash
git status
git diff
git add .
git status
git diff --staged
git commit -m "Add basic Git workflow"
git push origin feature/basic-git-commands
```

## Working with one file

If you only want to commit one file:

```bash
git status
git diff README.md
git add README.md
git commit -m "Update README"
git push
```

This is useful when you do not want to include unrelated changes.

## Working with multiple files

If your changes are related and belong in the same commit:

```bash
git add .
git commit -m "Add Git introduction docs"
```

Use this when all changes are part of the same task.

## Professional commit workflow

A more careful professional workflow is:

```bash
git status
git diff
git add file-name
git diff --staged
git commit -m "Clear commit message"
git log --oneline
git push
```

This reduces mistakes because you review the changes before committing.

## Commit messages

A commit message should clearly describe what changed.

Good examples:

```txt
Add Git lifecycle documentation
Fix typo in README
Update branch workflow example
Create basic commands cheatsheet
```

Bad examples:

```txt
changes
update
stuff
final
fix
```

## Commit message style

A good commit message usually starts with a verb in imperative form.

Examples:

```txt
Add setup instructions
Update README structure
Fix broken documentation link
Remove duplicated section
Create branching guide
```

## Small commits vs large commits

Small commits are easier to review and understand.

Recommended:

```txt
Commit 1: Add Git introduction
Commit 2: Add Git lifecycle diagram
Commit 3: Add basic command examples
```

Not recommended:

```txt
Commit 1: Add all documentation, examples, workflows, fixes, and updates
```

## When to commit

Create a commit when you complete a logical unit of work.

Examples:

- After adding one documentation section.
- After fixing one bug.
- After creating one example.
- After updating one workflow.

Avoid committing random incomplete changes unless you are saving work temporarily in a personal branch.

## Check commit history

To see recent commits:

```bash
git log --oneline
```

Example output:

```txt
a1b2c3d Add basic Git workflow
e4f5g6h Add Git lifecycle documentation
i7j8k9l Add Git introduction
```

## Push to a specific branch

```bash
git push origin feature/basic-git-commands
```

This pushes your local commits to the remote branch named `feature/basic-git-commands`.

## Pull before pushing

If other people are working on the same branch, you may need to pull before pushing.

```bash
git pull
git push
```

However, in professional workflows, it is better to understand what `git pull` does before using it automatically.

## Common basic workflow commands

| Command | Purpose |
|---|---|
| `git status` | Shows current repository state |
| `git diff` | Shows unstaged changes |
| `git add` | Stages changes |
| `git diff --staged` | Shows staged changes |
| `git commit -m "message"` | Creates a commit |
| `git push` | Uploads commits |
| `git pull` | Downloads and integrates remote changes |
| `git log --oneline` | Shows commit history in short format |

## Common mistakes

### Mistake 1: Committing without checking status

Always check:

```bash
git status
```

before committing.

### Mistake 2: Using git add . without reviewing

This can accidentally stage files you did not want to commit.

Better:

```bash
git status
git diff
git add .
git diff --staged
```

### Mistake 3: Writing unclear commit messages

Avoid messages like:

```txt
update
fix
changes
```

Use clear messages instead:

```txt
Add basic Git workflow documentation
```

### Mistake 4: Forgetting to push

A commit is local.

To send it to GitHub, use:

```bash
git push
```

### Mistake 5: Mixing unrelated changes

Do not include unrelated changes in the same commit.

For example, avoid one commit that does all of this:

```txt
Update README
Fix login bug
Add CSS styles
Delete old images
```

Separate changes into logical commits.

## Beginner workflow checklist

Before committing, ask:

```txt
Did I check git status?
Did I review the changes?
Did I stage only the correct files?
Is my commit message clear?
Did I push the commit if needed?
```

## Example for this repository

If you are working on this Git guide repository:

```bash
git status
git add docs/01-basic-commands/basic-workflow.md
git commit -m "Add basic Git workflow documentation"
git push origin feature/basic-git-commands
```

## Summary

The basic Git workflow is:

```txt
Edit → Status → Add → Commit → Push
```

Main commands:

```bash
git status
git add .
git commit -m "Message"
git push
```

Professional developers use this workflow every day.

## Recommended next topic

Continue with:

```txt
docs/01-basic-commands/status-add-commit.md
```