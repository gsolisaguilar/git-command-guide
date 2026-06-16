# Delete and Rename Branches

Branches are created for specific tasks.

After a branch is merged or no longer needed, it is a good practice to delete it.

Sometimes, you may also need to rename a branch if the name is unclear, incorrect, or does not follow the team convention.

## Why delete branches?

Deleting old branches helps keep the repository clean.

Benefits:

- Reduces confusion.
- Makes branch lists easier to read.
- Avoids using outdated branches.
- Keeps the repository organized.
- Helps teams focus on active work.

## Why rename branches?

Renaming branches is useful when:

- The branch name has a typo.
- The branch name is unclear.
- The branch name does not follow conventions.
- The task changed.
- The branch needs to include a ticket number.

Example:

```txt
old name: test
new name: feature/branching-guide
```

## List branches before deleting or renaming

Before making changes, list your branches:

```bash
git branch
```

Example:

```txt
  main
* feature/basic-git-commands
  feature/old-test
```

To see remote branches:

```bash
git branch -r
```

To see all branches:

```bash
git branch -a
```

## Delete a local branch safely

Use:

```bash
git branch -d branch-name
```

Example:

```bash
git branch -d feature/old-test
```

The `-d` option deletes the branch only if it has already been merged.

This is safer than forcing deletion.

## Force delete a local branch

Use:

```bash
git branch -D branch-name
```

Example:

```bash
git branch -D feature/old-test
```

The `-D` option forces deletion even if the branch has not been merged.

Be careful because unmerged work may be lost.

## Difference between -d and -D

| Command | Meaning |
|---|---|
| `git branch -d branch-name` | Safe delete. Only deletes if already merged |
| `git branch -D branch-name` | Force delete. Deletes even if not merged |

## Delete a remote branch

To delete a branch from the remote repository:

```bash
git push origin --delete branch-name
```

Example:

```bash
git push origin --delete feature/old-test
```

This deletes the branch from GitHub or another remote repository.

## Delete local and remote branch

Example:

```bash
git branch -d feature/old-test
git push origin --delete feature/old-test
```

This deletes the branch locally and remotely.

## Clean remote-tracking branches

Sometimes a remote branch was deleted on GitHub, but your local Git still shows it.

To clean outdated remote-tracking branches:

```bash
git fetch --prune
```

Or:

```bash
git remote prune origin
```

## Rename the current local branch

If you are currently on the branch you want to rename:

```bash
git branch -m new-branch-name
```

Example:

```bash
git branch -m feature/branching-guide
```

## Rename another local branch

If you are not currently on the branch:

```bash
git branch -m old-branch-name new-branch-name
```

Example:

```bash
git branch -m test feature/branching-guide
```

## Rename a branch that was already pushed

Renaming a branch that already exists on GitHub requires more steps.

### Step 1: Rename the local branch

If you are on the branch:

```bash
git branch -m new-branch-name
```

Example:

```bash
git branch -m feature/branching-guide
```

### Step 2: Delete the old remote branch

```bash
git push origin --delete old-branch-name
```

Example:

```bash
git push origin --delete test
```

### Step 3: Push the new branch

```bash
git push -u origin new-branch-name
```

Example:

```bash
git push -u origin feature/branching-guide
```

## Full rename example

Old branch:

```txt
test
```

New branch:

```txt
feature/branching-guide
```

Commands:

```bash
git branch -m test feature/branching-guide
git push origin --delete test
git push -u origin feature/branching-guide
```

## Rename current branch example

If you are currently on `test`:

```bash
git branch -m feature/branching-guide
git push origin --delete test
git push -u origin feature/branching-guide
```

## Change upstream after renaming

If needed, set upstream manually:

```bash
git branch --set-upstream-to=origin/branch-name
```

Example:

```bash
git branch --set-upstream-to=origin/feature/branching-guide
```

## Check branch tracking

Use:

```bash
git branch -vv
```

Example:

```txt
* feature/branching-guide a1b2c3d [origin/feature/branching-guide] Add branch docs
  main                    e4f5g6h [origin/main] Initial commit
```

## Deleting a branch after merge

A common professional workflow is:

```bash
git switch main
git pull origin main
git merge feature/branching-guide
git branch -d feature/branching-guide
git push origin --delete feature/branching-guide
```

This keeps `main` updated and removes the completed branch.

## Deleting a branch after pull request merge

If you merged a pull request on GitHub, the remote branch may be deleted from the GitHub interface.

Then locally, run:

```bash
git switch main
git pull origin main
git branch -d feature/branching-guide
git fetch --prune
```

## When not to delete a branch

Do not delete a branch if:

- It has not been merged.
- You are not sure if the work is still needed.
- Another person is still using it.
- It is a long-living branch such as `main`, `develop`, or `release`.
- It is used by automation or deployment processes.

## Protect important branches

Branches like `main` or `develop` should not be deleted casually.

In GitHub, teams often use branch protection rules to protect important branches.

Examples of protected branches:

```txt
main
develop
release/v1.0.0
```

## Useful commands

| Command | Purpose |
|---|---|
| `git branch` | Lists local branches |
| `git branch -r` | Lists remote branches |
| `git branch -a` | Lists all branches |
| `git branch -d branch-name` | Safely deletes a local branch |
| `git branch -D branch-name` | Force deletes a local branch |
| `git push origin --delete branch-name` | Deletes a remote branch |
| `git fetch --prune` | Removes outdated remote-tracking branches |
| `git branch -m new-name` | Renames current branch |
| `git branch -m old-name new-name` | Renames another local branch |
| `git branch -vv` | Shows upstream tracking information |

## Common mistakes

### Mistake 1: Deleting a branch before merging

Before deleting, verify the branch has been merged.

```bash
git branch --merged
```

This shows branches already merged into the current branch.

### Mistake 2: Force deleting without checking

Avoid this unless you are sure:

```bash
git branch -D branch-name
```

Use the safe option first:

```bash
git branch -d branch-name
```

### Mistake 3: Deleting only the local branch

Deleting a local branch does not delete the remote branch.

Local delete:

```bash
git branch -d branch-name
```

Remote delete:

```bash
git push origin --delete branch-name
```

### Mistake 4: Renaming locally but not updating the remote

If the branch was pushed before, remember to push the new name and delete the old remote branch.

```bash
git push origin --delete old-name
git push -u origin new-name
```

## Professional recommendation

After a branch is merged, clean it up.

Example:

```bash
git switch main
git pull origin main
git branch -d feature/completed-task
git push origin --delete feature/completed-task
git fetch --prune
```

This keeps your local and remote repository clean.

## Checklist before deleting a branch

Ask:

```txt
Was the branch merged?
Is anyone else using this branch?
Is this branch protected?
Do I need to keep it for reference?
Am I deleting the correct local branch?
Am I deleting the correct remote branch?
```

## Summary

Use safe delete when possible:

```bash
git branch -d branch-name
```

Use force delete only when necessary:

```bash
git branch -D branch-name
```

Delete remote branches with:

```bash
git push origin --delete branch-name
```

Rename branches with:

```bash
git branch -m old-name new-name
```

Clean outdated remote references with:

```bash
git fetch --prune
```

Deleting and renaming branches correctly keeps a Git repository clean and professional.

## Recommended next topic

Continue with:

```txt
docs/03-remote-repositories/remotes.md
```