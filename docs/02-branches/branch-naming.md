# Branch Naming

Branch naming is important in professional Git workflows.

A good branch name helps developers understand the purpose of the work without opening the files or commits.

## Why branch naming matters

Clear branch names help teams:

- Understand the purpose of a branch.
- Organize work by type.
- Identify features, fixes, releases, or documentation tasks.
- Improve collaboration.
- Make pull requests easier to review.
- Keep repository history cleaner.

## Basic branch naming format

A common format is:

```txt
type/short-description
```

Example:

```txt
feature/login-form
```

This branch name has two parts:

```txt
feature = type of work
login-form = short description
```

## Common branch types

| Type | Purpose |
|---|---|
| `feature/` | New feature or new functionality |
| `bugfix/` | Fix for a non-urgent bug |
| `hotfix/` | Urgent fix, usually for production |
| `release/` | Prepare a new release |
| `docs/` | Documentation changes |
| `chore/` | Maintenance tasks |
| `refactor/` | Code restructuring without changing behavior |
| `test/` | Test-related changes |
| `experiment/` | Experimental work |

## Feature branches

Use `feature/` for new functionality or new sections.

Examples:

```txt
feature/user-login
feature/payment-page
feature/basic-git-commands
feature/branching-guide
```

## Bugfix branches

Use `bugfix/` for normal bug fixes.

Examples:

```txt
bugfix/fix-login-validation
bugfix/fix-navbar-alignment
bugfix/fix-readme-link
```

## Hotfix branches

Use `hotfix/` for urgent production fixes.

Examples:

```txt
hotfix/fix-production-login-error
hotfix/fix-critical-payment-bug
hotfix/restore-missing-config
```

## Release branches

Use `release/` when preparing a new version.

Examples:

```txt
release/v1.0.0
release/v2.1.0
release/2026-06
```

## Documentation branches

Use `docs/` when the change is only documentation.

Examples:

```txt
docs/update-readme
docs/add-git-lifecycle
docs/fix-setup-guide
```

In this repository, `feature/` can also be used for documentation sections if each section is treated as a feature of the guide.

Example:

```txt
feature/basic-git-commands
feature/branching-guide
```

## Chore branches

Use `chore/` for maintenance tasks that do not directly change application behavior.

Examples:

```txt
chore/update-dependencies
chore/clean-folder-structure
chore/update-gitignore
```

## Refactor branches

Use `refactor/` when improving code structure without changing behavior.

Examples:

```txt
refactor/user-service
refactor/auth-module
refactor/project-structure
```

## Test branches

Use `test/` when adding or improving tests.

Examples:

```txt
test/add-login-tests
test/update-api-tests
test/fix-unit-tests
```

## Experiment branches

Use `experiment/` for temporary ideas or prototypes.

Examples:

```txt
experiment/new-layout
experiment/api-cache-strategy
experiment/git-docs-format
```

## Recommended naming rules

Use lowercase letters.

Recommended:

```txt
feature/basic-git-commands
```

Avoid uppercase:

```txt
Feature/Basic-Git-Commands
```

Use hyphens to separate words.

Recommended:

```txt
feature/user-profile-page
```

Avoid spaces:

```txt
feature/user profile page
```

Avoid special characters.

Recommended:

```txt
bugfix/fix-login-error
```

Avoid:

```txt
bugfix/fix@login#error!
```

## Good branch name examples

```txt
feature/basic-git-commands
feature/branching-guide
feature/remote-repositories
bugfix/fix-readme-link
hotfix/fix-production-error
docs/update-installation-guide
chore/update-folder-structure
release/v1.0.0
```

## Bad branch name examples

```txt
test
changes
update
final
new
my-branch
fix
branch1
jessica
```

These names are not clear enough.

## Branch names with issue numbers

Some teams include ticket or issue numbers.

Format:

```txt
type/ticket-number-short-description
```

Examples:

```txt
feature/123-add-login-form
bugfix/456-fix-payment-error
docs/789-update-readme
```

Another common format:

```txt
type/TICKET-123-short-description
```

Examples:

```txt
feature/PROJ-123-add-login-form
bugfix/PROJ-456-fix-payment-error
```

This is useful when working with tools like Jira, GitHub Issues, Azure DevOps, or Trello.

## Branch naming for this repository

For this repository, recommended branches are:

```txt
feature/basic-git-commands
feature/branching-guide
feature/remote-repositories
feature/merge-conflict-guide
feature/rebase-guide
feature/undoing-changes
feature/stash-guide
feature/tags-and-releases
feature/advanced-git-commands
feature/professional-workflows
feature/cheatsheets
feature/final-docs-polish
```

## Naming by difficulty level

Since this repository is a Git guide from beginner to expert, branches can also follow the learning path.

Examples:

```txt
feature/beginner-git
feature/intermediate-branches
feature/advanced-rebase
feature/expert-workflows
```

However, topic-based names are usually clearer.

## Professional recommendation

Use this pattern:

```txt
type/short-clear-description
```

Examples:

```txt
feature/branching-guide
bugfix/fix-broken-link
docs/update-git-lifecycle
chore/update-folder-structure
```

Keep names:

- Short.
- Clear.
- Lowercase.
- Related to the task.
- Easy to understand.

## Create a branch with a good name

Example:

```bash
git switch -c feature/branching-guide
```

Older syntax:

```bash
git checkout -b feature/branching-guide
```

## Rename a badly named branch

If you created a branch with a bad name, rename it.

If you are currently on the branch:

```bash
git branch -m new-branch-name
```

Example:

```bash
git branch -m feature/branching-guide
```

If you are renaming another local branch:

```bash
git branch -m old-branch-name new-branch-name
```

Example:

```bash
git branch -m test feature/branching-guide
```

## Common mistakes

### Mistake 1: Using vague names

Avoid:

```txt
fix
changes
update
```

Use:

```txt
bugfix/fix-login-error
docs/update-readme-navigation
```

### Mistake 2: Using personal names only

Avoid:

```txt
jessica
gabriel
my-work
```

Use the task name instead:

```txt
feature/basic-git-commands
```

### Mistake 3: Using spaces

Avoid:

```txt
feature/basic git commands
```

Use:

```txt
feature/basic-git-commands
```

### Mistake 4: Making names too long

Avoid:

```txt
feature/this-is-the-branch-where-i-am-going-to-add-all-the-basic-git-commands-for-the-guide
```

Use:

```txt
feature/basic-git-commands
```

## Branch naming checklist

Before creating a branch, ask:

```txt
Does the name describe the task?
Does it use a clear type?
Is it lowercase?
Does it use hyphens instead of spaces?
Is it short but understandable?
```

## Summary

A good branch name makes the repository easier to understand.

Recommended format:

```txt
type/short-description
```

Examples:

```txt
feature/basic-git-commands
bugfix/fix-readme-link
docs/update-setup-guide
hotfix/fix-production-error
release/v1.0.0
```

Good branch naming is a small habit that makes Git workflows more professional.

## Recommended next topic

Continue with:

```txt
docs/02-branches/delete-and-rename-branches.md
```