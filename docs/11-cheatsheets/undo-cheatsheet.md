# Undo Cheatsheet

Quick reference for undoing changes safely in Git.

## Important warning

Some undo commands can delete work.

Before undoing anything, run:

```bash
git status
```

If needed, also run:

```bash
git diff
git log --oneline
```

## Undo command overview

| Command | Best for |
|---|---|
| `git restore` | Discard file changes or unstage files |
| `git reset` | Move branch history or undo local commits |
| `git revert` | Safely undo pushed/shared commits |
| `git clean` | Remove untracked files |
| `git reflog` | Recover lost commits or previous states |

## Unstage files

Unstage one file:

```bash
git restore --staged file-name
```

Unstage all files:

```bash
git restore --staged .
```

Older syntax:

```bash
git reset HEAD file-name
```

## Discard unstaged changes

Discard one file:

```bash
git restore file-name
```

Discard all unstaged tracked changes:

```bash
git restore .
```

Warning:

```txt
This removes local modifications in tracked files.
```

## Unstage and discard a file

```bash
git restore --staged file-name
git restore file-name
```

## Undo last commit but keep changes staged

```bash
git reset --soft HEAD~1
```

Use when:

```txt
You want to redo the last commit.
You want to change the commit message.
You want to combine changes differently.
```

## Undo last commit but keep changes unstaged

```bash
git reset HEAD~1
```

Same as:

```bash
git reset --mixed HEAD~1
```

Use when:

```txt
You committed too early and want to reorganize files.
```

## Undo last commit and discard changes

```bash
git reset --hard HEAD~1
```

Warning:

```txt
This removes the commit and discards its changes from tracked files.
Use carefully.
```

## Reset modes

| Command | Keeps changes? | Staged? | Risk |
|---|---|---|---|
| `git reset --soft HEAD~1` | Yes | Yes | Low |
| `git reset HEAD~1` | Yes | No | Medium |
| `git reset --hard HEAD~1` | No | No | High |

## Revert a commit safely

```bash
git revert commit-hash
```

Use when:

```txt
The commit was already pushed.
The commit is on a shared branch.
You do not want to rewrite history.
```

## Revert without editor

```bash
git revert --no-edit commit-hash
```

## Revert without committing immediately

```bash
git revert --no-commit commit-hash
```

or:

```bash
git revert -n commit-hash
```

Then:

```bash
git commit -m "Revert selected changes"
```

## Reset vs revert

| Situation | Recommended command |
|---|---|
| Commit is local and not pushed | `git reset` |
| Commit is pushed or shared | `git revert` |
| Need to keep history safe | `git revert` |
| Need to rewrite local history | `git reset` |

## Remove untracked files

Preview first:

```bash
git clean -n
```

Remove untracked files:

```bash
git clean -f
```

Preview files and directories:

```bash
git clean -nd
```

Remove files and directories:

```bash
git clean -fd
```

## Remove ignored files too

Preview:

```bash
git clean -ndx
```

Remove:

```bash
git clean -fdx
```

Warning:

```txt
This can delete ignored files like build outputs, logs, dependencies, or local generated files.
```

## Clean command options

| Command | Purpose |
|---|---|
| `git clean -n` | Preview untracked files |
| `git clean -f` | Remove untracked files |
| `git clean -nd` | Preview untracked files and directories |
| `git clean -fd` | Remove untracked files and directories |
| `git clean -fdx` | Remove untracked and ignored files/directories |
| `git clean -i` | Interactive clean |

## Recover lost commits

Use reflog:

```bash
git reflog
```

Create recovery branch:

```bash
git switch -c recovery/lost-work commit-hash
```

Or reset back:

```bash
git reset --hard commit-hash
```

Safer option:

```bash
git switch -c recovery/lost-work HEAD@{1}
```

## Abort operations

Abort merge:

```bash
git merge --abort
```

Abort rebase:

```bash
git rebase --abort
```

Abort cherry-pick:

```bash
git cherry-pick --abort
```

Abort revert:

```bash
git revert --abort
```

## Common scenarios

### I staged the wrong file

```bash
git restore --staged file-name
```

### I modified a file but want to discard the change

```bash
git restore file-name
```

### I committed too early

```bash
git reset HEAD~1
```

### I want to change the last local commit

```bash
git reset --soft HEAD~1
git commit -m "New message"
```

### I pushed a bad commit

```bash
git revert commit-hash
```

### I created temporary untracked files

```bash
git clean -n
git clean -f
```

### I think I lost a commit

```bash
git reflog
```

## Dangerous commands

Use carefully:

```bash
git reset --hard
git clean -fd
git clean -fdx
git push --force
```

Prefer safer alternatives when possible:

```bash
git revert
git restore --staged
git clean -n
git push --force-with-lease
```

## Common mistakes

| Mistake | Safer habit |
|---|---|
| Using `reset --hard` too quickly | Check `git status` and `git diff` first |
| Using `clean -fdx` without preview | Run `git clean -ndx` first |
| Resetting pushed commits | Use `git revert` |
| Thinking untracked files are recoverable | Add or back them up before cleaning |
| Panicking after lost commit | Check `git reflog` |

## Professional recommendation

When unsure, use this order:

```bash
git status
git diff
git log --oneline
```

Then decide:

```txt
File change? Use restore.
Local commit? Use reset.
Pushed commit? Use revert.
Untracked files? Use clean.
Lost commit? Use reflog.
```

## Summary

Safe undo commands:

```bash
git restore --staged file-name
git restore file-name
git revert commit-hash
git reflog
```

Riskier commands:

```bash
git reset --hard
git clean -fdx
```

Golden rule:

```txt
Use revert for shared history. Use reset carefully for local history.
```