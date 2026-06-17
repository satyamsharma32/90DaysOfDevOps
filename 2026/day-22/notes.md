# Day 22 - Introduction to Git: Understanding the Git Workflow and commands 

## 1. What is the difference between `git add` and `git commit`?

`git add` is used to move changes from the working directory to the staging area. It tells Git which changes should be included in the next commit.

`git commit` saves the staged changes into the local Git repository with a message describing what was changed. A commit acts like a snapshot of the project at a specific point in time.

### Example

```bash
git add file.txt
git commit -m "Added new feature"
```

---

## 2. What does the staging area do? Why doesn't Git just commit directly?

The staging area is an intermediate layer between the working directory and the repository. It allows developers to review and select specific changes before creating a commit.

Git does not commit directly because developers may not want to save every modification at once. The staging area provides flexibility by allowing only the required files or changes to be included in a commit.

### Benefits of the Staging Area

* Helps organize commits logically.
* Allows selective commits.
* Prevents accidental inclusion of unwanted changes.
* Improves project history readability.

---

## 3. What information does `git log` show you?

The `git log` command displays the commit history of a repository.

It typically shows:

* Commit ID (SHA hash)
* Author name
* Date and time of the commit
* Commit message

### Example

```bash
git log
```

### Sample Output

```text
commit a1b2c3d4e5f6...
Author: DevOpsUser
Date: Mon Jun 16 10:00:00 2026

    Added Git workflow notes
```

---

## 4. What is the `.git/` folder and what happens if you delete it?

The `.git/` folder is the hidden directory that stores all Git-related information for a repository.

It contains:

* Commit history
* Branch information
* Configuration settings
* References and metadata
* Object database

### If the `.git/` folder is deleted:

* The project files remain intact.
* Git tracking is removed.
* Commit history is lost.
* Branches are lost.
* The directory is no longer a Git repository.

You would need to run `git init` again to create a new repository.

---

## 5. What is the difference between a Working Directory, Staging Area, and Repository?

| Component         | Description                                                                        |
| ----------------- | ---------------------------------------------------------------------------------- |
| Working Directory | The files and folders you actively edit on your system.                            |
| Staging Area      | A temporary area where selected changes are prepared for the next commit.          |
| Repository        | The database where Git permanently stores committed snapshots and project history. |

### Git Workflow Diagram

```text
Working Directory
        |
        | git add
        v
   Staging Area
        |
        | git commit
        v
    Repository
```

### Summary

A typical Git workflow follows these steps:

1. Modify files in the Working Directory.
2. Add selected changes to the Staging Area using `git add`.
3. Save the staged changes to the Repository using `git commit`.
4. View commit history using `git log`.

Understanding these three areas is fundamental to working effectively with Git and forms the foundation for branching, merging, collaboration, and CI/CD workflows.

