# Reflog

`git reflog` shows a local history of where `HEAD` and branch references have been.

It is one of the most useful commands for recovering from mistakes.

## What is git reflog?

Reflog means reference log.

It records movements of references such as:

- `HEAD`
- Branches
- Checkouts
- Resets
- Rebases
- Commits
- Merges

In simple terms:

```txt
Reflog helps you find where your branch or HEAD was before.
```

## Why reflog is useful

Reflog can help recover from:

- Accidental reset.
- Lost commits.
- Bad rebase.
- Wrong branch checkout.
- Deleted branch references.
- Accidental history rewrite.
- Mistaken `git reset --hard`.

## Basic command

```bash
git reflog
```

Example output:

```txt
a1b2c3d HEAD@{0}: reset: moving to HEAD~1
e4f5g6h HEAD@{1}: commit: Add reflog documentation
i7j8k9l HEAD@{2}: checkout: moving from main to feature/advanced-git
```

Each entry shows a previous position of `HEAD`.

## Understanding HEAD@{n}

Reflog uses references like:

```txt
HEAD@{0}
HEAD@{1}
HEAD@{2}
```

Meaning:

| Reference | Meaning |
|---|---|
| `HEAD@{0}` | Current position |
| `HEAD@{1}` | Previous position |
| `HEAD@{2}` | Position before that |

## Recover from accidental reset

Imagine you ran:

```bash
git reset --hard HEAD~1
```

and lost the last commit.

Run:

```bash
git reflog
```

Find the commit before the reset:

```txt
e4f5g6h HEAD@{1}: commit: Add reflog documentation
```

Recover it:

```bash
git reset --hard e4f5g6h
```

## Recover a lost commit

If a commit disappeared after rebase or reset:

```bash
git reflog
```

Find the commit hash.

Then create a branch from it:

```bash
git switch -c recovery-branch commit-hash
```

Example:

```bash
git switch -c recovery/reflog-fix e4f5g6h
```

This is safer than immediately resetting.

## Recover after bad rebase

If a rebase went wrong and already completed:

```bash
git reflog
```

Find the position before the rebase:

```txt
a1b2c3d HEAD@{5}: rebase: checkout main
```

Then recover:

```bash
git reset --hard HEAD@{5}
```

Or safer:

```bash
git switch -c recovery-before-rebase HEAD@{5}
```

## View reflog for a specific branch

```bash
git reflog show branch-name
```

Example:

```bash
git reflog show main
```

## View reflog with dates

```bash
git reflog --date=local
```

Example output includes local dates.

## Use reflog with reset

```bash
git reset --hard HEAD@{1}
```

Warning:

```txt
reset --hard can discard current changes.
Use carefully.
```

## Safer recovery with a new branch

Instead of resetting immediately, create a recovery branch:

```bash
git switch -c recovery-branch HEAD@{1}
```

This lets you inspect the recovered state safely.

## Reflog is local

Important:

```txt
Reflog is local to your machine.
```

It is not normally pushed to GitHub.

Other developers do not have your reflog.

## Reflog expiration

Reflog entries are not kept forever.

Git eventually removes old reflog entries during garbage collection.

Because of that, recover lost commits as soon as possible.

## Reflog vs log

| Command | Shows |
|---|---|
| `git log` | Commit history reachable from the current branch |
| `git reflog` | Local movement history of HEAD and references |

`git log` may not show a lost commit.

`git reflog` may still show it.

## Example: log does not show commit

If a commit was removed from branch history by reset, it may disappear from:

```bash
git log --oneline
```

But it may still appear in:

```bash
git reflog
```

## Common reflog commands

| Command | Purpose |
|---|---|
| `git reflog` | Shows HEAD movement history |
| `git reflog --date=local` | Shows reflog with local dates |
| `git reflog show branch-name` | Shows reflog for a branch |
| `git reset --hard HEAD@{n}` | Resets to a previous reflog state |
| `git switch -c recovery HEAD@{n}` | Creates recovery branch from reflog state |
| `git show HEAD@{n}` | Shows details of a reflog entry |

## Common mistakes

### Mistake 1: Panicking after reset

If you accidentally reset, check reflog first:

```bash
git reflog
```

### Mistake 2: Resetting hard too quickly

Prefer creating a recovery branch first:

```bash
git switch -c recovery-branch HEAD@{1}
```

### Mistake 3: Thinking reflog is shared

Reflog is local.

Do not rely on someone else having your reflog.

### Mistake 4: Waiting too long

Reflog entries can expire.

Recover important commits quickly.

## Best practices

- Use reflog before assuming work is lost.
- Create a recovery branch when unsure.
- Use `reset --hard` carefully.
- Check `git status` before recovery commands.
- Do not depend on reflog as permanent backup.
- Push important work to a remote branch when appropriate.
- Make commits for important progress.

## Professional recommendation

If you think you lost work:

```bash
git reflog
```

Then create a recovery branch:

```bash
git switch -c recovery/lost-work commit-hash
```

After verifying, decide whether to merge, cherry-pick, or reset.

## Summary

`git reflog` shows local reference movement history.

Basic command:

```bash
git reflog
```

Recover safely:

```bash
git switch -c recovery-branch HEAD@{1}
```

Recover with reset:

```bash
git reset --hard HEAD@{1}
```

Golden rule:

```txt
Before assuming work is lost, check git reflog.
```

## Recommended next topic

Continue with:

```txt
docs/09-advanced-git/blame.md
```