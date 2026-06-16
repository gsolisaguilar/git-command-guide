# Reset

`git reset` is used to move the current branch pointer to another commit.

It can also change the staging area and working directory depending on the option used.

`git reset` is powerful, but it can be dangerous if used incorrectly.

## What is git reset?

`git reset` moves `HEAD` and the current branch to a different commit.

It can affect three areas:

```txt
Commit history
Staging area
Working directory
```

## Main reset modes

The most common reset modes are:

```bash
git reset --soft
git reset --mixed
git reset --hard
```

Each one affects your repository differently.

## The three Git areas

To understand reset, remember these areas:

```txt
Working Directory
Staging Area
Local Repository
```

| Area | Meaning |
|---|---|
| Working Directory | Your actual files |
| Staging Area | Changes prepared for commit |
| Local Repository | Commit history |

## git reset --soft

`--soft` moves the branch pointer but keeps changes staged.

Syntax:

```bash
git reset --soft commit-hash
```

Example:

```bash
git reset --soft HEAD~1
```

This undoes the last commit but keeps the changes staged.

## When to use --soft

Use `--soft` when:

- You want to undo a commit but keep the changes staged.
- You want to rewrite the last commit.
- You want to combine changes into a new commit.

Example:

```bash
git reset --soft HEAD~1
git commit -m "New commit message"
```

## git reset --mixed

`--mixed` is the default reset mode.

Syntax:

```bash
git reset --mixed commit-hash
```

Or simply:

```bash
git reset commit-hash
```

Example:

```bash
git reset HEAD~1
```

This undoes the last commit and moves the changes back to the working directory.

The changes are not staged.

## When to use --mixed

Use `--mixed` when:

- You want to undo a commit but keep the file changes.
- You want to restage changes differently.
- You committed too early and want to reorganize the commit.

## git reset --hard

`--hard` moves the branch pointer and discards changes from the staging area and working directory.

Syntax:

```bash
git reset --hard commit-hash
```

Example:

```bash
git reset --hard HEAD~1
```

Warning:

```txt
git reset --hard can permanently discard local changes.
Use it carefully.
```

## When to use --hard

Use `--hard` only when:

- You are sure you do not need the discarded changes.
- You want to completely return to a previous commit.
- You are cleaning a local branch.
- You understand that local uncommitted changes may be lost.

## Reset modes comparison

| Command | Moves HEAD | Changes staging area | Changes working directory |
|---|---|---|---|
| `git reset --soft` | Yes | No, keeps staged | No |
| `git reset --mixed` | Yes | Yes, unstages | No |
| `git reset --hard` | Yes | Yes | Yes, discards changes |

## Undo the last commit but keep changes staged

```bash
git reset --soft HEAD~1
```

Use this when you want to redo the last commit.

## Undo the last commit and unstage changes

```bash
git reset HEAD~1
```

This is the same as:

```bash
git reset --mixed HEAD~1
```

## Undo the last commit and discard changes

```bash
git reset --hard HEAD~1
```

Warning:

```txt
This removes the last commit and discards its changes from your working directory.
```

## Reset to a specific commit

First, find the commit:

```bash
git log --oneline
```

Example:

```txt
a1b2c3d Add reset documentation
e4f5g6h Add restore documentation
i7j8k9l Add rebase guide
```

Reset to a commit:

```bash
git reset --soft e4f5g6h
```

Or:

```bash
git reset --hard e4f5g6h
```

## Reset a staged file

If you staged a file by mistake, older Git workflows use:

```bash
git reset HEAD file-name
```

Example:

```bash
git reset HEAD README.md
```

Modern Git recommends:

```bash
git restore --staged README.md
```

## Reset current branch to remote branch

Sometimes you want your local branch to match the remote branch exactly.

Example:

```bash
git fetch origin
git reset --hard origin/main
```

Warning:

```txt
This discards local commits and local tracked file changes that are not in origin/main.
```

Use carefully.

## Reset before pushing

Reset is safer before pushing because the rewritten commits are only local.

Example:

```bash
git reset --soft HEAD~1
```

This changes local history but does not affect anyone else if the commit was not pushed.

## Reset after pushing

Be careful using reset on commits that were already pushed.

If you reset pushed commits, you rewrite history.

To update the remote, you may need:

```bash
git push --force-with-lease
```

This can affect other people.

## Safer alternative for pushed commits

If the commit was already pushed, prefer:

```bash
git revert commit-hash
```

`git revert` creates a new commit that undoes the old commit without rewriting history.

## Reset vs revert

| Command | Rewrites history | Safe for pushed commits |
|---|---|---|
| `git reset` | Yes | Usually no |
| `git revert` | No | Yes |

## Practical examples

### Example 1: Fix last commit message and content

```bash
git reset --soft HEAD~1
git add .
git commit -m "Better commit message"
```

### Example 2: Undo last commit but keep files changed

```bash
git reset HEAD~1
```

### Example 3: Completely discard last commit

```bash
git reset --hard HEAD~1
```

### Example 4: Unstage all files

```bash
git reset
```

Or modern option:

```bash
git restore --staged .
```

## Recovering after reset

If you accidentally reset, you may be able to recover using:

```bash
git reflog
```

Then find the previous commit and reset back to it.

Example:

```bash
git reflog
git reset --hard commit-hash
```

`git reflog` is covered in the advanced Git section.

## Common reset commands

| Command | Purpose |
|---|---|
| `git reset --soft HEAD~1` | Undo last commit, keep changes staged |
| `git reset HEAD~1` | Undo last commit, keep changes unstaged |
| `git reset --hard HEAD~1` | Undo last commit and discard changes |
| `git reset HEAD file.md` | Unstage one file |
| `git reset --hard origin/main` | Match local branch exactly to remote branch |
| `git reflog` | Helps recover previous branch positions |

## Common mistakes

### Mistake 1: Using --hard without understanding

This can discard changes:

```bash
git reset --hard
```

Always run:

```bash
git status
```

before using it.

### Mistake 2: Resetting pushed commits

Avoid resetting commits that were already pushed to a shared branch.

Use:

```bash
git revert
```

instead.

### Mistake 3: Confusing reset with restore

Use `restore` for file-level changes.

Use `reset` for moving branch history.

### Mistake 4: Resetting to the wrong commit

Always inspect history first:

```bash
git log --oneline
```

## Best practices

- Use `git status` before reset.
- Use `git log --oneline` to choose the correct commit.
- Prefer `--soft` or `--mixed` when learning.
- Be very careful with `--hard`.
- Avoid resetting shared history.
- Use `git revert` for pushed commits.
- Use `git reflog` if you need to recover.

## Professional recommendation

If the commit is only local:

```bash
git reset --soft HEAD~1
```

or:

```bash
git reset HEAD~1
```

If the commit is already pushed:

```bash
git revert commit-hash
```

If you are unsure, do not use `--hard`.

## Summary

`git reset` moves the current branch to another commit.

Soft reset:

```bash
git reset --soft HEAD~1
```

Mixed reset:

```bash
git reset HEAD~1
```

Hard reset:

```bash
git reset --hard HEAD~1
```

Golden rule:

```txt
Use reset for local history. Use revert for shared history.
```

## Recommended next topic

Continue with:

```txt
docs/06-undoing-changes/revert.md
```