# Setup and Configuration

Before using Git in a professional workflow, it is important to configure your local environment correctly.

Git configuration defines your identity, default behavior, preferred editor, branch naming, line endings, and other settings.

## Check if Git is installed

To verify if Git is installed, run:

```bash
git --version
```

Example output:

```txt
git version 2.45.0
```

If Git is not installed, download it from the official Git website:

```txt
https://git-scm.com/
```

## Configure your user name

Git uses your name to identify who created each commit.

```bash
git config --global user.name "Your Name"
```

Example:

```bash
git config --global user.name "Gabriel Solis"
```

## Configure your email

Git also uses your email in commits.

```bash
git config --global user.email "your-email@example.com"
```

Example:

```bash
git config --global user.email "gsolis@example.com"
```

This email should usually match the email associated with your GitHub account.

## Check your current configuration

To see your global Git configuration, run:

```bash
git config --global --list
```

Example output:

```txt
user.name=Jessica Santos
user.email=jessica@example.com
init.defaultbranch=main
```

## Configure the default branch name

Modern repositories usually use `main` as the default branch name.

```bash
git config --global init.defaultBranch main
```

This means new repositories created with `git init` will start with a branch named `main`.

## Configure the default editor

Git may open a text editor when writing commit messages, resolving conflicts, or rebasing.

Example using Visual Studio Code:

```bash
git config --global core.editor "code --wait"
```

Example using Vim:

```bash
git config --global core.editor "vim"
```

Example using Nano:

```bash
git config --global core.editor "nano"
```

## Configure line endings

Line endings can be different depending on the operating system.

Windows usually uses:

```txt
CRLF
```

Linux and macOS usually use:

```txt
LF
```

Recommended configuration for Windows:

```bash
git config --global core.autocrlf true
```

Recommended configuration for macOS or Linux:

```bash
git config --global core.autocrlf input
```

## Configure colored output

Git can show colored output in the terminal.

```bash
git config --global color.ui auto
```

This makes commands like `git status`, `git diff`, and `git log` easier to read.

## Configure pull behavior

When using `git pull`, Git needs to know how to integrate remote changes into your local branch.

A safe beginner-friendly option is:

```bash
git config --global pull.rebase false
```

This means `git pull` will use merge by default.

For a rebase-based workflow, you can use:

```bash
git config --global pull.rebase true
```

However, use this only when you already understand rebase.

## Configure push behavior

A common professional configuration is:

```bash
git config --global push.default simple
```

This means Git will push the current branch to its matching upstream branch.

## Useful configuration commands

| Command | Purpose |
|---|---|
| `git config --global user.name "Name"` | Sets your Git username |
| `git config --global user.email "email"` | Sets your Git email |
| `git config --global --list` | Shows global configuration |
| `git config --global init.defaultBranch main` | Sets `main` as the default branch |
| `git config --global core.editor "code --wait"` | Sets VS Code as the Git editor |
| `git config --global color.ui auto` | Enables colored Git output |
| `git config --global push.default simple` | Sets simple push behavior |

## Local vs global configuration

Git has different configuration levels.

| Level | Scope | Example |
|---|---|---|
| System | Applies to all users on the computer | `git config --system` |
| Global | Applies to the current user | `git config --global` |
| Local | Applies only to the current repository | `git config --local` |

Most personal settings should be configured globally.

Example:

```bash
git config --global user.name "Jessica Santos"
```

Repository-specific settings can be configured locally.

Example:

```bash
git config --local user.email "work-email@example.com"
```

## Where Git configuration is stored

Global Git configuration is usually stored in:

```txt
~/.gitconfig
```

Local repository configuration is stored in:

```txt
.git/config
```

## Check a specific configuration value

To check your configured username:

```bash
git config user.name
```

To check your configured email:

```bash
git config user.email
```

To check your default branch:

```bash
git config init.defaultBranch
```

## Edit Git configuration manually

You can open your global Git configuration file with:

```bash
git config --global --edit
```

This opens the configuration file in your configured editor.

## Professional recommendation

Before starting to work with Git, configure at least:

```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
git config --global init.defaultBranch main
git config --global color.ui auto
git config --global push.default simple
```

## Example complete setup

```bash
git config --global user.name "Jessica Santos"
git config --global user.email "jessica@example.com"
git config --global init.defaultBranch main
git config --global core.editor "code --wait"
git config --global color.ui auto
git config --global push.default simple
git config --global core.autocrlf true
```

## Verify final configuration

```bash
git config --global --list
```

Example output:

```txt
user.name=Jessica Santos
user.email=jessica@example.com
init.defaultbranch=main
core.editor=code --wait
color.ui=auto
push.default=simple
core.autocrlf=true
```

## Common mistakes

### Mistake 1: Not configuring user name and email

If you do not configure your name and email, Git may not identify your commits correctly.

### Mistake 2: Using the wrong email

If your Git email does not match your GitHub email, your commits may not appear correctly linked to your GitHub profile.

### Mistake 3: Forgetting to set the default branch

If you do not configure the default branch, Git may create new repositories with a different branch name depending on your version.

### Mistake 4: Not understanding global vs local configuration

Global configuration affects all repositories.

Local configuration affects only one repository.

## Summary

Git configuration is one of the first steps before working with repositories.

The most important settings are:

```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
git config --global init.defaultBranch main
```

A good configuration helps keep commits professional, consistent, and easier to track.

## Recommended next topic

Continue with:

```txt
docs/01-basic-commands/create-and-clone-repositories.md
```