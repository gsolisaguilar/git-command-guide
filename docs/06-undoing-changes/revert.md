# Revert

`git revert` is used to undo a commit by creating a new commit.

It is one of the safest ways to undo changes, especially when the commit has already been pushed to a shared repository.

## What is git revert?

`git revert` creates a new commit that reverses the changes introduced by an earlier commit.

It does not delete commit history.

Instead, it adds a new commit that cancels out the selected commit.

## Basic syntax

```bash
git revert commit-hash
```

Example:

```bash
git revert a1b2c3d
```

This creates a new commit that undoes the changes from commit `a1b2c3d`.

## Why revert is safe

Revert is safe because it does not rewrite history.

This makes it appropriate for:

- Shared branches.
- Remote branches.
- Production branches.
- Team repositories.
- Commits that were already pushed.

## Revert vs reset

| Command | What it does | Rewrites history | Safe for shared branches |
|---|---|---|---|
| `git revert` | Creates a new commit that undoes another commit | No | Yes |
| `git reset` | Moves branch history backward or elsewhere | Yes | Usually no |

## Example history before revert

```txt
A---B---C main
```

If commit `C` introduced a bug, you can revert it.

```bash
git revert C
```

After revert:

```txt
A---B---C---D main
```

Commit `D` undoes the changes from `C`.

## Revert the latest commit

First check the log:

```bash
git log --oneline
```

Example:

```txt
a1b2c3d Add broken change
e4f5g6h Add previous valid change
```

Revert the latest commit:

```bash
git revert a1b2c3d
```

Git opens an editor with a default commit message.

Save and close the editor to complete the revert.

## Revert without opening editor

Use:

```bash
git revert --no-edit commit-hash
```

Example:

```bash
git revert --no-edit a1b2c3d
```

This uses the default revert commit message.

## Revert multiple commits

You can revert multiple commits one by one:

```bash
git revert commit1
git revert commit2
```

Example:

```bash
git revert a1b2c3d
git revert e4f5g6h
```

## Revert a range of commits

You can revert a range:

```bash
git revert older-commit..newer-commit
```

Example:

```bash
git revert a1b2c3d..f6g7h8i
```

Important:

```txt
The older commit itself is not included in this range.
```

## Revert without committing immediately

Use:

```bash
git revert --no-commit commit-hash
```

or:

```bash
git revert -n commit-hash
```

Example:

```bash
git revert --no-commit a1b2c3d
```

This applies the reverted changes to your working directory and staging area, but does not create a commit automatically.

Then you can commit manually:

```bash
git commit -m "Revert broken documentation update"
```

## When to use --no-commit

Use `--no-commit` when:

- You want to revert multiple commits into one commit.
- You want to review the changes before committing.
- You want to adjust the revert before saving it.
- You want a custom commit message.

Example:

```bash
git revert --no-commit commit1
git revert --no-commit commit2
git commit -m "Revert unstable changes"
```

## Revert a merge commit

Reverting a merge commit requires specifying the mainline parent.

Syntax:

```bash
git revert -m parent-number merge-commit-hash
```

Example:

```bash
git revert -m 1 a1b2c3d
```

This is more advanced.

The `-m 1` usually means:

```txt
Keep the first parent, usually the branch you merged into.
```

Use caution when reverting merge commits.

## Revert conflicts

Sometimes revert may create conflicts.

Git will pause and show conflicted files.

Check status:

```bash
git status
```

Resolve the conflicts manually.

Then stage resolved files:

```bash
git add .
```

Continue:

```bash
git revert --continue
```

## Abort a revert

If something goes wrong:

```bash
git revert --abort
```

This cancels the revert operation.

## Skip a revert

If you are reverting multiple commits and want to skip the current one:

```bash
git revert --skip
```

Use carefully.

## Revert workflow

```bash
git log --oneline
git revert commit-hash
git status
git log --oneline
```

If conflicts happen:

```bash
git status
# resolve conflicts
git add .
git revert --continue
```

## Practical example

You have this history:

```txt
a1b2c3d Add incorrect Git reset example
e4f5g6h Add restore documentation
```

Revert the incorrect commit:

```bash
git revert a1b2c3d
```

After revert, history may look like:

```txt
z9y8x7w Revert "Add incorrect Git reset example"
a1b2c3d Add incorrect Git reset example
e4f5g6h Add restore documentation
```

The original commit remains in history, but its changes are undone.

## When to use revert

Use revert when:

- The commit was already pushed.
- You are working on `main`.
- You are working in a team.
- You want to undo changes without rewriting history.
- You need a clear record that something was reverted.

## When not to use revert

Avoid revert when:

- You only want to unstage files.
- You only want to discard local uncommitted changes.
- You want to rewrite local unpublished history.
- You are trying to clean up commits before sharing them.

For local unpublished commits, `git reset` may be more appropriate.

## Common revert commands

| Command | Purpose |
|---|---|
| `git revert commit-hash` | Reverts one commit |
| `git revert --no-edit commit-hash` | Reverts without opening editor |
| `git revert --no-commit commit-hash` | Applies revert without committing |
| `git revert -n commit-hash` | Short version of `--no-commit` |
| `git revert --continue` | Continues after resolving conflicts |
| `git revert --abort` | Cancels revert |
| `git revert -m 1 merge-commit` | Reverts a merge commit |

## Common mistakes

### Mistake 1: Using reset instead of revert on shared history

If the commit was already pushed, use:

```bash
git revert commit-hash
```

not:

```bash
git reset --hard commit-hash
```

### Mistake 2: Reverting the wrong commit

Always check:

```bash
git log --oneline
```

before reverting.

### Mistake 3: Thinking revert deletes commits

Revert does not delete the original commit.

It creates a new commit that undoes it.

### Mistake 4: Reverting merge commits without understanding

Reverting merge commits requires `-m`.

Be careful:

```bash
git revert -m 1 merge-commit-hash
```

## Best practices

- Use revert for pushed commits.
- Use revert on shared branches.
- Read the commit history before reverting.
- Use `--no-commit` if you want to review changes first.
- Test the project after reverting.
- Write clear revert commit messages.
- Be careful with merge commits.

## Professional recommendation

For local unpublished commits:

```bash
git reset HEAD~1
```

For pushed/shared commits:

```bash
git revert commit-hash
```

This keeps history safe and understandable.

## Summary

`git revert` safely undoes commits by creating a new commit.

Basic command:

```bash
git revert commit-hash
```

Without editor:

```bash
git revert --no-edit commit-hash
```

Without immediate commit:

```bash
git revert --no-commit commit-hash
```

Golden rule:

```txt
Use revert for shared or pushed history.
```

## Recommended next topic

Continue with:

```txt
docs/06-undoing-changes/clean.md
```