# Day 25 - Git Reset vs Revert & Branching Strategies

# Task 1: Git Reset - Hands-On

## Creating Sample Commits

Created three commits:

```bash
git commit -m "Commit A"
git commit -m "Commit B"
git commit -m "Commit C"
```

Commit history:

```text
A → B → C (HEAD)
```

---

## git reset --soft

Command:

```bash
git reset --soft HEAD~1
```

### Observation

Git moved HEAD back from Commit C to Commit B.

```text
A → B (HEAD)
```

However, the changes from Commit C were preserved in the **staging area**.

Checking status:

```bash
git status
```

showed the files as staged and ready to commit.

---

## git reset --mixed

Re-created Commit C and executed:

```bash
git reset --mixed HEAD~1
```

### Observation

Git removed Commit C from history and moved HEAD back to Commit B.

```text
A → B (HEAD)
```

The changes still existed in the working directory but were no longer staged.

Checking status:

```bash
git status
```

showed modified files that needed to be added again.

---

## git reset --hard

Re-created Commit C and executed:

```bash
git reset --hard HEAD~1
```

### Observation

Git moved HEAD back to Commit B.

```text
A → B (HEAD)
```

The changes from Commit C were completely removed from:

* Commit history
* Staging area
* Working directory

This action permanently deleted uncommitted work.

---

## Difference Between --soft, --mixed, and --hard

| Option  | Commit History | Staging Area | Working Directory |
| ------- | -------------- | ------------ | ----------------- |
| --soft  | Moves back     | Preserved    | Preserved         |
| --mixed | Moves back     | Cleared      | Preserved         |
| --hard  | Moves back     | Cleared      | Deleted           |

---

## Which One Is Destructive?

### git reset --hard

This is destructive because it permanently removes changes from both the staging area and working directory.

If the commits are not recoverable through reflog, the work may be lost forever.

---

## When Would You Use Each?

### git reset --soft

Use when:

* Commit message is wrong.
* Need to combine commits.
* Want to recommit changes immediately.

### git reset --mixed

Use when:

* Need to modify staged files.
* Want to review changes before recommitting.

### git reset --hard

Use when:

* Discarding unwanted local work.
* Returning repository to a known state.
* Cleaning experimental changes.

---

## Should You Use Reset on Pushed Commits?

Generally, **No**.

Reset rewrites commit history. If commits have already been pushed and shared with other team members, resetting can create synchronization problems and force conflicts.

For shared branches, Git Revert is usually the safer choice.

---

# Task 2: Git Revert - Hands-On

Created three commits:

```bash
git commit -m "Commit X"
git commit -m "Commit Y"
git commit -m "Commit Z"
```

History:

```text
X → Y → Z (HEAD)
```

---

## Reverting Commit Y

First identified the commit hash:

```bash
git log --oneline
```

Reverted the middle commit:

```bash
git revert <commit-hash-of-Y>
```

### Observation

Git created a brand-new commit that reversed the changes introduced by Commit Y.

History became:

```text
X → Y → Z → Revert-Y
```

---

## Is Commit Y Still in History?

Yes.

Commit Y remains visible in the Git log.

Git simply adds another commit that undoes its changes.

History remains complete and traceable.

---

## How Is Revert Different From Reset?

### Reset

* Removes commits from current branch history.
* Can rewrite history.
* May be destructive.

### Revert

* Creates a new commit.
* Preserves history.
* Safely undoes previous changes.

---

## Why Is Revert Safer for Shared Branches?

Because it does not rewrite history.

Everyone working on the repository keeps the same commit history.

No force pushes are required.

No synchronization problems occur.

---

## When Would You Use Revert vs Reset?

### Use Revert

* Shared branches.
* Production branches.
* Public repositories.
* Undoing mistakes safely.

### Use Reset

* Local branches.
* Private commits.
* Cleaning up work before pushing.

---

# Task 3: Reset vs Revert Summary

| Feature                          | git reset                     | git revert                               |
| -------------------------------- | ----------------------------- | ---------------------------------------- |
| What it does                     | Moves branch pointer backward | Creates a new commit that undoes changes |
| Removes commit from history?     | Yes                           | No                                       |
| Safe for shared/pushed branches? | No                            | Yes                                      |
| Rewrites history?                | Yes                           | No                                       |
| Requires force push?             | Often                         | No                                       |
| Best used for                    | Local cleanup                 | Shared repositories                      |

---

# Branching Strategies

Large software teams use branching strategies to manage development effectively.

---

## GitHub Flow

Simple workflow:

```text
main
  |
feature branch
  |
Pull Request
  |
Merge into main
```

### Used When

* Continuous deployment.
* Small teams.
* Fast-moving projects.

---

## Git Flow

Structured workflow:

```text
main
develop
feature/*
release/*
hotfix/*
```

### Used When

* Large teams.
* Multiple releases.
* Enterprise applications.

---

## Trunk-Based Development

All developers work from a single main branch using short-lived feature branches.

### Benefits

* Faster integration.
* Reduced merge conflicts.
* Common in modern DevOps environments.

---

# Real-World DevOps Perspective

In production environments:

* Use **revert** for undoing bad deployments.
* Use **reset** only on local branches before pushing.
* Prefer short-lived feature branches.
* Merge changes through Pull Requests.
* Avoid rewriting shared history.

---

# Summary

Today I learned:

* How git reset works.
* Differences between --soft, --mixed, and --hard.
* Why git reset --hard is dangerous.
* How git revert safely undoes changes.
* When to choose reset versus revert.
* Why revert is preferred for shared repositories.
* Common branching strategies used by software teams and DevOps engineers.

