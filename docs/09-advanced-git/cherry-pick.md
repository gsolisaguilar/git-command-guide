# Cherry Pick

`git cherry-pick` is used to apply a specific commit from one branch into another branch.

It is useful when you want only one commit or a few specific commits, without merging the entire branch.

## What is cherry-pick?

Cherry-pick takes a commit from one branch and applies it to your current branch.

In simple terms:

```txt
Cherry-pick copies a specific commit into another branch.
```

## Basic syntax

```bash
git cherry-pick commit-hash
```

Example:

```bash
git cherry-pick a1b2c3d
```

This applies the changes from commit `a1b2c3d` to your current branch.

## When to use cherry-pick

Use cherry-pick when:

- You need one specific fix from another branch.
- You want to apply a hotfix to another branch.
- You want to move a commit without merging the entire branch.
- You accidentally committed to the wrong branch.
- You need a specific change from a release branch.
- You want to backport a fix to an older version.

## When not to use cherry-pick

Avoid cherry-pick when:

- You actually need the entire branch.
- The commit depends on many other commits.
- The team workflow prefers merges or pull requests.
- It would create duplicated history unnecessarily.
- You do not understand the source commit.

## Example scenario

You have this history:

```txt
main:
A---B---C

feature:
A---B---D---E
```

You only want commit `D` from `feature`, but not commit `E`.

Switch to `main`:

```bash
git switch main
```

Cherry-pick commit `D`:

```bash
git cherry-pick D
```

Result:

```txt
main:
A---B---C---D'
```

Git creates a new commit `D'` with the same changes as `D`.

## Why the commit hash changes

Cherry-pick creates a new commit.

Even if the changes are the same, the commit hash is different because the commit has a new parent and new metadata.

## Find the commit to cherry-pick

First, view the history:

```bash
git log --oneline
```

Or view all branches:

```bash
git log --oneline --graph --decorate --all
```

Example:

```txt
a1b2c3d Fix typo in README
e4f5g6h Add stash documentation
i7j8k9l Add rebase guide
```

Then cherry-pick the commit:

```bash
git cherry-pick a1b2c3d
```

## Cherry-pick from another branch

Example:

```bash
git switch main
git log --oneline feature/advanced-git-commands
git cherry-pick a1b2c3d
```

This applies the selected commit from `feature/advanced-git-commands` into `main`.

## Cherry-pick multiple commits

You can cherry-pick more than one commit:

```bash
git cherry-pick commit1 commit2 commit3
```

Example:

```bash
git cherry-pick a1b2c3d e4f5g6h i7j8k9l
```

Git applies them in the order provided.

## Cherry-pick a range of commits

```bash
git cherry-pick start-commit..end-commit
```

Example:

```bash
git cherry-pick a1b2c3d..f6g7h8i
```

Important:

```txt
The start commit is not included in this range.
The end commit is included.
```

If you want to include the start commit, use:

```bash
git cherry-pick start-commit^..end-commit
```

## Cherry-pick without committing immediately

Use:

```bash
git cherry-pick --no-commit commit-hash
```

Or:

```bash
git cherry-pick -n commit-hash
```

Example:

```bash
git cherry-pick -n a1b2c3d
```

This applies the changes to your working directory and staging area but does not create a commit automatically.

Then commit manually:

```bash
git commit -m "Apply selected fix"
```

## Cherry-pick and conflicts

Sometimes cherry-pick causes conflicts.

Example:

```txt
CONFLICT (content): Merge conflict in README.md
error: could not apply a1b2c3d... Fix README section
```

Check status:

```bash
git status
```

Resolve the conflict manually.

Stage resolved files:

```bash
git add .
```

Continue:

```bash
git cherry-pick --continue
```

## Abort a cherry-pick

If something goes wrong:

```bash
git cherry-pick --abort
```

This cancels the cherry-pick and returns your branch to its previous state.

## Skip a cherry-pick

If cherry-picking multiple commits and one commit is not needed:

```bash
git cherry-pick --skip
```

Use carefully.

## Cherry-pick workflow

```bash
git switch target-branch
git log --oneline --graph --decorate --all
git cherry-pick commit-hash
git status
git log --oneline
```

## Example: move a commit from the wrong branch

You accidentally committed on `main`, but the commit should be on `feature/advanced-git-commands`.

Find the commit:

```bash
git log --oneline
```

Switch to the correct branch:

```bash
git switch feature/advanced-git-commands
```

Cherry-pick the commit:

```bash
git cherry-pick a1b2c3d
```

Then decide how to clean up `main`.

If the commit was not pushed, you may use reset carefully.

If the commit was pushed, use revert.

## Example: apply hotfix to release branch

```bash
git switch release/v1.0.0
git cherry-pick a1b2c3d
```

This applies a specific fix to the release branch.

## Common cherry-pick commands

| Command | Purpose |
|---|---|
| `git cherry-pick commit` | Applies one commit |
| `git cherry-pick commit1 commit2` | Applies multiple commits |
| `git cherry-pick start..end` | Applies a range of commits |
| `git cherry-pick -n commit` | Applies changes without committing |
| `git cherry-pick --continue` | Continues after resolving conflicts |
| `git cherry-pick --abort` | Cancels the cherry-pick |
| `git cherry-pick --skip` | Skips current commit |

## Common mistakes

### Mistake 1: Cherry-picking a commit without checking dependencies

Some commits depend on previous commits.

If you cherry-pick only one commit, the code or documentation may not work correctly.

### Mistake 2: Cherry-picking too many commits

If you need many commits, a merge or rebase may be better.

### Mistake 3: Cherry-picking into the wrong branch

Always check:

```bash
git branch
```

before cherry-picking.

### Mistake 4: Ignoring conflicts

Resolve conflicts carefully before continuing:

```bash
git add .
git cherry-pick --continue
```

## Best practices

- Use cherry-pick for specific commits only.
- Check commit history before cherry-picking.
- Make sure the commit does not depend on missing changes.
- Cherry-pick into the correct branch.
- Use `--no-commit` if you want to review or adjust changes first.
- Avoid using cherry-pick as a replacement for a normal merge workflow.

## Professional recommendation

Use cherry-pick when you need a specific change, not an entire branch.

Recommended flow:

```bash
git switch target-branch
git status
git log --oneline --graph --decorate --all
git cherry-pick commit-hash
```

If unsure, use:

```bash
git cherry-pick --no-commit commit-hash
```

Then review before committing.

## Summary

`git cherry-pick` applies a specific commit to the current branch.

Basic command:

```bash
git cherry-pick commit-hash
```

Continue after conflict:

```bash
git cherry-pick --continue
```

Abort:

```bash
git cherry-pick --abort
```

Golden rule:

```txt
Use cherry-pick when you need a specific commit, not an entire branch.
```

## Recommended next topic

Continue with:

```txt
docs/09-advanced-git/bisect.md
```