While basic commands get your code from your machine to the repository, advanced commands are about managing history, debugging efficiently, and safely undoing mistakes. 

### 1. History Rewriting & Clean Up
A clean Git history is essential for code reviews and automated CI/CD pipelines. These commands help you polish your commits before sharing them.

* **`git commit --amend`**: Modifies the very last commit. Use this if you made a typo in your last commit message or forgot to stage a file, rather than creating a whole new "fix typo" commit.
* **`git rebase -i HEAD~3`** (Interactive Rebase): Opens an interactive text editor allowing you to alter the last 3 commits. You can:
    * **Squash**: Combine multiple small, messy commits into one clean commit.
    * **Reword**: Change the commit messages of older commits.
    * **Drop**: Completely delete specific commits from history.
    


### 2. Advanced Debugging
When a bug makes it into the codebase, these commands act as a forensic toolkit to figure out exactly when and how it happened.

* **`git blame <file-name>`**: Annotates each line in the given file with information from the commit that last modified it, including the author and the commit hash. It is invaluable for figuring out who to ask about a specific block of code.
* **`git bisect`**: Automates the process of finding exactly which commit introduced a bug using a binary search. You tell Git a "bad" commit (where the bug exists) and a "good" commit (where it didn't), and Git will automatically check out commits in between for you to test until you isolate the exact culprit.



### 3. Precision Context Switching
Sometimes you need to move specific pieces of code around without merging entire branches.

* **`git stash`**: Takes your uncommitted, modified files and saves them away on a temporary stack, returning your working directory to a clean state. Perfect for when you need to urgently switch branches to fix a bug but aren't ready to commit your current work.
* **`git stash pop`**: Reapplies the most recently stashed changes back onto your current working directory and removes them from the stash stack.
* **`git cherry-pick <commit-hash>`**: Takes the exact changes introduced by a single commit on another branch and applies them to your current branch. This is heavily used to backport bug fixes to older release branches.



### 4. The Ultimate Safety Net
* **`git reflog`**: Short for "reference logs". Git secretly records every single time your `HEAD` pointer moves, even if you delete a branch, do a hard reset, or mess up a rebase. If you ever "lose" code in Git, `git reflog` will give you the hash needed to restore it. It is your ultimate undo button.

### 5. Precision Staging (Patch Mode)
Often, you might make several unrelated changes in a single file before realizing you should have committed them separately. Patch mode saves you from committing everything at once.

* **`git add -p`** (or `--patch`): Instead of staging a whole file, Git walks you through every modified chunk (hunk) of code and asks if you want to stage it. This is essential for creating clean, atomic commits—for example, staging a UI fix in a React component without staging the unfinished Django API call you were also testing in the same file.

### 6. Safe Reversals (Public vs. Private Undos)
Knowing how to undo a mistake depends entirely on whether you have pushed your code to a shared repository yet.



* **`git revert <commit-hash>`**: The only safe way to undo a mistake on a shared branch (like `main` or `dev`). Instead of deleting the bad commit (which breaks history for everyone else), `git revert` creates a *brand new commit* that does the exact mathematical opposite of the target commit.
* **`git reset --hard <commit-hash>`**: A destructive command. It moves your branch pointer back to a specific commit and permanently wipes out all uncommitted changes in your working directory. Use this only for local branches that haven't been pushed.

### 7. Parallel Development (Worktrees)
Sometimes stashing isn't enough. If you need to run two branches at the exact same time, worktrees are the professional solution.



* **`git worktree add <path> <branch>`**: Allows you to check out multiple branches simultaneously in separate directories on your machine, all linked to the same local repository. This is a game-changer when you are running a heavy local environment (like an ELK stack or Dockerized load balancer) on your feature branch, but need to instantly review a teammate's PR on a separate branch without tearing down your current environment.
* **`git worktree list`**: Shows all active worktrees and their associated branches.
* **`git worktree remove <path>`**: Safely deletes the worktree directory when you are done.

### 8. Deep Code Searching (The "Pickaxe")
When `git blame` isn't enough because the code was deleted months ago, you need to search the entire repository history.

* **`git log -S "search_string"`**: Searches the entire commit history for commits that specifically added or removed a given string (like a specific variable name, a deleted function, or a lost API key). 
* **`git log --grep="search_string"`**: Searches through commit *messages* rather than the actual code changes. Useful for finding all commits related to a specific issue number (e.g., `--grep="Resolves: #42"`).