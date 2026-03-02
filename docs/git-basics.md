# Git Basics Guide

This guide covers the fundamental concepts, workflows, and essential commands you need to start using Git effectively. 

## 1. Core Concepts

Understanding the basic terminology is the first step to mastering Git.

* **Repository (Repo):** A directory where Git tracks all changes to your files. It contains the history of the project.
* **Commit:** A saved snapshot of your project at a specific point in time. Every commit has a unique ID (hash) and a message describing the changes.
* **Branch:** A movable pointer to a specific commit. It allows you to work on different features or fixes in isolation without affecting the main project.
* **HEAD:** A special pointer that indicates the branch or commit you are currently looking at and working on.
* **Staging Area (Index):** An intermediate holding area where you organize and format changes before officially committing them to the project history.

---

## 2. The Standard Git Workflow

To understand how files move through Git, it helps to visualize the three main states a file can reside in:

1.  **Working Directory:** Where you actively edit your files.
2.  **Staging Area:** You use `git add` to move changes here, preparing them for a commit.
3.  **Local Repository:** You use `git commit` to permanently store the staged changes in your local Git history.
4.  **Remote Repository:** You use `git push` to upload your local commits to a remote server (like GitHub, GitLab, or Bitbucket) to share with others.

---

## 3. Essential Commands

Here are the day-to-day commands you will use most often.

### Starting a Project
* **`git init`**: Turns an existing local directory into a new Git repository.
* **`git clone <url>`**: Downloads a copy of an existing remote repository to your local machine.

### Tracking and Committing Changes
* **`git status`**: Shows the state of your working directory and staging area (which files are modified, untracked, or staged).
* **`git add <file>`**: Adds a specific file to the staging area. Use `git add .` to stage all modified files in the current directory.
* **`git commit -m "Your message here"`**: Takes everything in the staging area and saves it as a new commit with a descriptive message.

### Working with Remotes
* **`git push`**: Uploads your local branch commits to the remote repository.
* **`git pull`**: Downloads new commits from the remote repository and automatically integrates them into your current local branch.

### Reviewing History
* **`git log`**: Displays the chronological commit history for the current branch.

---

## 4. Branching Basics

Branching is one of Git's most powerful features, allowing multiple people to work on a project simultaneously.

* **`git branch`**: Lists all local branches. The current branch will have an asterisk (*) next to it.
* **`git branch <branch-name>`**: Creates a new branch at the current commit.
* **`git switch <branch-name>`** (or `git checkout <branch-name>`): Moves your HEAD pointer to the specified branch, updating your working directory to match.
* **`git switch -c <branch-name>`**: A shortcut to create a new branch and switch to it immediately ( or `git checkout -b <branch-name>`).
* **`git merge <branch-name>`**: Takes the commits from the specified branch and integrates them into the branch you are *currently* on.