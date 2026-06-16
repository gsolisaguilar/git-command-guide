# Create and Clone Repositories

A Git repository is a project tracked by Git.

There are two common ways to start working with a repository:

1. Create a new local repository.
2. Clone an existing remote repository.

## Create a new repository with git init

Use `git init` when you already have a local folder and want Git to start tracking it.

Example:

```bash
mkdir my-project
cd my-project
git init
```

This creates a hidden folder called:

```txt
.git
```

The `.git` folder contains the internal Git information required to track the repository.

## Check repository status

After initializing the repository, run:

```bash
git status
```

Example output:

```txt
On branch main

No commits yet

nothing to commit
```

This means Git is active in the folder, but no commits have been created yet.

## Create a README file

A common first file in a repository is `README.md`.

```bash
touch README.md
```

Then check the status:

```bash
git status
```

You may see:

```txt
Untracked files:
  README.md
```

This means Git sees the file, but it is not tracking it yet.

## Add files to the staging area

To stage the README file:

```bash
git add README.md
```

Or to stage all files:

```bash
git add .
```

## Create the first commit

```bash
git commit -m "Add initial README"
```

This saves the first snapshot of the project in the local Git history.

## Rename the main branch

If needed, rename the current branch to `main`:

```bash
git branch -M main
```

This is commonly used because `main` is the standard default branch name in many modern repositories.

## Create a remote repository on GitHub

To connect your local repository with GitHub:

1. Go to GitHub.
2. Create a new repository.
3. Copy the repository URL.

Example remote URL:

```txt
https://github.com/username/my-project.git
```

## Connect local repository to GitHub

Use `git remote add`:

```bash
git remote add origin https://github.com/username/my-project.git
```

`origin` is the default name commonly used for the main remote repository.

## Verify remote connection

```bash
git remote -v
```

Example output:

```txt
origin  https://github.com/username/my-project.git (fetch)
origin  https://github.com/username/my-project.git (push)
```

## Push the first commit

```bash
git push -u origin main
```

The `-u` option sets the upstream branch.

This means your local `main` branch will track the remote `main` branch.

After that, you can usually push with:

```bash
git push
```

## Full example: create a new repository

```bash
mkdir my-project
cd my-project
git init
touch README.md
git add README.md
git commit -m "Add initial README"
git branch -M main
git remote add origin https://github.com/username/my-project.git
git push -u origin main
```

## Clone an existing repository

Use `git clone` when the repository already exists on GitHub or another remote platform.

Example:

```bash
git clone https://github.com/username/my-project.git
```

This command:

1. Downloads the repository.
2. Creates a local folder.
3. Copies the full Git history.
4. Connects the local repository to the remote repository automatically.

## Clone into a specific folder

```bash
git clone https://github.com/username/my-project.git custom-folder-name
```

Example:

```bash
git clone https://github.com/username/my-project.git git-guide
```

This clones the repository into a folder named `git-guide`.

## Enter the cloned repository

```bash
cd my-project
```

Then verify the status:

```bash
git status
```

## Check remote after cloning

```bash
git remote -v
```

A cloned repository already has a remote named `origin`.

Example:

```txt
origin  https://github.com/username/my-project.git (fetch)
origin  https://github.com/username/my-project.git (push)
```

## git init vs git clone

| Command | Use when |
|---|---|
| `git init` | You are starting a new local project |
| `git clone` | You want to copy an existing remote repository |

## Example using git init

```bash
mkdir new-project
cd new-project
git init
```

Use this when you are creating a new project from zero.

## Example using git clone

```bash
git clone https://github.com/username/existing-project.git
```

Use this when the project already exists on GitHub.

## Common repository commands

| Command | Purpose |
|---|---|
| `git init` | Initializes a new Git repository |
| `git clone` | Copies an existing remote repository |
| `git remote add origin URL` | Connects a local repo to a remote repo |
| `git remote -v` | Shows configured remotes |
| `git branch -M main` | Renames the current branch to `main` |
| `git push -u origin main` | Pushes and sets upstream tracking |

## Common mistakes

### Mistake 1: Running git init in the wrong folder

Before running `git init`, make sure you are inside the correct project folder.

Check your location with:

```bash
pwd
```

Or on Windows Command Prompt:

```cmd
cd
```

### Mistake 2: Creating a GitHub repository but not connecting it locally

Creating a repo on GitHub does not automatically connect your local folder.

You need:

```bash
git remote add origin https://github.com/username/repository.git
```

### Mistake 3: Forgetting the first commit before pushing

You cannot push an empty repository unless it has commits.

Create a commit first:

```bash
git add .
git commit -m "Initial commit"
```

### Mistake 4: Cloning inside another Git repository by accident

Avoid cloning a repository inside another repository unless you know what you are doing.

This can create confusion.

## Professional recommendation

When starting a new project, always include a README file.

A good first commit could be:

```bash
git commit -m "Add initial project documentation"
```

For professional repositories, also consider adding:

```txt
.gitignore
LICENSE
CONTRIBUTING.md
docs/
```

## Summary

Use `git init` to start tracking a local project.

Use `git clone` to copy an existing remote repository.

Basic new repository workflow:

```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin repository-url
git push -u origin main
```

Basic clone workflow:

```bash
git clone repository-url
cd repository-name
git status
```

## Recommended next topic

Continue with:

```txt
docs/01-basic-commands/basic-workflow.md
```