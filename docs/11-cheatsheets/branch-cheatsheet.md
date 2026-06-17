# Branch Cheatsheet

Quick reference for creating, switching, naming, deleting, and managing Git branches.

## List branches

| Command | Description |
|---|---|
| `git branch` | List local branches |
| `git branch -r` | List remote branches |
| `git branch -a` | List local and remote branches |
| `git branch -vv` | Show local branches with upstream tracking |

## Switch branches

| Command | Description |
|---|---|
| `git switch branch-name` | Switch to an existing branch |
| `git switch -` | Switch to previous branch |
| `git checkout branch-name` | Older way to switch branches |

## Create branches

| Command | Description |
|---|---|
| `git branch branch-name` | Create branch without switching |
| `git switch -c branch-name` | Create and switch to a new branch |
| `git checkout -b branch-name` | Older way to create and switch |

## Recommended create branch workflow

```bash
git switch main
git pull origin main
git switch -c feature/new-topic
```

If working locally only:

```bash
git switch main
git switch -c feature/new-topic
```

## Push new branch

```bash
git push -u origin branch-name
```

Example:

```bash
git push -u origin feature/branches
```

## Branch naming

Recommended format:

```txt
type/short-description
```

Examples:

```txt
feature/basic-git-commands
feature/branches
feature/remote-repositories
bugfix/fix-readme-link
hotfix/fix-production-error
docs/update-readme
release/v1.0.0
```

## Common branch prefixes

| Prefix | Purpose |
|---|---|
| `feature/` | New feature or new section |
| `bugfix/` | Normal bug fix |
| `hotfix/` | Urgent production fix |
| `docs/` | Documentation-only change |
| `release/` | Release preparation |
| `chore/` | Maintenance task |
| `refactor/` | Code restructuring |
| `test/` | Test-related changes |

## Rename branches

| Command | Description |
|---|---|
| `git branch -m new-name` | Rename current branch |
| `git branch -m old-name new-name` | Rename another local branch |

Example:

```bash
git branch -m feature/old-name feature/new-name
```

## Delete local branches

| Command | Description |
|---|---|
| `git branch -d branch-name` | Safely delete merged local branch |
| `git branch -D branch-name` | Force delete local branch |

Recommended:

```bash
git branch -d feature/branches
```

Force delete only when sure:

```bash
git branch -D feature/branches
```

## Delete remote branches

```bash
git push origin --delete branch-name
```

Example:

```bash
git push origin --delete feature/branches
```

## Clean deleted remote references

```bash
git fetch --prune
```

or:

```bash
git fetch -p
```

## Check merged branches

```bash
git branch --merged
```

This shows branches already merged into the current branch.

## Check unmerged branches

```bash
git branch --no-merged
```

This shows branches not yet merged into the current branch.

## Common branch workflows

### Create a feature branch

```bash
git switch main
git switch -c feature/my-topic
```

### Work and commit

```bash
git status
git add .
git commit -m "Add my topic"
```

### Merge into main

```bash
git switch main
git merge feature/my-topic
```

### Delete after merge

```bash
git branch -d feature/my-topic
```

## Update feature branch with main

Using merge:

```bash
git switch feature/my-topic
git merge main
```

Using rebase:

```bash
git switch feature/my-topic
git rebase main
```

## Switch to remote branch

```bash
git fetch
git switch branch-name
```

If needed:

```bash
git switch -c branch-name origin/branch-name
```

## Common mistakes

| Mistake | Safer habit |
|---|---|
| Working directly on `main` | Create a feature branch |
| Creating branch from outdated `main` | Update `main` first |
| Using vague branch names | Use `type/description` |
| Deleting unmerged branch | Use `git branch -d` first |
| Forgetting current branch | Run `git branch` |

## Most important commands

```bash
git branch
git switch branch-name
git switch -c feature/name
git push -u origin feature/name
git branch -d feature/name
```

## Summary

Basic branch flow:

```bash
git switch main
git switch -c feature/new-topic
git add .
git commit -m "Add new topic"
git switch main
git merge feature/new-topic
git branch -d feature/new-topic
```