# Remotes

A remote is a version of your Git repository hosted somewhere outside your local computer.

Remote repositories are commonly hosted on platforms such as GitHub, GitLab, Bitbucket, or Azure DevOps.

In professional development, remotes are essential because they allow developers to collaborate, share code, back up work, and synchronize changes between local and online repositories.

## What is a remote repository?

A remote repository is an online copy of your Git project.

Example:

```txt
https://github.com/username/project-name.git
```

Your local repository lives on your computer.

Your remote repository lives on a hosting platform such as GitHub.

## Why remotes are useful

Remote repositories allow you to:

- Upload your local commits.
- Download changes from other developers.
- Collaborate with a team.
- Create pull requests.
- Review code before merging.
- Keep a backup of your project.
- Work from different computers.
- Share your project publicly or privately.

## Local repository vs remote repository

| Repository type | Location | Example |
|---|---|---|
| Local repository | Your computer | `C:/Users/user/projects/my-app` |
| Remote repository | Online platform | `https://github.com/user/my-app.git` |

## Common remote name: origin

The default remote name is usually:

```txt
origin
```

When you clone a repository, Git automatically creates a remote called `origin`.

Example:

```bash
git clone https://github.com/username/project-name.git
```

After cloning, you can check the remote:

```bash
git remote -v
```

Example output:

```txt
origin  https://github.com/username/project-name.git (fetch)
origin  https://github.com/username/project-name.git (push)
```

## Check existing remotes

To list the configured remotes:

```bash
git remote
```

Example output:

```txt
origin
```

To see the remote URLs:

```bash
git remote -v
```

Example output:

```txt
origin  https://github.com/username/git-commands-guide.git (fetch)
origin  https://github.com/username/git-commands-guide.git (push)
```

## Add a remote

If you created a local repository with `git init`, it does not have a remote by default.

You can add one with:

```bash
git remote add origin repository-url
```

Example:

```bash
git remote add origin https://github.com/username/git-commands-guide.git
```

After adding it, verify it with:

```bash
git remote -v
```

## Change a remote URL

If the remote URL is wrong, update it with:

```bash
git remote set-url origin new-repository-url
```

Example:

```bash
git remote set-url origin https://github.com/username/new-repository.git
```

Verify the change:

```bash
git remote -v
```

## Remove a remote

To remove a remote:

```bash
git remote remove origin
```

Or:

```bash
git remote rm origin
```

Use this only when you want to disconnect your local repository from that remote.

## Rename a remote

To rename a remote:

```bash
git remote rename old-name new-name
```

Example:

```bash
git remote rename origin github
```

After this, your remote is named `github` instead of `origin`.

## Show detailed remote information

Use:

```bash
git remote show origin
```

This shows detailed information about the remote repository, including:

- Fetch URL.
- Push URL.
- Remote branches.
- Local branches configured for pull.
- Local branches configured for push.

## Fetch URL and push URL

A remote can have a fetch URL and a push URL.

Example:

```txt
origin  https://github.com/username/project.git (fetch)
origin  https://github.com/username/project.git (push)
```

The fetch URL is used to download changes.

The push URL is used to upload changes.

Usually, both URLs are the same.

## HTTPS remote URL

Example:

```txt
https://github.com/username/project-name.git
```

HTTPS is common and easy to use.

Example command:

```bash
git remote add origin https://github.com/username/project-name.git
```

## SSH remote URL

Example:

```txt
git@github.com:username/project-name.git
```

SSH is commonly used by developers who configure SSH keys.

Example command:

```bash
git remote add origin git@github.com:username/project-name.git
```

## HTTPS vs SSH

| Option | Description |
|---|---|
| HTTPS | Uses a web URL and usually authentication through browser, token, or credential manager |
| SSH | Uses SSH keys for authentication |

Both are valid.

For beginners, HTTPS is often easier to start with.

For professional development, SSH is also very common.

## Example: connect a local repo to GitHub

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/username/git-commands-guide.git
git push -u origin main
```

## Example: check if your repo is connected to GitHub

```bash
git remote -v
```

Expected output:

```txt
origin  https://github.com/username/git-commands-guide.git (fetch)
origin  https://github.com/username/git-commands-guide.git (push)
```

## Common remote commands

| Command | Purpose |
|---|---|
| `git remote` | Lists remote names |
| `git remote -v` | Lists remote names and URLs |
| `git remote add origin URL` | Adds a remote repository |
| `git remote set-url origin URL` | Changes a remote URL |
| `git remote remove origin` | Removes a remote |
| `git remote rename old new` | Renames a remote |
| `git remote show origin` | Shows detailed information about a remote |

## Common mistakes

### Mistake 1: Creating a GitHub repository but not adding the remote

A GitHub repository does not automatically connect to your local folder.

You need:

```bash
git remote add origin https://github.com/username/repository.git
```

### Mistake 2: Using the wrong remote URL

If you push to the wrong repository, check the remote URL:

```bash
git remote -v
```

Fix it with:

```bash
git remote set-url origin correct-url
```

### Mistake 3: Confusing origin with main

`origin` is the remote name.

`main` is usually a branch name.

Example:

```bash
git push origin main
```

This means:

```txt
Push the local main branch to the remote named origin.
```

### Mistake 4: Removing a remote by accident

If you remove a remote, your commits are not deleted, but your local repository is disconnected from that remote.

You can add it again with:

```bash
git remote add origin repository-url
```

## Professional recommendation

Before pushing or pulling, verify the remote:

```bash
git remote -v
```

This helps avoid sending changes to the wrong repository.

## Summary

A remote connects your local repository with an online repository.

Most common remote command:

```bash
git remote -v
```

Common remote name:

```txt
origin
```

Add a remote:

```bash
git remote add origin repository-url
```

Push to a remote:

```bash
git push origin branch-name
```

Remotes are essential for collaboration and professional Git workflows.

## Recommended next topic

Continue with:

```txt
docs/03-remote-repositories/push-and-pull.md
```