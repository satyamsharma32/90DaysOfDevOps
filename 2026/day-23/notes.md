# Day 23 - Git Branching & Working with GitHub


### 1. What is a branch in Git?

A branch is an independent line of development in a Git repository. It allows developers to work on new features, bug fixes, or experiments without affecting the main codebase.

Each branch has its own commit history and can later be merged into another branch when the work is complete.

---

### 2. Why do we use branches instead of committing everything to main?

Branches help keep the main branch stable and production-ready.

Benefits of using branches:

* Develop features without impacting the main code.
* Test changes safely.
* Allow multiple developers to work simultaneously.
* Make code reviews and collaboration easier.
* Reduce the risk of breaking working code.

---

### 3. What is HEAD in Git?

HEAD is a pointer that refers to the currently checked-out branch or commit.

When you make a new commit, Git adds it to the branch that HEAD is pointing to.

### Example

If HEAD points to `main`:

```text
HEAD → main → latest commit
```

If you switch to `feature-1`:

```text
HEAD → feature-1 → latest commit
```

---

### 4. What happens to your files when you switch branches?

When switching branches, Git updates the working directory to match the selected branch.

* Files unique to the target branch appear.
* Files not present in the target branch disappear.
* Uncommitted changes may prevent branch switching if conflicts could occur.

This allows each branch to maintain its own version of the project.

---

# Task 2: Branching Commands - Hands-On

## List All Branches

```bash
git branch
```

Displays all local branches and highlights the current branch with `*`.

---

## Create a New Branch

```bash
git branch feature-1
```

Creates a new branch named `feature-1`.

---

## Switch to feature-1

```bash
git checkout feature-1
```

or

```bash
git switch feature-1
```

Moves HEAD to the `feature-1` branch.

---

## Create and Switch to a New Branch in One Command

```bash
git checkout -b feature-2
```

or

```bash
git switch -c feature-2
```

Creates the branch and switches to it immediately.

---

## git switch vs git checkout

### git checkout

Used for multiple purposes:

* Switch branches
* Restore files
* Checkout commits

Example:

```bash
git checkout feature-1
```

### git switch

Introduced to make branch switching simpler and safer.

Example:

```bash
git switch feature-1
```

### Difference

| git checkout                   | git switch                         |
| ------------------------------ | ---------------------------------- |
| Multi-purpose command          | Dedicated branch-switching command |
| Can be confusing for beginners | Easier and more readable           |
| Older command                  | Newer command                      |

---

## Commit on feature-1

Switch to feature-1:

```bash
git switch feature-1
```

Create or modify a file:

```bash
echo "Feature 1 work" > feature1.txt
```

Commit the changes:

```bash
git add .
git commit -m "Added feature-1 changes"
```

---

## Verify Commit Is Not Present on main

Switch back to main:

```bash
git switch main
```

Check files:

```bash
ls
```

The file created in `feature-1` should not appear because the commit exists only on that branch.

Check commit history:

```bash
git log --oneline
```

The feature branch commit will not be visible on main.

---

## Delete an Unused Branch

Delete a merged branch:

```bash
git branch -d feature-2
```

Force delete:

```bash
git branch -D feature-2
```

---

# Task 5: Clone vs Fork

## What is Clone?

A clone creates a local copy of an existing Git repository on your machine.

### Example

```bash
git clone https://github.com/example/project.git
```

This downloads the repository and its complete commit history.

---

## What is Fork?

A fork creates a personal copy of another user's repository under your GitHub account.

You can freely make changes without affecting the original repository.

Typical workflow:

1. Fork repository on GitHub.
2. Clone your fork locally.
3. Make changes.
4. Push changes to your fork.
5. Create a Pull Request.

---

## Difference Between Clone and Fork

| Clone                                   | Fork                                       |
| --------------------------------------- | ------------------------------------------ |
| Local copy of a repository              | Copy of a repository on GitHub             |
| Created using Git commands              | Created through GitHub                     |
| Does not create a new GitHub repository | Creates a separate GitHub repository       |
| Used to work locally                    | Used for contributing to external projects |

---

## When Would You Clone vs Fork?

### Clone

Use clone when:

* Working on your own repository.
* You already have write access.
* You want a local copy for development.

### Fork

Use fork when:

* Contributing to someone else's repository.
* You do not have direct write access.
* You want to propose changes through Pull Requests.

---

## How Do You Keep Your Fork in Sync with the Original Repository?

Add the original repository as an upstream remote:

```bash
git remote add upstream https://github.com/original-owner/repository.git
```

Verify remotes:

```bash
git remote -v
```

Fetch updates from upstream:

```bash
git fetch upstream
```

Merge updates into your local branch:

```bash
git merge upstream/main
```

Push updates to your fork:

```bash
git push origin main
```

This keeps your fork updated with the latest changes from the original repository.

---

# Summary

Today I learned:

* What Git branches are and why they are important.
* How to create, switch, and delete branches.
* The role of HEAD in Git.
* How branch isolation works.
* The difference between `git switch` and `git checkout`.
* The difference between cloning and forking repositories.
* How to keep a fork synchronized with the original repository.
* Essential branching commands used in real-world DevOps workflows.

