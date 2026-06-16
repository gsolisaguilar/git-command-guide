# Status, Add, and Commit

The commands `git status`, `git add`, and `git commit` are part of the most important Git workflow.

They are used to check, prepare, and save changes.

## Overview

The basic flow is:

```txt
Working Directory → Staging Area → Local Repository
```

In commands:

```bash
git status
git add .
git commit -m "Commit message"
```

## git status

`git status` shows the current state of your repository.

```bash
git status
```

It tells you:

- Current branch.
- Modified files.
- Untracked files.
- Staged files.
- Whether your branch is ahead or behind.
- Whether there is anything to commit.

## Example: clean working tree

```txt
On branch main
nothing to commit, working tree clean
```

This means there are no pending changes.

## Example: modified file

```txt
On branch main

Changes not staged for commit:
  modified: README.md
```

This means `README.md` was modified, but the change is not staged yet.

## Example: untracked file

```txt
Untracked files:
  docs/new-file.md
```

This means Git sees the file, but it is not tracking it yet.

## Example: staged file

```txt
Changes to be committed:
  modified: README.md
```

This means the file is staged and ready to be committed.

## git add

`git add` moves changes from the working directory to the staging area.

## Stage one file

```bash
git add README.md
```

Use this when you want to stage a specific file.

## Stage multiple files

```bash
git add README.md docs/example.md
```

Use this when you want to stage selected files.

## Stage all changes

```bash
git add .
```

This stages all changes in the current directory and its subdirectories.

## Stage all tracked files

```bash
git add -u
```

This stages modifications and deletions of tracked files, but it does not stage new untracked files.

## Stage all changes in the repository

```bash
git add -A
```

This stages:

- New files.
- Modified files.
- Deleted files.

## Difference between git add ., git add -u, and git add -A

| Command | New files | Modified files | Deleted files |
|---|---|---|---|
| `git add .` | Yes | Yes | Yes, from current directory |
| `git add -u` | No | Yes | Yes |
| `git add -A` | Yes | Yes | Yes |

## git commit

`git commit` saves staged changes into the local repository history.

```bash
git commit -m "Add README documentation"
```

The `-m` option allows you to write the commit message directly in the command.

## Commit message

A commit message should explain what changed.

Good examples:

```txt
Add Git setup instructions
Update README navigation
Fix typo in lifecycle documentation
Create basic workflow example
```

Bad examples:

```txt
update
changes
fix
final
test
```

## Commit only staged changes

Git only commits what is staged.

Example:

```bash
git add README.md
git commit -m "Update README"
```

Only `README.md` will be included in the commit.

Other unstaged changes will remain in the working directory.

## Check staged changes before committing

Use:

```bash
git diff --staged
```

This shows what will be included in the next commit.

Recommended flow:

```bash
git status
git diff
git add README.md
git diff --staged
git commit -m "Update README"
```

## Commit all tracked modified files

You can use:

```bash
git commit -am "Update tracked files"
```

This stages and commits modified tracked files in one step.

Important:

```txt
git commit -am does not include new untracked files.
```

Example:

```bash
git commit -am "Update documentation"
```

Use it carefully.

## Empty commit

Sometimes, developers create an empty commit to trigger CI/CD pipelines.

```bash
git commit --allow-empty -m "Trigger pipeline"
```

This creates a commit without file changes.

This is not common for beginners, but it can be useful in professional environments.

## Amend the last commit

If you need to fix the last commit message or include a missing file, use:

```bash
git commit --amend
```

Example:

```bash
git add missing-file.md
git commit --amend
```

To change only the commit message:

```bash
git commit --amend -m "New commit message"
```

Important:

```txt
Avoid amending commits that were already pushed to a shared branch unless you understand the impact.
```

## Practical example

Create a file:

```bash
touch notes.md
```

Check status:

```bash
git status
```

Stage it:

```bash
git add notes.md
```

Check staged changes:

```bash
git status
```

Commit it:

```bash
git commit -m "Add notes file"
```

Check history:

```bash
git log --oneline
```

## Professional workflow

```bash
git status
git diff
git add file-name
git status
git diff --staged
git commit -m "Clear commit message"
git log --oneline
```

This workflow helps you avoid mistakes.

## Common command examples

| Command | Purpose |
|---|---|
| `git status` | Shows repository status |
| `git add file.md` | Stages one file |
| `git add .` | Stages all changes in the current directory |
| `git add -A` | Stages all changes in the repository |
| `git commit -m "Message"` | Creates a commit |
| `git commit -am "Message"` | Stages and commits tracked modified files |
| `git commit --amend` | Edits the last commit |

## Common mistakes

### Mistake 1: Forgetting to stage before committing

If you run:

```bash
git commit -m "Update file"
```

without staging changes first, Git may show:

```txt
no changes added to commit
```

Fix:

```bash
git add .
git commit -m "Update file"
```

### Mistake 2: Staging unwanted files

If you accidentally stage files, you can unstage them with:

```bash
git restore --staged file-name
```

Example:

```bash
git restore --staged README.md
```

### Mistake 3: Using unclear commit messages

Avoid:

```bash
git commit -m "stuff"
```

Use:

```bash
git commit -m "Add setup and configuration documentation"
```

### Mistake 4: Amending pushed commits without understanding

`git commit --amend` rewrites the last commit.

Be careful when the commit has already been pushed to a shared branch.

## Best practices

- Run `git status` often.
- Review changes before staging.
- Stage only related changes.
- Write clear commit messages.
- Keep commits small and focused.
- Avoid committing temporary files.
- Do not commit secrets, passwords, or API keys.

## Summary

`git status`, `git add`, and `git commit` are essential commands.

Basic flow:

```bash
git status
git add .
git commit -m "Describe the change"
```

Professional flow:

```bash
git status
git diff
git add file-name
git diff --staged
git commit -m "Clear commit message"
```

## Recommended next topic

Continue with:

```txt
docs/01-basic-commands/log-and-history.md
```