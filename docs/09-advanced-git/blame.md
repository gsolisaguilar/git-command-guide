# Blame

`git blame` shows who last modified each line of a file and in which commit.

Despite the name, it should not be used to blame people. It should be used to understand history and context.

## What is git blame?

`git blame` displays line-by-line commit information for a file.

Basic syntax:

```bash
git blame file-name
```

Example:

```bash
git blame README.md
```

## Why git blame is useful

Use `git blame` to:

- Understand why a line was changed.
- Find the commit that introduced a line.
- Locate related changes.
- Investigate bugs.
- Find context before editing code.
- Identify who may know more about a section.
- Review history during debugging.

## Basic example

```bash
git blame README.md
```

Example output:

```txt
a1b2c3d4 (Jessica Santos 2026-06-16 10:30:00 -0600 1) # Git Commands Guide
e4f5g6h7 (Jessica Santos 2026-06-16 10:35:00 -0600 2) A curated Git reference.
```

Each line includes:

- Commit hash.
- Author.
- Date.
- Line number.
- Content.

## Show blame for a specific line range

```bash
git blame -L start,end file-name
```

Example:

```bash
git blame -L 10,25 README.md
```

This shows blame information only for lines 10 to 25.

## Show blame for one line

```bash
git blame -L 15,15 README.md
```

This shows who last changed line 15.

## Use short commit hashes

```bash
git blame --abbrev=7 README.md
```

This controls how many characters of the commit hash are shown.

## Ignore whitespace changes

Sometimes formatting changes make blame harder to read.

Use:

```bash
git blame -w file-name
```

Example:

```bash
git blame -w README.md
```

This ignores whitespace changes.

## Show email addresses

```bash
git blame -e file-name
```

Example:

```bash
git blame -e README.md
```

This shows author emails.

## Show original commit information

```bash
git blame --show-stats file-name
```

This includes additional statistics after the blame output.

## Inspect the related commit

After finding a commit hash from blame:

```bash
git show commit-hash
```

Example:

```bash
git show a1b2c3d
```

This shows the full commit details and changes.

## Blame with moved or copied lines

Git blame has options to detect moved or copied lines.

Detect moved lines within the same file:

```bash
git blame -M file-name
```

Detect copied lines from other files:

```bash
git blame -C file-name
```

You can combine them:

```bash
git blame -w -M -C file-name
```

## Professional use of blame

Good use:

```txt
This line changed in commit a1b2c3d. I will inspect that commit to understand the reason.
```

Bad use:

```txt
This person broke the code.
```

The goal is context, not blame.

## Example debugging workflow

```bash
git blame -L 40,60 src/app.js
git show commit-hash
git log --oneline -- src/app.js
```

This helps understand how and why a section changed.

## Blame vs log

| Command | Purpose |
|---|---|
| `git blame file` | Shows who last changed each line |
| `git log -- file` | Shows commit history for a file |
| `git show commit` | Shows details of one commit |

Use them together for better context.

## Blame with renamed files

If a file was renamed, normal blame may not show enough history.

Try:

```bash
git log --follow -- file-name
```

Example:

```bash
git log --follow -- README.md
```

Then inspect older commits.

## Common blame commands

| Command | Purpose |
|---|---|
| `git blame file.md` | Shows line-by-line history |
| `git blame -L 10,20 file.md` | Shows blame for lines 10 to 20 |
| `git blame -w file.md` | Ignores whitespace changes |
| `git blame -M file.md` | Detects moved lines |
| `git blame -C file.md` | Detects copied lines |
| `git show commit` | Shows details of a commit |
| `git log -- file.md` | Shows file history |
| `git log --follow -- file.md` | Follows file history across renames |

## Common mistakes

### Mistake 1: Using blame to accuse people

Use blame to understand context, not to assign fault.

### Mistake 2: Not checking the commit

After finding a line with blame, inspect the commit:

```bash
git show commit-hash
```

### Mistake 3: Ignoring whitespace changes

If blame looks confusing because of formatting, try:

```bash
git blame -w file-name
```

### Mistake 4: Assuming the last editor caused the bug

The last person who touched a line did not necessarily introduce the issue.

Always inspect the surrounding history.

## Best practices

- Use blame for context.
- Inspect the related commit.
- Combine blame with `git log` and `git show`.
- Ignore whitespace when needed.
- Be respectful when asking teammates about changes.
- Do not use blame as a tool for accusation.

## Professional recommendation

Use this workflow:

```bash
git blame -L start,end file-name
git show commit-hash
git log --oneline -- file-name
```

This helps you understand the history before making changes.

## Summary

`git blame` shows who last modified each line of a file.

Basic command:

```bash
git blame file-name
```

Specific lines:

```bash
git blame -L 10,20 file-name
```

Ignore whitespace:

```bash
git blame -w file-name
```

Golden rule:

```txt
Use git blame to understand history, not to blame people.
```

## Recommended next topic

Continue with:

```txt
docs/09-advanced-git/submodules.md
```