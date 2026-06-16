# Conflict Resolution

A merge conflict happens when Git cannot automatically combine changes from different branches.

Conflicts are normal in Git, especially when multiple branches modify the same lines of the same file.

## What is a merge conflict?

A merge conflict occurs when Git does not know which change to keep.

Example:

```txt
main changed line 10 in README.md
feature changed line 10 in README.md
```

When this happens, Git pauses the merge and asks you to resolve the conflict manually.

## When conflicts happen

Conflicts commonly happen when:

- Two branches modify the same line.
- One branch deletes a file while another branch modifies it.
- Two people edit the same section of a file.
- A branch is outdated and tries to merge into a newer branch.
- Large changes were made without updating from the main branch.

## Example conflict scenario

Start with this file:

```txt
Welcome to the Git guide.
```

On `main`, it changes to:

```txt
Welcome to the professional Git guide.
```

On `feature`, it changes to:

```txt
Welcome to the beginner Git guide.
```

When merging, Git cannot decide which sentence is correct.

## How Git marks a conflict

When a conflict happens, Git adds conflict markers to the file.

Example:

```txt
<<<<<<< HEAD
Welcome to the professional Git guide.
=======
Welcome to the beginner Git guide.
>>>>>>> feature/branching-guide
```

## Understanding conflict markers

| Marker | Meaning |
|---|---|
| `<<<<<<< HEAD` | Start of the current branch changes |
| `=======` | Separator between both versions |
| `>>>>>>> branch-name` | End of incoming branch changes |

## What is HEAD during a merge?

During a merge, `HEAD` usually represents your current branch.

Example:

```bash
git switch main
git merge feature/branching-guide
```

In this case:

```txt
HEAD = main
incoming branch = feature/branching-guide
```

## Check conflict status

When a conflict happens, run:

```bash
git status
```

Example output:

```txt
You have unmerged paths.

Unmerged paths:
  both modified: README.md
```

This shows which files need manual resolution.

## Basic conflict resolution workflow

```bash
git status
```

Open the conflicted file.

Edit the file manually.

Remove conflict markers.

Stage the resolved file:

```bash
git add file-name
```

Complete the merge:

```bash
git commit
```

In many cases, after staging all resolved files, Git may automatically complete the merge commit when you run:

```bash
git commit
```

## Step-by-step conflict resolution

### Step 1: Start merge

```bash
git switch main
git merge feature/branching-guide
```

### Step 2: Git reports conflict

Example:

```txt
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
```

### Step 3: Check status

```bash
git status
```

### Step 4: Open the conflicted file

Example conflict:

```txt
<<<<<<< HEAD
Welcome to the professional Git guide.
=======
Welcome to the beginner Git guide.
>>>>>>> feature/branching-guide
```

### Step 5: Decide final content

You decide what the correct final version should be.

Example:

```txt
Welcome to the professional Git guide for beginners and advanced developers.
```

### Step 6: Remove conflict markers

Make sure the file no longer contains:

```txt
<<<<<<<
=======
>>>>>>>
```

### Step 7: Stage the resolved file

```bash
git add README.md
```

### Step 8: Complete the merge

```bash
git commit
```

Or, if Git already prepared the merge message, save and close the editor.

## Example resolved file

Before:

```txt
<<<<<<< HEAD
Welcome to the professional Git guide.
=======
Welcome to the beginner Git guide.
>>>>>>> feature/branching-guide
```

After:

```txt
Welcome to the professional Git guide for beginners and advanced developers.
```

## Resolve by keeping current branch changes

Sometimes you want to keep the current branch version.

Use:

```bash
git checkout --ours file-name
```

Example:

```bash
git checkout --ours README.md
git add README.md
```

`--ours` means:

```txt
Keep the version from the current branch.
```

## Resolve by keeping incoming branch changes

Sometimes you want to keep the incoming branch version.

Use:

```bash
git checkout --theirs file-name
```

Example:

```bash
git checkout --theirs README.md
git add README.md
```

`--theirs` means:

```txt
Keep the version from the branch being merged.
```

## Ours vs theirs example

If you run:

```bash
git switch main
git merge feature/branching-guide
```

Then:

| Option | Keeps |
|---|---|
| `--ours` | Version from `main` |
| `--theirs` | Version from `feature/branching-guide` |

## Use git restore for conflict resolution

Modern Git also supports:

```bash
git restore --ours file-name
```

And:

```bash
git restore --theirs file-name
```

Example:

```bash
git restore --ours README.md
git add README.md
```

## Resolve all conflicts manually

For important files, it is usually better to resolve conflicts manually.

Manual resolution allows you to combine both changes correctly.

Example:

```txt
Current branch: professional Git guide
Incoming branch: beginner Git guide

Final version: professional Git guide from beginner to expert
```

## Check conflict markers before committing

Before finishing the merge, search for conflict markers.

You can use:

```bash
grep -n "<<<<<<<\|=======\|>>>>>>>" file-name
```

Example:

```bash
grep -n "<<<<<<<\|=======\|>>>>>>>" README.md
```

If nothing appears, the markers were removed.

## Check all files for conflict markers

```bash
grep -R "<<<<<<<\|=======\|>>>>>>>" .
```

This helps avoid committing unresolved conflict markers.

## Complete the merge

After resolving and staging all conflicted files:

```bash
git status
```

Then:

```bash
git commit
```

Or if Git already completed the merge after staging, check:

```bash
git log --oneline --graph --decorate --all
```

## Abort conflict resolution

If you do not want to continue the merge:

```bash
git merge --abort
```

This tries to return your repository to the state before the merge started.

## Tools for resolving conflicts

You can resolve conflicts using:

- A text editor.
- Visual Studio Code.
- Git command line.
- GitHub web editor.
- Merge tools.
- IDEs such as IntelliJ IDEA, Eclipse, or WebStorm.

## Visual Studio Code conflict options

VS Code often shows buttons like:

```txt
Accept Current Change
Accept Incoming Change
Accept Both Changes
Compare Changes
```

Meaning:

| Option | Meaning |
|---|---|
| Accept Current Change | Keep current branch version |
| Accept Incoming Change | Keep incoming branch version |
| Accept Both Changes | Keep both versions |
| Compare Changes | Review differences |

## Common conflict commands

| Command | Purpose |
|---|---|
| `git status` | Shows conflicted files |
| `git add file-name` | Marks conflict as resolved |
| `git commit` | Completes the merge |
| `git merge --abort` | Cancels the merge |
| `git checkout --ours file-name` | Keeps current branch version |
| `git checkout --theirs file-name` | Keeps incoming branch version |
| `git restore --ours file-name` | Modern way to keep current branch version |
| `git restore --theirs file-name` | Modern way to keep incoming branch version |

## Common mistakes

### Mistake 1: Committing conflict markers

Never commit files that still contain:

```txt
<<<<<<<
=======
>>>>>>>
```

Search before committing.

### Mistake 2: Accepting one side without understanding

Do not blindly accept current or incoming changes.

Review the context first.

### Mistake 3: Resolving the file but forgetting git add

After resolving a conflict, you must stage the file:

```bash
git add file-name
```

### Mistake 4: Panicking during conflicts

Conflicts are normal.

Git pauses the process so you can decide what the final version should be.

### Mistake 5: Continuing when you wanted to abort

If you are unsure and want to cancel:

```bash
git merge --abort
```

## Best practices

- Pull or fetch changes regularly.
- Keep branches short-lived when possible.
- Make small focused commits.
- Communicate with teammates when editing the same files.
- Resolve conflicts carefully.
- Run tests after resolving conflicts.
- Review the final file before committing.
- Do not commit conflict markers.

## Professional conflict workflow

```bash
git status
```

Open conflicted files and resolve manually.

Then:

```bash
grep -R "<<<<<<<\|=======\|>>>>>>>" .
git add .
git status
git commit
```

After that:

```bash
git log --oneline --graph --decorate --all
```

## Summary

A merge conflict happens when Git cannot automatically combine changes.

Basic conflict resolution:

```bash
git status
# edit conflicted files
git add resolved-file
git commit
```

Cancel merge:

```bash
git merge --abort
```

Keep current branch version:

```bash
git checkout --ours file-name
```

Keep incoming branch version:

```bash
git checkout --theirs file-name
```

Conflicts are not errors. They are Git asking you to decide the correct final content.

## Recommended next topic

Continue with:

```txt
docs/04-merges-and-conflicts/aborting-merges.md
```