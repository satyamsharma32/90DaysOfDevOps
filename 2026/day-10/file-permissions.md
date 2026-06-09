# Day 10 of learning of file permission in linux system
# Day 10 – File Permissions & File Operations Challenge

## Objective

Practice creating files, reading files, understanding Linux permissions, modifying permissions, and testing permission-related scenarios.

---

# Task 1: Create Files

## Create Empty File

### Command

```bash
touch devops.txt
```

### What It Does

Creates an empty file named `devops.txt`.

---

## Create File with Content

### Command

```bash
echo "Learning Linux File Permissions" > notes.txt
```

### What It Does

Creates `notes.txt` and writes content into it.

---

## Create Shell Script

### Command

```bash
vim script.sh
```

### Content

```bash
echo "Hello DevOps"
```

### What It Does

Creates a shell script file.

---

## Verify Files

### Command

```bash
ls -l
```

### What It Does

Displays file permissions, ownership, and file sizes.

---

# Task 2: Read Files

## Read notes.txt

### Command

```bash
cat notes.txt
```

### What It Does

Displays the complete content of the file.

---

## Open Script in Read-Only Mode

### Command

```bash
vim -R script.sh
```

### What It Does

Opens the file in read-only mode.

---

## View First 5 Lines of passwd File

### Command

```bash
head -n 5 /etc/passwd
```

### What It Does

Displays the first five lines of the passwd file.

---

## View Last 5 Lines of passwd File

### Command

```bash
tail -n 5 /etc/passwd
```

### What It Does

Displays the last five lines of the passwd file.

---

# Task 3: Understand Permissions

## Check Current Permissions

### Command

```bash
ls -l devops.txt notes.txt script.sh
```

### What It Does

Displays current file permissions.

---

## Permission Format

```text
rwxrwxrwx
│ │ │
│ │ └── Others
│ └──── Group
└────── Owner
```

### Permission Values

| Permission  | Value |
| ----------- | ----- |
| Read (r)    | 4     |
| Write (w)   | 2     |
| Execute (x) | 1     |

---

## Example

```text
-rw-r--r--
```

### Meaning

* Owner: Read and Write
* Group: Read Only
* Others: Read Only

---

# Task 4: Modify Permissions

## Make Script Executable

### Command

```bash
chmod +x script.sh
```

### Verify

```bash
ls -l script.sh
```

### Run Script

```bash
./script.sh
```

---

## Make devops.txt Read-Only

### Command

```bash
chmod a-w devops.txt
```

### Verify

```bash
ls -l devops.txt
```

### Result

Write permission removed for owner, group, and others.

---

## Set notes.txt Permission to 640

### Command

```bash
chmod 640 notes.txt
```

### Verify

```bash
ls -l notes.txt
```

### Meaning

```text
Owner  : Read + Write
Group  : Read
Others : No Permission
```

---

## Create Directory with 755 Permission

### Command

```bash
mkdir project
chmod 755 project
```

### Verify

```bash
ls -ld project
```

### Meaning

```text
Owner  : Read + Write + Execute
Group  : Read + Execute
Others : Read + Execute
```

---

# Task 5: Test Permissions

## Try Writing to Read-Only File

### Command

```bash
echo "New Content" >> devops.txt
```

### Observation

Permission denied or write operation blocked when write permission is unavailable.

---

## Remove Execute Permission

### Command

```bash
chmod -x script.sh
```

### Verify

```bash
ls -l script.sh
```

---

## Try Executing Script

### Command

```bash
./script.sh
```

### Observation

Permission denied because execute permission is missing.

---

# Key Learnings

* `touch` creates empty files.
* `cat` displays file contents.
* `head` shows the beginning of a file.
* `tail` shows the end of a file.
* `chmod` modifies permissions.
* `+x` adds execute permission.
* `-w` removes write permission.
* Numeric permissions provide precise access control.

---

# Why This Matters for DevOps

DevOps engineers frequently work with:

* Shell scripts
* Configuration files
* Log files
* Deployment automation

Understanding Linux permissions helps prevent security issues and ensures applications and scripts run correctly in production environments.

