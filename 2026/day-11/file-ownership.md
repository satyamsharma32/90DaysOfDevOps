# Day 11 of learning linux and file permission in linux 
# Day 11 – File Ownership Challenge (chown & chgrp)

## Objective

Practice Linux file ownership and group ownership management using `chown` and `chgrp`.

---

# Task 1: Understanding Ownership

## Check File Ownership

### Command

```bash
ls -l
```

### What It Does

Displays file permissions, owner, group, size, and modification date.

### Example Format

```text
-rw-r--r-- 1 owner group 0 Jun 15 devops-file.txt
```

### Understanding the Fields

* Owner: The user who owns the file.
* Group: The group associated with the file.

### Difference Between Owner and Group

* Owner has primary control over the file.
* Group permissions allow multiple users in the same group to access the file.

---

# Task 2: Basic chown Operations

## Create Test File

```bash
touch devops-file.txt
```

## Check Current Owner

```bash
ls -l devops-file.txt
```

## Create Users

```bash
sudo useradd -m tokyo
sudo useradd -m berlin
```

## Change Owner to Tokyo

```bash
sudo chown tokyo devops-file.txt
```

## Verify

```bash
ls -l devops-file.txt
```

## Change Owner to Berlin

```bash
sudo chown berlin devops-file.txt
```

## Verify Again

```bash
ls -l devops-file.txt
```

### Observation

Ownership changes successfully from one user to another.

---

# Task 3: Basic chgrp Operations

## Create File

```bash
touch team-notes.txt
```

## Check Current Group

```bash
ls -l team-notes.txt
```

## Create Group

```bash
sudo groupadd heist-team
```

## Change Group Ownership

```bash
sudo chgrp heist-team team-notes.txt
```

## Verify

```bash
ls -l team-notes.txt
```

### Observation

Group ownership successfully changed to heist-team.

---

# Task 4: Combined Owner & Group Change

## Create Configuration File

```bash
touch project-config.yaml
```

## Create User

```bash
sudo useradd -m professor
```

## Change Owner and Group Together

```bash
sudo chown professor:heist-team project-config.yaml
```

## Verify

```bash
ls -l project-config.yaml
```

---

## Create Directory

```bash
mkdir app-logs
```

## Change Directory Ownership

```bash
sudo chown berlin:heist-team app-logs
```

## Verify

```bash
ls -ld app-logs
```

### Observation

Owner and group can be changed using a single command.

---

# Task 5: Recursive Ownership

## Create Directory Structure

```bash
mkdir -p heist-project/vault
mkdir -p heist-project/plans

touch heist-project/vault/gold.txt
touch heist-project/plans/strategy.conf
```

## Create Group

```bash
sudo groupadd planners
```

## Change Ownership Recursively

```bash
sudo chown -R professor:planners heist-project
```

## Verify

```bash
ls -lR heist-project
```

### Observation

Ownership updated for all directories and files under heist-project.

---

# Task 6: Practice Challenge

## Create Users

```bash
sudo useradd -m tokyo
sudo useradd -m berlin
sudo useradd -m nairobi
```

## Create Groups

```bash
sudo groupadd vault-team
sudo groupadd tech-team
```

## Create Directory

```bash
mkdir bank-heist
```

## Create Files

```bash
touch bank-heist/access-codes.txt
touch bank-heist/blueprints.pdf
touch bank-heist/escape-plan.txt
```

## Assign Ownership

### access-codes.txt

```bash
sudo chown tokyo:vault-team bank-heist/access-codes.txt
```

### blueprints.pdf

```bash
sudo chown berlin:tech-team bank-heist/blueprints.pdf
```

### escape-plan.txt

```bash
sudo chown nairobi:vault-team bank-heist/escape-plan.txt
```

## Verify Ownership

```bash
ls -l bank-heist
```

### Observation

Each file has different ownership based on assigned user and group.

---

# Key Commands Used

```bash
ls -l
ls -ld
ls -lR
touch
mkdir
useradd
groupadd
chown
chgrp
chown -R
```

---

# Key Learnings

* Owner determines who primarily controls a file.
* Group ownership allows shared access among multiple users.
* `chown` changes file ownership.
* `chgrp` changes file group ownership.
* `chown owner:group` changes both owner and group together.
* `chown -R` applies ownership recursively to directories and files.

---

# Why This Matters for DevOps

DevOps engineers frequently manage:

* Application log directories
* Deployment artifacts
* Shared project directories
* Configuration files
* CI/CD workspace permissions

Proper ownership ensures security, controlled access, and smooth collaboration across teams.

