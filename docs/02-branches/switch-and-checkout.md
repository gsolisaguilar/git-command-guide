# Switch and Checkout

Git provides different commands to move between branches and restore files.

The two most common commands related to this are:

```bash
git switch
git checkout
```

`git switch` is the modern command used to change branches.

`git checkout` is the older command that can change branches, create branches, and restore files.

## Why there are two commands

For many years, `git checkout` was used for different tasks:

- Switching branches.
- Creating branches.
- Restoring files.
- Checking out commits.

Because it had many responsibilities, Git introduced newer commands to make things clearer:

```bash
git switch
git restore
```

In modern Git workflows:

| Task | Recommended command |
|---|---|
| Change branches | `git switch` |
| Create and switch branches | `git switch -c` |
| Restore files | `git restore` |
| Older branch switching | `git checkout` |

## Check current branch

Before switching branches, check where you are:

```bash
git branch
```

Example:

```txt
* feature/basic-git-commands
  main
```

The `*` indicates the current branch.

You can also use:

```bash
git status
```

Example:

```txt
On branch feature/basic-git-commands
```

## Switch to an existing branch

Use:

```bash
git switch branch-name
```

Example:

```bash
git switch main
```

This moves you to the `main` branch.

## Create and switch to a new branch

Use:

```bash
git switch -c branch-name
```

Example:

```bash
git switch -c feature/branching-guide
```

This creates the branch and switches to it.

## Switch back to the previous branch

You can switch back to the previous branch with:

```bash
git switch -
```

Example:

```bash
git switch main
git switch -
```

This returns you to the branch you were using before.

## Older syntax: git checkout

You may still see this command in many projects, tutorials, and teams:

```bash
git checkout branch-name
```

Example:

```bash
git checkout main
```

This switches to the `main` branch.

## Create and switch using checkout

Older syntax:

```bash
git checkout -b branch-name
```

Example:

```bash
git checkout -b feature/branching-guide
```

This does the same as:

```bash
git switch -c feature/branching-guide
```

## switch vs checkout

| Action | Modern command | Older command |
|---|---|---|
| Switch to existing branch | `git switch main` | `git checkout main` |
| Create and switch branch | `git switch -c feature/name` | `git checkout -b feature/name` |
| Switch to previous branch | `git switch -` | `git checkout -` |
| Restore a file | `git restore file.md` | `git checkout -- file.md` |

## Recommended usage

For beginners and modern workflows, prefer:

```bash
git switch
```

Use `git checkout` only when:

- Working on older projects.
- Following old documentation.
- Checking out specific commits.
- Your Git version does not support `git switch`.

## Switching with uncommitted changes

If you have uncommitted changes, Git may prevent you from switching branches.

Example error:

```txt
error: Your local changes to the following files would be overwritten by checkout
```

This means switching branches could overwrite your work.

## What to do before switching branches

Before switching, check:

```bash
git status
```

If you have changes, you can:

1. Commit them.
2. Stash them.
3. Discard them if they are not needed.

## Option 1: Commit before switching

```bash
git add .
git commit -m "Save current work"
git switch main
```

Use this when your changes are ready to be saved.

## Option 2: Stash before switching

```bash
git stash
git switch main
```

Use this when your changes are not ready for a commit.

Later, you can recover them with:

```bash
git stash pop
```

## Option 3: Discard changes before switching

Be careful with this option because it removes local changes.

To discard changes in one file:

```bash
git restore file-name
```

Example:

```bash
git restore README.md
```

To discard all local changes in tracked files:

```bash
git restore .
```

## Switch to a remote branch

If a branch exists on GitHub but not locally, first fetch remote references:

```bash
git fetch
```

Then switch to the branch:

```bash
git switch branch-name
```

Example:

```bash
git switch feature/remote-branch
```

If Git cannot find it automatically, use:

```bash
git switch -c branch-name origin/branch-name
```

Example:

```bash
git switch -c feature/remote-branch origin/feature/remote-branch
```

## Checkout a specific commit

Sometimes you may want to inspect an old commit.

Use:

```bash
git checkout commit-hash
```

Example:

```bash
git checkout a1b2c3d
```

This puts you in a detached HEAD state.

## Detached HEAD

Detached HEAD means you are not currently on a branch.

You are viewing a specific commit directly.

Example:

```txt
HEAD detached at a1b2c3d
```

This is useful for inspection, but you should be careful when making changes in this state.

## Return from detached HEAD

To go back to a branch:

```bash
git switch main
```

Or:

```bash
git switch feature/basic-git-commands
```

## Create a branch from a specific commit

If you want to create a branch starting from an old commit:

```bash
git switch -c branch-name commit-hash
```

Example:

```bash
git switch -c experiment/old-version a1b2c3d
```

## Common examples

### Switch to main

```bash
git switch main
```

### Create a feature branch

```bash
git switch -c feature/add-readme-section
```

### Switch back to previous branch

```bash
git switch -
```

### Use older checkout syntax

```bash
git checkout main
```

### Create branch with older checkout syntax

```bash
git checkout -b feature/add-readme-section
```

## Professional branch switching workflow

Before switching branches:

```bash
git status
```

If clean:

```bash
git switch main
```

If not clean:

```bash
git add .
git commit -m "Save current progress"
git switch main
```

Or:

```bash
git stash
git switch main
```

## Common mistakes

### Mistake 1: Switching branches with unsaved work

Always check:

```bash
git status
```

before switching.

### Mistake 2: Confusing switch and checkout

Use `git switch` for branch movement.

Use `git restore` for restoring files.

Use `git checkout` when needed for older workflows or checking out commits.

### Mistake 3: Working in detached HEAD without realizing it

If you see:

```txt
HEAD detached
```

you are not on a normal branch.

Return to a branch with:

```bash
git switch main
```

### Mistake 4: Creating a branch from the wrong base

Before creating a branch, make sure you are on the correct branch.

Example:

```bash
git switch main
git pull origin main
git switch -c feature/new-task
```

## Useful commands

| Command | Purpose |
|---|---|
| `git switch branch-name` | Switches to an existing branch |
| `git switch -c branch-name` | Creates and switches to a new branch |
| `git switch -` | Switches to the previous branch |
| `git checkout branch-name` | Older way to switch branches |
| `git checkout -b branch-name` | Older way to create and switch branches |
| `git checkout commit-hash` | Checks out a specific commit |
| `git fetch` | Updates remote branch references |
| `git status` | Checks if it is safe to switch |

## Summary

Use `git switch` for branch navigation.

Basic examples:

```bash
git switch main
git switch -c feature/new-task
git switch -
```

Older syntax:

```bash
git checkout main
git checkout -b feature/new-task
```

Before switching branches, always check:

```bash
git status
```

## Recommended next topic

Continue with:

```txt
docs/02-branches/branch-naming.md
```