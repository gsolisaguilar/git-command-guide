# What is Git?

Git is a distributed version control system used to track changes in files and coordinate work between developers.

In professional software development, Git helps teams manage source code, review changes, collaborate safely, and keep a complete history of a project.

## What is version control?

Version control is a system that records changes made to files over time.

Instead of saving multiple copies manually, such as:

```txt
project-final.zip
project-final-v2.zip
project-final-real-final.zip
project-final-fixed.zip
```

Git allows you to keep a clean history of changes through commits.

Each commit represents a specific point in the history of a project.

## Why is Git useful?

Git is useful because it allows you to:

* Track changes in your code.
* See who changed something and when.
* Return to previous versions of a project.
* Work on new features without affecting the main code.
* Collaborate with other developers.
* Review code before merging it.
* Fix mistakes safely.
* Manage different versions of a project.

## Git is distributed

Git is called a distributed version control system because every developer has a complete copy of the repository history on their own computer.

This means you can work locally without needing to be connected to the internet all the time.

For example, you can do the following locally:

```bash
git status
git add .
git commit -m "Add login validation"
git log
```

Later, when you are ready, you can send your changes to a remote repository such as GitHub.

```bash
git push origin main
```

## Repository

A repository, often called a repo, is a project tracked by Git.

A Git repository contains:

* Project files.
* Folders.
* Commit history.
* Branches.
* Configuration files.
* Git metadata.

When a folder is initialized with Git, Git creates a hidden folder called `.git`.

```bash
git init
```

The `.git` folder stores the internal information Git needs to track the project.

## Commit

A commit is a saved snapshot of your project at a specific moment.

Each commit has:

* A unique identifier.
* An author.
* A date.
* A commit message.
* The changes made.

Example:

```bash
git commit -m "Add initial README"
```

A good commit message should describe what changed.

## Branch

A branch is an independent line of development.

Branches allow you to work on new features, fixes, or experiments without directly changing the main branch.

Example:

```bash
git checkout -b feature/login-form
```

Common branch names include:

```txt
main
develop
feature/basic-git-commands
bugfix/fix-login-error
hotfix/production-issue
release/v1.0.0
```

## Working directory

The working directory is the folder where you edit your files.

When you create, modify, or delete files, those changes happen first in your working directory.

You can check the current state of your working directory with:

```bash
git status
```

## Staging area

The staging area is where you prepare changes before committing them.

You add changes to the staging area with:

```bash
git add README.md
```

Or:

```bash
git add .
```

The staging area lets you decide exactly what will be included in the next commit.

## Local repository

The local repository is the Git repository stored on your own computer.

When you create commits, they are saved locally first.

Example:

```bash
git commit -m "Add basic Git explanation"
```

At this point, the commit exists on your computer but not necessarily on GitHub.

## Remote repository

A remote repository is a version of your project hosted somewhere else, such as GitHub, GitLab, or Bitbucket.

A common remote name is:

```txt
origin
```

You can send your local commits to the remote repository with:

```bash
git push origin main
```

You can download changes from the remote repository with:

```bash
git pull origin main
```

## Basic Git workflow

A common Git workflow looks like this:

```bash
git status
git add .
git commit -m "Describe the change"
git push origin branch-name
```

In simple terms:

1. You modify files.
2. You check the status.
3. You stage the changes.
4. You create a commit.
5. You push the commit to a remote repository.

## Example

```bash
git init
git status
git add README.md
git commit -m "Add README file"
git branch -M main
git remote add origin https://github.com/username/repository.git
git push -u origin main
```

This example:

1. Initializes a Git repository.
2. Checks the repository status.
3. Adds the README file to the staging area.
4. Creates the first commit.
5. Renames the branch to `main`.
6. Connects the local repository to GitHub.
7. Pushes the project to GitHub.

## Git in professional development

In real software teams, Git is used for much more than saving changes.

Professional teams use Git to:

* Create feature branches.
* Review pull requests.
* Merge code safely.
* Resolve conflicts.
* Rebase branches.
* Create releases.
* Track bugs.
* Roll back problematic changes.
* Maintain a clean project history.

## Key concepts summary

| Concept           | Meaning                                                 |
| ----------------- | ------------------------------------------------------- |
| Repository        | A project tracked by Git                                |
| Commit            | A saved snapshot of changes                             |
| Branch            | An independent line of development                      |
| Working directory | Where files are modified                                |
| Staging area      | Where changes are prepared before commit                |
| Local repository  | Repository stored on your computer                      |
| Remote repository | Repository hosted on a platform like GitHub             |
| Push              | Send local commits to a remote repository               |
| Pull              | Download and integrate changes from a remote repository |
| Merge             | Combine changes from one branch into another            |

## Recommended next topic

After understanding what Git is, continue with:

```txt
docs/00-introduction/git-vs-github.md
```
