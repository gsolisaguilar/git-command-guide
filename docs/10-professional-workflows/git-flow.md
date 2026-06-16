# Git Flow

Git Flow is a branching model used to organize software development with multiple long-lived and short-lived branches.

It is commonly used in projects that have planned releases, versioning, maintenance branches, and production hotfixes.

## What is Git Flow?

Git Flow is a workflow that uses specific branch types for different purposes.

The main branches are usually:

```txt
main
develop
feature/*
release/*
hotfix/*
```

Each branch has a specific role in the development and release process.

## Main idea

Git Flow separates stable production code from active development.

In simple terms:

```txt
main = production-ready code
develop = integration branch for upcoming work
feature/* = new features
release/* = release preparation
hotfix/* = urgent production fixes
```

## Main branches

### main

The `main` branch contains production-ready code.

It should always represent a stable version of the project.

Common uses:

- Production releases.
- Version tags.
- Stable code.
- Hotfix merges.

Example:

```txt
main
```

### develop

The `develop` branch contains the latest integrated development work.

It is usually more active than `main`.

Common uses:

- Integration of completed features.
- Preparation for future releases.
- Shared development base.

Example:

```txt
develop
```

## Supporting branches

### feature branches

Feature branches are used to develop new functionality.

They usually start from `develop`.

Example:

```txt
feature/user-login
feature/payment-page
feature/git-flow-docs
```

Create a feature branch:

```bash
git switch develop
git pull origin develop
git switch -c feature/git-flow-docs
```

Merge it back into `develop`:

```bash
git switch develop
git merge feature/git-flow-docs
```

### release branches

Release branches are used to prepare a new production release.

They usually start from `develop`.

Example:

```txt
release/v1.0.0
```

Create a release branch:

```bash
git switch develop
git pull origin develop
git switch -c release/v1.0.0
```

Release branches are used for:

- Final testing.
- Bug fixes.
- Documentation updates.
- Version number updates.
- Release notes.

After the release is ready, merge it into `main` and `develop`.

```bash
git switch main
git merge release/v1.0.0
git tag -a v1.0.0 -m "Release version 1.0.0"

git switch develop
git merge release/v1.0.0
```

### hotfix branches

Hotfix branches are used for urgent fixes in production.

They usually start from `main`.

Example:

```txt
hotfix/v1.0.1
```

Create a hotfix branch:

```bash
git switch main
git pull origin main
git switch -c hotfix/v1.0.1
```

After fixing the issue:

```bash
git add .
git commit -m "Fix production issue"
```

Merge into `main`:

```bash
git switch main
git merge hotfix/v1.0.1
git tag -a v1.0.1 -m "Release version 1.0.1"
```

Also merge into `develop`:

```bash
git switch develop
git merge hotfix/v1.0.1
```

## Git Flow diagram

```txt
main:    A----------------M---------H
          \              /         /
develop:   B---C---D----R----E----/
             \       \
feature:      F---G   \
release:              R1---R2
hotfix:                          H1
```

## Typical Git Flow process

```txt
1. Create feature branch from develop.
2. Complete feature work.
3. Merge feature branch into develop.
4. Create release branch from develop.
5. Test and prepare release.
6. Merge release branch into main.
7. Tag the release.
8. Merge release branch back into develop.
9. Create hotfix branches from main when needed.
```

## Feature workflow example

```bash
git switch develop
git pull origin develop
git switch -c feature/git-flow-docs

# make changes

git add .
git commit -m "Add Git Flow documentation"

git switch develop
git merge feature/git-flow-docs
```

## Release workflow example

```bash
git switch develop
git pull origin develop
git switch -c release/v1.0.0

# final fixes and release notes

git add .
git commit -m "Prepare release v1.0.0"

git switch main
git merge release/v1.0.0
git tag -a v1.0.0 -m "Release version 1.0.0"

git switch develop
git merge release/v1.0.0
```

## Hotfix workflow example

```bash
git switch main
git pull origin main
git switch -c hotfix/v1.0.1

# fix production issue

git add .
git commit -m "Fix production issue"

git switch main
git merge hotfix/v1.0.1
git tag -a v1.0.1 -m "Release version 1.0.1"

git switch develop
git merge hotfix/v1.0.1
```

## Advantages of Git Flow

Git Flow is useful because it:

- Provides clear branch roles.
- Supports planned releases.
- Supports production hotfixes.
- Keeps production and development separate.
- Works well for versioned software.
- Makes release preparation organized.

## Disadvantages of Git Flow

Git Flow can be:

- More complex than simpler workflows.
- Too heavy for small teams.
- Too slow for continuous deployment.
- Branch-heavy.
- Harder for beginners.
- More difficult to maintain if releases are frequent.

## When to use Git Flow

Use Git Flow when:

- The project has scheduled releases.
- Production must be very stable.
- Multiple versions are maintained.
- Hotfixes are common.
- The team needs strict release control.
- The product is not deployed continuously.

## When not to use Git Flow

Avoid Git Flow when:

- The team deploys many times per day.
- The project is small.
- The team wants a very simple workflow.
- Trunk-based development is preferred.
- Long-lived branches create integration problems.

## Git Flow vs GitHub Flow

| Workflow | Main idea |
|---|---|
| Git Flow | Uses `main`, `develop`, `feature`, `release`, and `hotfix` branches |
| GitHub Flow | Uses `main` and short-lived feature branches |

Git Flow is more structured.

GitHub Flow is simpler.

## Recommended branch naming

```txt
feature/add-login
feature/git-flow-docs
release/v1.0.0
hotfix/fix-production-error
```

## Common mistakes

### Mistake 1: Forgetting to merge hotfix into develop

A hotfix should usually go into both:

```txt
main
develop
```

Otherwise, the bug may come back in the next release.

### Mistake 2: Keeping feature branches open too long

Long-lived feature branches can create difficult merges.

### Mistake 3: Using Git Flow for a project that does not need it

Git Flow is powerful but can be too complex for simple projects.

### Mistake 4: Tagging before the release is ready

Only tag stable release commits.

## Best practices

- Keep `main` stable.
- Use `develop` for integrated development.
- Keep feature branches focused.
- Keep release branches short-lived.
- Merge hotfixes into both `main` and `develop`.
- Tag releases from `main`.
- Delete completed feature, release, and hotfix branches.
- Document the workflow for the team.

## Professional recommendation

Use Git Flow when your project needs formal releases and production stability.

For smaller projects or documentation repositories, GitHub Flow may be simpler.

## Summary

Git Flow is a structured branching model.

Main branches:

```txt
main
develop
```

Supporting branches:

```txt
feature/*
release/*
hotfix/*
```

Basic idea:

```txt
Features go into develop.
Releases go from develop to main.
Hotfixes go from main back into main and develop.
```

## Recommended next topic

Continue with:

```txt
docs/10-professional-workflows/github-flow.md
```