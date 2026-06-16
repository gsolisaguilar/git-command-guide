# Bisect

`git bisect` is used to find the commit that introduced a bug.

It uses a binary search through your commit history to identify the problematic commit efficiently.

## What is git bisect?

`git bisect` helps you find the first bad commit.

In simple terms:

```txt
Git checks commits between a known good commit and a known bad commit until it finds where the problem started.
```

## Why bisect is useful

Bisect is useful when:

- A bug exists now, but you do not know when it started.
- The project has many commits.
- Manually checking every commit would take too long.
- You know one commit where the project worked.
- You know one commit where the project is broken.

## Basic idea

You tell Git:

```txt
This commit is bad.
This older commit was good.
```

Then Git checks a commit in the middle.

You test the project and tell Git:

```txt
good
```

or:

```txt
bad
```

Git repeats this until it finds the first bad commit.

## Start bisect

```bash
git bisect start
```

## Mark current commit as bad

If the current version has the bug:

```bash
git bisect bad
```

## Mark a known good commit

Find a commit where the bug did not exist:

```bash
git log --oneline
```

Then mark it as good:

```bash
git bisect good commit-hash
```

Example:

```bash
git bisect good a1b2c3d
```

## Bisect workflow

```bash
git bisect start
git bisect bad
git bisect good a1b2c3d
```

Git will checkout a commit in the middle.

Test the project.

If the bug exists:

```bash
git bisect bad
```

If the bug does not exist:

```bash
git bisect good
```

Repeat until Git identifies the first bad commit.

## Example output

```txt
b4c5d6e is the first bad commit
commit b4c5d6e
Author: Developer <developer@example.com>
Date:   Tue Jun 16 10:00:00 2026 -0600

    Update authentication logic
```

This means commit `b4c5d6e` introduced the bug.

## End bisect

After finding the bad commit, return to your original branch:

```bash
git bisect reset
```

This is important.

## Full bisect example

```bash
git bisect start
git bisect bad
git bisect good a1b2c3d
```

Git checks out a middle commit.

Test manually.

If bad:

```bash
git bisect bad
```

If good:

```bash
git bisect good
```

After Git finds the bad commit:

```bash
git bisect reset
```

## Bisect with tags

If you know a version was good:

```bash
git bisect good v1.0.0
```

If current version is bad:

```bash
git bisect bad
```

## Bisect with branches

You can also use branch names.

Example:

```bash
git bisect start
git bisect bad main
git bisect good release/v1.0.0
```

## Automating bisect

If you have an automated test that detects the bug, you can use:

```bash
git bisect run command
```

Example:

```bash
git bisect run npm test
```

Git will automatically run the command on each commit.

If the command exits with status `0`, Git treats it as good.

If the command exits with non-zero status, Git treats it as bad.

## Example with a script

```bash
git bisect start
git bisect bad
git bisect good a1b2c3d
git bisect run ./test.sh
```

Your script should return:

```txt
0 = good
non-zero = bad
```

## Skip a commit

Sometimes a commit cannot be tested because the project does not build.

Use:

```bash
git bisect skip
```

Git will choose another commit.

## Check bisect status

```bash
git bisect log
```

This shows the bisect steps taken.

## Replay bisect log

If you saved a bisect log, you can replay it:

```bash
git bisect replay file-name
```

This is advanced and useful for reproducing bisect sessions.

## Common bisect commands

| Command | Purpose |
|---|---|
| `git bisect start` | Starts bisect mode |
| `git bisect bad` | Marks current commit as bad |
| `git bisect bad commit` | Marks a specific commit as bad |
| `git bisect good commit` | Marks a specific commit as good |
| `git bisect good` | Marks current commit as good |
| `git bisect skip` | Skips current commit |
| `git bisect reset` | Ends bisect and returns to original state |
| `git bisect run command` | Runs automated test during bisect |
| `git bisect log` | Shows bisect history |

## Common mistakes

### Mistake 1: Forgetting to reset bisect

After finishing, always run:

```bash
git bisect reset
```

### Mistake 2: Marking commits incorrectly

If you mark a bad commit as good, the result may be wrong.

Test carefully before answering Git.

### Mistake 3: Using bisect without a known good commit

You need at least:

```txt
One known bad commit.
One known good commit.
```

### Mistake 4: Testing inconsistently

Use the same test process for each commit.

## Best practices

- Start with a clean working tree.
- Know one good commit and one bad commit.
- Test consistently.
- Use automated tests when possible.
- Use `git bisect reset` when done.
- Record the bad commit and investigate it carefully.
- Do not make unrelated changes during bisect.

## Professional recommendation

Use bisect when the bug is difficult to locate manually.

Recommended flow:

```bash
git status
git bisect start
git bisect bad
git bisect good known-good-commit
# test each commit
git bisect good
# or
git bisect bad
git bisect reset
```

## Summary

`git bisect` helps find the commit that introduced a bug.

Basic flow:

```bash
git bisect start
git bisect bad
git bisect good commit-hash
```

Then test each commit and mark it:

```bash
git bisect good
git bisect bad
```

Finish:

```bash
git bisect reset
```

Golden rule:

```txt
Use bisect when you know one good commit and one bad commit.
```

## Recommended next topic

Continue with:

```txt
docs/09-advanced-git/reflog.md
```