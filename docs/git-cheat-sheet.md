# The Practical Git Cheat Sheet

A clean, practical Git cheat sheet — the kind you actually use daily, not the 200-command monster nobody remembers. Organized by real-world workflow.

## 1. Setup & Config (One-time stuff)

```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
git config --global init.defaultBranch main
git config --list

```

## 2. Starting a Repository

**Create new repo**

```bash
git init

```

**Clone existing repo**

```bash
git clone <repo-url>

```

## 3. Daily Workflow (Most Used Commands)

**Check status**

```bash
git status

```

**Add changes**

```bash
git add file.txt
git add .            # add everything

```

**Commit**

```bash
git commit -m "Your message"

```

**See commit history**

```bash
git log
git log --oneline --graph --decorate

```

## 4. Branching (Super Important)

**Create branch**

```bash
git branch feature-x

```

**Switch branch**

```bash
git checkout feature-x
# Modern way:
git switch feature-x

```

**Create + switch**

```bash
git checkout -b feature-x
# Modern way:
git switch -c feature-x

```

**See branches**

```bash
git branch
git branch -a

```

## 5. Merging

**Merge branch into current**

```bash
git merge feature-x

```

**Rebase (cleaner history)**

```bash
git rebase main

```

## 6. Remote (GitHub / GitLab Workflow)

**Add remote**

```bash
git remote add origin <repo-url>

```

**See remotes**

```bash
git remote -v

```

**Push**

```bash
git push origin main
git push -u origin main   # set upstream

```

**Pull latest**

```bash
git pull

```

**Fetch only**

```bash
git fetch

```

## 7. Investigating Code

**Who changed a line?**

```bash
git blame file.js

```

**Show commit details**

```bash
git show <commit-hash>

```

**See file changes**

```bash
git diff
git diff file.js

```

## 8. Undo / Fix Mistakes (Very Important)

**Unstage file**

```bash
git restore --staged file.txt

```

**Discard local changes**

```bash
git restore file.txt

```

**Reset last commit (keep changes)**

```bash
git reset --soft HEAD~1

```

**Reset last commit (remove changes)**

```bash
git reset --hard HEAD~1
# WARNING: --hard deletes changes permanently.

```

## 9. Stashing (Temporary Save)

```bash
git stash
git stash list
git stash apply
git stash pop

```

## 10. Tags (Releases)

```bash
git tag v1.0
git tag
git push origin v1.0

```

## 11. Emergency Commands

**Abort merge**

```bash
git merge --abort

```

**Abort rebase**

```bash
git rebase --abort

```

**See reflog (life saver)**

```bash
git reflog
# If you mess up badly, git reflog can rescue you.

```

---

## The 80/20 Rule (What You Actually Use Daily)

If you remember just these, you’re already 80% covered:

* `git status`
* `git add`
* `git commit`
* `git push`
* `git pull`
* `git switch -c`
* `git merge`
* `git log --oneline`
* `git reflog`
