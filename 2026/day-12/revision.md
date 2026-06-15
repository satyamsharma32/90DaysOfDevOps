# Day 12 of learning completing from day 1 to 11
# Day 12 – Revision (Days 01–11)

## Objective

Review and reinforce Linux fundamentals learned during Days 01–11.

---

# Section 1: Mindset & Learning Plan Review

### Original Goal

* Learn Linux fundamentals.
* Build strong troubleshooting skills.
* Prepare for DevOps and Cloud Engineer roles.
* Become comfortable working in Linux without a GUI.

### Current Progress

* Comfortable navigating Linux directories.
* Able to manage files and permissions.
* Understand basic user and group management.
* Able to troubleshoot processes and services.

### Improvement Areas

* Faster troubleshooting during incidents.
* More confidence with systemd services.
* More practice with permissions and ownership.

---

# Section 2: Processes & Services Review

## Process Check

### Command

```bash
ps -ef
```

### Observation

Displayed all running processes and their associated users.

---

### Command

```bash
top
```

### Observation

Monitored CPU and memory utilization in real time.

---

## Service Check

### Command

```bash
systemctl status ssh
```

### Observation

Verified SSH service status and uptime.

---

### Command

```bash
journalctl -u ssh -n 20
```

### Observation

Reviewed recent SSH service logs and found no critical issues.

---

# Section 3: File Skills Practice

## Create Directory

### Command

```bash
mkdir revision-practice
```

### Observation

Created a test directory successfully.

---

## Append Content

### Command

```bash
echo "Linux Revision Practice" >> notes.txt
```

### Observation

Added new content to an existing file.

---

## Check Permissions

### Command

```bash
ls -l
```

### Observation

Verified ownership and permissions of files.

---

## Modify Permissions

### Command

```bash
chmod 640 notes.txt
```

### Observation

Updated file permissions successfully.

---

## Copy File

### Command

```bash
cp notes.txt backup-notes.txt
```

### Observation

Created a backup copy of the file.

---

# Section 4: Cheat Sheet Refresh

## Top 5 Commands I Would Use During an Incident

### 1. ps -ef

Used to view running processes.

### 2. top

Used to identify CPU or memory-intensive processes.

### 3. systemctl status

Used to check service health and status.

### 4. journalctl -u

Used to review service logs.

### 5. ls -l

Used to verify file permissions and ownership.

---

# Section 5: User & Group Review

## Create User

### Command

```bash
sudo useradd -m testuser
```

### Verification

```bash
id testuser
```

### Observation

Verified user creation successfully.

---

## Change File Ownership

### Command

```bash
sudo chown testuser notes.txt
```

### Verification

```bash
ls -l notes.txt
```

### Observation

Ownership changed successfully.

---

# Mini Self-Check

## 1. Which 3 commands save you the most time right now and why?

### top

Quickly identifies CPU and memory issues.

### systemctl status

Provides immediate service health information.

### ls -l

Quickly verifies permissions and ownership.

---

## 2. How do you check if a service is healthy?

### Commands

```bash
systemctl status ssh
journalctl -u ssh -n 20
ps -ef | grep ssh
```

### Reason

These commands verify service status, logs, and running processes.

---

## 3. How do you safely change ownership and permissions?

### Example

```bash
sudo chown user1:developers app.conf
chmod 640 app.conf
```

### Reason

Ownership is assigned first, then permissions are adjusted carefully to avoid access issues.

---

## 4. What will you focus on improving in the next 3 days?

* Linux networking fundamentals.
* Advanced troubleshooting techniques.
* More real-world DevOps scenarios.
* Faster command-line navigation.

---

# Key Takeaways

* Linux troubleshooting follows a structured approach.
* Logs are the first place to investigate service issues.
* Permissions and ownership are critical for security.
* User and group management is essential for multi-user environments.
* Consistent practice improves troubleshooting speed and confidence.

---

# Revision Complete

Days Reviewed: 01–11

Status: Completed Successfully

