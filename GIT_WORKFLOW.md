# Git Workflow and Commands

A practical guide to day-to-day Git usage, including working tree flow, branch flow, collaboration, release, and recovery.

## 1) Core Concepts (Very Short)

- Working directory: your files on disk.
- Staging area (index): what will go into the next commit.
- Repository history: committed snapshots.
- Remote: shared repo (for example, `origin`).

## 2) First-Time Setup

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
git config --global core.editor "vim"
git config --list
```

## 3) Create or Clone Repository

```bash
# Start new repo
mkdir my-project && cd my-project
git init
echo "# My Project" > README.md
git add README.md
git commit -m "chore: initial commit"

# Or clone existing
git clone https://github.com/org/repo.git
cd repo
```

## 4) Daily Working Tree Workflow

```bash
git status                    # see changed/untracked files
git add file.txt              # stage one file
git add .                     # stage all current changes
git restore --staged file.txt # unstage file
git diff                      # unstaged diff
git diff --staged             # staged diff
git commit -m "feat: add login validation"
git log --oneline --graph --decorate -n 15
```

Recommended loop:
1. Pull latest changes.
2. Create/update feature branch.
3. Make small, focused commits.
4. Push branch.
5. Open PR and merge.

## 5) Branch Workflow (Feature Branch)

```bash
# update local main
git checkout main
git pull origin main

# create feature branch
git checkout -b feat/user-profile

# work and commit
git add .
git commit -m "feat(profile): show user avatar"

# publish branch
git push -u origin feat/user-profile
```

After PR merge:

```bash
git checkout main
git pull origin main
git branch -d feat/user-profile         # delete local branch
git push origin --delete feat/user-profile  # delete remote branch
```

## 6) Keep Branch Updated (Merge or Rebase)

### Merge main into feature

```bash
git checkout feat/user-profile
git fetch origin
git merge origin/main
```

### Rebase feature on latest main (cleaner linear history)

```bash
git checkout feat/user-profile
git fetch origin
git rebase origin/main
# if conflicts: edit files -> git add <file> -> git rebase --continue
```

If branch already pushed and rebased:

```bash
git push --force-with-lease
```

## 7) Collaboration Workflow

```bash
git fetch origin                        # get latest remote refs
git branch -a                           # list local + remote branches
git checkout -b fix/api-timeout origin/fix/api-timeout

# review someone's branch
git log --oneline --decorate -n 20
git diff main...HEAD
```

## 8) Stash Workflow (Temporary Save)

```bash
git stash push -m "wip: checkout flow"
git stash list
git stash show -p stash@{0}
git stash apply stash@{0}   # keep stash
git stash pop               # apply + drop latest stash
git stash drop stash@{0}
```

## 9) Undo and Recovery

### Undo file changes (not committed)

```bash
git restore file.txt
```

### Undo staged changes

```bash
git restore --staged file.txt
```

### Amend last commit

```bash
git commit --amend -m "feat: better commit message"
```

### Revert a commit safely (shared history)

```bash
git revert <commit_sha>
```

### Reset branch pointer (local history rewriting)

```bash
git reset --soft HEAD~1   # keep changes staged
git reset --mixed HEAD~1  # keep changes unstaged
git reset --hard HEAD~1   # discard changes (danger)
```

### Recover lost commit using reflog

```bash
git reflog
git checkout <lost_commit_sha>
# or
git reset --hard <lost_commit_sha>
```

## 10) Conflict Resolution Workflow

```bash
git pull --rebase origin main
# conflict happens -> edit conflict markers
# <<<<<<<, =======, >>>>>>>
git add resolved-file
git rebase --continue
# or cancel
git rebase --abort
```

## 11) Tags and Release Workflow

```bash
git tag                         # list tags
git tag -a v1.0.0 -m "release 1.0.0"
git push origin v1.0.0
git push origin --tags
```

Typical release flow:
1. Stabilize release branch or main.
2. Bump version and changelog.
3. Commit and tag (`vX.Y.Z`).
4. Push commit + tag.
5. Build/deploy from tag.

## 12) Useful Inspection Commands

```bash
git show <sha>                 # commit details
git blame path/file            # line-by-line authorship
git shortlog -sn               # commits by contributor
git remote -v                  # remote URLs
git ls-files                   # tracked files
git clean -nd                  # preview untracked deletions
```

## 13) Good Practices

- Commit small, logically grouped changes.
- Write clear commit messages (`type(scope): summary`).
- Pull/fetch before starting work.
- Prefer `--force-with-lease` over `--force`.
- Never rewrite shared branch history unless team agrees.
- Protect `main` with PR reviews and CI.

## 14) Example End-to-End (Feature to Merge)

```bash
git checkout main
git pull origin main
git checkout -b feat/search-filter
# edit code
git add .
git commit -m "feat(search): add category filter"
git push -u origin feat/search-filter
# open PR, get review, merge

git checkout main
git pull origin main
git branch -d feat/search-filter
```
