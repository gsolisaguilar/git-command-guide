# Tags

Tags are references used to mark specific points in Git history.

They are commonly used to identify versions, releases, milestones, or important commits.

## What is a tag?

A tag is a name assigned to a specific commit.

Unlike branches, tags usually do not move.

A branch changes as new commits are added.

A tag stays pointing to the same commit.

## Why tags are useful

Tags are useful because they allow you to:

- Mark release versions.
- Identify stable points in history.
- Reference important commits.
- Create GitHub releases.
- Track production deployments.
- Roll back to known versions.
- Communicate version numbers clearly.

## Common tag examples

```txt
v1.0.0
v1.1.0
v2.0.0
v2.0.1
release-2026-06
stable
```

## Tags vs branches

| Concept | Moves over time | Common use |
|---|---|---|
| Branch | Yes | Active development |
| Tag | No | Marking a specific version |

Example:

```txt
main moves as new commits are added.
v1.0.0 always points to the same release commit.
```

## Types of tags

Git has two main types of tags:

```txt
Lightweight tags
Annotated tags
```

## Lightweight tag

A lightweight tag is a simple pointer to a commit.

Create a lightweight tag:

```bash
git tag v1.0.0
```

This creates a tag named `v1.0.0` on the current commit.

## Annotated tag

An annotated tag includes extra information, such as:

- Tagger name.
- Email.
- Date.
- Message.

Create an annotated tag:

```bash
git tag -a v1.0.0 -m "Release version 1.0.0"
```

Annotated tags are recommended for professional releases.

## List tags

To list all tags:

```bash
git tag
```

Example output:

```txt
v1.0.0
v1.1.0
v2.0.0
```

## List tags matching a pattern

```bash
git tag -l "v1.*"
```

Example output:

```txt
v1.0.0
v1.1.0
v1.2.0
```

## Show tag details

```bash
git show v1.0.0
```

For an annotated tag, this shows:

- Tag name.
- Tag message.
- Tagger.
- Commit information.
- Changes in the commit.

## Create a tag on the latest commit

```bash
git tag v1.0.0
```

This creates a tag on `HEAD`, which usually means the latest commit on the current branch.

## Create a tag on a specific commit

First, check commit history:

```bash
git log --oneline
```

Example:

```txt
a1b2c3d Add release workflow
e4f5g6h Add annotated tags guide
i7j8k9l Add tags guide
```

Create a tag on a specific commit:

```bash
git tag v1.0.0 a1b2c3d
```

## Push a tag to remote

By default, `git push` does not always push tags automatically.

Push one tag:

```bash
git push origin v1.0.0
```

## Push all tags

```bash
git push origin --tags
```

Use this carefully because it pushes all local tags.

## Delete a local tag

```bash
git tag -d tag-name
```

Example:

```bash
git tag -d v1.0.0
```

## Delete a remote tag

```bash
git push origin --delete tag-name
```

Example:

```bash
git push origin --delete v1.0.0
```

Another syntax:

```bash
git push origin :refs/tags/v1.0.0
```

## Checkout a tag

You can inspect the project at a tag:

```bash
git checkout v1.0.0
```

This puts you in a detached HEAD state.

This is useful for inspection, but you are not on a normal branch.

## Create a branch from a tag

If you want to work from a tagged version:

```bash
git switch -c branch-name tag-name
```

Example:

```bash
git switch -c hotfix/v1.0.1 v1.0.0
```

This creates a new branch starting from the tagged commit.

## Tag naming conventions

Common tag naming uses semantic versioning:

```txt
vMAJOR.MINOR.PATCH
```

Example:

```txt
v1.0.0
```

Meaning:

```txt
MAJOR = breaking changes
MINOR = new compatible features
PATCH = bug fixes
```

## Semantic versioning examples

| Version | Meaning |
|---|---|
| `v1.0.0` | First stable release |
| `v1.1.0` | New feature added |
| `v1.1.1` | Bug fix |
| `v2.0.0` | Breaking change |

## Tags in GitHub

GitHub can use tags to create releases.

A GitHub release usually points to a Git tag and may include:

- Release title.
- Release notes.
- Source code archive.
- Assets.
- Version information.

## Common tag commands

| Command | Purpose |
|---|---|
| `git tag` | Lists tags |
| `git tag v1.0.0` | Creates a lightweight tag |
| `git tag -a v1.0.0 -m "Message"` | Creates an annotated tag |
| `git tag v1.0.0 commit-hash` | Creates a tag on a specific commit |
| `git show v1.0.0` | Shows tag details |
| `git push origin v1.0.0` | Pushes one tag |
| `git push origin --tags` | Pushes all tags |
| `git tag -d v1.0.0` | Deletes a local tag |
| `git push origin --delete v1.0.0` | Deletes a remote tag |

## Common mistakes

### Mistake 1: Thinking tags move like branches

Tags usually stay fixed.

If you need a moving reference, use a branch.

### Mistake 2: Forgetting to push tags

Creating a tag locally does not automatically upload it.

Push it with:

```bash
git push origin v1.0.0
```

### Mistake 3: Tagging the wrong commit

Always check history first:

```bash
git log --oneline
```

Then create the tag.

### Mistake 4: Using unclear tag names

Avoid:

```txt
final
latest
release
version
```

Prefer:

```txt
v1.0.0
v1.1.0
v2.0.0
```

## Best practices

- Use tags for releases.
- Prefer annotated tags for official releases.
- Use clear version numbers.
- Follow semantic versioning when possible.
- Check the commit before tagging.
- Push tags intentionally.
- Avoid deleting or rewriting published tags unless necessary.
- Document release changes.

## Professional recommendation

For official versions, prefer annotated tags:

```bash
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin v1.0.0
```

For temporary local markers, lightweight tags may be enough:

```bash
git tag test-point
```

## Summary

Tags mark specific commits in Git history.

List tags:

```bash
git tag
```

Create lightweight tag:

```bash
git tag v1.0.0
```

Create annotated tag:

```bash
git tag -a v1.0.0 -m "Release version 1.0.0"
```

Push tag:

```bash
git push origin v1.0.0
```

Golden rule:

```txt
Use tags to mark important stable points in project history.
```

## Recommended next topic

Continue with:

```txt
docs/08-tags-and-releases/annotated-tags.md
```