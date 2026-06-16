# Stash Pop and Apply

`git stash pop` and `git stash apply` are used to restore changes saved with `git stash`.

Both commands bring stashed changes back into your working directory, but they behave differently.

## Main difference

```txt
git stash apply restores the stash and keeps it in the stash list.
git stash pop restores the stash and removes it from the stash list if successful.
```

## git stash apply

Use `git stash apply` when you want to restore a stash but keep it saved.

```bash
git stash apply
```

This applies the latest stash:

```txt
stash@{0}
```

## git stash pop

Use `git stash pop` when you want to restore a stash and remove it from the stash list.

```bash
git stash pop
```

If the pop is successful, the stash is deleted from the stash list.

## Apply vs pop

| Command | Restores changes | Removes stash from list |
|---|---|---|
| `git stash apply` | Yes | No |
| `git stash pop` | Yes | Yes, if successful |

## Recommended option when unsure

When you are not completely sure, use:

```bash
git stash apply
```

This is safer because the stash remains available.

After confirming everything is correct, you can remove it manually:

```bash
git stash drop stash@{0}
```

## List available stashes

Before applying or popping a stash, check:

```bash
git stash list
```

Example:

```txt
stash@{0}: On feature/stash-guide: WIP stash guide
stash@{1}: On main: Temporary README update
stash@{2}: On feature/rebase-guide: Resolve rebase docs
```

## Apply the latest stash

```bash
git stash apply
```

This applies:

```txt
stash@{0}
```

## Pop the latest stash

```bash
git stash pop
```

This applies and removes:

```txt
stash@{0}
```

## Apply a specific stash

```bash
git stash apply stash@{1}
```

Example:

```bash
git stash apply stash@{1}
```

This applies the stash identified as `stash@{1}`.

## Pop a specific stash

```bash
git stash pop stash@{1}
```

This applies and removes that specific stash if successful.

## View stash before applying

To see a summary:

```bash
git stash show stash@{1}
```

To see detailed changes:

```bash
git stash show -p stash@{1}
```

Recommended flow:

```bash
git stash list
git stash show -p stash@{1}
git stash apply stash@{1}
```

## Drop a stash manually

To delete a stash manually:

```bash
git stash drop stash@{1}
```

Example:

```bash
git stash drop stash@{0}
```

Use this after verifying that the applied changes are correct.

## Clear all stashes

To remove all stashes:

```bash
git stash clear
```

Warning:

```txt
This deletes all stashes.
Use carefully.
```

## What happens if apply causes conflicts?

Sometimes applying a stash creates conflicts.

This can happen when the files changed since the stash was created.

Example:

```txt
CONFLICT (content): Merge conflict in README.md
```

Check status:

```bash
git status
```

Resolve conflicts manually.

Then stage the resolved files:

```bash
git add .
```

## What happens if pop causes conflicts?

If `git stash pop` causes conflicts, Git usually keeps the stash instead of deleting it.

This is helpful because your stashed changes are not lost.

Check the stash list:

```bash
git stash list
```

Then resolve conflicts manually.

## Conflict workflow after stash apply or pop

```bash
git status
# open conflicted files and resolve conflicts
git add .
git status
```

Then continue working normally.

There is no `git stash --continue`.

Once conflicts are resolved and staged, you decide whether to commit or keep working.

## Example: safe apply workflow

```bash
git stash list
git stash show -p stash@{0}
git stash apply stash@{0}
git status
```

If everything is correct:

```bash
git stash drop stash@{0}
```

This is safe because you only delete the stash after verifying the result.

## Example: quick pop workflow

```bash
git stash list
git stash pop
git status
```

Use this when you are confident that the latest stash is the one you need.

## Apply stash on a different branch

You can apply a stash on a different branch.

Example:

```bash
git switch feature/new-branch
git stash apply stash@{0}
```

This can be useful when you started work on the wrong branch and want to move changes to the correct branch.

## Example: move changes to another branch

You are on `main` and accidentally made changes there.

```bash
git status
git stash push -m "Move changes to correct branch"
git switch feature/stash-guide
git stash pop
```

Now the changes are on `feature/stash-guide`.

## Apply stash to a new branch

Git can create a new branch from a stash:

```bash
git stash branch new-branch-name stash@{0}
```

Example:

```bash
git stash branch feature/stashed-work stash@{0}
```

This creates a new branch and applies the stash there.

## When to use apply

Use `git stash apply` when:

- You want a safer restore.
- You are not sure if conflicts will happen.
- You want to keep the stash as backup.
- You are applying an older stash.
- You want to test the stash before deleting it.

## When to use pop

Use `git stash pop` when:

- You are sure the stash is correct.
- You want to restore and remove it in one step.
- You are working with the latest stash.
- You do not need to keep the stash as backup.

## Apply specific stash example

```bash
git stash list
git stash show -p stash@{2}
git stash apply stash@{2}
```

## Pop specific stash example

```bash
git stash list
git stash pop stash@{1}
```

## Common commands

| Command | Purpose |
|---|---|
| `git stash apply` | Applies latest stash and keeps it |
| `git stash pop` | Applies latest stash and removes it |
| `git stash apply stash@{n}` | Applies a specific stash |
| `git stash pop stash@{n}` | Pops a specific stash |
| `git stash show -p stash@{n}` | Shows detailed stash changes |
| `git stash drop stash@{n}` | Deletes one stash |
| `git stash clear` | Deletes all stashes |
| `git stash branch branch-name stash@{n}` | Creates a branch from a stash |

## Common mistakes

### Mistake 1: Using pop when apply would be safer

If you are unsure, prefer:

```bash
git stash apply
```

Then manually drop the stash later.

### Mistake 2: Applying the wrong stash

Always check:

```bash
git stash list
```

and inspect if needed:

```bash
git stash show -p stash@{n}
```

### Mistake 3: Clearing all stashes by accident

Be careful with:

```bash
git stash clear
```

This removes all stashes.

### Mistake 4: Forgetting that stash can conflict

A stash can conflict just like a merge.

If that happens, resolve the files manually.

## Best practices

- Use `git stash list` before applying old stashes.
- Use `git stash show -p` to inspect important stashes.
- Prefer `apply` when unsure.
- Use `pop` for quick restoration of the latest stash.
- Drop stashes only after verifying the changes.
- Avoid keeping too many old stashes.
- Use clear stash messages.

## Professional recommendation

For safer restoration:

```bash
git stash list
git stash show -p stash@{0}
git stash apply stash@{0}
git status
```

If everything is correct:

```bash
git stash drop stash@{0}
```

This gives you more control than `git stash pop`.

## Summary

`git stash apply` restores a stash and keeps it saved.

```bash
git stash apply
```

`git stash pop` restores a stash and removes it if successful.

```bash
git stash pop
```

Safe workflow:

```bash
git stash apply stash@{0}
git stash drop stash@{0}
```

Use `apply` when unsure and `pop` when you are confident.

## Recommended next topic

Continue with:

```txt
docs/07-stash/stash-advanced.md
```