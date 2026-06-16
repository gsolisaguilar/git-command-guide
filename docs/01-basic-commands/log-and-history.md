# Log and History

Git keeps a history of commits.

The command `git log` allows you to review that history.

Understanding Git history is important because it helps you know what changed, when it changed, and who changed it.

## Basic git log

To see the commit history:

```bash
git log
```

This shows detailed information about each commit.

Example output:

```txt
commit a1b2c3d4e5f6
Author: Jessica Santos <jessica@example.com>
Date:   Tue Jun 16 10:30:00 2026 -0600

    Add basic Git workflow documentation
```

## Information shown by git log

A commit usually includes:

- Commit hash.
- Author.
- Date.
- Commit message.

## Commit hash

Each commit has a unique identifier called a hash.

Example:

```txt
a1b2c3d4e5f6
```

A short version is often enough:

```txt
a1b2c3d
```

Git uses this hash to identify specific commits.

## Short log format

A very useful format is:

```bash
git log --oneline
```

Example output:

```txt
a1b2c3d Add basic Git workflow documentation
e4f5g6h Add Git lifecycle documentation
i7j8k9l Add README structure
```

This is easier to read than the full log.

## Show commit graph

To see branches and merges visually:

```bash
git log --oneline --graph
```

A more complete version:

```bash
git log --oneline --graph --decorate --all
```

Example output:

```txt
* a1b2c3d Add basic Git workflow
* e4f5g6h Add Git lifecycle documentation
* i7j8k9l Add README structure
```

## Show latest commits

To show only the latest commits:

```bash
git log -n 5
```

This shows the last 5 commits.

You can also use:

```bash
git log --oneline -n 5
```

## Show commits by author

```bash
git log --author="Jessica"
```

This shows commits created by an author matching that name.

## Show commits for a specific file

```bash
git log -- README.md
```

This shows the commit history related to `README.md`.

Example:

```bash
git log -- docs/01-basic-commands/basic-workflow.md
```

## Show changes included in commits

```bash
git log -p
```

This shows each commit with the actual changes.

To limit it:

```bash
git log -p -n 2
```

This shows the changes from the last 2 commits.

## Show statistics

```bash
git log --stat
```

This shows which files changed and how many lines were added or removed.

Example output:

```txt
README.md | 10 +++++-----
1 file changed, 5 insertions(+), 5 deletions(-)
```

## Show a specific commit

Use `git show` with a commit hash:

```bash
git show a1b2c3d
```

This displays:

- Commit information.
- Commit message.
- Files changed.
- Actual code or text differences.

## Compare history with git diff

`git diff` can compare different commits.

Example:

```bash
git diff commit1 commit2
```

Using example hashes:

```bash
git diff a1b2c3d e4f5g6h
```

## Show current branch history

```bash
git log --oneline
```

This shows the history of the current branch.

## Show all branches history

```bash
git log --oneline --all
```

This includes commits from all branches.

## Show decorated history

```bash
git log --oneline --decorate
```

This shows branch and tag references next to commits.

Example:

```txt
a1b2c3d (HEAD -> main, origin/main) Add README
```

## Useful git log formats

| Command | Purpose |
|---|---|
| `git log` | Shows full commit history |
| `git log --oneline` | Shows compact commit history |
| `git log --oneline --graph` | Shows history as a graph |
| `git log --oneline --graph --decorate --all` | Shows a complete visual history |
| `git log -n 5` | Shows latest 5 commits |
| `git log --author="Name"` | Shows commits by author |
| `git log -- file-name` | Shows history of a specific file |
| `git log -p` | Shows commits with detailed changes |
| `git log --stat` | Shows file change statistics |
| `git show commit-hash` | Shows details of one commit |

## Practical examples

### Example 1: View short history

```bash
git log --oneline
```

Use this when you want a quick view of recent commits.

### Example 2: View branch graph

```bash
git log --oneline --graph --decorate --all
```

Use this when working with branches, merges, or rebases.

### Example 3: View history of README

```bash
git log -- README.md
```

Use this when you want to know how a specific file changed over time.

### Example 4: View details of one commit

```bash
git show a1b2c3d
```

Use this when you want to inspect a specific commit.

## Professional recommendation

A very useful command for daily work is:

```bash
git log --oneline --graph --decorate --all
```

This gives a clear view of:

- Commits.
- Branches.
- Merges.
- Current HEAD.
- Remote references.

## Understanding HEAD

`HEAD` points to your current position in the repository.

Usually, `HEAD` points to the latest commit of the current branch.

Example:

```txt
a1b2c3d (HEAD -> feature/basic-git-commands) Add log documentation
```

This means you are currently on the branch `feature/basic-git-commands`, and the latest commit is `a1b2c3d`.

## Understanding origin

`origin` is the default name of the remote repository.

Example:

```txt
origin/main
```

This means the `main` branch on the remote repository named `origin`.

## Understanding branch references

Example:

```txt
a1b2c3d (HEAD -> main, origin/main) Add README
```

This means:

- Your current branch is `main`.
- Your local `main` points to this commit.
- The remote `origin/main` also points to this commit.

## Common mistakes

### Mistake 1: Not checking history before changing branches

Before switching branches, it can be useful to check:

```bash
git log --oneline --graph --decorate --all
```

### Mistake 2: Not understanding commit hashes

Commit hashes are important when using commands like:

```bash
git show
git revert
git reset
git cherry-pick
```

### Mistake 3: Only using git log without options

The default `git log` can be too detailed.

For daily use, this is often better:

```bash
git log --oneline
```

### Mistake 4: Ignoring the graph view

When working with branches and merges, the graph view helps understand the project history.

Use:

```bash
git log --oneline --graph --decorate --all
```

## Basic history workflow

```bash
git status
git log --oneline
git log --oneline --graph --decorate --all
```

## Example for this repository

```bash
git log --oneline --graph --decorate --all
```

Example output:

```txt
* 3f4a5b6 (HEAD -> feature/basic-git-commands) Add log and history documentation
* 2c3d4e5 Add status add commit documentation
* 1a2b3c4 Add basic workflow documentation
```

## Summary

Git history helps you understand the evolution of a project.

Main commands:

```bash
git log
git log --oneline
git log --oneline --graph --decorate --all
git show commit-hash
git log -- file-name
```

Use Git history to review changes, understand branches, inspect commits, and work more safely.

## Recommended next topic

Continue with:

```txt
docs/11-cheatsheets/basic-commands-cheatsheet.md
```