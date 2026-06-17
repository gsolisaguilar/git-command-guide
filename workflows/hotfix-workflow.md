# Hotfix Workflow

A hotfix workflow is used to fix urgent problems in a stable branch, usually `main`.

Hotfixes are commonly used when a production issue must be corrected quickly.

## Goal

The goal of a hotfix workflow is to apply a small, urgent fix safely and quickly.

## When to use this workflow

Use this workflow when:

- There is a critical bug.
- Production is affected.
- A release has an urgent issue.
- The fix must be made from a stable branch.
- The change is small and focused.
- The fix should be tagged as a patch version.

## Main idea

```txt
Create hotfix branch from main.
Fix the issue.
Merge back into main.
Tag a patch release.
Merge fix into development branch if needed.
```

## Recommended branch name

```txt
hotfix/short-description
```

Examples:

```txt
hotfix/fix-login-error
hotfix/fix-readme-link
hotfix/fix-release-notes
hotfix/v1.0.1
```

## Step 1: Start from main

```bash
git switch main
```

If using GitHub:

```bash
git pull origin main
```

## Step 2: Create a hotfix branch

```bash
git switch -c hotfix/fix-issue
```

Example:

```bash
git switch -c hotfix/fix-readme-link
```

## Step 3: Make the fix

Edit only what is necessary for the hotfix.

Check status:

```bash
git status
```

## Step 4: Commit the fix

```bash
git add .
git commit -m "Fix README link"
```

## Step 5: Merge hotfix into main

```bash
git switch main
git merge hotfix/fix-readme-link
```

## Step 6: Tag patch release

If the hotfix represents a release, create an annotated tag.

Example:

```bash
git tag -a v1.0.1 -m "Release version 1.0.1"
```

## Step 7: Push changes

If using GitHub:

```bash
git push origin main
git push origin v1.0.1
```

## Step 8: Delete hotfix branch

Local:

```bash
git branch -d hotfix/fix-readme-link
```

Remote, if pushed:

```bash
git push origin --delete hotfix/fix-readme-link
```

## Full local hotfix workflow

```bash
git switch main
git switch -c hotfix/fix-readme-link

# fix issue

git status
git add .
git commit -m "Fix README link"

git switch main
git merge hotfix/fix-readme-link
git tag -a v1.0.1 -m "Release version 1.0.1"
git branch -d hotfix/fix-readme-link
```

## Full GitHub hotfix workflow

```bash
git switch main
git pull origin main
git switch -c hotfix/fix-readme-link

# fix issue

git add .
git commit -m "Fix README link"
git push -u origin hotfix/fix-readme-link
```

Open a pull request into `main`.

After merge:

```bash
git switch main
git pull origin main
git tag -a v1.0.1 -m "Release version 1.0.1"
git push origin v1.0.1
git branch -d hotfix/fix-readme-link
```

## Hotfix with develop branch

In Git Flow, after merging the hotfix into `main`, also merge it into `develop`.

```bash
git switch develop
git merge hotfix/fix-readme-link
```

This prevents the bug from returning in future releases.

## Hotfix with release branch

If you maintain release branches:

```bash
git switch release/v1.0.0
git cherry-pick commit-hash
```

This applies the hotfix to a specific release branch.

## Patch versioning

Hotfixes often increase the patch version.

Example:

```txt
v1.0.0 → v1.0.1
v1.0.1 → v1.0.2
v2.3.4 → v2.3.5
```

## Emergency hotfix checklist

Before merging the hotfix:

```txt
Is the branch created from main?
Is the fix small and focused?
Did I test the fix?
Did I review git diff?
Is the commit message clear?
Is the version tag correct?
Does the fix need to be merged into develop too?
```

## Commands to review before merge

```bash
git status
git diff
git log --oneline --graph --decorate --all
```

## Common mistakes

### Mistake 1: Starting hotfix from the wrong branch

Hotfixes usually start from `main`.

```bash
git switch main
git switch -c hotfix/fix-issue
```

### Mistake 2: Making unrelated changes

A hotfix should be small and focused.

Do not include unrelated refactors or new features.

### Mistake 3: Forgetting the tag

If the hotfix is a release, tag it:

```bash
git tag -a v1.0.1 -m "Release version 1.0.1"
```

### Mistake 4: Forgetting to merge into develop

In Git Flow, merge the hotfix into both:

```txt
main
develop
```

### Mistake 5: Deleting branch before confirming merge

Use:

```bash
git branch --merged
```

Then delete:

```bash
git branch -d hotfix/fix-issue
```

## Best practices

- Keep hotfixes small.
- Start from stable branch.
- Use clear branch names.
- Test the fix.
- Tag patch releases.
- Merge hotfixes back into active development branches if needed.
- Delete hotfix branches after merge.
- Document the issue and fix.

## Summary

Hotfix workflow:

```txt
main → hotfix branch → fix → merge into main → tag patch release → delete branch
```

Basic commands:

```bash
git switch main
git switch -c hotfix/fix-issue
git add .
git commit -m "Fix issue"
git switch main
git merge hotfix/fix-issue
git tag -a v1.0.1 -m "Release version 1.0.1"
git branch -d hotfix/fix-issue
```

Golden rule:

```txt
A hotfix should be urgent, small, focused, and based on a stable branch.
```