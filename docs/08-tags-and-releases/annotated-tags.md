# Annotated Tags

Annotated tags are Git tags that include extra metadata.

They are recommended for official releases because they contain more information than lightweight tags.

## What is an annotated tag?

An annotated tag is a full Git object that stores:

- Tag name.
- Tagger name.
- Tagger email.
- Date.
- Message.
- Reference to a commit.

## Create an annotated tag

Basic syntax:

```bash
git tag -a tag-name -m "Tag message"
```

Example:

```bash
git tag -a v1.0.0 -m "Release version 1.0.0"
```

This creates an annotated tag named `v1.0.0`.

## Annotated tag vs lightweight tag

| Type | Command | Contains metadata | Recommended for releases |
|---|---|---|---|
| Lightweight tag | `git tag v1.0.0` | No | No |
| Annotated tag | `git tag -a v1.0.0 -m "Message"` | Yes | Yes |

## Why use annotated tags?

Annotated tags are useful because they:

- Store a release message.
- Include author and date information.
- Are better for official releases.
- Provide more context.
- Can be signed for extra verification.
- Are easier to inspect later.

## Show annotated tag details

```bash
git show v1.0.0
```

Example output may include:

```txt
tag v1.0.0
Tagger: Jessica Santos <jessica@example.com>
Date:   Tue Jun 16 12:00:00 2026 -0600

Release version 1.0.0
```

Then Git shows the commit associated with the tag.

## Create annotated tag on current commit

```bash
git tag -a v1.0.0 -m "Release version 1.0.0"
```

This tags the current `HEAD`.

## Create annotated tag on specific commit

First, check history:

```bash
git log --oneline
```

Example:

```txt
a1b2c3d Add release workflow documentation
e4f5g6h Add annotated tags documentation
i7j8k9l Add tags documentation
```

Create tag on a specific commit:

```bash
git tag -a v1.0.0 a1b2c3d -m "Release version 1.0.0"
```

## Use a detailed tag message

For important releases, use a meaningful message.

Example:

```bash
git tag -a v1.0.0 -m "Release version 1.0.0: initial Git guide documentation"
```

## Create annotated tag with editor

If you do not use `-m`, Git opens your editor:

```bash
git tag -a v1.0.0
```

Then you can write a longer tag message.

Example message:

```txt
Release version 1.0.0

Includes:
- Introduction to Git
- Basic commands
- Branching guide
- Remote repositories
- Merge and conflict documentation
```

## Push annotated tag

Creating a tag locally does not automatically upload it.

Push one tag:

```bash
git push origin v1.0.0
```

## Push all tags

```bash
git push origin --tags
```

Use this carefully because it pushes every local tag.

## Verify remote tag

After pushing, you can fetch tags:

```bash
git fetch --tags
```

Then list tags:

```bash
git tag
```

## Delete annotated tag locally

```bash
git tag -d v1.0.0
```

This deletes the local tag.

## Delete annotated tag remotely

```bash
git push origin --delete v1.0.0
```

This deletes the tag from the remote repository.

## Recreate a tag

If you tagged the wrong commit locally and have not pushed yet:

```bash
git tag -d v1.0.0
git tag -a v1.0.0 correct-commit-hash -m "Release version 1.0.0"
```

If the tag was already pushed, be careful. Other people may already have fetched it.

## Signed tags

Git also supports signed tags using GPG.

Example:

```bash
git tag -s v1.0.0 -m "Release version 1.0.0"
```

Signed tags verify the identity of the person who created the tag.

This is more advanced and requires GPG configuration.

## Verify a signed tag

```bash
git tag -v v1.0.0
```

This verifies the signature of a signed tag.

## Annotated tags in release workflows

A common release workflow is:

```bash
git switch main
git pull origin main
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin v1.0.0
```

Then, on GitHub, you can create a release based on that tag.

## Example for documentation project

For this repository, a tag could mark a completed documentation milestone.

Example:

```bash
git tag -a v1.0.0 -m "Release version 1.0.0: initial Git command guide"
```

Then push:

```bash
git push origin v1.0.0
```

## Suggested tag messages for this repository

```txt
Release version 1.0.0: initial Git guide from basics to workflows
Release version 1.1.0: add advanced Git commands
Release version 1.2.0: add professional workflow documentation
```

## Common annotated tag commands

| Command | Purpose |
|---|---|
| `git tag -a v1.0.0 -m "Message"` | Creates annotated tag |
| `git tag -a v1.0.0 commit -m "Message"` | Tags a specific commit |
| `git show v1.0.0` | Shows tag details |
| `git push origin v1.0.0` | Pushes one tag |
| `git push origin --tags` | Pushes all tags |
| `git tag -d v1.0.0` | Deletes local tag |
| `git push origin --delete v1.0.0` | Deletes remote tag |
| `git tag -s v1.0.0 -m "Message"` | Creates signed tag |
| `git tag -v v1.0.0` | Verifies signed tag |

## Common mistakes

### Mistake 1: Using lightweight tags for official releases

For professional releases, prefer:

```bash
git tag -a v1.0.0 -m "Release version 1.0.0"
```

instead of:

```bash
git tag v1.0.0
```

### Mistake 2: Forgetting to push the tag

After creating the tag:

```bash
git push origin v1.0.0
```

### Mistake 3: Tagging before final changes are merged

Make sure `main` contains the final release changes before tagging.

### Mistake 4: Reusing the same tag name incorrectly

Avoid deleting and recreating published tags unless absolutely necessary.

Tags are expected to be stable.

## Best practices

- Use annotated tags for releases.
- Use semantic version names like `v1.0.0`.
- Write meaningful tag messages.
- Create release tags from stable branches.
- Push tags intentionally.
- Avoid changing published tags.
- Use signed tags for higher security when needed.
- Document what each release includes.

## Professional recommendation

For official releases:

```bash
git switch main
git status
git log --oneline -n 5
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin v1.0.0
```

This creates a clear and professional release marker.

## Summary

Annotated tags are recommended for official releases.

Create annotated tag:

```bash
git tag -a v1.0.0 -m "Release version 1.0.0"
```

Push tag:

```bash
git push origin v1.0.0
```

Inspect tag:

```bash
git show v1.0.0
```

Golden rule:

```txt
Use annotated tags for meaningful, stable release points.
```

## Recommended next topic

Continue with:

```txt
docs/08-tags-and-releases/release-workflow.md
```