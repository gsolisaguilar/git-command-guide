# Stash Advanced

Advanced stash commands help you manage temporary work more precisely.

You can stash specific files, include untracked files, create branches from stashes, inspect stash content, and clean old stashes safely.

## Review basic stash first

Before using advanced stash commands, understand:

```bash
git stash push -m "message"
git stash list
git stash apply
git stash pop
```

These are the most common stash commands.

## Stash with a message

Use clear messages to identify stashes later.

```bash
git stash push -m "WIP advanced stash documentation"
```

Then check:

```bash
git stash list
```

Example:

```txt
stash@{0}: On feature/stash-guide: WIP advanced stash documentation
```

## Stash untracked files

By default, Git does not stash untracked files.

To include untracked files:

```bash
git stash push -u -m "Stash tracked and untracked files"
```

Or:

```bash
git stash push --include-untracked -m "Stash tracked and untracked files"
```

This is useful when you created new files but are not ready to commit them.

## Stash ignored files

To include ignored files too:

```bash
git stash push -a -m "Stash all files"
```

Or:

```bash
git stash push --all -m "Stash all files"
```

Warning:

```txt
This may include ignored files such as dependencies, build output, logs, or temporary files.
Use carefully.
```

## Stash only specific files

You can stash only selected files:

```bash
git stash push -m "Stash README changes" README.md
```

Multiple files:

```bash
git stash push -m "Stash selected documentation" README.md docs/example.md
```

This is useful when you want to keep working on some files but temporarily save changes from others.

## Stash only staged changes

If you want to stash only what is staged:

```bash
git stash push --staged -m "Stash staged changes"
```

This requires a Git version that supports `--staged`.

Workflow:

```bash
git add README.md
git stash push --staged -m "Stash staged README changes"
```

## Keep staged changes while stashing unstaged changes

Use:

```bash
git stash push --keep-index -m "Stash unstaged changes only"
```

This stashes unstaged changes but keeps staged changes in the index.

This is useful when you staged part of your work and want to temporarily hide the rest.

## Patch mode

Patch mode lets you choose parts of changes to stash interactively.

```bash
git stash push -p -m "Stash selected hunks"
```

Git will ask you which changes to stash.

This is useful when a file contains multiple unrelated changes.

## Create a branch from a stash

You can create a new branch from a stash:

```bash
git stash branch branch-name stash@{n}
```

Example:

```bash
git stash branch feature/stashed-work stash@{0}
```

This command:

1. Creates a new branch.
2. Checks out that branch.
3. Applies the stash.
4. Drops the stash if applying was successful.

## Why use git stash branch?

Use it when:

- Applying a stash to the current branch causes conflicts.
- You want to continue stashed work separately.
- You accidentally worked on the wrong branch.
- You want to preserve the original context of the stash.

## Show stash summary

```bash
git stash show stash@{0}
```

Example output:

```txt
README.md | 10 +++++-----
1 file changed, 5 insertions(+), 5 deletions(-)
```

## Show stash detailed diff

```bash
git stash show -p stash@{0}
```

This shows the actual line-by-line changes.

## Show stash as a commit

A stash is stored internally like a commit.

You can inspect it with:

```bash
git show stash@{0}
```

This shows detailed information about the stash.

## Apply stash without restoring staged state

By default, stash apply restores changes into the working directory.

```bash
git stash apply stash@{0}
```

## Apply stash and restore staged state

To try restoring the staged state as well:

```bash
git stash apply --index stash@{0}
```

This attempts to restore both working directory changes and staged changes.

## Pop stash and restore staged state

```bash
git stash pop --index stash@{0}
```

Use this when the staged/unstaged separation matters.

## Drop a specific stash

```bash
git stash drop stash@{0}
```

This deletes one stash.

## Clear all stashes

```bash
git stash clear
```

Warning:

```txt
This deletes all stashes.
Only use it when you are sure you do not need them.
```

## Recover a dropped stash

Recovering a dropped stash may be possible using `git fsck` or `git reflog`, but it is advanced and not guaranteed.

Because of that, avoid dropping or clearing stashes too quickly.

A safer habit is:

```bash
git stash apply stash@{0}
```

Then delete only after checking:

```bash
git stash drop stash@{0}
```

## Stash workflow for wrong branch

You accidentally edited files on `main`.

```bash
git status
git stash push -m "Move work to feature branch"
git switch feature/stash-guide
git stash pop
```

Now the changes are moved to the feature branch.

## Stash workflow before rebase

Before rebasing, your working tree should be clean.

If you have unfinished changes:

```bash
git stash push -m "Temporary changes before rebase"
git rebase main
git stash pop
```

If conflicts happen, resolve them manually.

## Stash workflow before pull

```bash
git status
git stash push -m "Temporary changes before pull"
git pull origin main
git stash pop
```

This is useful when local changes block a pull.

## Stash workflow with untracked files

```bash
git status
git stash push -u -m "WIP including new files"
git status
```

Later:

```bash
git stash pop
```

## Advanced stash commands

| Command | Purpose |
|---|---|
| `git stash push -m "message"` | Creates a stash with a message |
| `git stash push -u -m "message"` | Includes untracked files |
| `git stash push -a -m "message"` | Includes ignored files |
| `git stash push -p -m "message"` | Interactively chooses changes to stash |
| `git stash push --keep-index` | Stashes unstaged changes but keeps staged changes |
| `git stash push --staged` | Stashes only staged changes |
| `git stash branch branch-name stash@{n}` | Creates a branch from a stash |
| `git stash show -p stash@{n}` | Shows detailed stash changes |
| `git stash apply --index stash@{n}` | Applies stash and tries to restore staged state |
| `git stash drop stash@{n}` | Deletes one stash |
| `git stash clear` | Deletes all stashes |

## Common mistakes

### Mistake 1: Using stash as permanent storage

Stash is temporary.

If the work matters, create a commit.

### Mistake 2: Not using stash messages

Avoid:

```bash
git stash
```

Prefer:

```bash
git stash push -m "WIP clear description"
```

### Mistake 3: Forgetting untracked files

If new files matter, use:

```bash
git stash push -u
```

### Mistake 4: Clearing all stashes accidentally

Be careful with:

```bash
git stash clear
```

This removes every stash.

### Mistake 5: Applying stash to the wrong branch

Before applying a stash, check:

```bash
git branch
git status
```

## Best practices

- Use stash for temporary work only.
- Add meaningful stash messages.
- Use `git stash list` often.
- Inspect important stashes before applying.
- Prefer `apply` before `drop` when unsure.
- Include untracked files with `-u` if needed.
- Avoid `--all` unless you fully understand what will be included.
- Clean old stashes regularly but carefully.

## Professional recommendation

Safe advanced stash workflow:

```bash
git status
git stash push -u -m "WIP clear description"
git stash list
git stash show -p stash@{0}
```

Restore safely:

```bash
git stash apply stash@{0}
git status
```

If everything is correct:

```bash
git stash drop stash@{0}
```

## Summary

Advanced stash commands give you more control over temporary work.

Stash with untracked files:

```bash
git stash push -u -m "Message"
```

Stash selected files:

```bash
git stash push -m "Message" file-name
```

Create a branch from a stash:

```bash
git stash branch branch-name stash@{0}
```

Inspect stash:

```bash
git stash show -p stash@{0}
```

Golden rule:

```txt
Stash is temporary. Use commits for important progress.
```

## Recommended next topic

Continue with:

```txt
docs/08-tags-and-releases/tags.md
```