# Code Review Workflow

Code review is the process of examining changes before they are merged into the main branch.

It is one of the most important practices in professional software development.

## What is code review?

Code review is a collaborative process where one or more people review proposed changes.

The goal is to improve quality, catch mistakes, share knowledge, and keep the project maintainable.

## Why code review matters

Code review helps teams:

- Find bugs early.
- Improve code quality.
- Improve documentation.
- Share knowledge.
- Keep standards consistent.
- Reduce production issues.
- Improve security.
- Support collaboration.
- Maintain a stable main branch.

## Code review in Git workflows

Code review usually happens inside a pull request.

Example:

```txt
feature/code-review-workflow → main
```

A reviewer checks the changes before they are merged.

## Author responsibilities

The author is the person who created the changes.

The author should:

- Keep the pull request focused.
- Write clear commit messages.
- Explain what changed.
- Explain why the change is needed.
- Test the changes.
- Respond to feedback.
- Update the pull request when needed.

## Reviewer responsibilities

The reviewer should:

- Understand the purpose of the change.
- Check correctness.
- Look for bugs or risks.
- Review readability.
- Check maintainability.
- Confirm tests or validation.
- Ask questions respectfully.
- Suggest improvements clearly.
- Approve only when ready.

## What to review

During code review, check:

```txt
Correctness
Readability
Maintainability
Security
Performance
Tests
Documentation
Consistency
Error handling
User impact
```

For documentation projects, check:

```txt
Clarity
Accuracy
Structure
Markdown formatting
Examples
Links
Consistency
Typos
```

## Basic code review process

```txt
1. Author opens a pull request.
2. Reviewer reads the description.
3. Reviewer checks the changed files.
4. Reviewer leaves comments or questions.
5. Author responds and updates the branch.
6. Automated checks pass.
7. Reviewer approves.
8. Pull request is merged.
```

## Review your own pull request first

Before requesting review, authors should review their own changes.

Use:

```bash
git diff main...feature/code-review-workflow
```

Or check in GitHub under the "Files changed" tab.

## Good review comments

Good comments are clear, respectful, and specific.

Example:

```txt
Could we rename this section to make the purpose clearer?
```

Example:

```txt
This command may be destructive. Can we add a warning before the example?
```

Example:

```txt
Consider adding an example output so beginners understand what to expect.
```

## Poor review comments

Avoid comments that are vague or disrespectful.

Bad examples:

```txt
This is bad.
Wrong.
Fix this.
I do not like it.
```

Better:

```txt
This section may be confusing for beginners. Could we add a short explanation before the command?
```

## Types of review comments

| Type | Example |
|---|---|
| Question | `Why did we choose this approach?` |
| Suggestion | `Consider using a clearer branch name here.` |
| Required change | `This command can delete files; please add a warning.` |
| Praise | `This example is clear and helpful.` |
| Note | `This is not blocking, but we may improve it later.` |

## Blocking vs non-blocking feedback

Blocking feedback means the pull request should not be merged until it is addressed.

Example:

```txt
This command is dangerous without a warning. Please add one before merge.
```

Non-blocking feedback is optional.

Example:

```txt
Optional: We could add one more example in the future.
```

## Author response to feedback

Good author responses:

```txt
Updated. I added a warning before the command.
```

```txt
Good point. I renamed the section for clarity.
```

```txt
I kept the original wording because it matches the previous docs, but I added an example.
```

## Handling disagreement

If author and reviewer disagree:

- Focus on the project goal.
- Explain reasoning.
- Ask for clarification.
- Use team standards.
- Involve another reviewer if needed.
- Avoid personal comments.

## Code review checklist

For code:

```txt
Does the change solve the problem?
Is the code readable?
Are edge cases handled?
Are errors handled correctly?
Are tests included or updated?
Is performance acceptable?
Is security considered?
Is documentation updated?
```

For documentation:

```txt
Is the explanation clear?
Are commands correct?
Are examples useful?
Are warnings included for risky commands?
Is Markdown formatting correct?
Are links valid?
Is the style consistent?
```

## Review commands locally

A reviewer may fetch and test a branch locally.

```bash
git fetch origin
git switch feature/code-review-workflow
```

If the branch does not exist locally:

```bash
git switch -c feature/code-review-workflow origin/feature/code-review-workflow
```

Run checks or review files.

## Compare branches locally

```bash
git diff main...feature/code-review-workflow
```

Show commits:

```bash
git log --oneline main..feature/code-review-workflow
```

## Approving a review

Approve when:

- The change is correct.
- Feedback was addressed.
- Tests or checks pass.
- The pull request is focused.
- The code or documentation is maintainable.

## Requesting changes

Request changes when:

- There is a bug.
- The explanation is incorrect.
- A risky command lacks warning.
- The change breaks standards.
- Required tests are missing.
- The pull request is not ready.

## Merging after review

After approval and checks, merge using the team’s preferred method:

```txt
Merge commit
Squash and merge
Rebase and merge
```

## Common code review mistakes

### Mistake 1: Reviewing only formatting

Formatting matters, but correctness and clarity are more important.

### Mistake 2: Being disrespectful

Review the work, not the person.

### Mistake 3: Making huge pull requests

Large pull requests make review harder.

### Mistake 4: Ignoring documentation

Good code often needs good documentation.

### Mistake 5: Approving without understanding

Ask questions if something is unclear.

## Best practices for authors

- Keep pull requests small.
- Explain the change clearly.
- Add screenshots or examples if helpful.
- Review your own changes first.
- Respond respectfully.
- Make requested updates in follow-up commits.
- Keep the branch updated.

## Best practices for reviewers

- Be respectful and specific.
- Focus on correctness and maintainability.
- Ask questions instead of assuming.
- Separate required changes from suggestions.
- Praise good work when appropriate.
- Review promptly.
- Avoid personal criticism.

## Professional recommendation

A good code review culture is respectful, clear, and focused on the project.

The best reviews improve the work without discouraging the author.

## Summary

Code review helps improve quality before changes are merged.

Basic flow:

```txt
Open PR → Review changes → Discuss feedback → Update branch → Approve → Merge
```

Good review comments are:

```txt
Specific
Respectful
Actionable
Focused on the work
```

Golden rule:

```txt
Review the change, not the person.
```

## Recommended next topic

Continue with:

```txt
docs/11-cheatsheets/basic-commands-cheatsheet.md
```