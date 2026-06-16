# Trunk-Based Development

Trunk-based development is a Git workflow where developers integrate small changes frequently into a single main branch.

The main branch is often called the trunk.

## What is trunk-based development?

Trunk-based development focuses on keeping one main integration branch stable and updated.

The trunk is usually:

```txt
main
```

or sometimes:

```txt
trunk
```

Developers make small changes and integrate them frequently.

## Main idea

```txt
Everyone integrates small changes into main frequently.
```

Branches, if used, are short-lived.

## Trunk-based development diagram

```txt
main: A---B---C---D---E---F
          \     \
feature:   x     y
```

Feature branches exist briefly and are merged quickly.

## Why use trunk-based development?

Trunk-based development helps teams:

- Integrate changes frequently.
- Reduce long-lived branch conflicts.
- Support continuous integration.
- Support continuous delivery.
- Keep development moving quickly.
- Detect integration problems earlier.
- Avoid large painful merges.

## Core principles

Trunk-based development usually requires:

- Small changes.
- Frequent integration.
- Automated tests.
- Continuous integration.
- Code review.
- Feature flags for incomplete features.
- Stable main branch.
- Fast feedback.

## Short-lived branches

In trunk-based development, branches should live for a short time.

Examples:

```txt
feature/update-readme
fix/login-validation
docs/add-workflow-guide
```

A branch might exist for:

```txt
a few hours
one day
a couple of days
```

Long-lived branches are avoided.

## Direct commits to main

Some teams commit directly to `main`.

This requires strong discipline and automated tests.

Other teams use short-lived branches and pull requests.

Both can be part of trunk-based development, depending on team rules.

## Feature flags

Feature flags allow incomplete work to be merged without exposing it to users.

Example:

```txt
New checkout page is merged into main but disabled until ready.
```

This allows frequent integration without waiting for a large feature to be fully finished.

## Basic trunk-based workflow with branches

```bash
git switch main
git pull origin main
git switch -c feature/small-change
```

Make a small change:

```bash
git add .
git commit -m "Add small change"
```

Merge quickly:

```bash
git switch main
git pull origin main
git merge feature/small-change
```

Push:

```bash
git push origin main
```

Delete branch:

```bash
git branch -d feature/small-change
```

## Trunk-based workflow with pull request

```txt
1. Update main.
2. Create a short-lived branch.
3. Make a small change.
4. Push branch.
5. Open pull request.
6. Run automated checks.
7. Review quickly.
8. Merge into main.
9. Delete branch.
```

## Example with GitHub

```bash
git switch main
git pull origin main
git switch -c docs/add-trunk-workflow

# make changes

git add .
git commit -m "Add trunk-based development documentation"
git push -u origin docs/add-trunk-workflow
```

Then open a pull request and merge quickly after review.

## Trunk-based development vs Git Flow

| Workflow | Branch style |
|---|---|
| Git Flow | Multiple long-lived branches like `main` and `develop` |
| Trunk-based development | One main branch with frequent integration |

## Trunk-based development vs GitHub Flow

| Workflow | Similarity |
|---|---|
| GitHub Flow | Uses short-lived branches and pull requests |
| Trunk-based development | Also uses frequent integration into main |

GitHub Flow can be considered close to trunk-based development when branches are short-lived and `main` is always stable.

## Advantages

Trunk-based development is useful because it:

- Reduces merge conflicts.
- Encourages small changes.
- Supports CI/CD.
- Keeps main updated.
- Detects problems earlier.
- Avoids long-running feature branches.
- Helps teams release faster.

## Disadvantages

Trunk-based development can be difficult if:

- There are no automated tests.
- The team makes very large changes.
- Code review is slow.
- Main is not protected.
- Developers are not disciplined.
- Feature flags are not used.
- Incomplete work is merged without safeguards.

## When to use trunk-based development

Use it when:

- The team integrates frequently.
- Automated tests exist.
- The project uses CI/CD.
- Small changes are encouraged.
- Main can remain stable.
- The team wants fast delivery.

## When not to use trunk-based development

Avoid it when:

- The project has long release cycles.
- Automated testing is weak.
- Features require long isolation.
- The team is not ready for frequent integration.
- There is no process to protect `main`.

## Branch protection

Trunk-based development often requires branch protection rules.

Examples:

```txt
Require pull request reviews.
Require status checks to pass.
Require branch to be up to date.
Prevent force pushes.
Prevent deletion of main.
```

## CI/CD

Continuous Integration helps validate each change.

Common checks:

- Build.
- Unit tests.
- Integration tests.
- Linting.
- Security checks.
- Documentation checks.

## Small commits

Trunk-based development works best with small commits.

Good examples:

```txt
Add README navigation
Fix typo in Git workflow guide
Add trunk-based development section
```

Bad example:

```txt
Add entire application rewrite
```

## Common commands

| Command | Purpose |
|---|---|
| `git switch main` | Move to main branch |
| `git pull origin main` | Update main |
| `git switch -c feature/name` | Create short-lived branch |
| `git add .` | Stage changes |
| `git commit -m "Message"` | Commit small change |
| `git push -u origin feature/name` | Push branch |
| `git merge feature/name` | Merge short-lived branch |
| `git branch -d feature/name` | Delete merged branch |

## Common mistakes

### Mistake 1: Keeping branches open too long

Long-lived branches create integration problems.

### Mistake 2: Merging large incomplete changes without feature flags

Use feature flags or break work into smaller safe changes.

### Mistake 3: Not protecting main

Main should stay stable.

Use reviews and automated checks.

### Mistake 4: No automated tests

Frequent integration is risky without tests.

### Mistake 5: Slow review process

If reviews take too long, branches become long-lived.

## Best practices

- Keep branches short-lived.
- Merge small changes frequently.
- Protect `main`.
- Use automated tests.
- Use feature flags.
- Review pull requests quickly.
- Avoid large batch changes.
- Keep the project deployable.

## Professional recommendation

Use trunk-based development when your team has strong testing, fast review, and a CI/CD culture.

For beginner projects, start with GitHub Flow first, then move toward trunk-based development as the process matures.

## Summary

Trunk-based development focuses on frequent integration into a stable main branch.

Basic idea:

```txt
Small changes → short-lived branches → frequent merge into main
```

Basic workflow:

```bash
git switch main
git pull origin main
git switch -c feature/small-change
git add .
git commit -m "Add small change"
git push -u origin feature/small-change
```

Golden rule:

```txt
Keep main stable and integrate small changes frequently.
```

## Recommended next topic

Continue with:

```txt
docs/10-professional-workflows/pull-request-workflow.md
```