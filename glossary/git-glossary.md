# Git Glossary

This glossary explains common Git and GitHub terms in a simple and practical way.

Use it as a quick reference when reading the documentation or working with Git commands.

## A

### Add

`git add` moves changes from the working directory to the staging area.

Example:

```bash
git add README.md
```

To add all changes:

```bash
git add .
```

## Alias

An alias is a shortcut for a Git command.

Example:

```bash
git config --global alias.st status
```

After that, you can run:

```bash
git st
```

instead of:

```bash
git status
```

## Annotated Tag

An annotated tag is a Git tag that stores extra information such as the tagger, date, and message.

Example:

```bash
git tag -a v1.0.0 -m "Release version 1.0.0"
```

Annotated tags are recommended for official releases.

## B

### Bare Repository

A bare repository is a Git repository without a working directory.

It is usually used as a remote repository.

A bare repository normally ends with:

```txt
.git
```

Example:

```txt
project.git
```

## Base Branch

The base branch is the branch where changes will be merged.

In a pull request, the base branch is usually:

```txt
main
```

Example:

```txt
feature/login-form → main
```

Here, `main` is the base branch.

## Bisect

`git bisect` helps find the commit that introduced a bug.

It uses binary search between a known good commit and a known bad commit.

Example:

```bash
git bisect start
git bisect bad
git bisect good a1b2c3d
```

## Blame

`git blame` shows who last modified each line of a file.

Example:

```bash
git blame README.md
```

It should be used to understand history, not to blame people.

## Branch

A branch is an independent line of development.

Example:

```bash
git switch -c feature/basic-git-commands
```

Branches allow you to work on new changes without affecting `main`.

## Branch Protection

Branch protection is a rule used on platforms like GitHub to protect important branches.

Examples of protection rules:

```txt
Require pull request reviews.
Require status checks.
Prevent force pushes.
Prevent branch deletion.
```

## C

### Checkout

`git checkout` is an older Git command used to switch branches or restore files.

Example:

```bash
git checkout main
```

Modern Git recommends:

```bash
git switch main
```

for switching branches.

## Cherry Pick

`git cherry-pick` applies a specific commit from one branch into another.

Example:

```bash
git cherry-pick a1b2c3d
```

Use it when you need one specific commit, not an entire branch.

## Clean

`git clean` removes untracked files from the working directory.

Preview before deleting:

```bash
git clean -n
```

Remove untracked files:

```bash
git clean -f
```

Use carefully because deleted untracked files may not be recoverable.

## Clone

`git clone` copies an existing repository to your computer.

Example:

```bash
git clone https://github.com/username/repository.git
```

## Commit

A commit is a saved snapshot of your project.

Example:

```bash
git commit -m "Add README"
```

Each commit has:

```txt
Commit hash
Author
Date
Message
Changes
```

## Commit Hash

A commit hash is a unique identifier for a commit.

Example:

```txt
a1b2c3d
```

Git uses commit hashes to reference specific commits.

## Conflict

A conflict happens when Git cannot automatically combine changes.

Example conflict markers:

```txt
<<<<<<< HEAD
Current branch changes
=======
Incoming branch changes
>>>>>>> feature-branch
```

Conflicts must be resolved manually.

## Continuous Integration

Continuous Integration, often called CI, is the practice of automatically testing changes when they are pushed or opened in a pull request.

Common CI checks:

```txt
Build
Tests
Linting
Security scans
Formatting checks
```

## D

### Detached HEAD

Detached HEAD means Git is pointing directly to a commit instead of a branch.

Example:

```bash
git checkout a1b2c3d
```

This is useful for inspection, but be careful when making changes.

Return to a branch with:

```bash
git switch main
```

## Diff

`git diff` shows differences between files, commits, or branches.

Example:

```bash
git diff
```

Show staged changes:

```bash
git diff --staged
```

## Directory

A directory is another word for folder.

Example:

```txt
docs/
examples/
workflows/
```

## Distributed Version Control System

Git is a distributed version control system.

This means every developer has a full copy of the repository history on their own computer.

## E

### Editor

Git may open an editor when writing commit messages, rebasing, or resolving merge commits.

You can configure an editor:

```bash
git config --global core.editor "code --wait"
```

## F

### Fast-Forward Merge

A fast-forward merge happens when Git can move the branch pointer forward without creating a merge commit.

Example:

```bash
git merge --ff-only feature/my-topic
```

Fast-forward merges create a linear history.

## Fetch

`git fetch` downloads changes from a remote repository without merging them into your current branch.

Example:

```bash
git fetch origin
```

It is safer than `git pull` when you want to inspect changes first.

## Feature Branch

A feature branch is a branch created for a specific task or feature.

Example:

```txt
feature/basic-git-commands
feature/branches
feature/remote-repositories
```

## Force Push

A force push overwrites remote history.

Example:

```bash
git push --force
```

A safer option is:

```bash
git push --force-with-lease
```

Use force push carefully.

## Fork

A fork is a personal copy of another repository, usually created on platforms like GitHub.

Forks are common in open-source collaboration.

## G

### Git

Git is a distributed version control system used to track changes in files and coordinate work between developers.

## GitHub

GitHub is an online platform that hosts Git repositories.

Git is the version control tool.

GitHub is a hosting and collaboration platform.

## Git Flow

Git Flow is a branching workflow that uses branches such as:

```txt
main
develop
feature/*
release/*
hotfix/*
```

It is useful for projects with planned releases.

## GitHub Flow

GitHub Flow is a simpler workflow based on:

```txt
main
feature branches
pull requests
```

It is commonly used for frequent integration and deployment.

## Gitignore

`.gitignore` is a file that tells Git which files or folders to ignore.

Example:

```txt
node_modules/
.env
*.log
dist/
```

## H

### HEAD

`HEAD` points to your current position in the repository.

Usually, it points to the latest commit of your current branch.

Example:

```txt
HEAD -> main
```

## Hotfix

A hotfix is an urgent fix, usually created from a stable branch like `main`.

Example:

```bash
git switch -c hotfix/fix-production-error
```

## I

### Index

The index is another name for the staging area.

It contains changes prepared for the next commit.

Example:

```bash
git add README.md
```

This adds the file to the index.

## Interactive Rebase

Interactive rebase allows you to edit commit history.

Example:

```bash
git rebase -i HEAD~3
```

You can use it to:

```txt
Reword commits
Squash commits
Fixup commits
Drop commits
Reorder commits
```

## L

### Lightweight Tag

A lightweight tag is a simple pointer to a commit.

Example:

```bash
git tag v1.0.0
```

For official releases, annotated tags are usually better.

## Local Branch

A local branch exists only on your computer.

Example:

```txt
feature/basic-git-commands
```

## Local Repository

A local repository is the Git repository stored on your computer.

It contains:

```txt
Files
Branches
Commits
Git history
```

## Log

`git log` shows commit history.

Example:

```bash
git log --oneline
```

A useful visual version:

```bash
git log --oneline --graph --decorate --all
```

## M

### Main

`main` is the default branch name commonly used for stable code.

Example:

```bash
git switch main
```

## Merge

A merge combines changes from one branch into another.

Example:

```bash
git switch main
git merge feature/my-topic
```

This merges `feature/my-topic` into `main`.

## Merge Commit

A merge commit is created when Git combines two branches that have diverged.

Example history:

```txt
A---B---C------M main
     \        /
      D---E feature
```

`M` is the merge commit.

## Merge Conflict

A merge conflict happens when Git cannot automatically combine changes.

You must edit the conflicted files manually, then run:

```bash
git add .
git commit
```

## N

### Non-Fast-Forward

A non-fast-forward situation happens when Git cannot simply move the branch pointer forward.

Example error:

```txt
non-fast-forward
```

This can happen when remote and local histories differ.

## O

### Origin

`origin` is the default name for the main remote repository.

Example:

```bash
git remote -v
```

Output:

```txt
origin  https://github.com/username/repository.git (fetch)
origin  https://github.com/username/repository.git (push)
```

## P

### Patch

A patch is a set of changes.

In Git, patches can be shown with:

```bash
git diff
```

## Pull

`git pull` downloads and integrates changes from a remote branch.

Example:

```bash
git pull origin main
```

`git pull` is similar to:

```txt
git fetch + git merge
```

## Pull Request

A pull request is a request to merge changes from one branch into another.

Example:

```txt
feature/my-topic → main
```

Pull requests are used for:

```txt
Code review
Discussion
Automated checks
Approval
Collaboration
```

## Push

`git push` uploads local commits to a remote repository.

Example:

```bash
git push origin main
```

First push of a new branch:

```bash
git push -u origin feature/my-topic
```

## R

### Rebase

`git rebase` moves or replays commits onto a new base.

Example:

```bash
git switch feature/my-topic
git rebase main
```

Rebase creates a cleaner linear history but rewrites commit hashes.

## Reflog

`git reflog` shows local history of where `HEAD` and branches have been.

Example:

```bash
git reflog
```

It can help recover lost commits.

## Remote

A remote is a version of your repository hosted somewhere else, such as GitHub.

Example:

```bash
git remote -v
```

## Remote Branch

A remote branch is a branch stored in a remote repository.

Example:

```txt
origin/main
origin/feature/basic-git-commands
```

## Remote-Tracking Branch

A remote-tracking branch is a local reference to a remote branch.

Example:

```txt
origin/main
```

It represents the state of the remote branch the last time you fetched.

## Repository

A repository, or repo, is a project tracked by Git.

It contains project files and Git history.

## Reset

`git reset` moves the current branch pointer to another commit.

Examples:

```bash
git reset --soft HEAD~1
git reset HEAD~1
git reset --hard HEAD~1
```

Be careful with:

```bash
git reset --hard
```

because it can discard local changes.

## Restore

`git restore` is used to discard file changes or unstage files.

Discard changes:

```bash
git restore README.md
```

Unstage file:

```bash
git restore --staged README.md
```

## Revert

`git revert` creates a new commit that undoes another commit.

Example:

```bash
git revert a1b2c3d
```

It is safer than reset for shared or pushed commits.

## S

### Semantic Versioning

Semantic Versioning is a version format:

```txt
MAJOR.MINOR.PATCH
```

Example:

```txt
v1.0.0
```

Meaning:

```txt
MAJOR = breaking changes
MINOR = new compatible features
PATCH = bug fixes
```

## Squash

Squash means combining multiple commits into one.

Example with interactive rebase:

```bash
git rebase -i HEAD~3
```

Example with merge:

```bash
git merge --squash feature/my-topic
```

## Staging Area

The staging area is where changes are prepared before committing.

Example:

```bash
git add README.md
```

## Stash

`git stash` temporarily saves uncommitted changes.

Example:

```bash
git stash push -m "Work in progress"
```

Restore latest stash:

```bash
git stash pop
```

## Status

`git status` shows the current state of your repository.

Example:

```bash
git status
```

It shows modified files, staged files, untracked files, and current branch.

## Submodule

A submodule is a Git repository inside another Git repository.

Example:

```bash
git submodule add https://github.com/username/library.git libs/library
```

Submodules are useful but can add complexity.

## Switch

`git switch` is used to change branches.

Example:

```bash
git switch main
```

Create and switch to a new branch:

```bash
git switch -c feature/my-topic
```

## T

### Tag

A tag marks a specific commit.

Example:

```bash
git tag v1.0.0
```

Annotated tag:

```bash
git tag -a v1.0.0 -m "Release version 1.0.0"
```

Tags are commonly used for releases.

## Trunk

The trunk is the main integration branch in trunk-based development.

It is usually:

```txt
main
```

## Trunk-Based Development

Trunk-based development is a workflow where developers integrate small changes frequently into one main branch.

It depends on:

```txt
Small changes
Short-lived branches
Automated tests
Stable main branch
```

## U

### Untracked File

An untracked file is a file Git sees but is not tracking yet.

Example:

```txt
Untracked files:
  notes.md
```

Track it with:

```bash
git add notes.md
```

## Upstream Branch

An upstream branch is the remote branch connected to your local branch.

Example:

```txt
Local branch: feature/my-topic
Upstream branch: origin/feature/my-topic
```

Set upstream:

```bash
git push -u origin feature/my-topic
```

## W

### Working Directory

The working directory is where you edit your project files.

It contains the actual files you see and modify.

## Working Tree

Working tree is another name for the working directory.

Example:

```txt
nothing to commit, working tree clean
```

This means there are no pending changes.

## Worktree

A Git worktree allows multiple working directories for one repository.

Example:

```bash
git worktree add ../project-hotfix hotfix/fix-readme
```

Worktrees are useful when working on multiple branches at the same time.

## Common Git Areas

Git has three important local areas:

```txt
Working Directory
Staging Area
Local Repository
```

## Working Directory

Where you edit files.

## Staging Area

Where you prepare changes.

## Local Repository

Where commits are saved.

## Remote Repository

Where commits are shared online.

## Common Git Flow

```txt
Working Directory → Staging Area → Local Repository → Remote Repository
```

Commands:

```bash
git add
git commit
git push
```

## Common Command Summary

| Command | Meaning |
|---|---|
| `git status` | Show repository status |
| `git add` | Stage changes |
| `git commit` | Save staged changes |
| `git push` | Upload commits |
| `git pull` | Download and integrate changes |
| `git fetch` | Download changes without integrating |
| `git branch` | List or manage branches |
| `git switch` | Switch branches |
| `git merge` | Combine branches |
| `git rebase` | Replay commits onto another base |
| `git restore` | Restore files or unstage changes |
| `git reset` | Move branch pointer or undo local commits |
| `git revert` | Safely undo commits with a new commit |
| `git stash` | Temporarily save changes |
| `git tag` | Mark a specific commit |
| `git log` | Show commit history |
| `git reflog` | Show local reference history |

## Beginner Terms

| Term | Simple meaning |
|---|---|
| Repository | A project tracked by Git |
| Commit | A saved snapshot |
| Branch | A separate line of work |
| Merge | Combine branches |
| Pull | Download and integrate changes |
| Push | Upload commits |
| Staging | Preparing changes for commit |
| Remote | Online version of the repository |
| Main | Stable default branch |

## Intermediate Terms

| Term | Simple meaning |
|---|---|
| Rebase | Move commits onto a new base |
| Conflict | Git needs help combining changes |
| Stash | Temporarily save work |
| Tag | Mark a version |
| Upstream | Connected remote branch |
| Fetch | Download remote changes only |
| Squash | Combine commits |
| Pull request | Request to merge reviewed changes |

## Advanced Terms

| Term | Simple meaning |
|---|---|
| Cherry-pick | Apply one specific commit |
| Bisect | Find the commit that introduced a bug |
| Reflog | Recover previous HEAD positions |
| Blame | See who last changed each line |
| Submodule | Repository inside another repository |
| Worktree | Multiple working folders for one repo |
| Detached HEAD | Viewing a commit directly |
| Force push | Rewrite remote history |

## Final Notes

This glossary is designed as a quick reference.

For deeper explanations, review the related documentation sections:

```txt
docs/00-introduction/
docs/01-basic-commands/
docs/02-branches/
docs/03-remote-repositories/
docs/04-merges-and-conflicts/
docs/05-rebase/
docs/06-undoing-changes/
docs/07-stash/
docs/08-tags-and-releases/
docs/09-advanced-git/
docs/10-professional-workflows/
docs/11-cheatsheets/
```

Golden rule:

```txt
When unsure, run git status first.
```