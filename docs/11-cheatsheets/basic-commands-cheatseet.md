# Basic Git Commands Cheatsheet

Quick reference for essential Git commands used in daily development.

## Setup

| Command | Description |
|---|---|
| `git --version` | Check installed Git version |
| `git config --global user.name "Your Name"` | Set global Git username |
| `git config --global user.email "email@example.com"` | Set global Git email |
| `git config --global --list` | Show global Git configuration |
| `git config --global init.defaultBranch main` | Set `main` as default branch |
| `git config --global core.editor "code --wait"` | Set VS Code as Git editor |

## Create or clone repositories

| Command | Description |
|---|---|
| `git init` | Initialize a new Git repository |
| `git clone repository-url` | Clone an existing repository |
| `git clone repository-url folder-name` | Clone into a custom folder |
| `git remote add origin repository-url` | Connect local repo to remote |
| `git remote -v` | Show remote URLs |
| `git branch -M main` | Rename current branch to `main` |

## Basic workflow

| Command | Description |
|---|---|
| `git status` | Show repository status |
| `git diff` | Show unstaged changes |
| `git add file-name` | Stage one file |
| `git add .` | Stage all changes |
| `git diff --staged` | Show staged changes |
| `git commit -m "Message"` | Commit staged changes |
| `git push` | Push commits to configured remote branch |
| `git push -u origin branch-name` | Push branch and set upstream |
| `git pull` | Pull from configured remote branch |

## Recommended beginner workflow

```bash
git status
git diff
git add .
git diff --staged
git commit -m "Describe the change"
git push
```

## First push of a new branch

```bash
git push -u origin branch-name
```

Example:

```bash
git push -u origin feature/basic-git-commands
```

## Check history

| Command | Description |
|---|---|
| `git log` | Show full commit history |
| `git log --oneline` | Show compact commit history |
| `git log --oneline --graph --decorate --all` | Show visual branch history |
| `git show commit-hash` | Show details of a specific commit |

## Useful file status meanings

| Status | Meaning |
|---|---|
| Untracked | Git sees the file but is not tracking it |
| Modified | File changed but is not staged |
| Staged | File is ready to be committed |
| Committed | Change is saved in local history |
| Pushed | Commit is uploaded to remote repository |

## Common examples

### Start a new local repository

```bash
mkdir my-project
cd my-project
git init
touch README.md
git add README.md
git commit -m "Add initial README"
```

### Connect local repository to GitHub

```bash
git remote add origin https://github.com/username/repository.git
git branch -M main
git push -u origin main
```

### Clone an existing repository

```bash
git clone https://github.com/username/repository.git
cd repository
git status
```

### Commit one file

```bash
git status
git add README.md
git commit -m "Update README"
```

### Commit all changes

```bash
git status
git add .
git commit -m "Update documentation"
```

## Common mistakes

| Mistake | Safer habit |
|---|---|
| Committing without checking files | Run `git status` first |
| Using `git add .` blindly | Run `git diff` first |
| Writing vague commit messages | Use clear messages |
| Forgetting to push | Run `git push` after commit |
| Using wrong remote | Check `git remote -v` |

## Good commit messages

```txt
Add Git setup instructions
Update README navigation
Fix typo in Git lifecycle guide
Create basic commands cheatsheet
```

## Bad commit messages

```txt
update
fix
changes
final
stuff
```

## Most important commands

```bash
git status
git add .
git commit -m "Message"
git push
git pull
git log --oneline
```

## Summary

Basic Git workflow:

```txt
Edit files → Check status → Stage changes → Commit → Push
```

Recommended command sequence:

```bash
git status
git diff
git add .
git commit -m "Clear message"
git push
```