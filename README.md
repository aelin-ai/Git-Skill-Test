# Git Rebase Skill Test

## Overview

This test evaluates your ability to use **git rebase** in realistic development scenarios, including history rewriting, conflict resolution, and safe collaboration practices.

---

## Prerequisites Setup

Before starting the test, complete the following setup steps:

### 1. Clone the Repository

```bash
git clone <REMOTE_REPOSITORY_URL>
cd <REPOSITORY_NAME>
```

### 2. Configure Git Identity

```bash
git config user.name "Your Name"
git config user.email "your.email@example.com"
```

### 3. Configure Git Hooks Path

```bash
git config core.hooksPath .githooks
```

Verify configuration:

```bash
git config --list
```

---

## Scenario: "The Messy Feature Branch"

You are part of a team working on a production application. The repository has several branches with **incomplete and minimal file states**, created during rapid experimentation.

### Repository Overview

After cloning, you will find the following branches:

* `master`

  * Stable, production-ready
  * Full project structure

* `feature/checkout`

  * Messy commit history
  * Contains full feature implementation
  * Out of date with `master`

* `feature/cart`

  * Contains only minimal files (partial implementation)
  * Missing dependencies and shared modules

* `feature/payment`

  * Based on an old commit
  * Includes experimental logic
  * Conflicts heavily with `master`

### Your Objective

You must:

* Identify which branches are safe to rebase
* Handle branches with **minimal or incomplete files**
* Rebase feature branches onto the latest `master`
* Clean up commit history where necessary
* Avoid breaking the working state of the project

---

## Tasks

### Task 1: Sync with Latest Master

Rebase your feature branch onto the latest `master`:

```bash
git checkout feature/checkout
git fetch origin
git rebase origin/master
```

---

### Task 2: Interactive Rebase (History Cleanup)

Clean up the last 6 commits:

```bash
git rebase -i HEAD~6
```

Requirements:

* Squash unnecessary commits
* Remove redundant commits
* Rewrite commit messages to follow **Conventional Commits** format

Example:

```
feat: implement checkout flow
fix: resolve payment validation bug
```

---

### Task 3: Resolve Conflicts

During rebase, conflicts will occur.

Steps:

1. Identify conflicted files:

   ```bash
   git status
   ```
2. Manually resolve conflicts in files
3. Stage resolved files:

   ```bash
   git add <file>
   ```
4. Continue rebase:

   ```bash
   git rebase --continue
   ```

If needed:

```bash
git rebase --abort
```

---

### Task 4: Validate History

Ensure the commit history is clean:

```bash
git log --oneline
```

Expected outcome:

* Minimal number of commits
* Clear, meaningful commit messages
* Linear history (no merge commits)

---

### Task 5: Force Push Safely

After rewriting history, push changes:

```bash
git push origin feature/checkout --force-with-lease
```

---

## Advanced Challenge (Optional)

### Task 6: Rebase Onto Specific Commit

Rebase your branch onto a specific commit hash from `master`:

```bash
git rebase --onto <commit-hash> <old-base>
```

Explain what this command does.

---

### Task 7: Split a Commit

During interactive rebase, split a large commit into smaller logical commits.

Hints:

```bash
git reset HEAD^
```

---

### Task 8: Recover from Mistakes

You accidentally lost commits during rebase.

Recover using:

```bash
git reflog
```

Restore previous state.

---

## Evaluation Criteria

* Proper use of rebase commands
* Clean and meaningful commit history
* Correct conflict resolution
* Safe force push usage
* Understanding of advanced rebase features

---

## Submission

Provide:

1. Final commit history (`git log --oneline` output)
2. List of commands used
3. Brief explanation of conflict resolution steps
4. Screenshot or log proving successful rebase

---

## Notes

* Do NOT use `git merge` unless explicitly instructed
* Focus on maintaining a clean, professional history
* Assume this branch will be reviewed by senior engineers
