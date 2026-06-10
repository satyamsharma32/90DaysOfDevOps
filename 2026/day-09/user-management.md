# Day 9 learning of learning user group and management 
# Day 09 – Linux User & Group Management Challeinge

## Objective

Practice Linux user and group management by creating users, groups, assigning permissions, and configuring shared directories.

---

# Task 1: Create Users

## Create Three Users

### Commands

```bash
sudo useradd -m user1
sudo useradd -m user2
sudo useradd -m user3
```

### Set Passwords

```bash
sudo passwd user1
sudo passwd user2
sudo passwd user3
```

### Verification

```bash
cat /etc/passwd | grep user
ls /home
```

### Observation

- Three users created successfully.
- Home directories created under `/home`.

---

# Task 2: Create Groups

## Create Developers Group

```bash
sudo groupadd developers
```

## Create Admins Group

```bash
sudo groupadd admins
```

### Verification

```bash
cat /etc/group | grep developers
cat /etc/group | grep admins
```

### Observation

- Developers group created successfully.
- Admins group created successfully.

---

# Task 3: Assign Users to Groups

## Add Users to Developers Group

```bash
sudo usermod -aG developers user1
sudo usermod -aG developers user2
```

## Add User to Admins Group

```bash
sudo usermod -aG admins user3
```

### Verification

```bash
groups user1
groups user2
groups user3
```

### Observation

- user1 and user2 belong to developers group.
- user3 belongs to admins group.

---

# Task 4: Shared Directory

## Create Shared Directory

```bash
sudo mkdir -p /opt/dev-project
```

## Change Group Ownership

```bash
sudo chgrp developers /opt/dev-project
```

## Set Permissions

```bash
sudo chmod 775 /opt/dev-project
```

### Verification

```bash
ls -ld /opt/dev-project
```

### Test File Creation

Switch user:

```bash
su - user1
touch /opt/dev-project/user1-file.txt
```

Switch another user:

```bash
su - user2
touch /opt/dev-project/user2-file.txt
```

### Verify Files

```bash
ls -l /opt/dev-project
```

### Observation

- Both users can create files inside the shared directory.
- Group permissions are working correctly.

---

# Task 5: Team Workspace

## Create User

```bash
sudo useradd -m nairobi
sudo passwd nairobi
```

## Create Group

```bash
sudo groupadd project-team
```

## Add Users to Group

```bash
sudo usermod -aG project-team user1
sudo usermod -aG project-team user2
sudo usermod -aG project-team nairobi
```

### Verify Membership

```bash
groups user1
groups user2
groups nairobi
```

## Create Workspace Directory

```bash
sudo mkdir -p /opt/team-workspace
```

## Assign Group Ownership

```bash
sudo chgrp project-team /opt/team-workspace
```

## Set Permissions

```bash
sudo chmod 775 /opt/team-workspace
```

### Verification

```bash
ls -ld /opt/team-workspace
```

### Test Access

```bash
su - user1
touch /opt/team-workspace/test-file.txt
```

### Verify

```bash
ls -l /opt/team-workspace
```

### Observation

- Team members can collaborate in the shared workspace.
- Group permissions allow read, write, and execute access.

---

# Key Commands Used

```bash
useradd
passwd
groupadd
usermod
groups
mkdir
chgrp
chmod
ls -l
ls -ld
touch
```

---

# Key Learnings

- Created Linux users and home directories.
- Created groups and assigned users.
- Managed group ownership using `chgrp`.
- Configured shared directories using `chmod 775`.
- Verified permissions and group membership.
- Practiced real-world DevOps style user management.

---

# Why This Matters for DevOps

User and group management is essential for:

- Managing server access.
- Controlling permissions.
- Securing applications.
- Supporting team collaboration.
- Managing production environments efficiently.
