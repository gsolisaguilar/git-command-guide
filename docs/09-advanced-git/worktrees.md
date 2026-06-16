# Worktrees

`git worktree` allows you to have multiple working directories connected to the same Git repository.

This lets you work on multiple branches at the same time without constantly switching branches in one folder.

## What is a worktree?

A worktree is an additional working directory linked to the same Git repository.

In simple terms:

```txt
Worktrees let you check out multiple branches in separate folders.
```

## Why worktrees are useful

Worktrees are useful when:

- You need to work on multiple branches at the same time.
- You want to test a branch without disturbing current work.
- You need to apply a hotfix while keeping unfinished work.
- You want separate folders for separate tasks.
- You want to avoid excessive stashing or branch switching.

## Basic concept

Without worktrees, one repository folder usually has one active branch at a time.

With worktrees, you can have:

```txt
project/
project-feature/
project-hotfix/
```

Each folder can be on a different branch.

## Check existing worktrees

```bash
git worktree list
```

Example:

```txt
C:/projects/git-commands-guide        a1b2c3d [main]
C:/projects/git-commands-guide-rebase e4f5g6h [feature/rebase-guide]
```

## Add a worktree for an existing branch

```bash
git worktree add path branch-name
```

Example:

```bash
git worktree add ../git-commands-guide-rebase feature/rebase-guide
```

This creates a new folder one level up and checks out the branch there.

## Add a worktree with a new branch

```bash
git worktree add -b new-branch-name path
```

Example:

```bash
git worktree add -b feature/worktrees ../git-commands-guide-worktrees
```

This creates a new branch and a new worktree folder.

## Example folder structure

```txt
projects/
├── git-commands-guide/
│   └── main branch
│
├── git-commands-guide-rebase/
│   └── feature/rebase-guide branch
│
└── git-commands-guide-worktrees/
    └── feature/worktrees branch
```

## Work on a branch in another folder

After creating the worktree:

```bash
cd ../git-commands-guide-worktrees
git status
```

You are now working in a separate folder but still connected to the same repository.

## Important rule

The same branch cannot normally be checked out in two worktrees at the same time.

Example:

```txt
main cannot be active in two worktrees at once.
```

This prevents conflicting changes in the same branch.

## Remove a worktree

When you no longer need a worktree:

```bash
git worktree remove path
```

Example:

```bash
git worktree remove ../git-commands-guide-worktrees
```

The worktree must usually be clean before removal.

## Force remove a worktree

If needed:

```bash
git worktree remove --force path
```

Use carefully.

## Prune stale worktree information

If a worktree folder was deleted manually, Git may still remember it.

Clean stale records:

```bash
git worktree prune
```

## Lock a worktree

You can lock a worktree to prevent accidental pruning.

```bash
git worktree lock path
```

Example:

```bash
git worktree lock ../git-commands-guide-release
```

## Unlock a worktree

```bash
git worktree unlock path
```

## Worktree for hotfix example

You are working on a feature and have unfinished changes.

Instead of stashing, create a separate hotfix worktree:

```bash
git worktree add -b hotfix/fix-readme-link ../git-commands-guide-hotfix main
```

Then:

```bash
cd ../git-commands-guide-hotfix
```

Fix the issue, commit it, and merge later.

## Worktree for release example

```bash
git worktree add -b release/v1.0.0 ../git-commands-guide-release main
```

This gives you a separate folder to prepare a release.

## Worktree for reviewing another branch

```bash
git worktree add ../review-branch feature/advanced-git-commands
```

Now you can inspect that branch without switching your main working directory.

## Worktree vs clone

| Option | Description |
|---|---|
| Clone | Creates a completely separate copy of the repository |
| Worktree | Creates another working directory linked to the same repository |

Worktrees are usually more efficient than cloning the same repo multiple times.

## Worktree vs stash

| Situation | Better option |
|---|---|
| Temporary unfinished changes | `git stash` |
| Work on two branches at the same time | `git worktree` |
| Quick branch switch | `git switch` |
| Long parallel tasks | `git worktree` |

## Common worktree commands

| Command | Purpose |
|---|---|
| `git worktree list` | Lists worktrees |
| `git worktree add path branch` | Adds worktree for existing branch |
| `git worktree add -b branch path` | Creates new branch and worktree |
| `git worktree remove path` | Removes a worktree |
| `git worktree remove --force path` | Force removes a worktree |
| `git worktree prune` | Cleans stale worktree records |
| `git worktree lock path` | Locks a worktree |
| `git worktree unlock path` | Unlocks a worktree |

## Common mistakes

### Mistake 1: Manually deleting a worktree folder

If you manually delete a worktree folder, Git may keep stale metadata.

Use:

```bash
git worktree prune
```

Better:

```bash
git worktree remove path
```

### Mistake 2: Trying to checkout the same branch in multiple worktrees

Git usually prevents the same branch from being active in two worktrees.

Create a new branch if needed.

### Mistake 3: Forgetting which folder is which branch

Use:

```bash
git worktree list
```

and:

```bash
git branch
```

### Mistake 4: Removing a worktree with uncommitted changes

Check status inside the worktree:

```bash
git status
```

Commit, stash, or discard changes before removing it.

## Best practices

- Use clear folder names for worktrees.
- Use one branch per worktree.
- Check `git worktree list` often.
- Remove worktrees when no longer needed.
- Avoid manually deleting worktree folders.
- Use worktrees for hotfixes, releases, and parallel work.
- Keep each worktree clean and focused.

## Professional recommendation

Use worktrees when you need parallel work without interrupting your current branch.

Example:

```bash
git worktree add -b feature/worktrees ../git-commands-guide-worktrees main
```

Then work in the new folder:

```bash
cd ../git-commands-guide-worktrees
git status
```

## Summary

`git worktree` allows multiple working directories for one repository.

List worktrees:

```bash
git worktree list
```

Create worktree:

```bash
git worktree add path branch-name
```

Create worktree with new branch:

```bash
git worktree add -b branch-name path
```

Remove worktree:

```bash
git worktree remove path
```

Golden rule:

```txt
Use worktrees when you need to work on multiple branches at the same time.
```

## Recommended next topic

Continue with:

```txt
docs/10-professional-workflows/git-flow.md
```