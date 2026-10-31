# Git & GitHub Cheat Sheet

## Setup
- `git config --global user.name "Your Name"` – Set username
- `git config --global user.email "you@example.com"` – Set email
- `git config --list` – View config

## Repository
- `git init` – Initialize repo
- `git clone <repo_url>` – Clone repo

## Staging & Committing
- `git status` – Check status
- `git add <file>` – Stage file
- `git add .` – Stage all
- `git commit -m "msg"` – Commit
- `git commit -am "msg"` – Stage & commit

## Branching & Merging
- `git branch` – List branches
- `git branch <name>` – Create branch
- `git checkout <name>` / `git switch <name>` – Switch branch
- `git branch -m <new-branch-name>` - Rename current branch
- `git branch -m <old-branch-name> <new-branch-name>` - Rename another branch (not checked out)
- `git checkout -b <name>` – Create & switch
- `git merge <name>` – Merge branch
- `git branch -d <name>` – Delete branch

## Undoing Changes
- `git reset <file>` – Unstage file
- `git reset --hard` – Reset to last commit
- `git revert <hash>` – Undo commit

## History & Diffs
- `git log` – View history
- `git log --oneline --graph --decorate --all` – Compact history
- `git diff` – Show changes

## Remote & GitHub
- `git remote add origin <url>` – Add remote
- `git remote -v` – View remotes
- `git push origin <branch>` – Push branch
- `git push -u origin <branch>` – Push & set upstream
- `git pull origin <branch>` – Pull changes
- `git fetch` – Fetch updates

## Forking & Contributing
1. Fork repo on GitHub
2. `git clone <your_fork_url>`
3. `git checkout -b feature`
4. Make changes, `git add .`, `git commit -m "msg"`
5. `git push origin feature`
6. Create Pull Request

## Extras
- `git stash` – Save changes
- `git stash pop` – Restore
- `git tag <tag>` – Create tag
- `git cherry-pick <hash>` – Apply commit
