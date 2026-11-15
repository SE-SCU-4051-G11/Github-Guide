# Git Branching Guide: Mastering Parallel Development

> **Audience:** Beginner to Intermediate Software Engineering Students  
> **Course:** Software Engineering Laboratory / Team Project  
> **Topic:** Branching Concepts, Rationale, and Mechanics in Git

---

## Table of Contents
1. [Introduction to Branching](#1-introduction-to-branching)
   - [What is a Branch?](#what-is-a-branch)
   - [How Git Implements Branches Under the Hood](#how-git-implements-branches-under-the-hood)
   - [Real-World Analogy](#real-world-analogy)
2. [Why Direct Commits to the `main` Branch Are Forbidden](#2-why-direct-commits-to-the-main-branch-are-forbidden)
   - [Production Stability & Code Integrity](#production-stability--code-integrity)
   - [Enabling Peer Code Reviews (Pull Requests)](#enabling-peer-code-reviews-pull-requests)
   - [Parallel Team Workflows & Isolation](#parallel-team-workflows--isolation)
   - [Continuous Integration & Automated Testing](#continuous-integration--automated-testing)
   - [Effortless Rollback & Traceability](#effortless-rollback--traceability)
3. [Visualizing Git Branches](#3-visualizing-git-branches)
   - [Linear History vs. Branching History](#linear-history-vs-branching-history)
   - [The Role of `HEAD`](#the-role-of-head)
4. [Essential Branching Commands & Operations](#4-essential-branching-commands--operations)
   - [Creating Branches (`git branch`)](#creating-branches-git-branch)
   - [Listing & Inspecting Branches (`git branch -a`, `-v`)](#listing--inspecting-branches-git-branch--a--v)
   - [Switching Branches: The Legacy Way vs. The Modern Way](#switching-branches-the-legacy-way-vs-the-modern-way)
     - [The Legacy Way: `git checkout`](#the-legacy-way-git-checkout)
     - [The Modern Way: `git switch` (Git 2.23+)](#the-modern-way-git-switch-git-223)
   - [Creating and Switching in One Step](#creating-and-switching-in-one-step)
   - [Renaming Branches (`git branch -m`)](#renaming-branches-git-branch--m)
   - [Deleting Branches (Local & Remote)](#deleting-branches-local--remote)
5. [Team Branching Conventions & Strategies](#5-team-branching-conventions--strategies)
   - [Branch Naming Standards](#branch-naming-standards)
   - [Feature Branch Workflow](#feature-branch-workflow)
6. [Step-by-Step Hands-on Practice Scenario](#6-step-by-step-hands-on-practice-scenario)
   - [Phase 1: Syncing with Upstream](#phase-1-syncing-with-upstream)
   - [Phase 2: Branch Creation and Work](#phase-2-branch-creation-and-work)
   - [Phase 3: Making Meaningful Commits](#phase-3-making-meaningful-commits)
   - [Phase 4: Publishing the Branch](#phase-4-publishing-the-branch)
7. [Common Beginner Pitfalls & Troubleshooting](#7-common-beginner-pitfalls--troubleshooting)
   - [Pitfall 1: Uncommitted Changes Blocking a Branch Switch](#pitfall-1-uncommitted-changes-blocking-a-branch-switch)
   - [Pitfall 2: Accidental Commits on `main`](#pitfall-2-accidental-commits-on-main)
   - [Pitfall 3: Detached HEAD State](#pitfall-3-detached-head-state)
8. [Quick Reference Cheat Sheet](#8-quick-reference-cheat-sheet)

---

## 1. Introduction to Branching

### What is a Branch?
In version control systems, a **branch** represents an independent line of development. Think of it as a separate workspace diverged from the primary codebase, allowing you to develop new features, fix bugs, or experiment freely without affecting the stable, working version of your software.

When multiple developers collaborate on a single repository, working directly on the same code line leads to constant friction, broken builds, and overwrites. Branching provides isolated sandboxes where each developer or sub-team can work independently.

### How Git Implements Branches Under the Hood
Unlike older version control systems (such as SVN or CVS) where creating a branch meant copying the entire directory structure (a slow and storage-heavy operation), **Git branches are remarkably lightweight**.

In Git:
- A commit is a snapshot of your repository along with metadata (author, timestamp, commit message, and pointer to parent commit(s)).
- A **branch is simply a lightweight, movable pointer to a specific commit hash** (a 40-character SHA-1/SHA-256 string).
- Creating a branch consumes virtually zero disk space (only 41 bytes for the pointer file inside `.git/refs/heads/`) and happens almost instantaneously.

### Real-World Analogy
Imagine writing a book with a team of co-authors:
- The **`main` branch** is the published, printed edition in the bookstore. Readers expect it to be completely free of typos, missing chapters, or draft notes.
- If you want to draft a new chapter or rewrite an ending, you don't edit the bookstore copies directly. Instead, you photocopy the latest approved chapter onto a scratchpad (create a **feature branch**).
- You write, edit, and experiment on your scratchpad (make **commits**).
- Once the chapter is polished, you invite your editor and co-authors to review your draft (open a **Pull Request**).
- After their review and approval, your new chapter is officially bound into the manuscript (merged into **`main`**).

---

## 2. Why Direct Commits to the `main` Branch Are Forbidden

In professional software engineering teams and academic collaborative projects alike, **pushing or committing directly to the `main` branch is strictly prohibited**. Here are the core reasons:

```
[STRICT RULE]
❌ NO DIRECT COMMITS TO MAIN:
   developer -> (direct commit / push) -> [main] (Risky & Prohibited!)

✅ CORRECT WORKFLOW:
   developer -> [feature branch] -> [Pull Request] -> [Peer Review] -> [Merge to main]
```

### Production Stability & Code Integrity
The `main` branch represents deployable, production-ready software. If developers commit unfinished or untested code directly to `main`, any other teammate pulling from `main` immediately inherits broken code, blocking the entire team from working or compiling the project.

### Enabling Peer Code Reviews (Pull Requests)
Quality software is a team product. By requiring changes to live on an isolated branch, teammates can review the diffs, verify logic, check edge cases, and suggest improvements through a Pull Request before the code enters the shared baseline.

### Parallel Team Workflows & Isolation
In a team of 3 to 10 engineers, everyone works on different issues concurrently:
- Developer A develops authentication.
- Developer B fixes a database query.
- Developer C documents the API.
If all three work directly on `main`, their half-finished edits will clash constantly. Branching isolates their work until each task is fully done and tested.

### Continuous Integration & Automated Testing
Modern software projects utilize CI pipelines (such as GitHub Actions). When a branch is pushed or a PR is opened, automated tests, linters, and security checks run automatically. If a test fails, the branch is flagged, preventing bad code from ever contaminating `main`.

### Effortless Rollback & Traceability
If an experimental feature proves unfeasible or unwanted, abandoning or deleting a branch is as simple as running a single command. The `main` branch history remains clean, pristine, and linear.

---

## 3. Visualizing Git Branches

### Linear History vs. Branching History

Before branching, history is a straight sequence of commits:

```
commit C1 --------> commit C2 --------> commit C3 [main, HEAD]
```

When you create a feature branch named `feature/login` from commit `C3` and add new commits, the history diverges:

```
                  commit C4 --------> commit C5 [feature/login, HEAD]
                 /
commit C1 ---> C2 ---> C3 [main]
```

- Commit `C3` is the common ancestor (base).
- `main` remains cleanly parked at `C3`.
- `feature/login` moves forward to `C4` and then `C5`.
- Teammates working on `main` are completely unaffected by changes in `C4` and `C5`.

### The Role of `HEAD`
In Git, `HEAD` is a special pointer that tells Git **which branch (and commit) your working directory currently reflects**.

When you run:
```bash
git branch
```
Git inspects `HEAD` to display an asterisk `*` next to your active branch:

```text
* feature/login   <-- HEAD points here
  main
```

When `HEAD` points to a branch, any new commit you create moves that branch pointer forward, while `HEAD` stays attached to the branch tip.

---

## 4. Essential Branching Commands & Operations

### Creating Branches (`git branch`)
To create a new branch pointing to the current commit without immediately switching to it:

```bash
git branch <branch-name>
```

**Example:**
```bash
# Creates a branch called 'feature/student-profile' pointing to HEAD
git branch feature/student-profile
```

### Listing & Inspecting Branches (`git branch -a`, `-v`)
Git offers several flags to inspect local and remote branches:

```bash
# List local branches (* indicates the current active branch)
git branch

# List all branches including remote-tracking branches
git branch -a

# List branches with their latest commit hash and commit subject
git branch -v

# List branches that have already been merged into the current branch
git branch --merged

# List branches that still have unmerged changes
git branch --no-merged
```

Sample output:
```text
  main                   e55ffcf Initial commit
* feature/branching-guide 625a7c4 docs(branching): introduce core concepts
  remotes/origin/main    e55ffcf Initial commit
```

### Switching Branches: The Legacy Way vs. The Modern Way

#### The Legacy Way: `git checkout`
Historically, `git checkout` was used for multiple unrelated operations: switching branches, creating branches, checking out individual files from older commits, and discarding working directory changes. Because overloaded commands cause student confusion, Git introduced dedicated commands in version 2.23+.

```bash
# Switch to an existing branch
git checkout <branch-name>
```

#### The Modern Way: `git switch` (Git 2.23+)
To improve user experience and clarity, Git 2.23 introduced `git switch` specifically dedicated to navigating branches:

```bash
# Switch to an existing branch (modern syntax)
git switch <branch-name>
```

**Why prefer `git switch`?**
- Safer: `git switch` cannot accidentally overwrite or discard files like `git checkout -- <file>` could.
- Clear intent: Its only job is switching and creating branches.

### Creating and Switching in One Step
In daily development, developers rarely create a branch without wanting to work on it immediately. You can create and switch in a single command:

**Modern syntax (Recommended):**
```bash
git switch -c <branch-name>
```
*(The `-c` flag stands for `--create`.)*

**Classic syntax:**
```bash
git checkout -b <branch-name>
```

**Example:**
```bash
git switch -c feature/export-pdf
# Output: Switched to a new branch 'feature/export-pdf'
```

### Renaming Branches (`git branch -m`)
If you made a typo in your branch name or need to update it to follow team conventions:

```bash
# Rename the currently active branch
git branch -m <new-branch-name>

# Rename a specific branch from anywhere
git branch -m <old-branch-name> <new-branch-name>
```

### Deleting Branches (Local & Remote)

#### Safe Deletion (Local)
Git protects you from accidentally losing unmerged work. The `-d` (lowercase) flag only deletes the branch if all of its commits have already been merged upstream:

```bash
git branch -d <branch-name>
```

#### Force Deletion (Local)
If a feature branch was an experiment you intentionally want to discard, `-d` will warn you and refuse to delete it. Use `-D` (uppercase) to force deletion:

```bash
git branch -D <branch-name>
```

#### Deleting a Remote Branch
When a Pull Request has merged on GitHub, the remote branch should be deleted to prevent repository clutter:

```bash
# Modern syntax
git push origin --delete <branch-name>

# Alternative legacy shorthand
git push origin :<branch-name>
```

---

## 5. Team Branching Conventions & Strategies

### Branch Naming Standards
Consistent branch naming keeps large team projects readable and organized. Teams prefix branch names with the type of work being performed:

| Prefix | Usage | Example |
| :--- | :--- | :--- |
| `feature/` | New features or enhancements | `feature/oauth2-login` |
| `bugfix/` | Fixing a bug reported in development | `bugfix/null-pointer-student-id` |
| `hotfix/` | Urgent fixes applied directly to production | `hotfix/security-token-leak` |
| `docs/` | Documentation additions or updates | `docs/branching-guide` |
| `refactor/` | Code refactoring without changing functionality | `refactor/database-queries` |
| `test/` | Adding or fixing test suites | `test/auth-unit-tests` |

> **Pro Tip:** Include the GitHub Issue number in the branch name for automatic traceability:  
> `feature/issue-4-branching-guide` or `docs/4-branching`

### Feature Branch Workflow
In student and enterprise teams alike, the **Feature Branch Workflow** is standard practice:
1. `main` is always stable and ready for deployment.
2. Every new feature or bugfix lives in its own dedicated branch.
3. Developers push their feature branch to GitHub and create a Pull Request.
4. Teammates review the code, suggest changes, and approve.
5. The feature branch is merged into `main`, and the feature branch is deleted.

```
       [issue created]
             │
             ▼
      git switch -c feature/auth
             │
             ▼
   [make multiple commits]
             │
             ▼
      git push origin feature/auth
             │
             ▼
       [open Pull Request]
             │
             ▼
   [peer review & approval]
             │
             ▼
       [merge into main]
```

---

## 6. Step-by-Step Hands-on Practice Scenario

Follow this walkthrough to experience the complete branching lifecycle:

### Phase 1: Syncing with Upstream
Always make sure your local `main` has the latest commits from your teammates before branching:

```bash
# 1. Switch to main
git switch main

# 2. Fetch and pull latest changes
git pull origin main
```

### Phase 2: Branch Creation and Work
Create a dedicated branch for your task:

```bash
# 3. Create and switch to your feature branch
git switch -c feature/calculator-ui

# 4. Confirm you are on the new branch
git status
```

### Phase 3: Making Meaningful Commits
Do your work incrementally. A good rule of thumb is **one logical change per commit**:

```bash
# 5. Create or modify your code files
# (e.g., editing calculator.py)

# 6. Check the diff of your changes
git diff

# 7. Stage and commit the first logical milestone
git add calculator.py
git commit -m "feat(calc): implement basic arithmetic operators"

# 8. Make a second modification (e.g., adding input validation)
git add calculator.py
git commit -m "feat(calc): add zero-division error handling"
```

### Phase 4: Publishing the Branch
Push your branch to GitHub so your team can review your work:

```bash
# 9. Push to remote with upstream tracking (-u)
git push -u origin feature/calculator-ui
```
*Note: The `-u` (or `--set-upstream`) flag links your local branch to the remote branch so future pushes/pulls only require `git push` or `git pull`.*

---

## 7. Common Beginner Pitfalls & Troubleshooting

### Pitfall 1: Uncommitted Changes Blocking a Branch Switch
**Symptom:** You try to switch branches, but Git throws an error:
```text
error: Your local changes to the following files would be overwritten by checkout:
    app.js
Please commit your changes or stash them before you switch branches.
```

**Solution:**
You have two safe options:
1. **Commit your changes:**
   ```bash
   git add app.js
   git commit -m "wip: temporary progress on app"
   git switch target-branch
   ```
2. **Stash your changes (shelve them temporarily):**
   ```bash
   # Save changes to stash
   git stash
   
   # Switch to the other branch and do what you need
   git switch target-branch
   
   # When you return to your branch, restore your changes:
   git switch feature-branch
   git stash pop
   ```

### Pitfall 2: Accidental Commits on `main`
**Symptom:** You made 2 commits directly on `main` instead of creating a feature branch first!

**Solution (Before pushing to remote):**
```bash
# 1. Create a new branch pointing to your current commits
git branch feature/my-saved-work

# 2. Reset local main back by 2 commits to match origin/main
git reset --hard origin/main

# 3. Switch to your new branch where your commits are safely preserved
git switch feature/my-saved-work
```

### Pitfall 3: Detached HEAD State
**Symptom:** Git displays:
```text
You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.
```
This happens when you check out a specific commit hash rather than a branch name.

**Solution:**
If you made commits while in detached HEAD state that you want to keep, create a new branch immediately:
```bash
git switch -c recovered-work
```
If you just want to return to safety:
```bash
git switch main
```

---

## 8. Quick Reference Cheat Sheet

| Task | Modern Command (Git 2.23+) | Classic Command |
| :--- | :--- | :--- |
| Create branch | `git branch <name>` | `git branch <name>` |
| Switch branch | `git switch <name>` | `git checkout <name>` |
| Create & switch | `git switch -c <name>` | `git checkout -b <name>` |
| List local branches | `git branch` | `git branch` |
| List all (incl. remote) | `git branch -a` | `git branch -a` |
| Rename branch | `git branch -m <old> <new>` | `git branch -m <old> <new>` |
| Delete merged branch | `git branch -d <name>` | `git branch -d <name>` |
| Force delete branch | `git branch -D <name>` | `git branch -D <name>` |
| Delete remote branch | `git push origin -d <name>` | `git push origin :<name>` |
| Stash uncommitted work | `git stash` | `git stash` |
| Restore stashed work | `git stash pop` | `git stash pop` |

---
*Created as part of the Software Engineering Git Guide Series for SCU.*
