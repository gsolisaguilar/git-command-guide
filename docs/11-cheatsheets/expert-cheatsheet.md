# Expert Git Cheatsheet

Quick reference for advanced Git commands and professional troubleshooting.

## Advanced history commands

| Command | Description |
|---|---|
| `git log --oneline --graph --decorate --all` | Visualize full branch history |
| `git show commit-hash` | Show commit details |
| `git diff commit1 commit2` | Compare two commits |
| `git log -- file-name` | Show history for a file |
| `git log --follow -- file-name` | Follow history across renames |
| `git reflog` | Show local HEAD/reference movement history |

## Cherry-pick

| Command | Description |
|---|---|
| `git cherry-pick commit-hash` | Apply one commit to current branch |
| `git cherry-pick commit1 commit2` | Apply multiple commits |
| `git cherry-pick start..end` | Apply a range of commits |
| `git cherry-pick -n commit-hash` | Apply without committing |
| `git cherry-pick --continue` | Continue after conflict |
| `git cherry-pick --abort` | Abort cherry-pick |
| `git cherry-pick --skip` | Skip current commit |

Example:

```bash
git switch release/v1.0.0
git cherry-pick a1b2c3d
```

## Bisect

| Command | Description |
|---|---|
| `git bisect start` | Start bisect mode |
| `git bisect bad` | Mark current commit as bad |
| `git bisect good commit-hash` | Mark known good commit |
| `git bisect good` | Mark current commit as good |
| `git bisect skip` | Skip current commit |
| `git bisect reset` | Exit bisect mode |
| `git bisect run command` | Automate bisect with a test command |

Basic flow:

```bash
git bisect start
git bisect bad
git bisect good known-good-commit
# test each commit
git bisect good
# or
git bisect bad
git bisect reset
```

Automated example:

```bash
git bisect start
git bisect bad
git bisect good v1.0.0
git bisect run npm test
git bisect reset
```

## Reflog recovery

| Command | Description |
|---|---|
| `git reflog` | Show local reference movement |
| `git reflog --date=local` | Show reflog with dates |
| `git show HEAD@{1}` | Inspect previous HEAD state |
| `git switch -c recovery HEAD@{1}` | Recover safely into new branch |
| `git reset --hard HEAD@{1}` | Reset to previous state |

Safer recovery:

```bash
git reflog
git switch -c recovery/lost-work HEAD@{1}
```

Riskier recovery:

```bash
git reset --hard HEAD@{1}
```

## Blame

| Command | Description |
|---|---|
| `git blame file-name` | Show who last changed each line |
| `git blame -L 10,20 file-name` | Blame specific line range |
| `git blame -w file-name` | Ignore whitespace changes |
| `git blame -M file-name` | Detect moved lines |
| `git blame -C file-name` | Detect copied lines |
| `git show commit-hash` | Inspect the related commit |

Professional usage:

```bash
git blame -L 10,20 README.md
git show commit-hash
```

## Submodules

| Command | Description |
|---|---|
| `git submodule add URL path` | Add submodule |
| `git submodule status` | Show submodule status |
| `git submodule update --init --recursive` | Initialize and update submodules |
| `git clone --recurse-submodules URL` | Clone repo with submodules |
| `git submodule update --remote` | Update submodule from remote |
| `git submodule deinit -f path` | Deinitialize submodule |
| `git rm -f path` | Remove submodule path |

Clone with submodules:

```bash
git clone --recurse-submodules repository-url
```

If already cloned:

```bash
git submodule update --init --recursive
```

## Worktrees

| Command | Description |
|---|---|
| `git worktree list` | List worktrees |
| `git worktree add path branch-name` | Add worktree for existing branch |
| `git worktree add -b branch-name path` | Create branch and worktree |
| `git worktree remove path` | Remove worktree |
| `git worktree remove --force path` | Force remove worktree |
| `git worktree prune` | Clean stale worktree metadata |
| `git worktree lock path` | Lock worktree |
| `git worktree unlock path` | Unlock worktree |

Example:

```bash
git worktree add -b hotfix/fix-readme ../git-commands-guide-hotfix main
```

## Advanced stash

| Command | Description |
|---|---|
| `git stash push -m "message"` | Create named stash |
| `git stash push -u -m "message"` | Include untracked files |
| `git stash push -a -m "message"` | Include ignored files |
| `git stash push -p -m "message"` | Stash selected hunks |
| `git stash push --keep-index` | Stash unstaged changes only |
| `git stash branch branch-name stash@{0}` | Create branch from stash |
| `git stash show -p stash@{0}` | Inspect stash details |

Safe stash restore:

```bash
git stash apply stash@{0}
git status
git stash drop stash@{0}
```

## Advanced merge and rebase

| Command | Description |
|---|---|
| `git merge --no-ff branch-name` | Force merge commit |
| `git merge --ff-only branch-name` | Only allow fast-forward |
| `git merge --squash branch-name` | Combine branch into one staged change |
| `git rebase -i HEAD~3` | Edit last 3 commits |
| `git rebase --onto newbase oldbase branch` | Advanced rebase onto different base |
| `git push --force-with-lease` | Safer force push after rewriting history |

## Interactive rebase actions

| Action | Meaning |
|---|---|
| `pick` | Keep commit |
| `reword` | Change commit message |
| `edit` | Modify commit |
| `squash` | Combine with previous commit and edit message |
| `fixup` | Combine with previous commit and discard message |
| `drop` | Remove commit |

## Tags and releases

| Command | Description |
|---|---|
| `git tag` | List tags |
| `git tag v1.0.0` | Create lightweight tag |
| `git tag -a v1.0.0 -m "Message"` | Create annotated tag |
| `git show v1.0.0` | Show tag details |
| `git push origin v1.0.0` | Push one tag |
| `git push origin --tags` | Push all tags |
| `git tag -d v1.0.0` | Delete local tag |
| `git push origin --delete v1.0.0` | Delete remote tag |

Release example:

```bash
git switch main
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin main
git push origin v1.0.0
```

## Remote and upstream

| Command | Description |
|---|---|
| `git remote -v` | Show remote URLs |
| `git remote set-url origin URL` | Change remote URL |
| `git fetch --prune` | Clean deleted remote branch references |
| `git branch -vv` | Show branch upstream tracking |
| `git push -u origin branch-name` | Push and set upstream |
| `git branch --set-upstream-to=origin/branch` | Set upstream manually |

## Troubleshooting commands

| Problem | Command |
|---|---|
| Lost commit | `git reflog` |
| Wrong staged file | `git restore --staged file` |
| Wrong local commit | `git reset HEAD~1` |
| Bad pushed commit | `git revert commit-hash` |
| Messy untracked files | `git clean -n` then `git clean -f` |
| Merge conflict | Resolve files, `git add .`, `git commit` |
| Rebase conflict | Resolve files, `git add .`, `git rebase --continue` |
| Need one commit from another branch | `git cherry-pick commit-hash` |
| Need to find bug-introducing commit | `git bisect` |

## Dangerous commands

Use carefully:

```bash
git reset --hard
git clean -fdx
git push --force
git rebase shared-branch
git branch -D branch-name
git stash clear
```

Safer alternatives:

```bash
git revert commit-hash
git clean -n
git push --force-with-lease
git branch -d branch-name
git stash apply
```

## Expert safety checklist

Before destructive commands:

```txt
Did I run git status?
Did I check git log?
Is this branch shared?
Did I push this commit already?
Do I need a backup branch?
Can I use revert instead of reset?
Can I use --force-with-lease instead of --force?
```

Create backup branch before risky work:

```bash
git branch backup/before-risky-change
```

## Most useful expert commands

```bash
git log --oneline --graph --decorate --all
git reflog
git cherry-pick commit-hash
git bisect start
git blame -L 10,20 file-name
git worktree list
git stash branch branch-name stash@{0}
git push --force-with-lease
```

## Summary

Advanced Git commands are powerful but require care.

Golden rules:

```txt
Use reflog before assuming work is lost.
Use cherry-pick for specific commits.
Use bisect to find when a bug started.
Use blame to understand context, not to accuse.
Use submodules only when necessary.
Use worktrees for parallel branch work.
Avoid rewriting shared history unless agreed.
```