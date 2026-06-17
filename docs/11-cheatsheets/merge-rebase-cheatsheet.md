# Merge and Rebase Cheatsheet

Quick reference for integrating branches using merge and rebase.

## Merge basics

| Command | Description |
|---|---|
| `git merge branch-name` | Merge branch into current branch |
| `git merge --no-ff branch-name` | Force a merge commit |
| `git merge --ff-only branch-name` | Merge only if fast-forward is possible |
| `git merge --abort` | Abort an active merge |

## Basic merge workflow

```bash
git switch main
git merge feature/my-topic
```

Meaning:

```txt
Merge feature/my-topic into main.
```

## Merge direction matters

This:

```bash
git switch main
git merge feature/my-topic
```

means:

```txt
feature/my-topic → main
```

This:

```bash
git switch feature/my-topic
git merge main
```

means:

```txt
main → feature/my-topic
```

## Rebase basics

| Command | Description |
|---|---|
| `git rebase main` | Rebase current branch onto `main` |
| `git rebase --continue` | Continue rebase after resolving conflicts |
| `git rebase --abort` | Abort active rebase |
| `git rebase --skip` | Skip current commit during rebase |
| `git rebase -i HEAD~3` | Interactive rebase last 3 commits |
| `git rebase -i main` | Interactive rebase current branch onto main |

## Basic rebase workflow

```bash
git switch feature/my-topic
git rebase main
```

Meaning:

```txt
Replay feature/my-topic commits on top of main.
```

## Merge vs rebase

| Topic | Merge | Rebase |
|---|---|---|
| Main purpose | Combine branches | Move commits to a new base |
| History | Preserves branch structure | Creates linear history |
| Rewrites commits | No | Yes |
| Safer for shared branches | Yes | No |
| Good for beginners | Yes | After learning basics |
| May require force push | Usually no | Sometimes yes |

## When to use merge

Use merge when:

```txt
You want safety.
You are working on shared branches.
You want to preserve branch history.
You are not sure which option to use.
```

Command:

```bash
git switch main
git merge feature/my-topic
```

## When to use rebase

Use rebase when:

```txt
You want a clean linear history.
You are working on your own local branch.
Your team uses a rebase workflow.
You understand history rewriting.
```

Command:

```bash
git switch feature/my-topic
git rebase main
```

## Fast-forward merge

```bash
git merge --ff-only feature/my-topic
```

Use when you only want a linear fast-forward merge.

## No fast-forward merge

```bash
git merge --no-ff feature/my-topic
```

Use when you want to preserve feature branch context with a merge commit.

## Squash merge

```bash
git merge --squash feature/my-topic
git commit -m "Add my topic"
```

Use when you want one clean commit on the target branch.

## Rebase then fast-forward merge

```bash
git switch feature/my-topic
git rebase main
git switch main
git merge --ff-only feature/my-topic
```

This creates a linear history.

## Merge conflict workflow

If merge causes conflicts:

```bash
git status
# edit conflicted files
git add .
git commit
```

Abort merge:

```bash
git merge --abort
```

## Rebase conflict workflow

If rebase causes conflicts:

```bash
git status
# edit conflicted files
git add .
git rebase --continue
```

Abort rebase:

```bash
git rebase --abort
```

## Conflict markers

```txt
<<<<<<< HEAD
Current branch changes
=======
Incoming changes
>>>>>>> branch-name
```

Remove these markers after resolving the file.

## Keep current branch version during conflict

```bash
git checkout --ours file-name
git add file-name
```

or:

```bash
git restore --ours file-name
git add file-name
```

## Keep incoming version during conflict

```bash
git checkout --theirs file-name
git add file-name
```

or:

```bash
git restore --theirs file-name
git add file-name
```

## Interactive rebase actions

| Action | Meaning |
|---|---|
| `pick` | Keep commit |
| `reword` | Change commit message |
| `edit` | Stop to modify commit |
| `squash` | Combine with previous commit and edit message |
| `fixup` | Combine with previous commit and discard message |
| `drop` | Remove commit |

## Interactive rebase example

```bash
git rebase -i HEAD~3
```

Example editor:

```txt
pick a1b2c3d Add rebase basics
fixup e4f5g6h Fix typo
fixup i7j8k9l Update example
```

## Safe rebase rule

```txt
Do not rebase public/shared branches unless your team agreed to it.
```

## Force push after rebase

If branch was already pushed and you rebased it:

```bash
git push --force-with-lease
```

Avoid:

```bash
git push --force
```

unless you fully understand the risk.

## Common mistakes

| Mistake | Safer habit |
|---|---|
| Merging into wrong branch | Check `git branch` first |
| Rebasing shared branches | Rebase only your own branches |
| Ignoring conflicts | Resolve carefully and check files |
| Using force push carelessly | Prefer `--force-with-lease` |
| Forgetting direction | Current branch receives the merge/rebase result |

## Recommended workflows

### Simple merge

```bash
git switch main
git merge feature/my-topic
```

### Clean linear history

```bash
git switch feature/my-topic
git rebase main
git switch main
git merge --ff-only feature/my-topic
```

### One commit per topic

```bash
git switch main
git merge --squash feature/my-topic
git commit -m "Add my topic"
```

## Summary

Merge:

```bash
git switch main
git merge feature/my-topic
```

Rebase:

```bash
git switch feature/my-topic
git rebase main
```

Abort merge:

```bash
git merge --abort
```

Abort rebase:

```bash
git rebase --abort
```

Golden rule:

```txt
Use merge when unsure. Use rebase when you understand history rewriting.
```