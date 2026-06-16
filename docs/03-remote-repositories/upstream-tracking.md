# Upstream Tracking

Upstream tracking connects a local branch with a remote branch.

When a local branch tracks a remote branch, Git knows where to push and where to pull from by default.

## What is an upstream branch?

An upstream branch is the remote branch connected to your current local branch.

Example:

```txt
Local branch:  feature/remote-repositories
Remote branch: origin/feature/remote-repositories
```

If these are connected, your local branch tracks the remote branch.

## Why upstream tracking is useful

Upstream tracking allows you to use shorter commands.

Instead of:

```bash
git push origin feature/remote-repositories
```

You can use:

```bash
git push
```

Instead of:

```bash
git pull origin feature/remote-repositories
```

You can use:

```bash
git pull
```

## First push with upstream

When pushing a new branch for the first time, use:

```bash
git push -u origin branch-name
```

Example:

```bash
git push -u origin feature/remote-repositories
```

The `-u` means:

```txt
Set this remote branch as the upstream branch for my current local branch.
```

After that, you can use:

```bash
git push
```

and:

```bash
git pull
```

## Alternative long option

The `-u` option is short for:

```bash
--set-upstream
```

So this:

```bash
git push -u origin feature/remote-repositories
```

is the same as:

```bash
git push --set-upstream origin feature/remote-repositories
```

## Check upstream tracking

Use:

```bash
git branch -vv
```

Example output:

```txt
* feature/remote-repositories a1b2c3d [origin/feature/remote-repositories] Add remote docs
  main                        e4f5g6h [origin/main] Add branch docs
```

This means:

```txt
feature/remote-repositories tracks origin/feature/remote-repositories
main tracks origin/main
```

## Check current branch status

Use:

```bash
git status
```

Example output:

```txt
On branch feature/remote-repositories
Your branch is up to date with 'origin/feature/remote-repositories'.
```

This means your local branch is connected to the remote branch.

## When upstream is missing

If your branch does not have upstream configured, Git may show:

```txt
fatal: The current branch feature/remote-repositories has no upstream branch.
```

Or:

```txt
There is no tracking information for the current branch.
```

To fix this, use:

```bash
git push -u origin feature/remote-repositories
```

## Set upstream for an existing branch

If the remote branch already exists, you can connect your local branch to it:

```bash
git branch --set-upstream-to=origin/branch-name
```

Example:

```bash
git branch --set-upstream-to=origin/feature/remote-repositories
```

Then verify:

```bash
git branch -vv
```

## Set upstream while pushing

Most common option:

```bash
git push -u origin branch-name
```

Example:

```bash
git push -u origin feature/remote-repositories
```

This both pushes the branch and configures upstream tracking.

## Unset upstream

To remove upstream tracking from the current branch:

```bash
git branch --unset-upstream
```

This disconnects the local branch from its tracked remote branch.

## Upstream and git push

If upstream is configured, this works:

```bash
git push
```

If upstream is not configured, you need:

```bash
git push origin branch-name
```

or:

```bash
git push -u origin branch-name
```

## Upstream and git pull

If upstream is configured, this works:

```bash
git pull
```

If upstream is not configured, you need:

```bash
git pull origin branch-name
```

or you need to set the upstream branch.

## Upstream and branch status

When upstream is configured, `git status` can show whether your branch is:

- Up to date.
- Ahead of remote.
- Behind remote.
- Diverged from remote.

## Branch is ahead

Example:

```txt
Your branch is ahead of 'origin/feature/remote-repositories' by 2 commits.
```

This means you have local commits that are not on GitHub yet.

Fix:

```bash
git push
```

## Branch is behind

Example:

```txt
Your branch is behind 'origin/main' by 3 commits.
```

This means the remote branch has commits that your local branch does not have.

Fix:

```bash
git pull
```

Or inspect first:

```bash
git fetch
```

## Branch has diverged

Example:

```txt
Your branch and 'origin/main' have diverged.
```

This means both your local branch and the remote branch have different commits.

You may need to merge or rebase.

Example with merge:

```bash
git pull
```

Example with rebase:

```bash
git pull --rebase
```

Use rebase only when it fits your workflow.

## Tracking main

Usually, local `main` tracks `origin/main`.

Check:

```bash
git branch -vv
```

Example:

```txt
main e4f5g6h [origin/main] Add documentation
```

If not configured:

```bash
git branch --set-upstream-to=origin/main main
```

## Tracking a feature branch

Example for your current branch:

```bash
git switch feature/remote-repositories
git push -u origin feature/remote-repositories
```

Now the local branch tracks:

```txt
origin/feature/remote-repositories
```

## Rename branch and upstream tracking

If you rename a branch, you may need to update upstream tracking.

Example:

```bash
git branch -m old-name new-name
git push origin --delete old-name
git push -u origin new-name
```

Then verify:

```bash
git branch -vv
```

## Delete old remote branch after merge

After a feature branch is merged into `main`, you can delete it remotely:

```bash
git push origin --delete feature/remote-repositories
```

Then clean local remote-tracking references:

```bash
git fetch --prune
```

## Common upstream commands

| Command | Purpose |
|---|---|
| `git push -u origin branch-name` | Pushes branch and sets upstream |
| `git push --set-upstream origin branch-name` | Same as `git push -u` |
| `git branch -vv` | Shows upstream tracking |
| `git branch --set-upstream-to=origin/branch-name` | Sets upstream manually |
| `git branch --unset-upstream` | Removes upstream tracking |
| `git status` | Shows ahead/behind status |

## Common mistakes

### Mistake 1: Not using -u on first push

If you push a branch without upstream:

```bash
git push origin feature/remote-repositories
```

It may work, but later `git push` may not know where to push.

Better:

```bash
git push -u origin feature/remote-repositories
```

### Mistake 2: Pulling without tracking information

If Git says there is no tracking information, set upstream:

```bash
git branch --set-upstream-to=origin/branch-name
```

Or push with:

```bash
git push -u origin branch-name
```

### Mistake 3: Confusing local branch with remote branch

Example:

```txt
feature/remote-repositories
```

is local.

```txt
origin/feature/remote-repositories
```

is remote-tracking.

### Mistake 4: Deleting a remote branch but not pruning locally

If deleted branches still appear locally:

```bash
git fetch --prune
```

## Professional recommendation

When creating a new branch, use this flow:

```bash
git switch main
git pull origin main
git switch -c feature/remote-repositories
git push -u origin feature/remote-repositories
```

Then you can use:

```bash
git push
git pull
```

without writing the full remote and branch name each time.

## Summary

Upstream tracking connects a local branch to a remote branch.

Most common command:

```bash
git push -u origin branch-name
```

Check tracking:

```bash
git branch -vv
```

Set tracking manually:

```bash
git branch --set-upstream-to=origin/branch-name
```

Once upstream is configured, you can use:

```bash
git push
git pull
```

without specifying the remote and branch every time.

## Recommended next topic

Continue with:

```txt
docs/04-merges-and-conflicts/merge-basics.md
```