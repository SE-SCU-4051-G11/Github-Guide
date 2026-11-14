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
