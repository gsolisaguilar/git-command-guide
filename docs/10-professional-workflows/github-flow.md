# GitHub Flow

GitHub Flow is a simple Git workflow based on short-lived branches and pull requests.

It is commonly used by teams that deploy frequently and want a lightweight collaboration process.

## What is GitHub Flow?

GitHub Flow is a branch-based workflow where `main` is always stable and deployable.

The basic idea is:

```txt
Create a branch.
Make changes.
Open a pull request.
Review and test.
Merge into main.
Deploy.
```

## Main branch

In GitHub Flow, the main branch is usually:

```txt
main
```

The `main` branch should always be stable.

It should contain code that is ready to deploy or documentation that is ready to publish.

## Feature branches

All changes are made in branches created from `main`.

Examples:

```txt
feature/github-flow-docs
fix/readme-link
docs/update-workflow-guide
```

## Basic GitHub Flow process

```txt
1. Update main.
2. Create a new branch from main.
3. Make changes.
4. Commit changes.
5. Push the branch.
6. Open a pull request.
7. Review and discuss.
8. Run tests or checks.
9. Merge into main.
10. Delete the branch.
```

## Create a branch

```bash
git switch main
git pull origin main
git switch -c feature/github-flow-docs
```

If you are working locally only and have not pushed yet:

```bash
git switch main
git switch -c feature/github-flow-docs
```

## Make changes and commit

```bash
git status
git add .
git commit -m "Add GitHub Flow documentation"
```

## Push branch

```bash
git push -u origin feature/github-flow-docs
```

This uploads your branch to GitHub and sets upstream tracking.

## Open a pull request

After pushing, open a pull request on GitHub.

The pull request should explain:

- What changed.
- Why it changed.
- How it was tested.
- Any risks or notes.

## Pull request review

Team members review the pull request.

They may:

- Ask questions.
- Suggest changes.
- Approve the work.
- Request updates.
- Check tests or automation results.

## Merge into main

After approval, merge the pull request into `main`.

Common merge options include:

```txt
Merge commit
Squash and merge
Rebase and merge
```

## Delete branch after merge

After the branch is merged, delete it.

Local branch:

```bash
git branch -d feature/github-flow-docs
```

Remote branch:

```bash
git push origin --delete feature/github-flow-docs
```

If using GitHub, the remote branch can often be deleted from the pull request page.

## GitHub Flow diagram

```txt
main:    A---B---------M
              \       /
feature:       C---D
```

The feature branch starts from `main`, gets reviewed, and is merged back into `main`.

## GitHub Flow with squash merge

Some teams prefer squash merge.

Feature branch:

```txt
C Add first draft
D Fix typo
E Update examples
```

After squash merge into `main`:

```txt
S Add GitHub Flow documentation
```

This keeps `main` history clean.

## GitHub Flow with rebase

Some teams prefer rebase before merge:

```bash
git switch feature/github-flow-docs
git rebase main
git switch main
git merge --ff-only feature/github-flow-docs
```

This keeps history linear.

## Advantages of GitHub Flow

GitHub Flow is useful because it is:

- Simple.
- Easy to understand.
- Good for small and medium teams.
- Good for frequent releases.
- Good for continuous deployment.
- Pull-request focused.
- Easy to combine with automated checks.

## Disadvantages of GitHub Flow

GitHub Flow may not be ideal when:

- Releases require long stabilization periods.
- Multiple versions are maintained.
- Production hotfixes need a separate process.
- `main` is not kept stable.
- The team does not review pull requests carefully.

## When to use GitHub Flow

Use GitHub Flow when:

- The team wants a simple workflow.
- Changes are integrated frequently.
- Pull requests are used.
- The project has automated checks.
- `main` can remain stable.
- Releases are frequent or continuous.

## When not to use GitHub Flow

Avoid GitHub Flow when:

- The project needs strict release branches.
- Multiple release versions must be maintained.
- Deployments are rare and heavily controlled.
- The team needs a more formal release process.

## GitHub Flow for documentation repositories

GitHub Flow works very well for documentation projects.

Example:

```txt
main
feature/basic-git-commands
feature/branches
feature/remote-repositories
feature/github-flow-docs
```

Each topic can be created in a separate branch, reviewed, and merged into `main`.

## Example workflow for this repository

```bash
git switch main
git switch -c feature/github-flow-docs

# create or edit files

git add docs/10-professional-workflows/github-flow.md
git commit -m "Add GitHub Flow documentation"

git switch main
git merge feature/github-flow-docs
git branch -d feature/github-flow-docs
```

If using GitHub:

```bash
git push -u origin feature/github-flow-docs
```

Then open a pull request.

## Common commands

| Command | Purpose |
|---|---|
| `git switch main` | Move to main branch |
| `git pull origin main` | Update main |
| `git switch -c feature/name` | Create feature branch |
| `git add .` | Stage changes |
| `git commit -m "Message"` | Commit changes |
| `git push -u origin feature/name` | Push branch to GitHub |
| `git branch -d feature/name` | Delete local branch |
| `git push origin --delete feature/name` | Delete remote branch |

## Common mistakes

### Mistake 1: Working directly on main

In GitHub Flow, create a branch for each change.

```bash
git switch -c feature/my-change
```

### Mistake 2: Keeping branches open too long

Short-lived branches reduce conflicts.

### Mistake 3: Not reviewing pull requests

GitHub Flow depends on review and feedback.

### Mistake 4: Merging without checks

Use tests, linters, builds, or manual review before merging.

### Mistake 5: Not deleting merged branches

Delete branches after they are merged to keep the repository clean.

## Best practices

- Keep `main` stable.
- Create one branch per task.
- Use clear branch names.
- Make small commits.
- Open pull requests early.
- Review changes carefully.
- Use automated checks when possible.
- Delete branches after merge.
- Keep branches short-lived.

## Professional recommendation

For most small projects, documentation repositories, and GitHub-based teams, GitHub Flow is a good default workflow.

It is simpler than Git Flow and easier to maintain.

## Summary

GitHub Flow is a simple workflow based on branches and pull requests.

Basic process:

```txt
Branch → Commit → Push → Pull Request → Review → Merge → Delete branch
```

Basic commands:

```bash
git switch main
git pull origin main
git switch -c feature/my-change
git add .
git commit -m "Add my change"
git push -u origin feature/my-change
```

## Recommended next topic

Continue with:

```txt
docs/10-professional-workflows/trunk-based-development.md
```