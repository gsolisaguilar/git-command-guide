# Clean

`git clean` is used to remove untracked files from your working directory.

It is useful when you want to delete files that Git is not tracking, such as temporary files, generated files, or accidental files.

## What are untracked files?

Untracked files are files that exist in your project folder but are not tracked by Git.

Example:

```txt
Untracked files:
  notes.txt
  temp-file.md
  build-output/
```

Git sees these files, but they are not part of the repository history.

## What does git clean do?

`git clean` removes untracked files from your working directory.

Basic command:

```bash
git clean
```

However, Git usually requires extra options because deleting files can be dangerous.

## Important warning

`git clean` can permanently delete untracked files.

Before using it, always run:

```bash
git status
```

Then run a dry run:

```bash
git clean -n
```

## Dry run

A dry run shows what would be deleted without actually deleting anything.

```bash
git clean -n
```

Example output:

```txt
Would remove notes.txt
Would remove temp-file.md
```

This is the safest first step.

## Remove untracked files

To actually remove untracked files:

```bash
git clean -f
```

The `-f` means force.

Example:

```bash
git clean -f
```

This removes untracked files but not untracked directories.

## Remove untracked directories

To remove untracked directories too:

```bash
git clean -fd
```

Example:

```bash
git clean -fd
```

This removes untracked files and directories.

## Preview files and directories before deleting

Before running `git clean -fd`, preview with:

```bash
git clean -nd
```

Example output:

```txt
Would remove temp/
Would remove notes.txt
```

## Remove ignored files too

By default, `git clean` does not remove ignored files.

To remove ignored files as well:

```bash
git clean -fx
```

To remove ignored files and directories:

```bash
git clean -fdx
```

Warning:

```txt
This can delete files like build outputs, dependencies, logs, or environment-generated files.
Use with extreme caution.
```

## Remove only ignored files

To remove only ignored files:

```bash
git clean -fX
```

With directories:

```bash
git clean -fdX
```

Difference:

| Option | Meaning |
|---|---|
| `-x` | Remove ignored and untracked files |
| `-X` | Remove only ignored files |

## Interactive clean

You can use interactive mode:

```bash
git clean -i
```

This lets you choose what to remove.

It is safer than deleting everything immediately.

## Common clean options

| Command | Purpose |
|---|---|
| `git clean -n` | Preview untracked files that would be removed |
| `git clean -f` | Remove untracked files |
| `git clean -nd` | Preview untracked files and directories |
| `git clean -fd` | Remove untracked files and directories |
| `git clean -fx` | Remove untracked and ignored files |
| `git clean -fdx` | Remove untracked and ignored files/directories |
| `git clean -fX` | Remove only ignored files |
| `git clean -i` | Interactive clean |

## git clean does not remove tracked changes

`git clean` only removes untracked files.

It does not discard changes in tracked files.

For tracked file changes, use:

```bash
git restore file-name
```

or:

```bash
git reset --hard
```

depending on the situation.

## Clean vs restore

| Command | Used for |
|---|---|
| `git clean` | Remove untracked files |
| `git restore` | Discard changes in tracked files |

## Clean vs reset

| Command | Used for |
|---|---|
| `git clean` | Remove untracked files/directories |
| `git reset` | Move branch history or reset tracked files |

## Example: remove accidental notes file

Check status:

```bash
git status
```

Example:

```txt
Untracked files:
  notes.txt
```

Preview:

```bash
git clean -n
```

Remove:

```bash
git clean -f
```

## Example: remove generated folder

Check status:

```bash
git status
```

Example:

```txt
Untracked files:
  build/
```

Preview:

```bash
git clean -nd
```

Remove:

```bash
git clean -fd
```

## Example: clean ignored build files

Preview ignored files:

```bash
git clean -nX
```

Remove ignored files:

```bash
git clean -fX
```

With directories:

```bash
git clean -fdX
```

## Example: full clean

This removes untracked and ignored files and directories:

```bash
git clean -fdx
```

Warning:

```txt
This is very destructive.
It may remove important local files that are not tracked by Git.
```

Use this only when you are absolutely sure.

## Safe clean workflow

Recommended:

```bash
git status
git clean -n
git clean -f
```

If directories are involved:

```bash
git status
git clean -nd
git clean -fd
```

If ignored files are involved:

```bash
git status
git clean -nX
git clean -fX
```

## Combine clean with restore

If you want to remove all untracked files and discard all tracked file changes:

```bash
git restore .
git clean -fd
```

Warning:

```txt
This discards tracked changes and removes untracked files.
Use carefully.
```

## Completely reset a working directory

A common advanced cleanup is:

```bash
git reset --hard
git clean -fd
```

This:

```txt
Discards tracked changes.
Removes untracked files and directories.
```

Warning:

```txt
This can delete work permanently.
Use only when you are sure.
```

## Common mistakes

### Mistake 1: Running git clean without preview

Avoid running this first:

```bash
git clean -fd
```

Preview first:

```bash
git clean -nd
```

### Mistake 2: Forgetting that untracked files may be important

Untracked files may include notes, local configs, or new files you forgot to add.

Check before deleting.

### Mistake 3: Using -x without understanding

This command removes ignored files too:

```bash
git clean -fdx
```

Be careful because ignored files may include generated but useful files.

### Mistake 4: Thinking clean can be undone easily

Files deleted by `git clean` are not stored in Git history if they were untracked.

Recovery may not be possible.

## Best practices

- Always run `git status` first.
- Always run `git clean -n` or `git clean -nd` before deleting.
- Use interactive mode if unsure.
- Avoid `-x` unless needed.
- Do not clean files you may need later.
- Add important files to Git before cleaning.
- Use `.gitignore` for files that should not be tracked.

## Professional recommendation

Use this safe sequence:

```bash
git status
git clean -nd
```

Review the output.

If everything listed can be deleted:

```bash
git clean -fd
```

For most beginners, avoid:

```bash
git clean -fdx
```

unless you fully understand what will be removed.

## Summary

`git clean` removes untracked files.

Preview first:

```bash
git clean -n
```

Remove files:

```bash
git clean -f
```

Remove files and directories:

```bash
git clean -fd
```

Remove ignored files too:

```bash
git clean -fdx
```

Golden rule:

```txt
Always preview before cleaning.
```

## Recommended next topic

Continue with:

```txt
docs/07-stash/stash-basics.md
```