# Submodules

Git submodules allow you to include one Git repository inside another Git repository.

They are useful when a project depends on another repository and you want to keep that dependency linked to a specific commit.

## What is a submodule?

A submodule is a Git repository nested inside another Git repository.

The main repository stores a reference to a specific commit of the submodule.

In simple terms:

```txt
A submodule lets one repository include another repository.
```

## Why use submodules?

Use submodules when:

- You need to include another repository as a dependency.
- You want to track a specific version of another project.
- You share common code across multiple projects.
- You want dependency code to remain separate.
- You need reproducible builds based on exact commits.

## When not to use submodules

Avoid submodules when:

- You only need a normal package dependency.
- Your team is not familiar with submodule workflows.
- You frequently need to modify both repositories together.
- You want a simpler development experience.
- A package manager would solve the problem better.

## Add a submodule

```bash
git submodule add repository-url path
```

Example:

```bash
git submodule add https://github.com/username/shared-library.git libs/shared-library
```

This creates:

```txt
.gitmodules
libs/shared-library/
```

## What is .gitmodules?

`.gitmodules` stores submodule configuration.

Example:

```ini
[submodule "libs/shared-library"]
    path = libs/shared-library
    url = https://github.com/username/shared-library.git
```

This file should be committed to the main repository.

## Commit a submodule

After adding a submodule:

```bash
git status
git add .gitmodules libs/shared-library
git commit -m "Add shared library submodule"
```

The main repository does not store all the submodule files directly.

It stores a reference to a specific commit inside the submodule.

## Clone a repository with submodules

Basic clone:

```bash
git clone repository-url
```

Then initialize and update submodules:

```bash
git submodule update --init --recursive
```

## Clone with submodules in one command

```bash
git clone --recurse-submodules repository-url
```

This clones the main repository and initializes submodules.

## Update submodules

```bash
git submodule update --remote
```

This updates submodules to the latest commit from their configured remote branch.

## Update submodules recursively

```bash
git submodule update --init --recursive
```

This is useful when submodules contain other submodules.

## Check submodule status

```bash
git submodule status
```

Example output:

```txt
a1b2c3d libs/shared-library (heads/main)
```

## Enter a submodule

A submodule is its own Git repository.

```bash
cd libs/shared-library
git status
git log --oneline
```

You can work inside it like a normal repository.

## Important concept

The parent repository tracks the submodule commit.

If you update the submodule to a new commit, you must commit that change in the parent repository.

## Update submodule commit reference

Enter the submodule:

```bash
cd libs/shared-library
git pull origin main
```

Return to parent repository:

```bash
cd ../..
git status
```

You may see:

```txt
modified: libs/shared-library
```

Commit the updated submodule reference:

```bash
git add libs/shared-library
git commit -m "Update shared library submodule"
```

## Remove a submodule

Removing submodules can be more complex than normal files.

Basic modern workflow:

```bash
git submodule deinit -f path
git rm -f path
rm -rf .git/modules/path
git commit -m "Remove submodule"
```

Example:

```bash
git submodule deinit -f libs/shared-library
git rm -f libs/shared-library
rm -rf .git/modules/libs/shared-library
git commit -m "Remove shared library submodule"
```

On Windows Git Bash, `rm -rf` works in Git Bash.

## Submodule branches

By default, submodules are usually checked out at a specific commit, not necessarily a branch.

You can configure a branch in `.gitmodules`.

Example:

```ini
[submodule "libs/shared-library"]
    path = libs/shared-library
    url = https://github.com/username/shared-library.git
    branch = main
```

Then update:

```bash
git submodule update --remote
```

## Common submodule commands

| Command | Purpose |
|---|---|
| `git submodule add URL path` | Adds a submodule |
| `git submodule status` | Shows submodule status |
| `git submodule update --init --recursive` | Initializes and updates submodules |
| `git clone --recurse-submodules URL` | Clones with submodules |
| `git submodule update --remote` | Updates submodule from remote |
| `git submodule deinit -f path` | Deinitializes a submodule |
| `git rm -f path` | Removes submodule path from Git |

## Common mistakes

### Mistake 1: Forgetting to initialize submodules after cloning

After cloning a repo with submodules:

```bash
git submodule update --init --recursive
```

### Mistake 2: Updating submodule but not committing parent repo change

If the submodule commit changes, commit the reference in the parent repo:

```bash
git add submodule-path
git commit -m "Update submodule"
```

### Mistake 3: Thinking submodule code is stored normally in the parent repo

The parent repo stores a reference to a commit, not the full independent history.

### Mistake 4: Editing submodule without understanding it is a separate repo

Inside the submodule, you are in another Git repository.

Check:

```bash
git status
```

## Best practices

- Use submodules only when they are truly needed.
- Document submodule setup in the README.
- Use `--recurse-submodules` when cloning.
- Commit `.gitmodules`.
- Commit submodule reference updates in the parent repo.
- Avoid unnecessary complexity.
- Make sure the team understands the workflow.

## Professional recommendation

For projects with submodules, document this command clearly:

```bash
git clone --recurse-submodules repository-url
```

If already cloned:

```bash
git submodule update --init --recursive
```

## Summary

Submodules let one Git repository include another Git repository.

Add submodule:

```bash
git submodule add repository-url path
```

Clone with submodules:

```bash
git clone --recurse-submodules repository-url
```

Initialize after clone:

```bash
git submodule update --init --recursive
```

Golden rule:

```txt
A submodule is a separate repository tracked at a specific commit.
```

## Recommended next topic

Continue with:

```txt
docs/09-advanced-git/worktrees.md
```