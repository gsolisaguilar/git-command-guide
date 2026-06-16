# Pull Request Workflow

A pull request is a collaboration process used to propose, review, discuss, and merge changes into another branch.

Pull requests are commonly used on platforms like GitHub, GitLab, Bitbucket, and Azure DevOps.

## What is a pull request?

A pull request is a request to merge changes from one branch into another branch.

Example:

```txt
feature/pull-request-workflow → main
```

It allows other people to review your changes before they are merged.

## Why pull requests are useful

Pull requests help teams:

- Review code before merging.
- Discuss proposed changes.
- Run automated checks.
- Catch mistakes early.
- Share knowledge.
- Improve code quality.
- Track why changes were made.
- Keep main stable.

## Basic pull request process

```txt
1. Create a branch.
2. Make changes.
3. Commit changes.
4. Push the branch.
5. Open a pull request.
6. Describe the changes.
7. Request review.
8. Address feedback.
9. Pass checks.
10. Merge the pull request.
11. Delete the branch.
```

## Create a branch

```bash
git switch main
git pull origin main
git switch -c feature/pull-request-workflow
```

## Make changes

Edit files in your project.

Then check status:

```bash
git status
```

## Commit changes

```bash
git add .
git commit -m "Add pull request workflow documentation"
```

## Push branch

```bash
git push -u origin feature/pull-request-workflow
```

## Open pull request

On GitHub, open a pull request from:

```txt
feature/pull-request-workflow
```

into:

```txt
main
```

## Pull request title

A good pull request title should be clear and specific.

Good examples:

```txt
Add pull request workflow documentation
Fix broken README links
Update Git rebase examples
```

Bad examples:

```txt
Changes
Update
Fix
Final
```

## Pull request description

A good pull request description may include:

```md
## Summary

- Added pull request workflow documentation.
- Included branch, commit, push, review, and merge steps.
- Added common mistakes and best practices.

## Testing

- Reviewed Markdown formatting.
- Checked internal documentation links.

## Notes

- This PR only updates documentation.
```

## Request reviewers

Ask one or more teammates to review the pull request.

Reviewers check:

- Correctness.
- Style.
- Documentation.
- Tests.
- Possible risks.
- Consistency with project standards.

## Automated checks

Pull requests often run automated checks such as:

- Build.
- Unit tests.
- Integration tests.
- Linting.
- Formatting.
- Security scanning.
- Documentation checks.

## Address review feedback

If changes are requested:

```bash
# make updates
git add .
git commit -m "Address review feedback"
git push
```

The pull request updates automatically after pushing to the same branch.

## Keep branch updated

If `main` changed while your pull request is open, update your branch.

Using merge:

```bash
git switch feature/pull-request-workflow
git fetch origin
git merge origin/main
git push
```

Using rebase:

```bash
git switch feature/pull-request-workflow
git fetch origin
git rebase origin/main
git push --force-with-lease
```

Use rebase only if your team allows it.

## Merge pull request

After approval and passing checks, merge the pull request.

Common merge methods:

```txt
Merge commit
Squash and merge
Rebase and merge
```

## Merge commit

A merge commit preserves the branch history.

Good for:

- Larger features.
- Preserving context.
- Showing branch integration.

## Squash and merge

Squash merge combines all commits into one commit on the target branch.

Good for:

- Cleaning messy commit history.
- One commit per feature.
- Documentation updates.

## Rebase and merge

Rebase and merge replays commits onto the base branch without creating a merge commit.

Good for:

- Linear history.
- Clean commit sequence.
- Teams that prefer rebase workflows.

## Delete branch after merge

After merging, delete the branch.

Local:

```bash
git branch -d feature/pull-request-workflow
```

Remote:

```bash
git push origin --delete feature/pull-request-workflow
```

## Pull latest main after merge

After the pull request is merged, update local `main`:

```bash
git switch main
git pull origin main
```

## Pull request workflow example

```bash
git switch main
git pull origin main
git switch -c feature/pull-request-workflow

# make changes

git add .
git commit -m "Add pull request workflow documentation"
git push -u origin feature/pull-request-workflow
```

Then open a pull request on GitHub.

After merge:

```bash
git switch main
git pull origin main
git branch -d feature/pull-request-workflow
```

## Pull request checklist

Before opening a pull request:

```txt
Is the branch up to date?
Is the change focused?
Are commit messages clear?
Did I review my own changes?
Did I run tests if needed?
Is the PR title clear?
Is the PR description complete?
```

## Good pull request size

Small pull requests are easier to review.

Recommended:

```txt
One topic.
One feature.
One fix.
One documentation section.
```

Avoid pull requests that include many unrelated changes.

## Draft pull requests

A draft pull request is useful when:

- Work is not ready to merge.
- You want early feedback.
- You want CI checks to run.
- You want visibility while still working.

## Common commands

| Command | Purpose |
|---|---|
| `git switch -c feature/name` | Creates feature branch |
| `git add .` | Stages changes |
| `git commit -m "Message"` | Commits changes |
| `git push -u origin feature/name` | Pushes branch |
| `git fetch origin` | Updates remote references |
| `git merge origin/main` | Updates branch with latest main using merge |
| `git rebase origin/main` | Updates branch with latest main using rebase |
| `git branch -d feature/name` | Deletes local merged branch |

## Common mistakes

### Mistake 1: Opening huge pull requests

Large pull requests are harder to review and more likely to contain mistakes.

### Mistake 2: Not describing the change

A pull request should explain what changed and why.

### Mistake 3: Ignoring review feedback

Review is part of collaboration.

### Mistake 4: Merging without checks

Make sure required checks pass before merging.

### Mistake 5: Forgetting to delete merged branches

Clean up branches after merge.

## Best practices

- Keep pull requests small.
- Use clear titles.
- Write useful descriptions.
- Review your own changes before requesting review.
- Respond respectfully to feedback.
- Keep branches updated.
- Wait for required checks.
- Delete branches after merging.
- Use draft PRs for early feedback.

## Professional recommendation

A strong pull request should answer:

```txt
What changed?
Why was it changed?
How was it tested?
Is there anything reviewers should know?
```

## Summary

A pull request is a professional way to review and merge changes.

Basic workflow:

```txt
Create branch → Commit changes → Push branch → Open PR → Review → Merge → Delete branch
```

Basic commands:

```bash
git switch -c feature/my-change
git add .
git commit -m "Add my change"
git push -u origin feature/my-change
```

## Recommended next topic

Continue with:

```txt
docs/10-professional-workflows/code-review-workflow.md
```