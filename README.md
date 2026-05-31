# Git & GitHub Exam Prep Guide

A comprehensive reference guide for essential Git and GitHub commands for exams.

## Table of Contents
1. [Git Setup](#git-setup)
2. [Basic Git Commands](#basic-git-commands)
3. [Branching](#branching)
4. [Commits](#commits)
5. [Undoing Changes](#undoing-changes)
6. [Remote Repositories](#remote-repositories)
7. [Merging & Rebasing](#merging--rebasing)
8. [Stashing](#stashing)
9. [GitHub Collaboration](#github-collaboration)
10. [Useful Git Tricks](#useful-git-tricks)

---

## Git Setup

### Configure Git Identity
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

### Verify Configuration
```bash
git config --list
git config user.name
```

### Set Default Branch
```bash
git config --global init.defaultBranch main
```

---

## Basic Git Commands

### Initialize Repository
```bash
git init                    # Initialize a new local repository
```

### Check Status
```bash
git status                  # Show current state of working directory
git status -s               # Short format status
```

### View Logs
```bash
git log                     # Show commit history
git log --oneline           # Condensed view (one line per commit)
git log --oneline -n 5      # Last 5 commits
git log --graph --all --decorate --oneline   # Visual branch history
```

### Staging Changes
```bash
git add <file>              # Stage specific file
git add .                   # Stage all changes
git add -A                  # Stage all changes (deleted, modified, new)
git add -p                  # Interactive staging (patch mode)
```

### Commit Changes
```bash
git commit -m "message"     # Commit with message
git commit                  # Open editor for detailed message
git commit --amend          # Modify last commit
git commit --amend --no-edit # Amend without changing message
```

### View Changes
```bash
git diff                    # Show unstaged changes
git diff --staged           # Show staged changes
git diff HEAD               # Changes since last commit
git diff <branch1> <branch2> # Compare branches
```

---

## Branching

### Create & Switch Branches
```bash
git branch                  # List local branches
git branch -a               # List all branches (local + remote)
git branch <branch-name>    # Create new branch
git checkout -b <branch-name>  # Create and switch to branch
git switch <branch-name>    # Switch to branch (newer syntax)
git switch -c <branch-name> # Create and switch (newer syntax)
```

### Delete Branches
```bash
git branch -d <branch-name>      # Delete local branch (safe)
git branch -D <branch-name>      # Force delete branch
git push origin --delete <branch-name>  # Delete remote branch
```

### Rename Branches
```bash
git branch -m <old-name> <new-name>  # Rename local branch
git push origin --delete <old-name>   # Delete old name from remote
git push -u origin <new-name>         # Push new name to remote
```

---

## Commits

### View Commit Details
```bash
git show <commit-hash>      # Show specific commit details
git show HEAD               # Show last commit
git log -p <file>           # Show commit history with changes for file
```

### Revert Commits
```bash
git revert <commit-hash>    # Create new commit undoing changes
git revert HEAD             # Revert last commit
```

### Reset Commits
```bash
git reset --soft HEAD~1     # Undo last commit, keep staged
git reset --mixed HEAD~1    # Undo last commit, unstage changes
git reset --hard HEAD~1     # Undo last commit, discard changes
git reset <file>            # Unstage file
```

---

## Undoing Changes

### Discard Working Directory Changes
```bash
git restore <file>          # Discard changes in working directory
git checkout -- <file>      # Discard changes (older syntax)
git clean -fd               # Remove untracked files and directories
```

### Restore Previous Version
```bash
git restore --source=<commit> <file>  # Restore file from specific commit
git checkout <commit> -- <file>       # Older syntax
```

---

## Remote Repositories

### Configure Remote
```bash
git remote                  # List remotes
git remote -v               # Show remote URLs
git remote add origin <url> # Add new remote
git remote remove origin    # Remove remote
git remote rename origin main-repo  # Rename remote
```

### Push & Pull
```bash
git push                    # Push to default remote/branch
git push origin <branch>    # Push to specific branch
git push -u origin <branch> # Push and set upstream
git push --all              # Push all branches
git push --tags             # Push all tags

git pull                    # Fetch and merge from remote
git pull --rebase           # Fetch and rebase instead of merge
git fetch                   # Download changes without merging
git fetch --all             # Fetch from all remotes
```

### Set Upstream
```bash
git branch -u origin/<branch>  # Set upstream for current branch
git branch --set-upstream-to=origin/<branch>  # Alternative syntax
```

---

## Merging & Rebasing

### Merge Branches
```bash
git merge <branch-name>     # Merge branch into current branch
git merge --no-ff <branch>  # Merge with merge commit
git merge --squash <branch> # Squash commits before merging
```

### Rebase
```bash
git rebase <branch>         # Rebase current branch
git rebase -i HEAD~3        # Interactive rebase last 3 commits
git rebase --continue       # Continue after resolving conflicts
git rebase --abort          # Cancel rebase
```

### Handle Conflicts
```bash
git status                  # Show conflicting files
# Edit files manually to resolve conflicts
git add <resolved-file>     # Stage resolved file
git commit                  # Commit after resolving
```

---

## Stashing

### Stash Changes
```bash
git stash                   # Stash all changes
git stash save "message"    # Stash with description
git stash list              # List all stashes
git stash show              # Show latest stash changes
git stash show stash@{n}    # Show specific stash
```

### Retrieve Stashed Changes
```bash
git stash pop               # Apply and remove latest stash
git stash pop stash@{n}     # Apply specific stash
git stash apply             # Apply without removing
git stash apply stash@{n}   # Apply specific stash without removing
git stash drop              # Delete latest stash
git stash drop stash@{n}    # Delete specific stash
git stash clear             # Delete all stashes
```

---

## GitHub Collaboration

### Fork & Clone
```bash
# Clone a repository
git clone <repository-url>          # Clone repo
git clone <url> <directory>         # Clone into specific directory
git clone --depth 1 <url>           # Shallow clone (latest version only)
```

### Pull Requests (via CLI)
```bash
# Using GitHub CLI (gh command)
gh pr create                # Create pull request interactively
gh pr create --title "Title" --body "Description"
gh pr view                  # View current PR
gh pr list                  # List open PRs
gh pr merge <pr-number>     # Merge PR
```

### Syncing with Upstream (for forks)
```bash
git remote add upstream <original-repo-url>
git fetch upstream
git merge upstream/main     # Merge upstream into your branch
git push origin main        # Push to your fork
```

---

## Useful Git Tricks

### Create Alias
```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.log-graph "log --graph --all --decorate --oneline"
```

### Check Git History of a Line
```bash
git blame <file>            # Show who changed each line
git log -L <start>,<end>:<file>  # History of specific lines
```

### Cherry Pick
```bash
git cherry-pick <commit-hash>  # Apply specific commit to current branch
git cherry-pick <hash1> <hash2>  # Apply multiple commits
```

### Tags
```bash
git tag                     # List tags
git tag <tag-name>          # Create lightweight tag
git tag -a <tag-name> -m "message"  # Annotated tag
git show <tag-name>         # Show tag details
git push origin <tag-name>  # Push specific tag
git push origin --tags      # Push all tags
git tag -d <tag-name>       # Delete local tag
git push origin --delete <tag-name>  # Delete remote tag
```

### Find Bugs
```bash
git bisect start            # Start binary search for bug
git bisect bad HEAD         # Mark current as bad
git bisect good <commit>    # Mark commit as good
git bisect reset            # End bisect
```

### Reflog (Recovery)
```bash
git reflog                  # Show reference logs (undo destructive commands)
git reflog show <branch>    # Show reflog for branch
git reset --hard HEAD@{n}   # Recover from reflog
```

---

## Key Concepts Summary

| Concept | Description |
|---------|-------------|
| **Repository** | A project folder with git history |
| **Staging Area** | Changes queued for commit |
| **Commit** | Snapshot of changes with message |
| **Branch** | Independent line of development |
| **Remote** | External repository (e.g., GitHub) |
| **Merge** | Combine branches, keeps both histories |
| **Rebase** | Replay commits on top of another branch |
| **Stash** | Temporarily save uncommitted changes |
| **Fork** | Copy of a repository you don't own |
| **Pull Request** | Propose changes to a repository |

---

## Quick Reference Cheat Sheet

```bash
# Start new project
git init
git add .
git commit -m "Initial commit"

# Work on feature
git checkout -b feature-name
git add .
git commit -m "Feature description"

# Push to GitHub
git push -u origin feature-name

# Update from remote
git pull origin main

# Merge feature into main
git checkout main
git merge feature-name
git push origin main

# Clean up
git branch -d feature-name
git push origin --delete feature-name
```

---

## Study Tips

✅ Practice commands in a test repository  
✅ Memorize common workflows (above)  
✅ Understand difference between local and remote  
✅ Know when to use merge vs rebase  
✅ Be comfortable with conflict resolution  
✅ Understand branching strategies (Git Flow, GitHub Flow)  

---

**Last Updated:** 2026-05-31  
**For:** GitHub Exams Preparation
