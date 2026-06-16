# Fetch

`git fetch` downloads information from a remote repository without automatically changing your current working branch.

It is one of the safest commands for checking remote changes.

## What is git fetch?

`git fetch` contacts the remote repository and downloads new commits, branches, and tags.

Basic command:

```bash
git fetch
```

Or:

```bash
git fetch origin
```

This updates your remote-tracking branches, such as:

```txt
origin/main
origin/feature/remote-repositories
```

## Fetch does not merge

The most important thing to understand is:

```txt
git fetch downloads changes but does not integrate them into your current branch.
```

This makes it safer than `git pull`.

## Fetch vs pull

| Command | Downloads changes | Integrates changes automatically |
|---|---|---|
| `git fetch` | Yes | No |
| `git pull` | Yes | Yes |

`git pull` is similar to:

```txt
git fetch + git merge
```

## Why use git fetch?

Use `git fetch` when you want to:

- See what changed remotely before merging.
- Update your remote-tracking branches.
- Check if your branch is behind.
- Review remote commits safely.
- Avoid unexpected automatic merges.
- Prepare for a rebase or merge.

## Basic fetch

```bash
git fetch origin
```

This downloads updates from the remote named `origin`.

## Fetch all remotes

If your repository has multiple remotes:

```bash
git fetch --all
```

This downloads updates from all configured remotes.

## Fetch and prune deleted branches

If a branch was deleted on GitHub but still appears locally as a remote-tracking branch, use:

```bash
git fetch --prune
```

Or:

```bash
git fetch -p
```

This cleans outdated remote-tracking references.

## Example: check remote changes before merging

First, fetch:

```bash
git fetch origin
```

Then compare your local branch with the remote branch:

```bash
git log --oneline main..origin/main
```

This shows commits that exist in `origin/main` but not in your local `main`.

## Compare local and remote branches

To see what is different between local `main` and remote `origin/main`:

```bash
git diff main origin/main
```

To see commits your local branch does not have:

```bash
git log --oneline main..origin/main
```

To see commits your local branch has that remote does not:

```bash
git log --oneline origin/main..main
```

## Update main using fetch and merge

Instead of using:

```bash
git pull origin main
```

You can do the steps manually:

```bash
git fetch origin
git merge origin/main
```

This gives you more control.

## Update main using fetch and rebase

Another option:

```bash
git fetch origin
git rebase origin/main
```

This reapplies your local commits on top of the latest remote branch.

Use this only when you understand rebase.

## Fetch a specific branch

```bash
git fetch origin branch-name
```

Example:

```bash
git fetch origin main
```

This fetches only the specified branch from the remote.

## Fetch tags

To fetch tags:

```bash
git fetch --tags
```

Tags are commonly used for releases and versions.

## Remote-tracking branches

Remote-tracking branches are local references that represent the state of remote branches.

Examples:

```txt
origin/main
origin/feature/basic-git-commands
origin/feature/remote-repositories
```

You usually do not commit directly to remote-tracking branches.

They are references used to see what exists on the remote.

## Check remote branches after fetch

```bash
git branch -r
```

Example output:

```txt
origin/main
origin/feature/basic-git-commands
origin/feature/branches
origin/feature/remote-repositories
```

## Check all branches

```bash
git branch -a
```

This shows both local and remote-tracking branches.

## Example: safe update workflow

```bash
git status
git fetch origin
git log --oneline main..origin/main
git merge origin/main
```

This lets you inspect remote changes before integrating them.

## Example: check if your feature branch is behind main

```bash
git fetch origin
git log --oneline feature/remote-repositories..origin/main
```

This shows commits in `origin/main` that are not in your feature branch.

## Example: bring latest main into feature branch

Using merge:

```bash
git switch feature/remote-repositories
git fetch origin
git merge origin/main
```

Using rebase:

```bash
git switch feature/remote-repositories
git fetch origin
git rebase origin/main
```

## Fetch before opening a pull request

Before creating a pull request, it is useful to update your view of the remote repository:

```bash
git fetch origin
git status
```

Then check your branch history:

```bash
git log --oneline --graph --decorate --all
```

## Common fetch commands

| Command | Purpose |
|---|---|
| `git fetch` | Fetches from the default remote |
| `git fetch origin` | Fetches from `origin` |
| `git fetch --all` | Fetches from all remotes |
| `git fetch --prune` | Removes outdated remote-tracking branches |
| `git fetch -p` | Short version of prune |
| `git fetch --tags` | Fetches tags |
| `git fetch origin main` | Fetches a specific branch |

## Common mistakes

### Mistake 1: Thinking fetch updates local main automatically

`git fetch` does not update your local branch directly.

It updates remote-tracking branches like:

```txt
origin/main
```

To update local `main`, you still need to merge or rebase.

### Mistake 2: Confusing origin/main with main

`main` is your local branch.

`origin/main` represents the remote branch.

They are related, but they are not the same.

### Mistake 3: Never pruning deleted remote branches

If old remote branches still appear locally, run:

```bash
git fetch --prune
```

### Mistake 4: Using pull when you only wanted to inspect remote changes

If you only want to inspect changes, use:

```bash
git fetch
```

not:

```bash
git pull
```

## Professional recommendation

Use `git fetch` when you want control.

Recommended inspection workflow:

```bash
git fetch origin
git log --oneline --graph --decorate --all
git status
```

Then decide whether to merge, rebase, or do nothing.

## Summary

`git fetch` downloads remote changes without modifying your current branch automatically.

Basic command:

```bash
git fetch origin
```

Fetch and clean deleted remote branches:

```bash
git fetch --prune
```

Compare local and remote:

```bash
git log --oneline main..origin/main
git diff main origin/main
```

`git fetch` is safer than `git pull` when you want to inspect changes first.

## Recommended next topic

Continue with:

```txt
docs/03-remote-repositories/upstream-tracking.md
```