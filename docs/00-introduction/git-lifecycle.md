# Git Lifecycle

The Git lifecycle describes how changes move through the different states of a Git repository.

Understanding the Git lifecycle is essential because almost every Git command affects one of these states.

## Main areas in Git

Git commonly works with four main areas:

```txt
Working Directory
Staging Area
Local Repository
Remote Repository
```

Each area represents a different stage in the life of a change.

## 1. Working Directory

The working directory is where you edit your project files.

When you create, modify, or delete a file, the change starts in the working directory.

Example:

```txt
README.md modified
app.js created
old-file.txt deleted
```

You can check the current state of your working directory with:

```bash
git status
```

Example output:

```txt
Changes not staged for commit:
  modified: README.md
```

This means Git detected a change, but the change has not been prepared for commit yet.

## 2. Staging Area

The staging area is where you prepare changes before committing them.

You move changes from the working directory to the staging area using:

```bash
git add file-name
```

Example:

```bash
git add README.md
```

To stage all current changes:

```bash
git add .
```

The staging area allows you to control exactly what will be included in the next commit.

## 3. Local Repository

The local repository is where Git stores your committed changes on your computer.

You move changes from the staging area to the local repository using:

```bash
git commit -m "Describe the change"
```

Example:

```bash
git commit -m "Add Git lifecycle documentation"
```

After committing, Git saves a snapshot of the staged changes.

## 4. Remote Repository

The remote repository is the online version of your repository.

It is commonly hosted on platforms like GitHub, GitLab, or Bitbucket.

You send local commits to the remote repository using:

```bash
git push
```

Example:

```bash
git push origin main
```

You can download changes from the remote repository using:

```bash
git pull
```

Example:

```bash
git pull origin main
```

## Basic Git lifecycle diagram

```txt
Working Directory
       |
       | git add
       v
Staging Area
       |
       | git commit
       v
Local Repository
       |
       | git push
       v
Remote Repository
```

To bring changes from the remote repository to your local environment:

```txt
Remote Repository
       |
       | git pull
       v
Local Repository + Working Directory
```

## Example workflow

Imagine you modify a file called `README.md`.

### Step 1: Check status

```bash
git status
```

Git shows that the file was modified.

### Step 2: Stage the file

```bash
git add README.md
```

The file is now in the staging area.

### Step 3: Commit the change

```bash
git commit -m "Update README introduction"
```

The change is now saved in the local repository.

### Step 4: Push the commit

```bash
git push origin feature/basic-git-commands
```

The change is now uploaded to the remote repository.

## File states in Git

Files in Git can have different states.

| State     | Meaning                                          |
| --------- | ------------------------------------------------ |
| Untracked | Git sees the file, but it is not tracking it yet |
| Modified  | The file changed, but the change is not staged   |
| Staged    | The change is prepared for the next commit       |
| Committed | The change is saved in the local repository      |
| Pushed    | The commit was uploaded to the remote repository |

## Untracked files

An untracked file is a file that exists in your working directory but has not been added to Git yet.

Example:

```txt
Untracked files:
  notes.md
```

To start tracking it:

```bash
git add notes.md
```

## Modified files

A modified file is a tracked file that has changed.

Example:

```txt
modified: README.md
```

To prepare it for commit:

```bash
git add README.md
```

## Staged files

A staged file is ready to be committed.

Example:

```txt
Changes to be committed:
  modified: README.md
```

To commit it:

```bash
git commit -m "Update README"
```

## Committed changes

Committed changes are saved in your local Git history.

You can see commit history with:

```bash
git log
```

A shorter version:

```bash
git log --oneline
```

## Pushed changes

Pushed changes are commits that have been uploaded to the remote repository.

Example:

```bash
git push origin main
```

Or, if the branch already tracks a remote branch:

```bash
git push
```

## Common lifecycle commands

| Command      | Purpose                                                           |
| ------------ | ----------------------------------------------------------------- |
| `git status` | Shows the current state of the working directory and staging area |
| `git add`    | Moves changes to the staging area                                 |
| `git commit` | Saves staged changes in the local repository                      |
| `git push`   | Uploads local commits to a remote repository                      |
| `git pull`   | Downloads and integrates remote changes                           |
| `git log`    | Shows commit history                                              |
| `git diff`   | Shows differences between changes                                 |

## Using git diff in the lifecycle

Before staging changes, you can review what changed:

```bash
git diff
```

After staging changes, you can review what is staged:

```bash
git diff --staged
```

This is useful before creating a commit.

## Professional recommendation

Before committing, it is a good habit to run:

```bash
git status
git diff
git diff --staged
```

This helps you verify what you changed and what you are about to commit.

## Example professional flow

```bash
git status
git diff
git add README.md
git diff --staged
git commit -m "Add Git lifecycle explanation"
git push origin feature/basic-git-commands
```

This flow helps avoid committing unwanted changes.

## Common mistakes

### Mistake 1: Modifying files but not staging them

If you modify a file but do not run `git add`, the file will not be included in the commit.

### Mistake 2: Staging everything without reviewing

Using this command can be useful:

```bash
git add .
```

However, you should check what you are adding before committing.

Recommended:

```bash
git status
git diff
```

### Mistake 3: Committing but forgetting to push

A commit only saves changes locally.

To upload the commit to GitHub, use:

```bash
git push
```

### Mistake 4: Pulling without checking local changes

Before pulling remote changes, check your local status:

```bash
git status
```

This helps avoid conflicts or unexpected changes.

## Summary

The Git lifecycle explains how changes move through Git.

```txt
Working Directory → Staging Area → Local Repository → Remote Repository
```

Main commands:

```bash
git status
git add
git commit
git push
git pull
git log
git diff
```

Understanding this lifecycle makes it easier to use Git correctly and avoid common mistakes.

## Recommended next topic

After understanding the Git lifecycle, continue with:

```txt
docs/01-basic-commands/setup-and-config.md
```
