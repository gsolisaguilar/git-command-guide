# Merge Conflict Example

This example shows how a merge conflict happens and how to resolve it manually.

Merge conflicts are normal in Git. They happen when Git cannot automatically combine changes from two branches.

## Scenario

You have a repository with a file called:

```txt
README.md
```

The same line is edited differently on two branches:

```txt
main
feature/update-title
```

When you try to merge, Git does not know which version to keep.

## Goal

The goal is to practice this workflow:

```txt
Create conflict → Inspect conflict → Resolve file → Stage file → Complete merge
```

## Step 1: Start on main

```bash
git switch main
```

Create or edit `README.md`:

```md
# Git Commands Guide

A practical guide for learning Git.
```

Commit it:

```bash
git add README.md
git commit -m "Add initial README title"
```

## Step 2: Create a feature branch

```bash
git switch -c feature/update-title
```

Edit `README.md`:

```md
# Professional Git Commands Guide

A practical guide for learning Git.
```

Commit the change:

```bash
git add README.md
git commit -m "Update README title for professional guide"
```

## Step 3: Go back to main

```bash
git switch main
```

Edit the same line in `README.md` differently:

```md
# Complete Git Commands Guide

A practical guide for learning Git.
```

Commit the change:

```bash
git add README.md
git commit -m "Update README title for complete guide"
```

## Step 4: Try to merge the feature branch

```bash
git merge feature/update-title
```

Example output:

```txt
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
```

Git could not automatically decide which title to keep.

## Step 5: Check status

```bash
git status
```

Example output:

```txt
On branch main
You have unmerged paths.

Unmerged paths:
  both modified: README.md
```

This means `README.md` has a conflict.

## Step 6: Open the conflicted file

The file may look like this:

```md
<<<<<<< HEAD
# Complete Git Commands Guide
=======
# Professional Git Commands Guide
>>>>>>> feature/update-title

A practical guide for learning Git.
```

## Step 7: Understand conflict markers

```txt
<<<<<<< HEAD
Current branch changes
=======
Incoming branch changes
>>>>>>> feature/update-title
```

In this example:

```txt
HEAD = main
Incoming branch = feature/update-title
```

## Step 8: Resolve the conflict

Decide the final content.

For example, combine both ideas:

```md
# Complete Professional Git Commands Guide

A practical guide for learning Git.
```

Important:

```txt
Remove all conflict markers:
<<<<<<<
=======
>>>>>>>
```

## Step 9: Stage the resolved file

```bash
git add README.md
```

## Step 10: Complete the merge

```bash
git commit
```

Git may open an editor with a default merge commit message.

You can keep the default message or write one like:

```txt
Merge feature/update-title into main
```

## Step 11: Verify final status

```bash
git status
```

Expected output:

```txt
On branch main
nothing to commit, working tree clean
```

## Step 12: Review history

```bash
git log --oneline --graph --decorate --all
```

Example output:

```txt
*   a1b2c3d (HEAD -> main) Merge feature/update-title into main
|\
| * e4f5g6h (feature/update-title) Update README title for professional guide
* | i7j8k9l Update README title for complete guide
|/
* m1n2o3p Add initial README title
```

## Full conflict resolution workflow

```bash
git merge feature/update-title
git status

# open file and resolve conflict manually

git add README.md
git commit
git status
```

## Abort the merge

If you do not want to resolve the conflict now:

```bash
git merge --abort
```

This cancels the merge and returns to the state before the merge started.

## Keep current branch version

If you want to keep the version from the current branch:

```bash
git checkout --ours README.md
git add README.md
git commit
```

Or with modern Git:

```bash
git restore --ours README.md
git add README.md
git commit
```

## Keep incoming branch version

If you want to keep the version from the branch being merged:

```bash
git checkout --theirs README.md
git add README.md
git commit
```

Or with modern Git:

```bash
git restore --theirs README.md
git add README.md
git commit
```

## Search for conflict markers

Before committing, check that no conflict markers remain.

```bash
grep -n "<<<<<<<\|=======\|>>>>>>>" README.md
```

To search all files:

```bash
grep -R "<<<<<<<\|=======\|>>>>>>>" .
```

## Common mistake: committing conflict markers

Do not commit this:

```md
<<<<<<< HEAD
# Complete Git Commands Guide
=======
# Professional Git Commands Guide
>>>>>>> feature/update-title
```

Always remove the markers and leave only the final content.

## Common mistake: forgetting git add

After resolving a conflict, Git still needs you to stage the resolved file:

```bash
git add README.md
```

## Common mistake: panicking during conflicts

Conflicts are not a disaster.

Git is simply asking you to decide the final version.

## Conflict resolution checklist

```txt
Did I run git status?
Did I open each conflicted file?
Did I remove conflict markers?
Did I keep the correct final content?
Did I stage the resolved files?
Did I complete the merge?
```

## Summary

A merge conflict happens when Git cannot automatically combine changes.

Basic conflict workflow:

```bash
git status
# resolve files manually
git add .
git commit
```

Abort if needed:

```bash
git merge --abort
```

Golden rule:

```txt
Resolve conflicts carefully and never commit conflict markers.
```