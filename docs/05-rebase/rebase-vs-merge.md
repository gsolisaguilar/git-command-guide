# Rebase vs Merge

`git merge` and `git rebase` are both used to integrate changes between branches.

However, they do it in different ways and produce different commit histories.

Understanding the difference helps you choose the right workflow.

## Main difference

```txt
Merge combines branches.
Rebase moves commits to a new base.
```

## What merge does

A merge integrates one branch into another.

Example:

```bash
git switch main
git merge feature/rebase-guide
```

This combines the changes from `feature/rebase-guide` into `main`.

If both branches have new commits, Git may create a merge commit.

## Merge example

Before merge:

```txt
A---B---C main
     \
      D---E feature
```

After merge:

```txt
A---B---C------M main
     \        /
      D---E feature
```

`M` is a merge commit.

## What rebase does

A rebase moves the commits from one branch and replays them on top of another branch.

Example:

```bash
git switch feature
git rebase main
```

Before rebase:

```txt
A---B---C main
     \
      D---E feature
```

After rebase:

```txt
A---B---C main
         \
          D'---E' feature
```

The commits `D` and `E` are recreated as `D'` and `E'`.

## Visual comparison

### Merge

```txt
A---B---C------M main
     \        /
      D---E feature
```

Merge preserves the branch structure.

### Rebase

```txt
A---B---C---D'---E' feature
```

Rebase creates a linear history.

## Merge history style

Merge keeps the real historical structure of the work.

It shows:

- Where a branch started.
- Where it ended.
- When it was integrated.
- Which commits belonged to that branch.

This is useful when you want to preserve context.

## Rebase history style

Rebase creates a cleaner, linear history.

It makes the project look like commits happened one after another.

This is useful when you want history to be easier to read.

## Merge advantages

Merge is useful because it:

- Does not rewrite commit history.
- Is safer for shared branches.
- Preserves the true branch structure.
- Is easier for beginners to understand.
- Works well in team workflows.
- Avoids force push in most cases.

## Merge disadvantages

Merge can:

- Create extra merge commits.
- Make history look more complex.
- Produce a non-linear commit graph.
- Become noisy if used too frequently.

## Rebase advantages

Rebase is useful because it:

- Creates a cleaner linear history.
- Avoids unnecessary merge commits.
- Makes commit history easier to read.
- Works well before merging a feature branch.
- Helps keep a feature branch updated with `main`.

## Rebase disadvantages

Rebase can:

- Rewrite commit history.
- Create problems if used on shared branches.
- Require force push after rebasing pushed branches.
- Be confusing for beginners.
- Require careful conflict resolution.

## Merge does not rewrite history

This is one of the safest things about merge.

When you merge, existing commits keep their original hashes.

Example:

```txt
D---E feature
```

After merge, `D` and `E` are still the same commits.

## Rebase rewrites history

When you rebase, Git creates new versions of your commits.

Example:

```txt
D---E
```

After rebase:

```txt
D'---E'
```

The changes may be the same, but the commit hashes are different.

## When to use merge

Use merge when:

- You want to preserve branch history.
- You are working on a shared branch.
- You want a safer integration method.
- Your team uses pull requests with merge commits.
- You are merging completed features into `main`.
- You want to avoid rewriting history.

Example:

```bash
git switch main
git merge feature/rebase-guide
```

## When to use rebase

Use rebase when:

- You want a linear history.
- You are working on your own local branch.
- You want to update your feature branch with the latest `main`.
- You want to clean up history before merging.
- Your team uses rebase-based workflows.

Example:

```bash
git switch feature/rebase-guide
git rebase main
```

## Common team workflow with merge

```bash
git switch main
git pull origin main
git switch -c feature/new-topic
# make changes
git add .
git commit -m "Add new topic"
git switch main
git merge feature/new-topic
```

This preserves merge history.

## Common team workflow with rebase

```bash
git switch main
git pull origin main
git switch -c feature/new-topic
# make changes
git add .
git commit -m "Add new topic"
git switch feature/new-topic
git rebase main
git switch main
git merge --ff-only feature/new-topic
```

This creates a linear history.

## Rebase before merge

A common professional workflow is to rebase a feature branch before merging it.

```bash
git switch feature/rebase-guide
git rebase main
git switch main
git merge --ff-only feature/rebase-guide
```

This keeps `main` linear.

## Merge main into feature branch

Instead of rebasing, you can update a feature branch by merging `main`.

```bash
git switch feature/rebase-guide
git merge main
```

This is safer because it does not rewrite history, but it may create merge commits.

## Rebase feature branch onto main

Alternative:

```bash
git switch feature/rebase-guide
git rebase main
```

This creates a cleaner history but rewrites the feature branch commits.

## Which one should beginners use?

Beginners should start with merge because it is safer and easier to understand.

Recommended beginner integration:

```bash
git switch main
git merge feature/branch-name
```

After understanding merge well, learn rebase.

## Which one should professionals use?

Professionals use both.

The choice depends on:

- Team rules.
- Repository history style.
- Whether the branch is shared.
- Whether the team wants linear history.
- Whether pull requests are used.
- Whether commits need cleanup.

## Decision table

| Situation | Recommended option |
|---|---|
| You are new to Git | Merge |
| You are working on a shared branch | Merge |
| You want to preserve branch history | Merge |
| You want a clean linear history | Rebase |
| You are updating your own local feature branch | Rebase |
| You are unsure | Merge |
| Your team requires rebase | Rebase |
| Your team requires merge commits | Merge |

## Merge command examples

```bash
git switch main
git merge feature/rebase-guide
```

Force a merge commit:

```bash
git merge --no-ff feature/rebase-guide
```

Fast-forward only:

```bash
git merge --ff-only feature/rebase-guide
```

## Rebase command examples

```bash
git switch feature/rebase-guide
git rebase main
```

Continue after conflicts:

```bash
git rebase --continue
```

Abort:

```bash
git rebase --abort
```

## Pull with merge vs pull with rebase

Default pull often behaves like:

```bash
git fetch
git merge
```

Pull with rebase:

```bash
git pull --rebase
```

This fetches changes and rebases your local commits on top of the remote branch.

## Common mistakes

### Mistake 1: Thinking merge and rebase do the same thing

They both integrate changes, but they create different histories.

### Mistake 2: Rebasing shared branches

Avoid rebasing branches other people are using.

### Mistake 3: Using merge when the team expects linear history

Some teams require rebase or squash before merge.

Follow the team workflow.

### Mistake 4: Using rebase without understanding conflict resolution

Before using rebase often, understand:

```bash
git rebase --continue
git rebase --abort
```

## Best practices

- Use merge when safety is more important than clean history.
- Use rebase when you want a clean linear history.
- Do not rebase shared branches without agreement.
- Follow the team’s Git workflow.
- Review history after merging or rebasing.
- Use `git status` before either operation.
- Use `git log --oneline --graph --decorate --all` to understand the result.

## Recommended workflow for this repository

Since this repository is a personal/professional documentation guide, a clean option is:

```bash
git switch feature/rebase-guide
git rebase main
git switch main
git merge --ff-only feature/rebase-guide
```

This keeps your history linear.

If you prefer to show each topic branch clearly, use:

```bash
git switch main
git merge --no-ff feature/rebase-guide
```

Both are valid.

Choose one style and keep it consistent.

## Summary

Merge and rebase both integrate changes.

Merge:

```txt
Combines branches and preserves history.
```

Rebase:

```txt
Replays commits and creates a linear history.
```

Basic merge:

```bash
git switch main
git merge feature/branch-name
```

Basic rebase:

```bash
git switch feature/branch-name
git rebase main
```

Golden rule:

```txt
Use merge when unsure. Use rebase when you understand the history impact.
```

## Recommended next topic

Continue with:

```txt
docs/05-rebase/interactive-rebase.md
```