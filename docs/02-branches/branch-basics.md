# Branch Basics

Branches are one of the most important concepts in Git.

A branch is an independent line of development that allows you to work on changes without directly affecting the main codebase.

Branches are commonly used to develop new features, fix bugs, test ideas, prepare releases, and organize professional workflows.

## What is a branch?

A branch is a pointer to a commit.

When you create a branch, Git creates a new reference that allows you to continue working from a specific point in the project history.

In simple terms:

```txt
A branch lets you work on a separate version of the project.
```

## Why branches are useful

Branches are useful because they allow you to:

- Work on new features safely.
- Fix bugs without affecting the main branch.
- Test ideas or experiments.
- Collaborate with other developers.
- Keep the main branch stable.
- Organize work by task, feature, bugfix, or release.
- Prepare changes before merging them.

## Common branch names

Common branch names include:

```txt
main
develop
feature/login-form
feature/basic-git-commands
bugfix/fix-navbar
hotfix/production-error
release/v1.0.0
```

## Main branch

The `main` branch usually contains the stable version of the project.

In many professional repositories, developers do not work directly on `main`.

Instead, they create separate branches, make changes there, and later merge those changes into `main`.

Example:

```txt
main
 └── feature/basic-git-commands
```

## Check the current branch

To see the current branch:

```bash
git branch
```

Example output:

```txt
* feature/basic-git-commands
  main
```

The `*` symbol shows the branch you are currently using.

## Create a new branch

To create a new branch:

```bash
git branch branch-name
```

Example:

```bash
git branch feature/login-form
```

This creates the branch, but it does not switch to it.

## Switch to a branch

To switch to an existing branch:

```bash
git switch branch-name
```

Example:

```bash
git switch feature/login-form
```

## Create and switch to a branch

A common command is:

```bash
git switch -c branch-name
```

Example:

```bash
git switch -c feature/login-form
```

This creates the branch and switches to it immediately.

## Older syntax with checkout

Before `git switch`, developers commonly used:

```bash
git checkout -b branch-name
```

Example:

```bash
git checkout -b feature/login-form
```

This command also creates and switches to the new branch.

## List local branches

```bash
git branch
```

This shows branches that exist locally on your computer.

## List remote branches

```bash
git branch -r
```

Example output:

```txt
origin/main
origin/feature/basic-git-commands
```

## List all branches

```bash
git branch -a
```

This shows both local and remote branches.

## How branches work

Imagine this commit history:

```txt
A---B---C main
```

If you create a new branch from `main`:

```txt
A---B---C main
         \
          feature/login-form
```

When you make commits on the feature branch:

```txt
A---B---C main
         \
          D---E feature/login-form
```

The `main` branch stays unchanged while your new work happens on the feature branch.

## Example workflow with branches

```bash
git switch main
git pull origin main
git switch -c feature/basic-git-commands
```

Then make changes:

```bash
git status
git add .
git commit -m "Add basic Git commands documentation"
```

Push the branch:

```bash
git push -u origin feature/basic-git-commands
```

## Branches and commits

A branch moves forward when you create commits on it.

Example:

```bash
git switch -c feature/readme-update
```

Create a commit:

```bash
git add README.md
git commit -m "Update README structure"
```

Now the branch `feature/readme-update` points to the new commit.

## Branches do not copy the entire project

A branch does not duplicate all files.

Git stores commits efficiently and uses references to track branch positions.

This makes branches lightweight and fast.

## Local branches vs remote branches

| Type | Meaning |
|---|---|
| Local branch | A branch stored on your computer |
| Remote branch | A branch stored in a remote repository like GitHub |

Example local branch:

```txt
feature/basic-git-commands
```

Example remote branch:

```txt
origin/feature/basic-git-commands
```

## Push a branch to GitHub

If the branch exists only locally, push it with:

```bash
git push -u origin branch-name
```

Example:

```bash
git push -u origin feature/basic-git-commands
```

The `-u` option sets the upstream branch.

After that, you can usually push with:

```bash
git push
```

## Check branch tracking

To see local branches and their upstream branches:

```bash
git branch -vv
```

Example output:

```txt
* feature/basic-git-commands a1b2c3d [origin/feature/basic-git-commands] Add docs
  main                       e4f5g6h [origin/main] Initial commit
```

## Merge a branch

To merge a feature branch into `main`:

```bash
git switch main
git merge feature/basic-git-commands
```

This integrates the changes from the feature branch into `main`.

## Branch workflow example

```bash
git switch main
git pull origin main
git switch -c feature/branching-guide
git add .
git commit -m "Add branch basics documentation"
git push -u origin feature/branching-guide
```

Later, after review:

```bash
git switch main
git pull origin main
git merge feature/branching-guide
git push origin main
```

## Professional use of branches

In professional environments, branches are usually created for specific work.

Examples:

| Branch type | Purpose |
|---|---|
| `feature/` | New feature or documentation section |
| `bugfix/` | Fix a non-urgent bug |
| `hotfix/` | Fix an urgent production issue |
| `release/` | Prepare a release |
| `chore/` | Maintenance tasks |
| `docs/` | Documentation changes |
| `refactor/` | Code restructuring without behavior changes |

## Best practices

- Create a branch for each task.
- Keep branches focused.
- Use descriptive branch names.
- Start branches from an updated `main`.
- Commit small logical changes.
- Push your branch to the remote repository.
- Open a pull request when the work is ready.
- Delete branches after they are merged.

## Common mistakes

### Mistake 1: Working directly on main

Avoid making changes directly on `main` unless it is a simple personal project.

Better:

```bash
git switch -c feature/my-change
```

### Mistake 2: Creating branches from outdated main

Before creating a new branch, update `main`:

```bash
git switch main
git pull origin main
git switch -c feature/new-task
```

### Mistake 3: Using unclear branch names

Avoid:

```txt
test
changes
new
fix
my-branch
```

Use:

```txt
feature/login-form
bugfix/fix-login-error
docs/add-git-branch-guide
```

### Mistake 4: Keeping old branches forever

After a branch has been merged and is no longer needed, delete it.

Local:

```bash
git branch -d branch-name
```

Remote:

```bash
git push origin --delete branch-name
```

## Useful branch commands

| Command | Purpose |
|---|---|
| `git branch` | Lists local branches |
| `git branch -r` | Lists remote branches |
| `git branch -a` | Lists all branches |
| `git switch branch-name` | Switches to a branch |
| `git switch -c branch-name` | Creates and switches to a new branch |
| `git checkout -b branch-name` | Older way to create and switch to a branch |
| `git push -u origin branch-name` | Pushes a branch and sets upstream |
| `git branch -vv` | Shows branch tracking information |
| `git merge branch-name` | Merges a branch into the current branch |
| `git branch -d branch-name` | Deletes a local branch safely |

## Summary

Branches allow you to work independently without affecting the main codebase.

Basic branch workflow:

```bash
git switch main
git pull origin main
git switch -c feature/new-task
git add .
git commit -m "Add new task"
git push -u origin feature/new-task
```

Branches are essential for professional Git workflows.

## Recommended next topic

Continue with:

```txt
docs/02-branches/switch-and-checkout.md
```