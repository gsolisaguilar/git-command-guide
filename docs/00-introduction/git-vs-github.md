# Git vs GitHub

Git and GitHub are related, but they are not the same thing.

Git is a version control system.

GitHub is a platform that hosts Git repositories online.

Understanding the difference is important because many beginners confuse them.

## What is Git?

Git is a tool installed on your computer that tracks changes in your project files.

You can use Git without GitHub.

For example, you can create a local Git repository with:

```bash
git init
```

You can make commits locally:

```bash
git add .
git commit -m "Add initial project files"
```

At this point, your project is being tracked by Git, even if it is not uploaded anywhere.

## What is GitHub?

GitHub is an online platform where you can store Git repositories remotely.

GitHub allows developers and teams to:

* Store code online.
* Collaborate with other developers.
* Review code using pull requests.
* Track issues.
* Manage projects.
* Host documentation.
* Create releases.
* Share open-source projects.

A GitHub repository is a remote copy of your Git project.

## Main difference

| Git                                            | GitHub                                                |
| ---------------------------------------------- | ----------------------------------------------------- |
| Version control system                         | Online hosting platform                               |
| Installed locally                              | Accessed through the web                              |
| Tracks file changes                            | Stores repositories online                            |
| Works without internet                         | Requires internet for remote collaboration            |
| Uses commands like `commit`, `branch`, `merge` | Provides pull requests, issues, actions, and releases |
| Manages history locally                        | Helps teams collaborate remotely                      |

## Simple explanation

Git is the tool that tracks changes.

GitHub is the website where you upload and share the repository.

Example:

```txt
Git = the version control system
GitHub = the platform that hosts Git repositories
```

## Can Git work without GitHub?

Yes.

You can use Git completely locally on your computer.

Example:

```bash
mkdir my-project
cd my-project
git init
touch README.md
git add README.md
git commit -m "Add README"
```

This project is already using Git, even if it is not connected to GitHub.

## Can GitHub work without Git?

GitHub is built around Git repositories, so Git is the foundation.

However, GitHub also provides a web interface where you can edit files, create branches, and manage pull requests without typing Git commands directly.

Still, understanding Git commands is essential for professional development.

## Local repository vs remote repository

A local repository is stored on your computer.

A remote repository is stored online, for example on GitHub.

Example local repository:

```txt
C:/Users/user/projects/my-app
```

Example remote repository:

```txt
https://github.com/username/my-app
```

## Connecting Git with GitHub

To connect a local Git repository to GitHub, you usually add a remote.

Example:

```bash
git remote add origin https://github.com/username/my-repository.git
```

Then you can push your local commits to GitHub:

```bash
git push -u origin main
```

## Common Git commands

These commands are part of Git:

```bash
git init
git status
git add .
git commit -m "Message"
git branch
git checkout
git switch
git merge
git rebase
git log
git push
git pull
git fetch
```

## Common GitHub features

These features are part of GitHub:

```txt
Repositories
Pull requests
Issues
Actions
Projects
Releases
Forks
Stars
Code review
Repository settings
Branch protection rules
```

## Example workflow using Git and GitHub

A typical workflow looks like this:

```bash
git clone https://github.com/username/project.git
cd project
git checkout -b feature/new-section
git add .
git commit -m "Add new documentation section"
git push origin feature/new-section
```

After pushing the branch to GitHub, you can create a pull request.

The pull request allows other people to review your changes before merging them into the main branch.

## What is a pull request?

A pull request is a GitHub feature used to propose changes.

It allows a developer to say:

```txt
I made changes in this branch. Please review them before merging into the main branch.
```

Pull requests are commonly used for:

* Code review.
* Discussion.
* Automated checks.
* Approval workflows.
* Safe collaboration.

## Git command vs GitHub action

Example with Git:

```bash
git commit -m "Fix typo in README"
```

This creates a commit locally.

Example with GitHub:

```txt
Open a pull request from feature/update-readme into main.
```

This happens on GitHub and is part of the collaboration process.

## Why developers use both

Developers use Git to manage changes and GitHub to collaborate.

Git helps with local version control.

GitHub helps with remote teamwork.

Together, they support professional software development workflows.

## Common beginner confusion

### Confusion 1: "I committed, so my code is already on GitHub"

Not necessarily.

A commit saves changes locally.

To upload changes to GitHub, you need:

```bash
git push
```

### Confusion 2: "I created a GitHub repo, so my local folder is connected automatically"

Not necessarily.

You need to connect your local repo to the remote repo:

```bash
git remote add origin https://github.com/username/repository.git
```

### Confusion 3: "GitHub and Git are the same"

No.

Git is the version control tool.

GitHub is a hosting and collaboration platform.

## Summary

| Question                                  | Answer                        |
| ----------------------------------------- | ----------------------------- |
| Is Git installed locally?                 | Yes                           |
| Is GitHub a website/platform?             | Yes                           |
| Can Git work without GitHub?              | Yes                           |
| Can GitHub host Git repositories?         | Yes                           |
| Does `git commit` upload code to GitHub?  | No                            |
| Does `git push` upload commits to GitHub? | Yes                           |
| Are pull requests a Git command?          | No, they are a GitHub feature |

## Recommended next topic

After understanding the difference between Git and GitHub, continue with:

```txt
docs/00-introduction/git-lifecycle.md
```
