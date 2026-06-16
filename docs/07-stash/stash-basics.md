# Stash Basics

`git stash` is used to temporarily save changes that are not ready to be committed.

It is useful when you need to switch branches, pull changes, or work on something else without losing your current progress.

## What is git stash?

`git stash` saves your uncommitted changes in a temporary storage area.

In simple terms:

```txt
Stash lets you save your current work without creating a commit.
```

After stashing, your working directory becomes clean, and you can continue working on another task.

## When to use git stash

Use `git stash` when:

- You need to switch branches but have unfinished changes.
- You want to pull changes but your working directory is not clean.
- You are interrupted and need to work on another task.
- You want to temporarily hide local changes.
- You are not ready to commit yet.
- You want to test something from a clean working tree.

## Basic stash command

```bash
git stash
```

This saves your tracked file changes and cleans your working directory.

## Check status before stashing

Before using stash, check your repository state:

```bash
git status
```

Example:

```txt
Changes not staged for commit:
  modified: README.md
```

Then stash:

```bash
git stash
```

After stashing:

```bash
git status
```

Example:

```txt
nothing to commit, working tree clean
```

## What git stash saves

By default, `git stash` saves:

- Modified tracked files.
- Staged tracked files.

By default, it does not save:

- Untracked files.
- Ignored files.

## Stash with a message

It is a good practice to add a message to your stash.

```bash
git stash push -m "Work in progress on stash documentation"
```

This makes it easier to identify later.

## List stashes

To see saved stashes:

```bash
git stash list
```

Example output:

```txt
stash@{0}: On feature/stash-guide: Work in progress on stash documentation
stash@{1}: On main: Temporary README update
```

The most recent stash is usually:

```txt
stash@{0}
```

## View stash details

To see what changed in the latest stash:

```bash
git stash show
```

To see a more detailed diff:

```bash
git stash show -p
```

To inspect a specific stash:

```bash
git stash show stash@{1}
```

Detailed version:

```bash
git stash show -p stash@{1}
```

## Apply the latest stash

To bring back the latest stash without deleting it from the stash list:

```bash
git stash apply
```

This reapplies the stashed changes but keeps the stash saved.

## Pop the latest stash

To bring back the latest stash and remove it from the stash list:

```bash
git stash pop
```

This reapplies the changes and deletes the stash if successful.

## Apply a specific stash

```bash
git stash apply stash@{1}
```

## Pop a specific stash

```bash
git stash pop stash@{1}
```

## Stash tracked and untracked files

If you also want to stash untracked files:

```bash
git stash push -u -m "Work in progress with new files"
```

Or:

```bash
git stash --include-untracked
```

This includes new files that Git is not tracking yet.

## Stash ignored files too

To include ignored files:

```bash
git stash push -a -m "Stash all files including ignored"
```

Or:

```bash
git stash --all
```

Warning:

```txt
This can include files such as dependencies, build outputs, logs, or environment files.
Use carefully.
```

## Stash only staged changes

To stash only staged changes:

```bash
git stash push --staged -m "Stash staged changes"
```

This is useful when you have staged changes that you want to temporarily save separately.

## Stash only specific files

```bash
git stash push -m "Stash README changes" README.md
```

You can also stash multiple files:

```bash
git stash push -m "Stash selected docs" README.md docs/example.md
```

## Basic stash workflow

```bash
git status
git stash push -m "Work in progress"
git status
```

Later:

```bash
git stash list
git stash pop
```

## Example: switch branches with unfinished work

You are working on:

```txt
feature/stash-guide
```

You have unfinished changes, but you need to switch to `main`.

```bash
git status
git stash push -m "WIP stash guide"
git switch main
```

Later, return to your branch:

```bash
git switch feature/stash-guide
git stash pop
```

## Example: pull changes with local modifications

If Git prevents you from pulling because you have local changes:

```bash
git status
git stash push -m "Temporary local changes"
git pull origin main
git stash pop
```

If conflicts happen after `stash pop`, resolve them like normal merge conflicts.

## Stash list example

```bash
git stash list
```

Output:

```txt
stash@{0}: On feature/stash-guide: WIP stash guide
stash@{1}: On main: Temporary README update
```

Apply the older stash:

```bash
git stash apply stash@{1}
```

## Common stash commands

| Command | Purpose |
|---|---|
| `git stash` | Saves tracked local changes temporarily |
| `git stash push -m "message"` | Saves changes with a message |
| `git stash list` | Shows saved stashes |
| `git stash show` | Shows summary of latest stash |
| `git stash show -p` | Shows detailed diff of latest stash |
| `git stash apply` | Applies latest stash but keeps it saved |
| `git stash pop` | Applies latest stash and removes it |
| `git stash push -u` | Stashes tracked and untracked files |
| `git stash push -a` | Stashes tracked, untracked, and ignored files |

## Common mistakes

### Mistake 1: Stashing without a message

Avoid:

```bash
git stash
```

Better:

```bash
git stash push -m "WIP update Git stash documentation"
```

Messages make stashes easier to identify.

### Mistake 2: Expecting untracked files to be stashed by default

By default, untracked files are not included.

Use:

```bash
git stash push -u
```

### Mistake 3: Forgetting that stash is temporary

Stash is useful, but it should not replace commits.

If the work is important and complete enough, create a commit.

### Mistake 4: Popping the wrong stash

Before using a specific stash, check:

```bash
git stash list
```

Then apply the correct one.

## Best practices

- Use stash for temporary work.
- Add messages to your stashes.
- Use commits for important saved progress.
- Check `git status` before and after stashing.
- Use `git stash list` before applying old stashes.
- Prefer `apply` when you are unsure.
- Use `pop` when you are sure you want to remove the stash after applying it.

## Professional recommendation

Use this safer stash workflow:

```bash
git status
git stash push -m "WIP clear message"
git stash list
```

When restoring:

```bash
git stash apply stash@{0}
```

If everything looks good, delete the stash manually:

```bash
git stash drop stash@{0}
```

This is safer than `git stash pop` because you do not remove the stash immediately.

## Summary

`git stash` temporarily saves uncommitted work.

Basic stash:

```bash
git stash push -m "Work in progress"
```

List stashes:

```bash
git stash list
```

Restore latest stash:

```bash
git stash apply
```

Restore and remove latest stash:

```bash
git stash pop
```

Include untracked files:

```bash
git stash push -u -m "Work in progress with new files"
```

## Recommended next topic

Continue with:

```txt
docs/07-stash/stash-pop-apply.md
```