# Merging in Git

## What is a merge?

Merging means combining the changes of one branch into another branch. Usually, when our work on a separate branch is finished, we merge it into the main branch (`main`).

## Fast-forward

If the main branch has not changed since the new branch was created, Git simply moves the `main` pointer forward and does not create a new commit. The history stays linear.

## Merge commit

If both branches have new commits after they diverged, Git creates a new commit with two parents. It keeps the history of both branches.

## Difference between the two

- Fast-forward: no new commit is created and the history is linear.
- Merge commit: a new commit is created and the path of each branch stays visible in the history.

## The git merge command

First switch to the target branch, then merge the source branch into it:

```bash
git checkout main
git pull origin main
git merge docs/merging
```

To view the history:

```bash
git log --oneline --graph --all
```

## Merging through a Pull Request

GitHub offers three merge options:

- **Create a merge commit:** the full history is preserved (we use this option in this project).
- **Squash and merge:** all commits are combined into one.
- **Rebase and merge:** the commits are replayed on top of main.

## What is a conflict?

When two people change the same line of a file in two different ways, Git cannot decide which one to keep and reports a conflict. It has to be resolved manually.