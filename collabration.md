# GitHub Collaboration Guide: Mastering Team Workflows

> **Audience:** Beginner to Intermediate Software Engineering Students  
> **Course:** Software Engineering Laboratory / Team Project  
> **Topic:** GitHub Team Workflows, Cloning, Issue Tracking, Pull Requests, and Code Reviews

---

## Table of Contents
1. [Introduction to Team Collaboration on GitHub](#1-introduction-to-team-collaboration-on-github)
   - [Centralized vs. Distributed Version Control](#centralized-vs-distributed-version-control)
   - [The GitHub Collaboration Lifecycle](#the-github-collaboration-lifecycle)
   - [Team Roles & Permissions](#team-roles--permissions)
2. [Setting Up Your Local Workspace](#2-setting-up-your-local-workspace)
   - [Cloning a Repository (`git clone`)](#cloning-a-repository-git-clone)
   - [Configuring Git Identity (Name & Email)](#configuring-git-identity-name--email)
   - [Managing Remotes (`git remote -v`)](#managing-remotes-git-remote--v)
3. [Task & Project Management with GitHub Issues](#3-task--project-management-with-github-issues)
   - [What is a GitHub Issue?](#what-is-a-github-issue)
   - [Structuring an Effective Issue](#structuring-an-effective-issue)
   - [Assignees, Labels, and Milestones](#assignees-labels-and-milestones)
   - [Linking Issues to Commits and Pull Requests](#linking-issues-to-commits-and-pull-requests)
4. [Pull Requests (PRs): The Core of Collaboration](#4-pull-requests-prs-the-core-of-collaboration)
   - [What is a Pull Request?](#what-is-a-pull-request)
   - [Pushing Your Feature Branch to GitHub](#pushing-your-feature-branch-to-github)
   - [Creating a Pull Request via GitHub UI](#creating-a-pull-request-via-github-ui)
   - [Writing an Exemplary PR Description](#writing-an-exemplary-pr-description)
   - [Draft Pull Requests](#draft-pull-requests)
5. [Conducting Effective Code Reviews](#5-conducting-effective-code-reviews)
   - [Why Code Reviews Matter](#why-code-reviews-matter)
   - [Step-by-Step: How to Review a Peer's Pull Request](#step-by-step-how-to-review-a-peers-pull-request)
   - [Using GitHub's Suggestion Blocks](#using-githubs-suggestion-blocks)
   - [Review Decisions: Comment, Approve, Request Changes](#review-decisions-comment-approve-request-changes)
   - [Iterating & Addressing Review Feedback](#iterating--addressing-review-feedback)
6. [Merging Pull Requests & Post-Merge Cleanup](#6-merging-pull-requests--post-merge-cleanup)
   - [Merge Strategies Compared](#merge-strategies-compared)
   - [Deleting Remote and Local Feature Branches](#deleting-remote-and-local-feature-branches)
   - [Updating Local `main` After a Merge](#updating-local-main-after-a-merge)
7. [Team Etiquette & Best Practices for Students](#7-team-etiquette--best-practices-for-students)
   - [Keep Pull Requests Small & Focused](#keep-pull-requests-small--focused)
   - [Constructive & Empathetic Communication](#constructive--empathetic-communication)
   - [Never Force-Push to Shared Branches](#never-force-push-to-shared-branches)
   - [Protect Sensitive Data & Secrets](#protect-sensitive-data--secrets)
8. [Hands-On Team Practice Walkthrough](#8-hands-on-team-practice-walkthrough)
9. [Quick Reference Cheat Sheet](#9-quick-reference-cheat-sheet)

---

## 1. Introduction to Team Collaboration on GitHub

Software development is fundamentally a collaborative discipline. In real-world software engineering, code is written, reviewed, tested, and maintained by cross-functional teams rather than isolated individuals. 

While **Git** is the local distributed version control engine running on your computer, **GitHub** is the cloud-based platform that facilitates team collaboration, code hosting, asynchronous discussions, automated CI/CD pipelines, and project tracking.

### Centralized vs. Distributed Version Control
Git is a **Distributed Version Control System (DVCS)**:
- Every member has a full copy of the entire repository history locally on their machine.
- You can commit, create branches, inspect logs, and diff code completely offline.
- GitHub acts as the central hub (the `origin` remote) where all teammates synchronize and integrate their work.

### The GitHub Collaboration Lifecycle
A professional team workflow follows an orderly, repeatable cycle:

```
┌──────────────────────────────────────────────────────────────────┐
│                   GitHub Collaboration Loop                      │
└──────────────────────────────────────────────────────────────────┘
   1. Issue Created       --> Define requirements and assign task
          │
          ▼
   2. Branch Created      --> Create isolated feature branch locally
          │
          ▼
   3. Commits Authored    --> Commit incremental, meaningful changes
          │
          ▼
   4. Branch Pushed       --> Push feature branch to GitHub remote
          │
          ▼
   5. Pull Request Opened --> Propose changes and link to the Issue
          │
          ▼
   6. Code Review         --> Teammates inspect diffs, comment, approve
          │
          ▼
   7. Merged into main    --> Feature lands in main; branch deleted
```

### Team Roles & Permissions
In student and professional GitHub repositories, team members typically share permissions:
- **Repository Admin / Scrum Master:** Manages repository settings, branch protection rules, collaborator invitations, and issue milestones.
- **Collaborators / Developers:** Clone the repository, create feature branches, author commits, submit PRs, and review peers' code.
- **Reviewers:** Team members assigned to inspect a teammate's PR, run tests locally if needed, suggest improvements, and formally approve the changes.

---

## 2. Setting Up Your Local Workspace

Before you can contribute to a team project, you must set up your local development environment.

### Cloning a Repository (`git clone`)
Cloning downloads a full copy of a remote GitHub repository to your local machine, including all branches, files, and commit history.

```bash
# Clone using HTTPS (Simple & standard)
git clone https://github.com/SE-SCU-4051-G11/Github-Guide.git

# Or clone using SSH (Recommended for passwordless, key-based authentication)
git clone git@github.com:SE-SCU-4051-G11/Github-Guide.git
```

After cloning, navigate into the project directory:
```bash
cd Github-Guide
```

### Configuring Git Identity (Name & Email)
Every commit in Git records the author's name and email address. **Your email must match your GitHub account email** so that GitHub properly attributes your contributions to your profile graph:

```bash
# Set your name and email globally (for all projects on your computer):
git config --global user.name "Your GitHub Username or Real Name"
git config --global user.email "your-email-registered-on-github@example.com"

# Or configure it locally for only this specific repository:
git config user.name "HA-ir"
git config user.email "hosienamiri2018@gmail.com"

# Verify your configuration:
git config user.name
git config user.email
```

### Managing Remotes (`git remote -v`)
When you clone a repository, Git automatically names the remote server `origin`. You can inspect configured remote URLs:

```bash
git remote -v
```

Expected output:
```text
origin  https://github.com/SE-SCU-4051-G11/Github-Guide.git (fetch)
origin  https://github.com/SE-SCU-4051-G11/Github-Guide.git (push)
```

If your team uses an upstream repository (e.g., in a fork-and-pull model), you can add an `upstream` remote:
```bash
git remote add upstream https://github.com/Original-Org/Original-Repo.git
```

---

## 3. Task & Project Management with GitHub Issues

Effective teams never write code without a clear purpose. **GitHub Issues** serve as the single source of truth for planning, tracking bugs, breaking down user stories, and allocating work.

### What is a GitHub Issue?
An Issue is a tracked ticket in your repository used to discuss ideas, report defects, or outline project milestones. In agile methodologies (such as Scrum), Issues often correspond to **Product Backlog Items (PBIs)**, **User Stories**, or **Technical Tasks**.

### Structuring an Effective Issue
A well-written Issue ensures all team members understand the requirements and the exact definition of "done".

**Recommended Issue Template:**
```markdown
## Description
A concise summary of the feature, enhancement, or bug being addressed.

## Acceptance Criteria
- [ ] Criterion 1 (e.g., Guide covers git switch and git checkout)
- [ ] Criterion 2 (e.g., Practical code examples included for each command)
- [ ] Criterion 3 (e.g., Passes peer review without outstanding change requests)

## Assignee
@Username of the team member responsible for this deliverable.
```

### Assignees, Labels, and Milestones
- **Assignees:** Assigning an Issue explicitly communicates accountability. In team projects, assign 1–2 developers per issue to prevent redundant or conflicting work.
- **Labels:** Color-coded tags that categorize issues (e.g., `bug`, `documentation`, `enhancement`, `help wanted`, `good first issue`).
- **Milestones:** Group related issues into scheduled sprints or deadlines (e.g., `Sprint 1 - Base Guide Structure`, `Release v1.0`).

### Linking Issues to Commits and Pull Requests
GitHub allows you to link commits and Pull Requests directly to Issues using special keywords. When the Pull Request is merged into `main`, the referenced Issue will automatically close!

**Supported Closing Keywords:**
- `close`, `closes`, `closed`
- `fix`, `fixes`, `fixed`
- `resolve`, `resolves`, `resolved`

**Example in a commit message:**
```bash
git commit -m "docs(collaboration): outline team workflows (fixes #5)"
```

**Example in a Pull Request description:**
```markdown
## Summary
This Pull Request writes the complete collaboration guide for students.

Closes #5
```

---

## 4. Pull Requests (PRs): The Core of Collaboration

### What is a Pull Request?
A **Pull Request (PR)** is a mechanism on GitHub where a developer asks the team to "pull" changes from their feature branch into the target base branch (typically `main`). 

A Pull Request is not just a merge proposal; it is a **collaborative workspace** that displays:
- The full list of commits.
- A visual diff showing every line added, modified, or deleted.
- Continuous Integration (CI) build and test results.
- An interactive discussion thread for peer feedback.

### Pushing Your Feature Branch to GitHub
Before you can open a PR, your local commits must be pushed to GitHub:

```bash
# Push your branch and configure upstream tracking (-u)
git push -u origin feature/collaboration-guide
```

Once pushed, GitHub outputs a direct link in your terminal to open a Pull Request.

### Creating a Pull Request via GitHub UI
1. Navigate to your repository on GitHub (`https://github.com/owner/repo`).
2. GitHub will typically show a yellow banner: **"Compare & pull request"**. Click it.
3. If the banner is not present:
   - Click the **Pull requests** tab.
   - Click the green **New pull request** button.
   - Set **base:** `main` and **compare:** `feature/collaboration-guide`.
4. Ensure the diff shows only your intended changes and says **"Able to merge"**.

### Writing an Exemplary PR Description
Reviewers should never have to guess what your PR does. A good description provides immediate context:

```markdown
## Overview
Comprehensive guide covering team collaboration on GitHub, including cloning, issue tracking, PR creation, code reviews, and merge strategies.

## Changes Made
- Documented cloning and local identity configuration.
- Added GitHub Issues guidelines with markdown task lists.
- Outlined step-by-step Pull Request creation and code review etiquette.
- Detailed merge methods (Merge Commit vs. Squash vs. Rebase).

## Related Issue
Closes #5

## Checklist
- [x] Tested all command examples locally.
- [x] Spell-checked and verified markdown formatting.
- [x] Includes practical code snippets and ASCII diagrams.
```

### Draft Pull Requests
If you are still working on a feature but want early feedback from teammates or want to run CI tests without accidentally triggering a merge, create a **Draft Pull Request**:
- Click the dropdown arrow next to **Create pull request** and select **Create draft pull request**.
- Draft PRs cannot be merged until you click **Ready for review**.

---

## 5. Conducting Effective Code Reviews

In software engineering, peer code review is the single most effective practice for catching defects early, maintaining architectural consistency, and sharing knowledge across the team.

### Why Code Reviews Matter
- **Defect Detection:** Finding bugs before code hits production.
- **Knowledge Sharing:** Helping teammates learn new patterns, commands, and conventions.
- **Code Consistency:** Ensuring uniform naming, style, and documentation across the codebase.
- **Shared Ownership:** The entire team becomes responsible for the health of the codebase.

### Step-by-Step: How to Review a Peer's Pull Request
1. Open the Pull Request on GitHub.
2. Read the **Conversation** tab to understand the author's summary and related issues.
3. Switch to the **Files changed** tab to inspect the diff:
   - Green lines with `+` indicate additions.
   - Red lines with `-` indicate deletions.
4. Hover over any specific line of code and click the blue **`+`** icon to start an inline comment.
5. Click **Start a review** for your first comment, then continue adding comments across the diff.
6. Once finished, click **Review changes** at the top right, write an overall summary, and select a verdict.

### Using GitHub's Suggestion Blocks
Rather than describing a code fix in words, you can propose the exact replacement code directly in the diff!

1. Select a line in the diff.
2. In the comment box, click the **Insert a suggestion** button (or write a ````suggestion ```` code block).
3. Modify the code inside the block:
   ````markdown
   ```suggestion
   git switch -c feature/new-task
   ```
   Prefer using `git switch -c` here as it is the modern standard since Git 2.23.
   ````
4. The PR author can click **Commit suggestion** directly in GitHub to apply your fix with one click!

### Review Decisions: Comment, Approve, Request Changes
GitHub offers three review options:
- **Comment:** Submit general notes or ask clarifying questions without giving an explicit approval or blocking the merge.
- **Approve:** Confirm that the code meets all quality criteria, has been tested, and is ready to merge into `main`.
- **Request changes:** Indicate critical issues or bugs that **must** be resolved before the PR can be merged.

### Iterating & Addressing Review Feedback
Receiving critique is normal and constructive:
1. Make the requested adjustments in your local branch.
2. Commit your changes:
   ```bash
   git add <modified-files>
   git commit -m "refactor: address review comments on PR #5"
   ```
3. Push to the same branch:
   ```bash
   git push origin feature/collaboration-guide
   ```
4. GitHub automatically updates the open Pull Request with your new commits and resolves addressed conversation threads!

---

## 6. Merging Pull Requests & Post-Merge Cleanup

Once a Pull Request is approved and passes all CI status checks, it can be merged into `main`.

### Merge Strategies Compared

GitHub provides three ways to integrate a PR:

| Strategy | Git Command Under the Hood | When to Use | Commit History Effect |
| :--- | :--- | :--- | :--- |
| **Create a merge commit** | `git merge --no-ff` | Default for large features and milestone branches | Preserves every individual commit plus creates a dedicated merge commit. Full historical detail. |
| **Squash and merge** | `git merge --squash` | Recommended for small feature branches or messy commit histories | Combines all branch commits into a single clean commit on `main`. Keeps `main` history strictly linear. |
| **Rebase and merge** | `git rebase` | When the team enforces a strictly linear commit history | Applies all branch commits directly onto the tip of `main` without a merge commit. |

```
Merge Commit (--no-ff):
main:    A --- B ------- M (Merge commit)
                \       /
feature:         C --- D

Squash and Merge:
main:    A --- B --- CD (Single squashed commit)

Rebase and Merge:
main:    A --- B --- C' --- D' (Commits re-applied linearly)
```

### Deleting Remote and Local Feature Branches
Once merged, the branch has served its purpose and should be pruned:
1. On GitHub: Click the **Delete branch** button on the merged PR page.
2. On your local machine:
   ```bash
   # Switch to main
   git switch main
   
   # Delete the local feature branch
   git branch -d feature/collaboration-guide
   
   # Prune deleted remote branches from your local tracking cache
   git fetch --prune
   ```

### Updating Local `main` After a Merge
Every team member should regularly pull the latest `main` into their local clone:
```bash
git switch main
git pull origin main
```

---

## 7. Team Etiquette & Best Practices for Students

### Keep Pull Requests Small & Focused
- **The Golden Rule:** A Pull Request should solve **one specific problem**.
- Large PRs (+500 lines) are exhausting to review, take days to approve, and hide bugs. Small PRs (<150 lines) are reviewed and merged quickly.
- If a task is huge, break it down into smaller sub-tasks and sequential PRs.

### Constructive & Empathetic Communication
- **Praise good work:** If a teammate used a clever solution or wrote great documentation, leave a thumbs up or compliment.
- **Focus on the code, not the person:** Say *"Consider renaming this function to clarify its output"* instead of *"You named this poorly"*.
- **Explain the reasoning:** Rather than saying *"Change this"*, explain *"Using `git switch` is recommended here because `git checkout` is legacy and overloaded"*.

### Never Force-Push to Shared Branches
Commands like `git push --force` overwrite history on the remote server. If multiple people are collaborating on the same branch, a force push can wipe out a teammate's commits. Use `--force-with-lease` only if strictly necessary on personal branches, and never on `main`.

### Protect Sensitive Data & Secrets
Never commit API keys, database passwords, or personal credentials. Add configuration files and `.env` files to `.gitignore` before making your initial commits.

---

## 8. Hands-On Team Practice Walkthrough

Here is a full real-world scenario of two students collaborating on a project:

### Scenario: Student A and Student B
1. **Scrum Master / Lead** creates Issue #5 on GitHub: *"Write collaboration.md guide"*, assigns `@HA-ir`.
2. **Student A (Assignee)** clones the repo and creates a branch:
   ```bash
   git switch -c feature/collaboration-guide
   ```
3. **Student A** writes the guide, makes incremental commits, and pushes:
   ```bash
   git add collaboration.md
   git commit -m "docs: write comprehensive collaboration guide (closes #5)"
   git push -u origin feature/collaboration-guide
   ```
4. **Student A** opens a Pull Request on GitHub, linking Issue #5.
5. **Student B (Reviewer)** opens the PR, inspects the diff, leaves a suggestion, and approves.
6. **Student A** applies the suggestion and pushes.
7. **Student B** clicks **Confirm merge**.
8. Both students update their local `main`:
   ```bash
   git switch main
   git pull origin main
   ```

---

## 9. Quick Reference Cheat Sheet

| Action | Command | Purpose |
| :--- | :--- | :--- |
| **Clone** | `git clone <url>` | Download remote repo to local machine |
| **Check Remotes** | `git remote -v` | Display remote repository URLs |
| **Create Branch** | `git switch -c <name>` | Create & switch to a new feature branch |
| **Stage & Commit** | `git add <file> && git commit -m "<msg>"` | Record snapshot with descriptive message |
| **Push Branch** | `git push -u origin <name>` | Publish local branch to GitHub |
| **Pull Updates** | `git pull origin main` | Fetch and merge latest main branch |
| **Prune Stale Refs** | `git fetch --prune` | Clean up deleted remote branch references |
| **Delete Local Branch** | `git branch -d <name>` | Safely delete merged local branch |
| **Delete Remote Branch** | `git push origin -d <name>` | Delete branch from GitHub |

---
*Created as part of the Software Engineering Git Guide Series for SCU.*
