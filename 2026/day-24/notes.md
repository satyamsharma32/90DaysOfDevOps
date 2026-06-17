# Day 24 - Advanced Git: Merge, Rebase, Stash & Cherry Pick


# Task 1: Git Merge

## Scenario 1: Merging feature-login into main

Created a branch named `feature-login` from `main` and added multiple commits.

```bash
git switch -c feature-login
```

Made a few commits:

```bash
git add .
git commit -m "Added login page"
git commit -m "Added login validation"
```

Switched back to main and merged:

```bash
git switch main
git merge feature-login
```

### Observation

Git performed a **Fast-Forward Merge** because no new commits existed on `main` after creating `feature-login`.

---

## Scenario 2: Merging feature-signup into main

Created another branch:

```bash
git switch -c feature-signup
```

Added commits:

```bash
git commit -m "Added signup page"
git commit -m "Added signup validation"
```

Before merging, switched to main and created another commit:

```bash
git switch main
git commit -m "Updated README"
```

Merged feature-signup:

```bash
git merge feature-signup
```

### Observation

Git created a **Merge Commit** because both branches had diverged and contained different commit histories.

---

## What is a Fast-Forward Merge?

A fast-forward merge occurs when the target branch has not moved ahead since the feature branch was created.

Git simply moves the branch pointer forward without creating an extra merge commit.

### Example

```text
main
  |
A---B---C
         \
feature    D---E
```

After merge:

```text
A---B---C---D---E
                ↑
              main
```

---

## When Does Git Create a Merge Commit?

Git creates a merge commit when both branches contain unique commits.

### Example

```text
       D---E
      /
A---B---C
      \
       F---G
```

Git must combine both histories and creates a new merge commit.

---

## What is a Merge Conflict?

A merge conflict occurs when the same lines of a file are modified differently in two branches.

Git cannot automatically determine which version should be kept.

### Example

Branch A:

```text
Application Version 1.0
```

Branch B:

```text
Application Version 2.0
```

When merged, Git asks the user to resolve the conflict manually.

---

# Task 2: Git Rebase

Created a branch:

```bash
git switch -c feature-dashboard
```

Added several commits:

```bash
git commit -m "Added dashboard layout"
git commit -m "Added dashboard widgets"
git commit -m "Added charts"
```

Moved main ahead:

```bash
git switch main
git commit -m "Updated navbar"
```

Rebased feature-dashboard:

```bash
git switch feature-dashboard
git rebase main
```

---

## What Does Rebase Actually Do?

Rebase takes commits from one branch and reapplies them on top of another branch.

Instead of creating a merge commit, Git rewrites commit history to make it appear as if the work started from the latest version of the target branch.

---

## How Is History Different from a Merge?

### Merge History

```text
A---B---C------M
     \        /
      D---E--F
```

### Rebase History

```text
A---B---C---D'---E'---F'
```

The history becomes linear and easier to read.

---

## Why Should You Never Rebase Shared Commits?

Rebase changes commit hashes and rewrites history.

If other team members already pulled those commits:

* Histories diverge.
* Pull conflicts occur.
* Collaboration becomes difficult.

Therefore, only rebase commits that have not been shared with others.

---

## When Would You Use Rebase vs Merge?

### Use Rebase

* To maintain clean history.
* Before creating pull requests.
* For local feature branches.

### Use Merge

* For preserving complete project history.
* For shared branches.
* For team collaboration.

---

# Task 3: Squash Commit vs Merge Commit

Created branch:

```bash
git switch -c feature-profile
```

Added several small commits:

```bash
git commit -m "Fixed typo"
git commit -m "Updated spacing"
git commit -m "Changed formatting"
git commit -m "Updated labels"
git commit -m "Minor cleanup"
```

Merged using squash:

```bash
git switch main
git merge --squash feature-profile
git commit -m "Added profile feature"
```

---

## Observation

Although five commits existed on the feature branch, only one commit was added to main.

---

## Regular Merge Example

Created:

```bash
git switch -c feature-settings
```

Added several commits and merged normally:

```bash
git switch main
git merge feature-settings
```

All commits remained visible in history.

---

## What Does Squash Merge Do?

Squash merge combines multiple commits into a single commit before merging.

---

## When Would You Use Squash Merge?

Use squash merge when:

* Many small commits exist.
* Commit history is noisy.
* Only final functionality matters.

---

## When Would You Use Regular Merge?

Use regular merge when:

* Commit history is important.
* Team wants detailed change tracking.
* Development progress needs to remain visible.

---

## Trade-Off of Squashing

### Advantage

* Cleaner history.
* Easier to review.

### Disadvantage

* Individual commit history is lost.
* Harder to track development steps.

---

# Task 4: Git Stash

Started modifying files without committing.

Attempted to switch branches:

```bash
git switch feature-login
```

Git warned about local changes.

Saved work:

```bash
git stash
```

Switched branches successfully.

Returned later and restored changes:

```bash
git stash pop
```

---

## Multiple Stashes

Create multiple stashes:

```bash
git stash
git stash
```

List all stashes:

```bash
git stash list
```

Example output:

```text
stash@{0}
stash@{1}
stash@{2}
```

Apply a specific stash:

```bash
git stash apply stash@{1}
```

---

## Difference Between git stash pop and git stash apply

### git stash pop

```bash
git stash pop
```

* Applies changes.
* Removes stash entry.

### git stash apply

```bash
git stash apply
```

* Applies changes.
* Keeps stash entry for future use.

---

## Real-World Use of Stash

Stash is useful when:

* Working on a feature.
* An urgent production issue appears.
* Need to switch branches quickly.
* Work is incomplete and should not be committed yet.

---

# Task 5: Cherry Pick

Created branch:

```bash
git switch -c feature-hotfix
```

Added three commits:

```bash
git commit -m "Hotfix 1"
git commit -m "Hotfix 2"
git commit -m "Hotfix 3"
```

Viewed commit hashes:

```bash
git log --oneline
```

Switched to main:

```bash
git switch main
```

Cherry-picked only the second commit:

```bash
git cherry-pick <commit-hash>
```

Verified history:

```bash
git log --oneline
```

Only the selected commit appeared on main.

---

## What Does Cherry-Pick Do?

Cherry-pick copies a specific commit from one branch and applies it to another branch.

Unlike merge, it does not bring all commits from the source branch.

---

## When Would You Use Cherry-Pick?

Common scenarios:

* Applying urgent production fixes.
* Moving a single bug fix to another branch.
* Copying specific changes without merging an entire feature branch.

---

## What Can Go Wrong with Cherry-Picking?

Potential issues:

* Merge conflicts.
* Duplicate commits.
* Confusing project history.
* Missing dependent commits.

If a selected commit depends on earlier commits, cherry-picking it alone may break functionality.

---

# Summary

Today I learned:

* Fast-forward merges and merge commits.
* Merge conflicts and conflict resolution.
* Rebase and how it creates a cleaner history.
* Why rebasing shared commits is dangerous.
* Squash merging versus regular merging.
* Stashing unfinished work and restoring it later.
* Cherry-picking specific commits between branches.
* Real-world Git workflows used in DevOps and software development.

