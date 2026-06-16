# Restore

`git restore` is used to discard or restore changes in your working directory or staging area.

It is a safer and clearer modern command for undoing local file changes.

## What is git restore?

`git restore` helps you undo changes in files.

You can use it to:

- Discard changes in a modified file.
- Unstage files from the staging area.
- Restore a file from a specific commit.
- Return a file to its last committed state.

## Important warning

Some `git restore` commands can permanently discard local changes.

Before using it, always check:

```bash
git status
```

If you are not sure, do not run destructive commands.

## Check repository status first

Before restoring anything, run:

```bash
git status
```

Example output:

```txt
Changes not staged for commit:
  modified: README.md
```

This means `README.md` has local changes that are not staged.

## Discard changes in one file

To discard changes in one file:

```bash
git restore file-name
```

Example:

```bash
git restore README.md
```

This restores `README.md` to the last committed version.

## Discard changes in multiple files

```bash
git restore file-one.md file-two.md
```

Example:

```bash
git restore README.md docs/intro.md
```

## Discard all unstaged changes

To discard all unstaged changes in tracked files:

```bash
git restore .
```

Warning:

```txt
This removes local modifications in tracked files.
Use it carefully.
```

## Restore does not remove untracked files

If you created a new file that Git is not tracking yet, `git restore .` will not remove it.

Example untracked file:

```txt
Untracked files:
  notes.md
```

To remove untracked files, use `git clean`.

That is covered in:

```txt
docs/06-undoing-changes/clean.md
```

## Unstage a file

If you added a file to the staging area by mistake:

```bash
git restore --staged file-name
```

Example:

```bash
git restore --staged README.md
```

This removes the file from the staging area but keeps the changes in your working directory.

## Unstage all staged files

```bash
git restore --staged .
```

This moves all staged changes back to the working directory.

## Difference between restore and restore --staged

| Command | Effect |
|---|---|
| `git restore file.md` | Discards unstaged changes in the working directory |
| `git restore --staged file.md` | Removes file from staging area but keeps local changes |

## Example: undo git add

You accidentally staged everything:

```bash
git add .
```

Check status:

```bash
git status
```

Unstage everything:

```bash
git restore --staged .
```

Your changes are still there, but they are no longer staged.

## Example: discard a file change

You modified `README.md`, but you do not want to keep the change.

```bash
git status
git restore README.md
git status
```

After this, the file returns to the last committed version.

## Restore a file from a specific commit

You can restore a file from another commit:

```bash
git restore --source=commit-hash file-name
```

Example:

```bash
git restore --source=a1b2c3d README.md
```

This restores `README.md` from commit `a1b2c3d` into your working directory.

## Restore a file from another branch

You can also restore a file from another branch:

```bash
git restore --source=branch-name file-name
```

Example:

```bash
git restore --source=main README.md
```

This restores the version of `README.md` from `main`.

## Restore from HEAD

`HEAD` usually represents the latest commit on your current branch.

This command:

```bash
git restore README.md
```

is similar to restoring the file from `HEAD`.

You can also write:

```bash
git restore --source=HEAD README.md
```

## Restore staged file to working directory

If a file is staged and you want to unstage it:

```bash
git restore --staged file-name
```

If you also want to discard the actual changes after unstaging:

```bash
git restore file-name
```

Example:

```bash
git restore --staged README.md
git restore README.md
```

## Restore workflow examples

### Example 1: Unstage but keep changes

```bash
git status
git restore --staged README.md
git status
```

Use this when you staged a file by mistake but still want to keep the edit.

### Example 2: Discard unstaged changes

```bash
git status
git restore README.md
git status
```

Use this when you do not want the local edit anymore.

### Example 3: Unstage and discard changes

```bash
git restore --staged README.md
git restore README.md
```

Use this when the file was staged and you want to completely discard the change.

## Restore vs checkout

Older Git workflows used:

```bash
git checkout -- file-name
```

Modern Git recommends:

```bash
git restore file-name
```

The newer command is clearer because it is focused on restoring files.

## Common restore commands

| Command | Purpose |
|---|---|
| `git restore file.md` | Discards unstaged changes in a file |
| `git restore .` | Discards all unstaged tracked file changes |
| `git restore --staged file.md` | Unstages a file |
| `git restore --staged .` | Unstages all staged files |
| `git restore --source=commit file.md` | Restores a file from a commit |
| `git restore --source=branch file.md` | Restores a file from another branch |

## Common mistakes

### Mistake 1: Running restore without checking status

Always run:

```bash
git status
```

before using restore.

### Mistake 2: Thinking restore --staged deletes changes

This command:

```bash
git restore --staged file.md
```

does not delete your changes.

It only removes the file from the staging area.

### Mistake 3: Using git restore . accidentally

This command discards all unstaged changes in tracked files:

```bash
git restore .
```

Use it carefully.

### Mistake 4: Expecting restore to delete untracked files

`git restore` does not remove untracked files.

Use `git clean` for untracked files.

## Best practices

- Use `git status` before restoring.
- Use `git diff` to review changes before discarding them.
- Use `git restore --staged` to undo accidental staging.
- Be careful with `git restore .`.
- Commit or stash changes if you may need them later.
- Do not use destructive commands when you are unsure.

## Professional workflow

Before discarding changes:

```bash
git status
git diff
```

If you are sure:

```bash
git restore file-name
```

If you only want to unstage:

```bash
git restore --staged file-name
```

## Summary

`git restore` is used to undo local file changes or unstage files.

Discard file changes:

```bash
git restore file-name
```

Unstage a file:

```bash
git restore --staged file-name
```

Discard all unstaged tracked changes:

```bash
git restore .
```

Always check `git status` before using restore.

## Recommended next topic

Continue with:

```txt
docs/06-undoing-changes/reset.md
```