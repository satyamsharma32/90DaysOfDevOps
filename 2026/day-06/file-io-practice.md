# day 6 of learning the linux
 # Day 06 – Linux Fundamentals: Read and Write Text Files

## Objective

Practice basic file operations in Linux using fundamental commands:

* Creating a file
* Writing text to a file
* Appending text to a file
* Reading file contents
* Using `tee` to write and display output simultaneously

---

## Create File

### Command

```bash
touch notes.txt
```

### What It Does

Creates an empty file named `notes.txt`.

---

## Write First Line

### Command

```bash
echo "Line 1 - Linux File Practice" > notes.txt
```

### What It Does

Writes the first line to the file. If the file already contains data, it will be overwritten.

---

## Append Second Line

### Command

```bash
echo "Line 2 - Learning Redirection" >> notes.txt
```

### What It Does

Appends a new line to the existing file without removing previous content.

---

## Append Third Line Using tee

### Command

```bash
echo "Line 3 - Added using tee" | tee -a notes.txt
```

### What It Does

Displays the text on the terminal and appends it to the file at the same time.

---

## Read Full File

### Command

```bash
cat notes.txt
```

### What It Does

Displays the complete contents of the file.

---

## Read First Two Lines

### Command

```bash
head -n 2 notes.txt
```

### What It Does

Displays the first two lines of the file.

---

## Read Last Two Lines

### Command

```bash
tail -n 2 notes.txt
```

### What It Does

Displays the last two lines of the file.

---

## Sample File Content

```text
Line 1 - Linux File Practice
Line 2 - Learning Redirection
Line 3 - Added using tee
```

---

## Key Learnings

* `touch` creates an empty file.
* `>` writes data and overwrites existing content.
* `>>` appends data to an existing file.
* `cat` displays the complete file.
* `head` displays the beginning of a file.
* `tail` displays the end of a file.
* `tee` writes output to a file and displays it simultaneously.

---

## Why This Matters for DevOps

DevOps engineers work with:

* Log files
* Configuration files
* Shell scripts
* Deployment outputs

Understanding file read and write operations helps in troubleshooting, automation, monitoring, and system administration.

