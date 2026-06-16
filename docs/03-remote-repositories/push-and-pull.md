# Push and Pull

`git push` and `git pull` are used to synchronize changes between your local repository and a remote repository.

These commands are essential when working with GitHub and collaborating with other developers.

## What is git push?

`git push` uploads local commits to a remote repository.

Basic syntax:

```bash
git push remote-name branch-name
```

Example:

```bash
git push origin main
```

This means:

```txt
Upload my local main branch to the remote repository named origin.
```

## What is git pull?

`git pull` downloads changes from a remote repository and integrates them into your current local branch.

Basic syntax:

```bash
git pull remote-name branch-name
```

Example:

```bash
git pull origin main
```

This means:

```txt
Download changes from origin/main and integrate them into my current branch.
```

## Push vs pull

| Command | Direction | Purpose |
|---|---|---|
| `git push` | Local to remote | Uploads local commits |
| `git pull` | Remote to local | Downloads and integrates remote changes |

## Before pushing

Before pushing, it is recommended to check your status:

```bash
git status
```

Then check your commit history:

```bash
git log --oneline
```

If everything looks correct, push:

```bash
git push
```

Or:

```bash
git push origin branch-name
```

## Push a branch for the first time

When pushing a new branch for the first time, use:

```bash
git push -u origin branch-name
```

Example:

```bash
git push -u origin feature/remote-repositories
```

The `-u` option sets the upstream branch.

After that, you can usually push with:

```bash
git push
```

## Push current branch

If the upstream is already configured:

```bash
git push
```

This pushes your current branch to its configured remote branch.

## Push to a specific branch

```bash
git push origin feature/remote-repositories
```

This pushes your local branch to the remote branch with the same name.

## Push local branch to a different remote branch name

```bash
git push origin local-branch:remote-branch
```

Example:

```bash
git push origin feature/remotes:feature/remote-repositories
```

This pushes local `feature/remotes` to remote `feature/remote-repositories`.

## Before pulling

Before pulling remote changes, check your local status:

```bash
git status
```

If you have uncommitted changes, Git may prevent the pull or create conflicts.

You can:

1. Commit your changes.
2. Stash your changes.
3. Discard your changes if they are not needed.

## Basic pull

```bash
git pull origin main
```

This fetches and integrates changes from `origin/main`.

## Pull current branch

If your branch has upstream tracking configured:

```bash
git pull
```

This pulls from the remote branch connected to your current local branch.

## What git pull actually does

`git pull` is a combination of two steps:

```txt
git fetch + git merge
```

In simple terms:

```txt
git fetch downloads remote changes.
git merge integrates those changes into your current branch.
```

So this:

```bash
git pull origin main
```

Is similar to:

```bash
git fetch origin
git merge origin/main
```

## Pull with rebase

Some teams prefer pulling with rebase:

```bash
git pull --rebase origin main
```

This downloads remote changes and reapplies your local commits on top of them.

This can create a cleaner history, but you should understand rebase before using it regularly.

## Pull with merge

Default pull behavior often uses merge:

```bash
git pull origin main
```

This may create a merge commit if local and remote histories have diverged.

## Example: working on a feature branch

Current branch:

```txt
feature/remote-repositories
```

Recommended workflow:

```bash
git status
git add .
git commit -m "Add remote repositories documentation"
git push -u origin feature/remote-repositories
```

If the branch already has upstream:

```bash
git push
```

## Example: update main before creating a new branch

```bash
git switch main
git pull origin main
git switch -c feature/new-topic
```

This ensures your new branch starts from the latest version of `main`.

## Example: update your feature branch with main

If `main` has new changes and you want your feature branch updated:

```bash
git switch main
git pull origin main
git switch feature/remote-repositories
git merge main
```

Or using rebase:

```bash
git switch main
git pull origin main
git switch feature/remote-repositories
git rebase main
```

Use rebase only if it fits your workflow.

## Push after merge to main

If you merged your feature branch into `main`, push `main`:

```bash
git switch main
git push origin main
```

## Common push commands

| Command | Purpose |
|---|---|
| `git push` | Pushes current branch to upstream |
| `git push origin main` | Pushes local `main` to `origin/main` |
| `git push -u origin branch-name` | Pushes and sets upstream |
| `git push origin --delete branch-name` | Deletes a remote branch |
| `git push --force-with-lease` | Safely force pushes, usually after rebase |

## Common pull commands

| Command | Purpose |
|---|---|
| `git pull` | Pulls from the upstream branch |
| `git pull origin main` | Pulls from `origin/main` |
| `git pull --rebase` | Pulls using rebase instead of merge |
| `git pull --ff-only` | Pulls only if fast-forward is possible |

## Fast-forward pull

A fast-forward happens when your local branch has no unique commits and Git can simply move the branch pointer forward.

Example:

```bash
git pull --ff-only
```

This is a safe option when you do not want Git to create merge commits automatically.

## Force push warning

Sometimes after rebase, Git may require a force push.

Avoid this unless you understand the impact:

```bash
git push --force
```

A safer option is:

```bash
git push --force-with-lease
```

`--force-with-lease` helps prevent overwriting someone else's remote work.

## Common mistakes

### Mistake 1: Committing but forgetting to push

A commit is local.

To upload it to GitHub:

```bash
git push
```

### Mistake 2: Pulling with uncommitted changes

Before pulling, check:

```bash
git status
```

If needed, commit or stash your changes.

### Mistake 3: Pushing to the wrong branch

Check your current branch:

```bash
git branch
```

Then push:

```bash
git push origin branch-name
```

### Mistake 4: Using force push carelessly

Avoid:

```bash
git push --force
```

Prefer:

```bash
git push --force-with-lease
```

Only use force push when you understand why it is needed.

### Mistake 5: Not setting upstream

If Git shows an error like:

```txt
The current branch has no upstream branch.
```

Use:

```bash
git push -u origin branch-name
```

## Professional recommendation

Before pushing:

```bash
git status
git log --oneline
```

Before pulling:

```bash
git status
```

When creating a new branch:

```bash
git push -u origin branch-name
```

When working with others, avoid force push unless agreed by the team.

## Summary

Use `git push` to upload commits.

Use `git pull` to download and integrate changes.

Basic push:

```bash
git push origin branch-name
```

Basic pull:

```bash
git pull origin branch-name
```

First push of a new branch:

```bash
git push -u origin branch-name
```

`git pull` is similar to:

```txt
git fetch + git merge
```

## Recommended next topic

Continue with:

```txt
docs/03-remote-repositories/fetch.md
```