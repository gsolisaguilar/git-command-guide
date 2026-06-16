# Release Workflow

A release workflow is the process used to prepare, mark, and publish a stable version of a project.

In Git, releases are commonly managed using branches, commits, tags, and sometimes GitHub releases.

## What is a release?

A release is a stable version of a project.

A release may include:

- New features.
- Bug fixes.
- Documentation updates.
- Version changes.
- Build artifacts.
- Release notes.

## Why release workflows matter

Release workflows help teams:

- Publish stable versions.
- Track what changed.
- Roll back if needed.
- Communicate updates.
- Organize deployments.
- Maintain version history.
- Connect Git history to product versions.

## Common release version format

A common version format is semantic versioning:

```txt
vMAJOR.MINOR.PATCH
```

Example:

```txt
v1.0.0
```

## Semantic versioning

| Part | Meaning | Example |
|---|---|---|
| MAJOR | Breaking changes | `v2.0.0` |
| MINOR | New compatible features | `v1.1.0` |
| PATCH | Bug fixes | `v1.0.1` |

## Example version changes

| Change | Version update |
|---|---|
| First stable version | `v1.0.0` |
| Add new documentation section | `v1.1.0` |
| Fix typo or broken link | `v1.1.1` |
| Major restructuring | `v2.0.0` |

## Basic release workflow

A simple Git release workflow is:

```bash
git switch main
git pull origin main
git status
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin main
git push origin v1.0.0
```

This creates and pushes a release tag.

## If you are working locally only

If you have not pushed to GitHub yet, the workflow is:

```bash
git switch main
git status
git log --oneline
git tag -a v1.0.0 -m "Release version 1.0.0"
```

When you are ready to upload everything:

```bash
git push origin main
git push origin v1.0.0
```

## Release branch workflow

Some teams use release branches.

Example branch:

```txt
release/v1.0.0
```

Create release branch:

```bash
git switch main
git switch -c release/v1.0.0
```

Use this branch to prepare the release.

## When to use a release branch

Use a release branch when:

- Final testing is needed.
- Documentation needs final updates.
- Version numbers need updates.
- Only release fixes should be added.
- The team wants to continue feature development separately.

## Release branch example

```bash
git switch main
git pull origin main
git switch -c release/v1.0.0
```

Make release changes:

```bash
git add .
git commit -m "Prepare release v1.0.0"
```

Merge back into main:

```bash
git switch main
git merge release/v1.0.0
```

Create tag:

```bash
git tag -a v1.0.0 -m "Release version 1.0.0"
```

Push:

```bash
git push origin main
git push origin v1.0.0
```

## GitHub release workflow

A GitHub release usually starts from a Git tag.

Typical process:

```txt
1. Merge final changes into main.
2. Create an annotated tag.
3. Push the tag to GitHub.
4. Create a GitHub release from that tag.
5. Add release notes.
6. Attach files if needed.
```

## Release notes

Release notes explain what changed in a version.

They may include:

- New features.
- Fixes.
- Breaking changes.
- Documentation changes.
- Known issues.
- Upgrade notes.

## Example release notes

```md
# Release v1.0.0

## Added

- Introduction to Git.
- Basic Git commands.
- Branch management guide.
- Remote repository documentation.
- Merge and conflict resolution guide.

## Changed

- Improved README structure.

## Fixed

- Corrected documentation links.
```

## Changelog

A changelog is a file that records changes across versions.

Common file name:

```txt
CHANGELOG.md
```

Example structure:

```md
# Changelog

## [v1.0.0] - 2026-06-16

### Added

- Initial Git command guide.
- Beginner Git documentation.
- Branching and merge documentation.
```

## Recommended release checklist

Before creating a release, check:

```txt
Is main updated?
Are all intended branches merged?
Are tests passing?
Is documentation updated?
Is the README updated?
Is the version number correct?
Are release notes ready?
Is the working tree clean?
```

## Commands before release

```bash
git switch main
git status
git log --oneline --graph --decorate --all
```

If using GitHub:

```bash
git pull origin main
```

## Create release tag

```bash
git tag -a v1.0.0 -m "Release version 1.0.0"
```

## Push release tag

```bash
git push origin v1.0.0
```

## Push main

```bash
git push origin main
```

## Verify tags

```bash
git tag
git show v1.0.0
```

## Delete release branch after merge

If you used a release branch and it is already merged:

```bash
git branch -d release/v1.0.0
```

If it exists remotely:

```bash
git push origin --delete release/v1.0.0
```

## Hotfix after a release

If a bug is found after release, create a hotfix branch.

Example:

```bash
git switch main
git switch -c hotfix/v1.0.1
```

Fix the issue:

```bash
git add .
git commit -m "Fix release documentation typo"
```

Merge into main:

```bash
git switch main
git merge hotfix/v1.0.1
```

Tag the patch version:

```bash
git tag -a v1.0.1 -m "Release version 1.0.1"
```

Push:

```bash
git push origin main
git push origin v1.0.1
```

## Release workflow for this repository

For this Git guide repository, a release can represent a completed documentation milestone.

Example:

```txt
v1.0.0 = initial guide from introduction to releases
v1.1.0 = advanced Git commands added
v1.2.0 = professional workflows added
```

## Example release workflow for this repository

```bash
git switch main
git status
git log --oneline --graph --decorate --all
git tag -a v1.0.0 -m "Release version 1.0.0: Git guide basics and workflows"
git push origin main
git push origin v1.0.0
```

If you have not pushed anything yet:

```bash
git switch main
git status
git tag -a v1.0.0 -m "Release version 1.0.0: Git guide basics and workflows"
```

Then later:

```bash
git push origin main
git push origin v1.0.0
```

## Release workflow with release branch

```bash
git switch main
git switch -c release/v1.0.0
git add .
git commit -m "Prepare release v1.0.0"
git switch main
git merge release/v1.0.0
git tag -a v1.0.0 -m "Release version 1.0.0"
git branch -d release/v1.0.0
```

## Common release commands

| Command | Purpose |
|---|---|
| `git switch main` | Move to main branch |
| `git pull origin main` | Update main from remote |
| `git tag -a v1.0.0 -m "Message"` | Create release tag |
| `git push origin main` | Push main branch |
| `git push origin v1.0.0` | Push release tag |
| `git show v1.0.0` | Inspect release tag |
| `git switch -c release/v1.0.0` | Create release branch |
| `git branch -d release/v1.0.0` | Delete local release branch |

## Common mistakes

### Mistake 1: Tagging before final merge

Make sure all intended work is merged into `main` before tagging.

### Mistake 2: Forgetting to push the tag

After tagging locally:

```bash
git push origin v1.0.0
```

### Mistake 3: Creating unclear release notes

Release notes should explain what changed.

Avoid:

```txt
Updated stuff
```

Use:

```txt
Added Git branch documentation and conflict resolution guide.
```

### Mistake 4: Reusing release tag names

Avoid deleting and recreating published release tags.

Tags should be stable.

### Mistake 5: Not checking the working tree

Before release:

```bash
git status
```

Make sure there are no unexpected changes.

## Best practices

- Release from a stable branch like `main`.
- Use annotated tags for releases.
- Follow semantic versioning when possible.
- Write release notes.
- Check history before tagging.
- Push the tag intentionally.
- Avoid changing published release tags.
- Use release branches when final preparation needs separation.
- Use hotfix branches for urgent fixes after release.

## Professional recommendation

For a clean release:

```bash
git switch main
git pull origin main
git status
git log --oneline -n 5
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin main
git push origin v1.0.0
```

If working locally only, skip `git pull` and `git push` until you are ready to upload.

## Summary

A release workflow helps publish stable versions of a project.

Basic release:

```bash
git switch main
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin main
git push origin v1.0.0
```

Optional release branch:

```bash
git switch -c release/v1.0.0
```

Patch release:

```bash
git switch -c hotfix/v1.0.1
```

Golden rule:

```txt
Create release tags only from stable and reviewed commits.
```

## Recommended next topic

Continue with:

```txt
docs/09-advanced-git/cherry-pick.md
```