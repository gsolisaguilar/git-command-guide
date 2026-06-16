# Aborting Merges

Sometimes a merge does not go as expected.

You may get conflicts, realize you are merging the wrong branch, or decide that you are not ready to merge yet.

In those cases, Git allows you to abort the merge.

## What does aborting a merge mean?

Aborting a merge means canceling the merge process and returning the repository to the state it had before the merge started.

The main command is:

```bash
git merge --abort
```

## When to abort a merge

You may want to abort a merge when:

- You merged the wrong branch.
- There are too many conflicts.
- You are not ready to resolve conflicts.
- You realize your current branch is not updated.
- You started the merge from the wrong branch.
- You want to review changes before trying again.
- You accidentally started a merge.

## Basic abort command

```bash
git merge --abort
```

This cancels the current merge.

## Example: wrong branch merge

Imagine you are on `main`.

```bash
git switch main
```

Then you accidentally run:

```bash
git merge feature/wrong-branch
```

If conflicts happen or you realize it was a mistake, run:

```bash
git merge --abort
```

Git will try to return your repository to the state before the merge.

## Check merge state

If a merge is in progress, `git status` may show:

```txt
You have unmerged paths.
  fix conflicts and run "git commit"
  use "git merge --abort" to abort the merge
```

This means you are currently in the middle of a merge.

## Abort workflow

```bash
git status
git merge --abort
git status
```

After aborting, check that your working tree is clean or returned to its previous state.

## What happens after git merge --abort?

Git attempts to:

- Stop the merge process.
- Remove merge conflict state.
- Restore files to the pre-merge state.
- Return the branch to where it was before the merge started.

## Important warning

`git merge --abort` works best when you did not make unrelated changes during the merge.

If you modify many files manually after the conflict appears, Git may not always be able to restore everything exactly.

## Before starting a merge

To make aborting safer, always check:

```bash
git status
```

If your working tree is clean, aborting a problematic merge is usually safer.

## Clean working tree before merge

Before merging:

```bash
git status
```

Ideal output:

```txt
nothing to commit, working tree clean
```

This means your current work is saved and the merge can be attempted safely.

## Abort a merge with conflicts

Example:

```bash
git switch main
git merge feature/branches
```

Conflict appears:

```txt
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
```

Abort:

```bash
git merge --abort
```

Check status:

```bash
git status
```

## If git merge --abort does not work

Sometimes Git may show an error if it cannot safely abort.

You can inspect the repository state:

```bash
git status
```

Then decide the next step carefully.

Common alternatives include:

```bash
git reset --merge
```

Or, in more advanced cases:

```bash
git reset --hard HEAD
```

Warning:

```txt
git reset --hard HEAD can discard local changes.
Use it carefully.
```

## git merge --abort vs git reset --merge

| Command | Purpose |
|---|---|
| `git merge --abort` | Cancels the merge and returns to pre-merge state |
| `git reset --merge` | Older alternative for aborting merge-like states |

In most cases, use:

```bash
git merge --abort
```

## Dangerous option: git reset --hard

This command discards changes in tracked files:

```bash
git reset --hard HEAD
```

Use it only when you are sure you do not need the current local changes.

It can be useful if you want to completely discard the current merge state and local changes, but it is risky.

## Safer approach before risky commands

Before using destructive commands, check:

```bash
git status
```

And if there are changes you might need, save them first.

Option 1: Copy files manually.

Option 2: Stash changes if possible:

```bash
git stash
```

Option 3: Commit changes if appropriate.

## Abort before resolving conflicts

If you are unsure how to resolve conflicts, it is okay to abort.

```bash
git merge --abort
```

Then review the situation:

```bash
git log --oneline --graph --decorate --all
git status
```

You can try again later.

## Example: abort, update main, try again

```bash
git merge --abort
git switch main
git pull origin main
git merge feature/branches
```

If you are working locally only and have not pushed yet, you can still update from your local branches.

## Example: abort and merge the correct branch

```bash
git merge --abort
git branch
git merge feature/correct-branch
```

## Abort does not delete branches

`git merge --abort` only cancels the merge process.

It does not delete any branch.

Example:

```bash
git merge --abort
git branch
```

Your branches will still exist.

## Abort does not undo completed merges

Important:

```txt
git merge --abort works only while a merge is in progress.
```

If the merge was already completed and committed, `git merge --abort` will not undo it.

To undo a completed merge, you need other commands such as:

```bash
git revert
```

or:

```bash
git reset
```

Those commands are covered in the undoing changes section.

## How to know if a merge is still in progress

Run:

```bash
git status
```

If Git says:

```txt
All conflicts fixed but you are still merging.
```

or:

```txt
You have unmerged paths.
```

then a merge is still in progress.

If Git says:

```txt
nothing to commit, working tree clean
```

then no merge is in progress.

## Common abort commands

| Command | Purpose |
|---|---|
| `git merge --abort` | Cancels an active merge |
| `git status` | Shows whether a merge is in progress |
| `git reset --merge` | Alternative way to cancel merge state |
| `git reset --hard HEAD` | Discards local tracked changes and resets to HEAD |

## Common mistakes

### Mistake 1: Trying to abort after the merge is already committed

If the merge is already completed, this will not work:

```bash
git merge --abort
```

You need to undo the merge with other Git commands.

### Mistake 2: Using reset hard too quickly

Avoid this unless you are sure:

```bash
git reset --hard HEAD
```

It can discard local changes.

### Mistake 3: Continuing a merge when you are unsure

If you are not sure, stop and check:

```bash
git status
git log --oneline --graph --decorate --all
```

If needed:

```bash
git merge --abort
```

### Mistake 4: Starting a merge with a dirty working tree

Before merging:

```bash
git status
```

Commit or stash local changes first.

## Best practices

- Always check `git status` before merging.
- Merge from a clean working tree.
- Abort if you merged the wrong branch.
- Abort if you need more time to resolve conflicts.
- Avoid destructive commands unless necessary.
- Review branch history before trying again.

## Professional recommendation

Safe merge attempt workflow:

```bash
git status
git log --oneline --graph --decorate --all
git merge branch-name
```

If something goes wrong:

```bash
git status
git merge --abort
git status
```

## Summary

Use this command to cancel an active merge:

```bash
git merge --abort
```

Use it when:

```txt
You merged the wrong branch.
You are not ready to resolve conflicts.
You want to return to the pre-merge state.
```

Remember:

```txt
git merge --abort only works while a merge is in progress.
```

## Recommended next topic

Continue with:

```txt
docs/04-merges-and-conflicts/merge-strategies.md
```