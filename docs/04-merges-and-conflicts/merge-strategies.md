# Merge Strategies

Git provides different ways to merge branches depending on the project workflow and history style.

Understanding merge strategies helps you decide how to integrate work safely and professionally.

## What is a merge strategy?

A merge strategy is the method Git uses to combine changes from branches.

In daily work, you will usually use simple merges, but professional workflows may require specific options such as:

```bash
git merge --no-ff
git merge --ff-only
git merge --squash
```

## Default merge

The default merge command is:

```bash
git merge branch-name
```

Example:

```bash
git switch main
git merge feature/remote-repositories
```

Git decides whether it can do a fast-forward merge or whether it needs to create a merge commit.

## Fast-forward merge

A fast-forward merge happens when the current branch has not changed since the feature branch was created.

Before merge:

```txt
A---B main
     \
      C---D feature
```

After merge:

```txt
A---B---C---D main
```

No merge commit is created.

Command:

```bash
git merge feature
```

## Advantages of fast-forward merge

- Keeps history linear.
- Does not create extra merge commits.
- Simple and clean for small changes.
- Easy to read with `git log --oneline`.

## Disadvantages of fast-forward merge

- Does not clearly show that work happened in a separate branch.
- Branch context may be less visible in history.
- Not always ideal for team workflows where feature boundaries matter.

## Force fast-forward only

Use:

```bash
git merge --ff-only branch-name
```

Example:

```bash
git merge --ff-only feature/remote-repositories
```

This tells Git:

```txt
Merge only if a fast-forward is possible.
```

If fast-forward is not possible, Git stops.

## When to use --ff-only

Use `--ff-only` when:

- You want to avoid merge commits.
- You want a linear history.
- You want Git to stop if branches diverged.
- Your team prefers rebase before merging.

Example workflow:

```bash
git switch main
git merge --ff-only feature/remote-repositories
```

## No fast-forward merge

Use:

```bash
git merge --no-ff branch-name
```

Example:

```bash
git merge --no-ff feature/remote-repositories
```

This forces Git to create a merge commit, even if a fast-forward merge is possible.

## Why use --no-ff?

`--no-ff` preserves the fact that the work was done in a separate branch.

Before merge:

```txt
A---B main
     \
      C---D feature
```

After `--no-ff` merge:

```txt
A---B-------M main
     \     /
      C---D feature
```

`M` is the merge commit.

## Advantages of --no-ff

- Preserves branch history.
- Shows where a feature started and ended.
- Useful for larger features.
- Useful for pull request workflows.
- Makes it easier to revert an entire feature later.

## Disadvantages of --no-ff

- Creates extra merge commits.
- History can look more complex.
- May be unnecessary for small changes.

## Squash merge

A squash merge combines all commits from a branch into one commit.

Command:

```bash
git merge --squash branch-name
```

Example:

```bash
git switch main
git merge --squash feature/remote-repositories
git commit -m "Add remote repositories documentation"
```

Important:

```txt
git merge --squash does not create a normal merge commit.
```

It stages the combined changes, and you create a new commit manually.

## When to use squash merge

Use squash merge when:

- A feature branch has many small commits.
- You want a clean main history.
- You want one commit per feature.
- You do not need to preserve every commit from the feature branch.

## Squash merge example

Feature branch history:

```txt
C Add remotes file
D Fix typo
E Update examples
F Fix formatting
```

After squash merge into `main`:

```txt
M Add remote repositories documentation
```

All feature commits become one commit on `main`.

## Advantages of squash merge

- Keeps main history clean.
- Combines messy commits into one clear commit.
- Useful for documentation branches.
- Useful for pull request workflows.

## Disadvantages of squash merge

- Original individual commits are not preserved on main.
- It is not a true merge commit.
- Branch relationship may be less visible.
- Repeated squash merges from the same branch can be confusing.

## Recursive merge

The recursive merge strategy is commonly used internally by Git when merging two branches.

In modern Git, Git may use newer internal strategies, but for normal users, this is usually automatic.

You usually do not need to specify it manually.

Typical command:

```bash
git merge branch-name
```

## Ours strategy

The `ours` strategy keeps the current branch content and records the merge.

Command:

```bash
git merge -s ours branch-name
```

Example:

```bash
git merge -s ours feature/old-experiment
```

This says:

```txt
Record the merge, but keep the current branch content.
```

This is an advanced strategy and should be used carefully.

## Ours option during conflicts

This is different from the `ours` strategy.

During a conflict, you may use:

```bash
git checkout --ours file-name
```

That means:

```txt
Keep the current branch version of this file.
```

Do not confuse:

```bash
git merge -s ours branch-name
```

with:

```bash
git checkout --ours file-name
```

They are related in wording but used for different purposes.

## Theirs during conflicts

During a conflict, you can keep the incoming branch version:

```bash
git checkout --theirs file-name
```

Example:

```bash
git checkout --theirs README.md
git add README.md
```

This is not the same as a full merge strategy for normal daily use.

## Choosing a merge strategy

| Strategy | Command | Best for |
|---|---|---|
| Default merge | `git merge branch-name` | General use |
| Fast-forward only | `git merge --ff-only branch-name` | Linear history |
| No fast-forward | `git merge --no-ff branch-name` | Preserving feature branch history |
| Squash merge | `git merge --squash branch-name` | One clean commit per feature |
| Ours strategy | `git merge -s ours branch-name` | Advanced cases |

## Recommended strategy for beginners

For beginners, start with:

```bash
git merge branch-name
```

This lets Git choose the appropriate behavior.

## Recommended strategy for this repository

For your Git guide repository, a clean workflow could be:

```bash
git switch main
git merge --no-ff feature/remote-repositories
```

This keeps a visible record that each topic was developed in its own branch.

Another good option is squash merge:

```bash
git switch main
git merge --squash feature/remote-repositories
git commit -m "Add remote repositories documentation"
```

This keeps `main` clean with one commit per topic.

## Merge strategy comparison for this repository

| Strategy | Result |
|---|---|
| Normal merge | Simple and easy |
| `--no-ff` merge | Keeps branch history visible |
| Squash merge | Keeps one clean commit per documentation topic |
| Rebase then fast-forward | Keeps linear history but requires more Git knowledge |

## If you want one commit per topic

Use squash merge:

```bash
git switch main
git merge --squash feature/remote-repositories
git commit -m "Add remote repositories documentation"
```

Then delete the branch if no longer needed:

```bash
git branch -d feature/remote-repositories
```

## If you want visible branch merges

Use no fast-forward:

```bash
git switch main
git merge --no-ff feature/remote-repositories
```

Then delete the branch:

```bash
git branch -d feature/remote-repositories
```

## If you want a linear history

You can rebase the feature branch onto main and then fast-forward merge:

```bash
git switch feature/remote-repositories
git rebase main
git switch main
git merge --ff-only feature/remote-repositories
```

This keeps history linear.

Use this workflow only when you understand rebase.

## Common mistakes

### Mistake 1: Using squash merge without understanding

Squash merge creates a new commit but does not preserve the original branch commits on `main`.

This is fine if that is what you want.

### Mistake 2: Using --no-ff for every tiny change

`--no-ff` can make history noisy if used for very small changes.

### Mistake 3: Using advanced strategies without a reason

Avoid this unless you know why you need it:

```bash
git merge -s ours branch-name
```

### Mistake 4: Confusing merge strategy with conflict resolution

Merge strategies decide how branches are combined.

Conflict resolution decides how specific file conflicts are solved.

## Best practices

- Choose a merge strategy that matches your team workflow.
- Use normal merge while learning.
- Use squash merge for clean topic-based histories.
- Use `--no-ff` when you want to preserve branch context.
- Use `--ff-only` when you want linear history.
- Avoid forceful or advanced strategies unless necessary.
- Always check history after merging.

## Useful commands

| Command | Purpose |
|---|---|
| `git merge branch-name` | Default merge |
| `git merge --ff-only branch-name` | Fast-forward only |
| `git merge --no-ff branch-name` | Forces a merge commit |
| `git merge --squash branch-name` | Combines branch changes into one commit |
| `git merge -s ours branch-name` | Keeps current branch content while recording merge |
| `git log --oneline --graph --decorate --all` | Reviews merge history |

## Professional recommendation

For a documentation repository like this one, two good options are:

Option 1: Preserve branch history.

```bash
git switch main
git merge --no-ff feature/remote-repositories
```

Option 2: Keep one clean commit per topic.

```bash
git switch main
git merge --squash feature/remote-repositories
git commit -m "Add remote repositories documentation"
```

Both are valid.

Choose one style and use it consistently.

## Summary

Merge strategies control how Git combines branches.

Common options:

```bash
git merge branch-name
git merge --ff-only branch-name
git merge --no-ff branch-name
git merge --squash branch-name
```

For beginners, normal merge is enough.

For professional workflows, choose a consistent strategy based on how clean or detailed you want the project history to be.

## Recommended next topic

Continue with:

```txt
docs/05-rebase/rebase-basics.md
```