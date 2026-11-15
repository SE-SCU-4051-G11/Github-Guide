# Git Basic Commands Guide: Foundation of Version Control

> **Audience:**  
> Beginner Software Engineering Students  
> **Course:**  
> Software Engineering Laboratory / Team Project  
> **Topic:**  
> Essential Git Commands, Local Workflow, Staging, Commits, and Connecting to GitHub

---

## Table of Contents

1. [Introduction to Git](#1-introduction-to-git)
   - [What is Git?](#what-is-git)
   - [Git vs. GitHub](#git-vs-github)
   - [The Three Areas of Git](#the-three-areas-of-git)
2. [Installing and Configuring Git](#2-installing-and-configuring-git)
   - [Checking Installation](#checking-installation)
   - [Setting Your Identity](#setting-your-identity)
   - [Useful Global Settings](#useful-global-settings)
3. [Creating and Initializing a Repository](#3-creating-and-initializing-a-repository)
   - [git init](#git-init)
   - [Understanding the .git Folder](#understanding-the-git-folder)
4. [The Daily Local Workflow](#4-the-daily-local-workflow)
   - [Checking Status (`git status`)](#checking-status-git-status)
   - [Staging Changes (`git add`)](#staging-changes-git-add)
   - [Creating Commits (`git commit`)](#creating-commits-git-commit)
   - [Viewing History (`git log`)](#viewing-history-git-log)
   - [Inspecting Changes (`git diff`)](#inspecting-changes-git-diff)
5. [Working with Remote Repositories](#5-working-with-remote-repositories)
   - [Connecting to GitHub (`git remote`)](#connecting-to-github-git-remote)
   - [Pushing Changes (`git push`)](#pushing-changes-git-push)
   - [Pulling Updates (`git pull`)](#pulling-updates-git-pull)
   - [Cloning a Repository (`git clone`)](#cloning-a-repository-git-clone)
6. [Ignoring Files with .gitignore](#6-ignoring-files-with-gitignore)
7. [Undoing Mistakes (Safe Basics)](#7-undoing-mistakes-safe-basics)
8. [Hands-On Practice Scenario](#8-hands-on-practice-scenario)
9. [Quick Reference Cheat Sheet](#9-quick-reference-cheat-sheet)

---

## 1. Introduction to Git

### What is Git?

**Git** is a free and open-source **Distributed Version Control System (DVCS)**.  
It records the complete history of changes made to your project files so you can:

- Go back to any previous version
- Work on multiple features at the same time
- Collaborate with teammates without overwriting each other’s work

Git works **entirely on your local machine**. You do not need an internet connection to commit, create branches, or view history.

### Git vs. GitHub

| Concept | Description |
|---------|-------------|
| **Git** | The tool that runs on your computer and manages version history |
| **GitHub** | A cloud platform that hosts Git repositories and adds collaboration features (Issues, Pull Requests, Code Review, etc.) |

You use **Git** for all local operations. You use **GitHub** when you want to share your work with others or backup your project online.

### The Three Areas of Git

Git manages your files in three distinct areas:

```
Working Directory  →  Staging Area (Index)  →  Repository (.git)
     (your files)         (git add)              (git commit)
```

1. **Working Directory**: The actual files you edit.
2. **Staging Area**: A temporary holding area where you prepare the next commit.
3. **Repository**: The permanent history of your project stored inside the hidden `.git` folder.

Understanding these three areas is the key to using Git correctly.

---

## 2. Installing and Configuring Git

### Checking Installation

Open a terminal (or Git Bash on Windows) and run:

```bash
git --version
```

If Git is installed, you will see something like `git version 2.45.0`.

### Setting Your Identity

Every commit records the author’s name and email. These must match your GitHub account so that contributions are correctly attributed:

```bash
# Set your name and email globally (recommended)
git config --global user.name "Your Full Name or GitHub Username"
git config --global user.email "your-email@example.com"

# Verify the settings
git config --global user.name
git config --global user.email
```

### Useful Global Settings

```bash
# Set the default branch name to main
git config --global init.defaultBranch main

# Set your preferred editor (example for VS Code)
git config --global core.editor "code --wait"

# Enable colored output
git config --global color.ui auto
```

---

## 3. Creating and Initializing a Repository

### `git init`

To turn any folder into a Git repository:

```bash
mkdir my-project
cd my-project
git init
```

This creates a hidden `.git` folder that stores the entire history of the project.

### Understanding the `.git` Folder

Never manually edit files inside `.git`. Git manages this folder automatically.  
If you delete the `.git` folder, the entire history of the project is lost.

---

## 4. The Daily Local Workflow

This is the most important section of the guide. Almost every day you will repeat this cycle:

```
Edit files → git status → git add → git commit → (later) git push
```

### Checking Status (`git status`)

```bash
git status
```

This command shows:
- Which files have been modified
- Which files are staged
- Which files are untracked

**Always run `git status` before and after important actions.**

Short form:

```bash
git status -s
```

### Staging Changes (`git add`)

You must explicitly tell Git which changes you want to include in the next commit.

```bash
# Stage a single file
git add README.md

# Stage all changes in the current directory
git add .

# Stage all changes of a specific type
git add *.md
```

### Creating Commits (`git commit`)

A commit is a permanent snapshot of the staged changes.

```bash
git commit -m "Add project introduction and team members"
```

**Good commit message rules:**
- Use the imperative mood (“Add feature” not “Added feature”)
- Be specific and meaningful
- Prefer short but descriptive messages

Examples of good messages:
- `docs: write basic Git commands guide`
- `fix: correct typo in README status line`
- `chore: add .gitignore for node_modules`

### Viewing History (`git log`)

```bash
# Full history
git log

# One-line summary (very useful)
git log --oneline

# Graphical view of branches
git log --oneline --graph --all
```

### Inspecting Changes (`git diff`)

```bash
# See unstaged changes
git diff

# See staged changes (what will be committed)
git diff --staged
```

---

## 5. Working with Remote Repositories

### Connecting to GitHub (`git remote`)

After creating a repository on GitHub, connect your local project to it:

```bash
git remote add origin https://github.com/SE-SCU-4051-G11/Github-Guide.git

# Verify the connection
git remote -v
```

### Pushing Changes (`git push`)

Send your local commits to GitHub:

```bash
# First time (sets upstream tracking)
git push -u origin main

# Subsequent pushes
git push
```

### Pulling Updates (`git pull`)

Download and merge the latest changes from GitHub:

```bash
git pull origin main
```

**Best practice:** Always pull before starting new work so you stay synchronized with your teammates.

### Cloning a Repository (`git clone`)

To download an existing project (the most common way to start working on a team repository):

```bash
git clone https://github.com/SE-SCU-4051-G11/Github-Guide.git
cd Github-Guide
```

---

## 6. Ignoring Files with `.gitignore`

Create a file named `.gitignore` in the root of your project to prevent Git from tracking unwanted files:

```gitignore
# Example .gitignore
node_modules/
.env
*.log
.DS_Store
dist/
__pycache__/
```

After creating or modifying `.gitignore`, stage and commit it:

```bash
git add .gitignore
git commit -m "chore: add .gitignore"
```

---

## 7. Undoing Mistakes (Safe Basics)

| Situation | Safe Command |
|-----------|--------------|
| Unstage a file | `git restore --staged <file>` |
| Discard changes in a file (be careful!) | `git restore <file>` |
| Amend the last commit message | `git commit --amend -m "New message"` |
| See what changed in the last commit | `git show` |

> **Warning:** Never use `git reset --hard` or `git push --force` on shared branches until you fully understand the consequences. These commands can permanently delete work.

---

## 8. Hands-On Practice Scenario

Follow these steps to practice the complete basic workflow:

1. Create a new folder and initialize Git:
   ```bash
   mkdir practice-git
   cd practice-git
   git init
   ```

2. Create a `README.md` file and write a short introduction.

3. Check status, stage, and commit:
   ```bash
   git status
   git add README.md
   git commit -m "docs: initial README"
   ```

4. Make a second change, stage it, and create another commit.

5. View the history:
   ```bash
   git log --oneline
   ```

6. (Optional) Create a repository on GitHub and push your work:
   ```bash
   git remote add origin https://github.com/YOUR-USERNAME/practice-git.git
   git push -u origin main
   ```

---

## 9. Quick Reference Cheat Sheet

| Action | Command | Purpose |
|--------|---------|---------|
| **Initialize** | `git init` | Create a new local repository |
| **Clone** | `git clone <url>` | Download a remote repository |
| **Status** | `git status` | See current state of files |
| **Stage** | `git add <file>` or `git add .` | Prepare changes for commit |
| **Commit** | `git commit -m "message"` | Save a snapshot |
| **History** | `git log --oneline` | View commit history |
| **Diff** | `git diff` / `git diff --staged` | See what changed |
| **Remote** | `git remote -v` | List remote repositories |
| **Push** | `git push -u origin main` | Upload commits to GitHub |
| **Pull** | `git pull` | Download + merge latest changes |
| **Config** | `git config --global user.name "..."` | Set your identity |

---

*This guide is the foundation of the Github-Guide series.  
After mastering these commands, continue with `branching.md` and `collabration.md` to learn parallel development and team collaboration.*