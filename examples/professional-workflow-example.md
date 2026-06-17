# Professional Workflow Example

This example shows a professional Git workflow using branches, commits, review, merge, tags, and cleanup.

It is designed for a repository like:

```txt
git-commands-guide
```

## Scenario

You are adding a new documentation section:

```txt
docs/10-professional-workflows/
```

You want to work professionally by creating a branch, committing changes, merging into `main`, tagging a release, and deleting completed branches.

## Goal

The goal is to practice a complete professional workflow:

```txt
Start from main → Create branch → Commit changes → Review history → Merge → Delete branch → Tag release
```

## Step 1: Start from main

```bash
git switch main
```

If using GitHub:

```bash
git pull origin main
```

If working locally only, make sure your local `main` already contains the latest merged work.

## Step 2: Create a feature branch

```bash
git switch -c feature/professional-workflows
```

## Step 3: Confirm current branch

```bash
git branch
```

Example output:

```txt
  main
* feature/professional-workflows
```

## Step 4: Create or edit files

Example files:

```txt
docs/10-professional-workflows/git-flow.md
docs/10-professional-workflows/github-flow.md
docs/10-professional-workflows/trunk-based-development.md
docs/10-professional-workflows/pull-request-workflow.md
docs/10-professional-workflows/code-review-workflow.md
```

## Step 5: Check status

```bash
git status
```

Example output:

```txt
On branch feature/professional-workflows

Untracked files:
  docs/10-professional-workflows/git-flow.md
  docs/10-professional-workflows/github-flow.md
  docs/10-professional-workflows/trunk-based-development.md
  docs/10-professional-workflows/pull-request-workflow.md
  docs/10-professional-workflows/code-review-workflow.md
```

## Step 6: Review changes

If files were modified:

```bash
git diff
```

For new files, you can still inspect them manually before staging.

## Step 7: Stage changes

```bash
git add docs/10-professional-workflows/
```

## Step 8: Review staged changes

```bash
git diff --staged
```

## Step 9: Commit changes

```bash
git commit -m "Add professional Git workflows documentation"
```

## Step 10: Review history

```bash
git log --oneline --graph --decorate --all
```

Example output:

```txt
* a1b2c3d (HEAD -> feature/professional-workflows) Add professional Git workflows documentation
* e4f5g6h (main) Add advanced Git commands documentation
```

## Step 11: Merge into main

Switch to `main`:

```bash
git switch main
```

Merge:

```bash
git merge feature/professional-workflows
```

## Alternative: no fast-forward merge

If you want to preserve the branch context:

```bash
git merge --no-ff feature/professional-workflows
```

## Alternative: squash merge

If you want one clean commit on `main`:

```bash
git merge --squash feature/professional-workflows
git commit -m "Add professional Git workflows documentation"
```

## Alternative: rebase then fast-forward

If you want linear history:

```bash
git switch feature/professional-workflows
git rebase main
git switch main
git merge --ff-only feature/professional-workflows
```

## Step 12: Verify main

```bash
git status
git log --oneline --graph --decorate --all
```

Expected status:

```txt
On branch main
nothing to commit, working tree clean
```

## Step 13: Delete merged branch

```bash
git branch -d feature/professional-workflows
```

## Step 14: Repeat for next topic

Example next branches:

```txt
feature/cheatsheets
feature/workflows
feature/examples
feature/glossary
feature/final-docs-polish
```

## Step 15: Create a release tag

After completing a stable milestone, create an annotated tag.

```bash
git tag -a v1.0.0 -m "Release version 1.0.0: Git Commands Guide"
```

Verify tag:

```bash
git show v1.0.0
```

## Step 16: Push to GitHub

If you are ready to upload everything to GitHub:

```bash
git push origin main
git push origin v1.0.0
```

If you still have local branches you want to push:

```bash
git push -u origin branch-name
```

## Full professional local workflow

```bash
git switch main
git switch -c feature/professional-workflows

# create or edit files

git status
git add docs/10-professional-workflows/
git diff --staged
git commit -m "Add professional Git workflows documentation"

git switch main
git merge feature/professional-workflows
git status
git log --oneline --graph --decorate --all
git branch -d feature/professional-workflows
```

## Full professional workflow with GitHub

```bash
git switch main
git pull origin main
git switch -c feature/professional-workflows

# create or edit files

git add docs/10-professional-workflows/
git commit -m "Add professional Git workflows documentation"
git push -u origin feature/professional-workflows
```

Then open a pull request.

After it is merged:

```bash
git switch main
git pull origin main
git branch -d feature/professional-workflows
git push origin --delete feature/professional-workflows
```

## Professional pull request description example

```md
## Summary

- Added Git Flow documentation.
- Added GitHub Flow documentation.
- Added trunk-based development documentation.
- Added pull request workflow documentation.
- Added code review workflow documentation.

## Testing

- Reviewed Markdown formatting.
- Checked command examples.
- Verified internal navigation references.

## Notes

This pull request only adds documentation.
```

## Professional checklist before merge

```txt
Is the branch focused on one topic?
Are all files related to the same change?
Are commit messages clear?
Did I check git status?
Did I review the staged changes?
Is main the branch receiving the merge?
Is the working tree clean after merge?
```

## Professional cleanup checklist

After merge:

```txt
Did I delete the local branch?
Did I delete the remote branch if it exists?
Did I update main?
Did I tag a release if this is a milestone?
Did I push the tag if using GitHub?
```

## Suggested branch sequence for this repository

```txt
feature/basic-git-commands
feature/branches
feature/remote-repositories
feature/merges-and-conflicts
feature/rebase-guide
feature/undoing-changes
feature/stash-guide
feature/tags-and-releases
feature/advanced-git
feature/professional-workflows
feature/cheatsheets
feature/workflows
feature/examples
feature/glossary
feature/final-docs-polish
```

## Common mistakes

### Mistake 1: Working directly on main

Use a branch for each topic:

```bash
git switch -c feature/topic-name
```

### Mistake 2: Forgetting to review staged changes

Before committing:

```bash
git diff --staged
```

### Mistake 3: Merging into the wrong branch

Always switch to the target branch first:

```bash
git switch main
git merge feature/topic-name
```

### Mistake 4: Not deleting completed branches

After merge:

```bash
git branch -d feature/topic-name
```

### Mistake 5: Tagging before the project is stable

Only tag stable milestones.

## Best practices

- Use one branch per topic.
- Use clear branch names.
- Keep commits focused.
- Review changes before committing.
- Merge into `main` only when ready.
- Delete branches after merge.
- Use tags for stable versions.
- Use pull requests when collaborating.
- Keep `main` clean and stable.

## Summary

Professional Git workflow:

```txt
Branch → Commit → Review → Merge → Cleanup → Release
```

Core commands:

```bash
git switch main
git switch -c feature/topic-name
git add .
git commit -m "Add topic documentation"
git switch main
git merge feature/topic-name
git branch -d feature/topic-name
git tag -a v1.0.0 -m "Release version 1.0.0"
```

Golden rule:

```txt
Keep main stable and make every branch represent one clear task.
```