# Release Workflow

A release workflow is used to prepare and publish a stable version of a project.

In Git, releases are usually managed with stable branches, release branches, tags, and release notes.

## Goal

The goal of this workflow is to mark a stable point in the project history and publish it as a version.

## When to use this workflow

Use this workflow when:

- A project milestone is complete.
- A stable version is ready.
- Documentation is ready to publish.
- A software version is ready for deployment.
- You want to create a Git tag.
- You want to create a GitHub release.
- You need release notes.

## Main idea

```txt
Prepare stable main → Create release tag → Push tag → Publish release notes
```

## Version format

A common format is semantic versioning:

```txt
vMAJOR.MINOR.PATCH
```

Example:

```txt
v1.0.0
```

## Semantic versioning

| Version part | Meaning | Example |
|---|---|---|
| MAJOR | Breaking changes | `v2.0.0` |
| MINOR | New compatible features | `v1.1.0` |
| PATCH | Bug fixes | `v1.0.1` |

## Example versions

```txt
v1.0.0 = first stable release
v1.1.0 = new section added
v1.1.1 = typo or link fix
v2.0.0 = major restructuring
```

## Step 1: Switch to main

```bash
git switch main
```

If using GitHub:

```bash
git pull origin main
```

## Step 2: Check repository status

```bash
git status
```

Recommended output:

```txt
nothing to commit, working tree clean
```

## Step 3: Review recent history

```bash
git log --oneline --graph --decorate --all
```

You can also check the last few commits:

```bash
git log --oneline -n 5
```

## Step 4: Create an annotated tag

```bash
git tag -a v1.0.0 -m "Release version 1.0.0"
```

For this repository, a more descriptive message could be:

```bash
git tag -a v1.0.0 -m "Release version 1.0.0: Git commands guide"
```

## Step 5: Verify the tag

```bash
git show v1.0.0
```

This shows tag details and the commit it points to.

## Step 6: Push main and tag

If using GitHub:

```bash
git push origin main
git push origin v1.0.0
```

If you have not pushed to GitHub yet, you can create the tag locally and push later.

## Basic local release workflow

```bash
git switch main
git status
git log --oneline -n 5
git tag -a v1.0.0 -m "Release version 1.0.0"
git show v1.0.0
```

## Basic GitHub release workflow

```bash
git switch main
git pull origin main
git status
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin main
git push origin v1.0.0
```

## Release branch workflow

Some teams use release branches for final preparation.

Create a release branch:

```bash
git switch main
git switch -c release/v1.0.0
```

Make final updates:

```bash
git add .
git commit -m "Prepare release v1.0.0"
```

Merge back into main:

```bash
git switch main
git merge release/v1.0.0
```

Tag release:

```bash
git tag -a v1.0.0 -m "Release version 1.0.0"
```

Delete release branch:

```bash
git branch -d release/v1.0.0
```

## Full release branch workflow

```bash
git switch main
git switch -c release/v1.0.0

# final updates

git add .
git commit -m "Prepare release v1.0.0"

git switch main
git merge release/v1.0.0
git tag -a v1.0.0 -m "Release version 1.0.0"
git branch -d release/v1.0.0
```

## GitHub release notes

After pushing a tag to GitHub, you can create a GitHub release.

Release notes usually include:

```txt
Added
Changed
Fixed
Removed
Known issues
```

## Example release notes

```md
# Release v1.0.0

## Added

- Git introduction documentation.
- Basic Git commands.
- Branch workflow guide.
- Remote repository documentation.
- Merge and conflict documentation.
- Rebase documentation.
- Undoing changes documentation.
- Stash guide.
- Tags and releases guide.
- Advanced Git commands.
- Professional workflows.
- Cheatsheets.

## Notes

This is the first stable version of the Git Commands Guide.
```

## Changelog file

A project may include:

```txt
CHANGELOG.md
```

Example:

```md
# Changelog

## [v1.0.0] - 2026-06-16

### Added

- Initial Git Commands Guide documentation.
- Beginner to advanced Git topics.
- Professional Git workflows.
```

## Release checklist

Before creating a release, verify:

```txt
Is main stable?
Is the working tree clean?
Are all intended branches merged?
Are documentation links correct?
Are release notes ready?
Is the version number correct?
Did I create an annotated tag?
Did I verify the tag?
Did I push the tag if using GitHub?
```

## Commands checklist

```bash
git switch main
git status
git log --oneline --graph --decorate --all
git tag -a v1.0.0 -m "Release version 1.0.0"
git show v1.0.0
```

## Patch release workflow

Use a patch release for small fixes.

Example:

```txt
v1.0.0 → v1.0.1
```

Commands:

```bash
git switch main
git switch -c hotfix/fix-release-docs

# fix issue

git add .
git commit -m "Fix release documentation"

git switch main
git merge hotfix/fix-release-docs
git tag -a v1.0.1 -m "Release version 1.0.1"
git branch -d hotfix/fix-release-docs
```

## Minor release workflow

Use a minor release when adding new compatible content.

Example:

```txt
v1.0.0 → v1.1.0
```

```bash
git switch main
git tag -a v1.1.0 -m "Release version 1.1.0"
```

## Major release workflow

Use a major release for large restructuring or breaking changes.

Example:

```txt
v1.0.0 → v2.0.0
```

```bash
git switch main
git tag -a v2.0.0 -m "Release version 2.0.0"
```

## Common mistakes

### Mistake 1: Tagging before final changes are merged

Make sure `main` has the final release content.

### Mistake 2: Forgetting to push the tag

Creating a tag locally does not upload it.

Push it with:

```bash
git push origin v1.0.0
```

### Mistake 3: Using lightweight tags for official releases

Prefer annotated tags:

```bash
git tag -a v1.0.0 -m "Release version 1.0.0"
```

### Mistake 4: Reusing a published tag

Avoid deleting and recreating tags that other people may have already fetched.

### Mistake 5: Not writing release notes

Release notes make the version understandable for users and collaborators.

## Best practices

- Release from `main`.
- Keep `main` stable.
- Use annotated tags.
- Follow semantic versioning.
- Write release notes.
- Verify the tag before pushing.
- Avoid changing published tags.
- Use hotfix branches for urgent patch releases.
- Keep a changelog for important projects.

## Summary

Release workflow:

```txt
Prepare main → Check status → Create annotated tag → Push tag → Publish release notes
```

Basic commands:

```bash
git switch main
git status
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin main
git push origin v1.0.0
```

Golden rule:

```txt
Create release tags only from stable, reviewed commits.
```