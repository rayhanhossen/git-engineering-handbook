These are the core commands you will use in your everyday development loop, from grabbing the latest code to publishing your changes.

### 1. Getting Updates (Syncing)

Before starting new work, always ensure your local repository is up to date with the remote server.

* **`git fetch`**: Downloads new data from the remote repository but does *not* integrate it into your working files. Great for seeing what others have been working on without altering your current code.
* **`git fetch --all`**: Downloads new data from *all* configured remote repositories. This is especially useful if your project uses multiple remotes (for example, an `origin` for your fork and an `upstream` for the main open-source repository).
* **`git pull`**: Downloads new data from the remote repository and immediately merges it into your current working branch. (Essentially `git fetch` + `git merge`).
* **`git pull origin dev`**: Specifically pulls the latest commits from the `dev` branch on the `origin` remote, and merges them into whatever local branch you are currently on. This is highly useful when you are working on a feature branch and need to sync it up with the latest baseline development code.

### 2. Checking Status
* **`git status`**: Your most used command. It shows the current state of your working directory (which branch you are on, what files are modified, and what is staged for the next commit).
* **`git diff`**: Shows the exact lines of code you have changed that are *not yet staged*. 
* **`git diff --staged`**: Shows the exact lines of code you have changed that *are staged* and ready to be committed.

### 3. Making Changes (The Core Loop)
* **`git add <file-name>`**: Stages a specific modified file.
* **`git add .`**: A massive time-saver. Stages *all* modified and new files in the current directory and its subdirectories.
* **`git commit -m "Your descriptive message"`**: Wraps up all your staged changes into a new, permanent snapshot in your local history.

### 4. Branching and Context Switching
* **`git branch`**: Lists all your local branches. The branch you are currently on will be highlighted with an asterisk (`*`).
* **`git switch <branch-name>`**: Moves you to an existing branch. (Note: `git checkout <branch-name>` does the exact same thing and is widely used).
* **`git switch -c <new-branch-name>`**: Creates a brand new branch and immediately switches you to it. 

### 5. Publishing Your Work
* **`git push`**: Uploads your local commits to the remote repository (like GitHub or GitLab) so others can see and pull your work.
* **`git push -u origin <branch-name>`**: Used the very first time you push a newly created local branch to the remote server. It sets up the tracking connection.

### 6. Reviewing History
* **`git log`**: Shows a list of all commits on your current branch.
* **`git log --oneline`**: A condensed version of `git log` that shows just the commit hash and the subject line, making it much easier to scan.
