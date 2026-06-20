# Day 28 - Revision Notes (Days 01–27)

## Objective

Today was focused on revising all concepts learned from Day 01 to Day 27. The goal was to identify weak areas, reinforce important concepts, and prepare for upcoming DevOps topics.

---

# Section 1: Topics Revised

## DevOps Fundamentals

* DevOps lifecycle and SDLC
* CI/CD concepts
* Cloud fundamentals
* Infrastructure Automation

## Linux Fundamentals

* Linux Architecture
* File System Hierarchy
* Process Management
* Services and systemd
* User and Group Management
* File Permissions and Ownership
* LVM (Logical Volume Manager)
* Linux Networking Basics

## Shell Scripting

* Variables and User Input
* Conditional Statements
* Loops (for, while, until)
* Functions
* Command Line Arguments
* Error Handling
* Text Processing Commands

## Git & GitHub

* Repository Initialization
* Branching and Merging
* Rebase
* Cherry Pick
* Reset and Revert
* GitHub CLI
* Pull Requests and Issues

---

# Section 2: Self Assessment

| Topic                     | Status             |
| ------------------------- | ------------------ |
| Linux Commands            | Confident          |
| File Permissions          | Confident          |
| Process Troubleshooting   | Confident          |
| Networking Basics         | Need More Practice |
| Shell Scripting Functions | Need More Practice |
| Git Rebase                | Need More Practice |
| GitHub CLI                | Learning           |
| LVM                       | Learning           |

---

# Section 3: Topics Revisited

## 1. Git Rebase

### What I Re-Learned

* Rebase moves commits to a new base commit.
* Keeps history linear and clean.
* Useful before pushing local commits.

### Commands Practiced

```bash
git fetch
git pull origin master --rebase
```

---

## 2. Linux Networking

### What I Re-Learned

* DNS converts domain names into IP addresses.
* Port numbers identify services.
* ss command shows listening services.

### Commands Practiced

```bash
ss -tulpn
ping google.com
curl -I https://google.com
```

---

## 3. Shell Scripting Functions

### What I Re-Learned

* Functions improve code reusability.
* Local variables prevent unwanted variable modification.
* Functions simplify large scripts.

### Example

```bash
greet() {
    echo "Hello User"
}

greet
```

---

# Section 4: Quick Fire Answers

## What does chmod 755 script.sh do?

Gives owner read, write, execute permissions and group/others read and execute permissions.

---

## Difference between Process and Service?

A process is a running program.

A service is a background process managed by systemd.

---

## How do you find which process is using port 8080?

```bash
ss -tulpn | grep 8080
```

---

## What does set -euo pipefail do?

* set -e → Exit on command failure
* set -u → Treat undefined variables as errors
* set -o pipefail → Detect failures inside pipelines

---

## Difference between git reset --hard and git revert?

git reset --hard removes commits and changes.

git revert creates a new commit that undoes previous changes.

---

## Recommended branching strategy for a team of 5 developers?

GitHub Flow because it is simple and works well for frequent deployments.

---

## What does git stash do?

Temporarily saves uncommitted changes without committing them.

---

## How do you schedule a script every day at 3 AM?

```bash
0 3 * * * /path/to/script.sh
```

---

## Difference between git fetch and git pull?

git fetch downloads changes.

git pull downloads and merges changes.

---

## What is LVM?

LVM allows flexible storage management by creating Logical Volumes that can be resized without repartitioning disks.

---

# Section 5: Teaching Back

## Explaining File Permissions

Linux permissions control who can access files and directories.

There are three permission categories:

* Owner
* Group
* Others

Permission values:

* r = Read (4)
* w = Write (2)
* x = Execute (1)

Example:

```bash
chmod 755 script.sh
```

Owner can read, write, and execute.

Group and others can read and execute.

Permissions help secure systems by preventing unauthorized access.

---

# Key Takeaways

* Linux troubleshooting requires understanding processes, logs, networking, and permissions.
* Shell scripting helps automate repetitive tasks.
* Git and GitHub are essential for version control and collaboration.
* Consistent revision improves troubleshooting confidence and interview readiness.

