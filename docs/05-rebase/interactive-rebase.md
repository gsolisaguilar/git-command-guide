# Interactive Rebase

Interactive rebase is an advanced Git feature that allows you to edit commit history.

It is commonly used to clean up commits before merging a branch.

With interactive rebase, you can:

- Rename commit messages.
- Combine commits.
- Reorder commits.
- Delete commits.
- Edit commits.
- Split commits.

## Basic syntax

```bash
git rebase -i base
```

Example:

```bash
git rebase -i main
```

This opens an interactive list of commits from your current branch that are not in `main`.

## Rebase last N commits

You can also rebase a specific number of commits.

Example:

```bash
git rebase -i HEAD~3
```

This allows you to edit the last 3 commits.

## Important warning

Interactive rebase rewrites commit history.

Do not use it on shared branches unless your team agrees.

Safe use case:

```txt
Cleaning up your own local feature branch before merging.
```

Risky use case:

```txt
Rewriting commits that other people already pulled.
```

## Example commit history

```bash
git log --oneline
```

Example output:

```txt
a1b2c3d Fix typo
b2c3d4e Update docs
c3d4e5f Add rebase basics
d4e5f6g Add merge guide
```

If you run:

```bash
git rebase -i HEAD~3
```

Git opens the last 3 commits:

```txt
pick c3d4e5f Add rebase basics
pick b2c3d4e Update docs
pick a1b2c3d Fix typo
```

## Interactive rebase actions

| Action | Meaning |
|---|---|
| `pick` | Use the commit as it is |
| `reword` | Change the commit message |
| `edit` | Stop to modify the commit |
| `squash` | Combine commit with the previous commit and edit the message |
| `fixup` | Combine commit with the previous commit and discard its message |
| `drop` | Remove the commit |
| `break` | Stop at that point during rebase |

## Pick

`pick` keeps the commit as it is.

Example:

```txt
pick c3d4e5f Add rebase basics
```

Use this when you do not want to change the commit.

## Reword

`reword` changes only the commit message.

Example:

```txt
reword c3d4e5f Add rebase basics
```

Git will stop and let you write a new commit message.

## Edit

`edit` stops at the selected commit so you can modify its content.

Example:

```txt
edit c3d4e5f Add rebase basics
```

After making changes:

```bash
git add .
git commit --amend
git rebase --continue
```

## Squash

`squash` combines a commit with the previous commit.

Example:

```txt
pick c3d4e5f Add rebase basics
squash b2c3d4e Update docs
squash a1b2c3d Fix typo
```

This combines all three commits into one and lets you edit the final message.

## Fixup

`fixup` also combines a commit with the previous commit, but discards the fixed commit message.

Example:

```txt
pick c3d4e5f Add rebase basics
fixup b2c3d4e Update docs
fixup a1b2c3d Fix typo
```

This keeps only the first commit message.

## Drop

`drop` removes a commit.

Example:

```txt
drop a1b2c3d Fix typo
```

Use this carefully because the commit will be removed from the rebased history.

## Reorder commits

You can reorder commits by moving lines in the interactive rebase editor.

Original:

```txt
pick c3d4e5f Add rebase basics
pick b2c3d4e Update docs
pick a1b2c3d Fix typo
```

Changed:

```txt
pick c3d4e5f Add rebase basics
pick a1b2c3d Fix typo
pick b2c3d4e Update docs
```

Git will replay commits in the new order.

## Change a commit message

Run:

```bash
git rebase -i HEAD~3
```

Change:

```txt
pick c3d4e5f Add rebase basics
```

To:

```txt
reword c3d4e5f Add rebase documentation
```

Save and close the editor.

Git will ask for the new commit message.

## Combine multiple commits into one

Run:

```bash
git rebase -i HEAD~3
```

Change:

```txt
pick c3d4e5f Add rebase basics
pick b2c3d4e Update docs
pick a1b2c3d Fix typo
```

To:

```txt
pick c3d4e5f Add rebase basics
squash b2c3d4e Update docs
squash a1b2c3d Fix typo
```

Then write a clean final commit message:

```txt
Add rebase documentation
```

## Split a commit

To split a commit, mark it as `edit`.

Example:

```txt
edit c3d4e5f Add multiple rebase documents
```

When Git stops:

```bash
git reset HEAD~
```

Then stage and commit changes separately:

```bash
git add file-one.md
git commit -m "Add rebase basics"

git add file-two.md
git commit -m "Add interactive rebase guide"

git rebase --continue
```

## Continue interactive rebase

After resolving an edit or conflict:

```bash
git rebase --continue
```

## Abort interactive rebase

If something goes wrong:

```bash
git rebase --abort
```

This returns the branch to the state it had before starting the rebase.

## Skip a commit

If a commit cannot be applied and you want to skip it:

```bash
git rebase --skip
```

Use carefully.

## Interactive rebase with conflicts

If conflicts happen:

```bash
git status
```

Resolve the files manually.

Then:

```bash
git add .
git rebase --continue
```

Repeat until complete.

## Check result after interactive rebase

After finishing:

```bash
git log --oneline
```

For a visual view:

```bash
git log --oneline --graph --decorate --all
```

## Force push after interactive rebase

If the branch was already pushed, you may need:

```bash
git push --force-with-lease
```

Use this only when:

- You understand why it is required.
- You are working on your own branch.
- Nobody else depends on your old commits.

## Example: clean up commits before merge

Before:

```txt
a1b2c3d Fix typo
b2c3d4e Small update
c3d4e5f Add rebase basics
```

Interactive rebase:

```bash
git rebase -i HEAD~3
```

Change to:

```txt
pick c3d4e5f Add rebase basics
fixup b2c3d4e Small update
fixup a1b2c3d Fix typo
```

After:

```txt
x1y2z3a Add rebase basics
```

## Useful interactive rebase commands

| Command | Purpose |
|---|---|
| `git rebase -i main` | Interactively rebase current branch onto `main` |
| `git rebase -i HEAD~3` | Edit the last 3 commits |
| `git rebase --continue` | Continue after resolving conflicts or edits |
| `git rebase --abort` | Cancel the interactive rebase |
| `git rebase --skip` | Skip the current commit |
| `git commit --amend` | Modify the current commit during edit |
| `git log --oneline` | Review commit history |

## Common mistakes

### Mistake 1: Squashing the first commit incorrectly

You cannot squash the first commit in the list into a previous commit because there is no previous commit in the selected range.

Example not recommended:

```txt
squash c3d4e5f Add rebase basics
pick b2c3d4e Update docs
```

The first line should usually stay as `pick`.

### Mistake 2: Rebasing too many commits at once

Start small.

Example:

```bash
git rebase -i HEAD~2
```

Then practice with more commits.

### Mistake 3: Dropping commits accidentally

`drop` removes commits.

Use it carefully.

### Mistake 4: Interactive rebasing shared commits

Do not rewrite commits that other people already pulled unless the team agreed.

### Mistake 5: Forgetting to check history afterward

Always review:

```bash
git log --oneline --graph --decorate --all
```

## Best practices

- Use interactive rebase to clean your own local branch.
- Keep the first commit as `pick` when squashing.
- Use `fixup` for small correction commits.
- Use `reword` for unclear commit messages.
- Use `drop` carefully.
- Abort if you are unsure.
- Review history after finishing.
- Avoid interactive rebase on shared branches.

## Professional recommendation

Before opening a pull request, clean your branch history if needed.

Example:

```bash
git switch feature/rebase-guide
git rebase -i main
git log --oneline
```

If your branch was already pushed and you need to update the remote:

```bash
git push --force-with-lease
```

## Summary

Interactive rebase allows you to clean and edit commit history.

Basic command:

```bash
git rebase -i HEAD~3
```

Common actions:

```txt
pick
reword
edit
squash
fixup
drop
```

Continue:

```bash
git rebase --continue
```

Abort:

```bash
git rebase --abort
```

Golden rule:

```txt
Use interactive rebase on your own local commits, not on shared history.
```

## Recommended next topic

Continue with:

```txt
docs/05-rebase/safe-rebase-workflow.md
```