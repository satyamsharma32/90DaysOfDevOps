# Day 18 – Shell Scripting: Functions & Intermediate Concepts

## Objective

Learn how to write reusable shell scripts using functions, local variables, strict mode, and system information reporting.

---

# Task 1: Basic Functions

## File: functions.sh

### Script

```bash
#!/bin/bash

greet() {
    echo "Hello, $1!"
}

add() {
    echo $(($1 + $2))
}

greet "user"

echo "Sum: $(add 10 20)"
```

### Example Output

```text
Hello, user!
Sum: 30
```

---

# Task 2: Functions with Return Values

## File: disk_check.sh

### Script

```bash
#!/bin/bash

check_disk() {
    echo "Disk Usage:"
    df -h /
}

check_memory() {
    echo "Memory Usage:"
    free -h
}

check_disk
echo

check_memory
```

### Example Output

```text
Disk Usage:
Filesystem      Size  Used Avail Use%
/dev/sda1        50G   20G   28G  42%

Memory Usage:
Mem: 7.5G 3.1G 2.8G
```

---

# Task 3: Strict Mode – set -euo pipefail

## File: strict_demo.sh

### Script

```bash
#!/bin/bash

set -euo pipefail

echo "$UNDEFINED_VARIABLE"

mkdir /tmp/test-dir

false

echo "This line will not execute"
```

### Observation

The script stops immediately when an undefined variable or failed command is encountered.

---

## What Does Each Flag Do?

### set -e

Exit immediately if any command returns a non-zero status.

---

### set -u

Treat undefined variables as errors and exit the script.

---

### set -o pipefail

If any command in a pipeline fails, the entire pipeline fails.

---

# Task 4: Local Variables

## File: local_demo.sh

### Script

```bash
#!/bin/bash

demo_local() {
    local NAME="user1"
    echo "Inside Function: $NAME"
}

demo_global() {
    CITY="Mumbai"
}

demo_local

echo "Outside Function: ${NAME:-Not Available}"

demo_global

echo "Global Variable: $CITY"
```

### Example Output

```text
Inside Function: user
Outside Function: Not Available
Global Variable: Mumbai
```

### Observation

Local variables remain inside the function scope while global variables remain available throughout the script.

---

# Task 5: Build a Script – System Info Reporter

## File: system_info.sh

### Script

```bash
#!/bin/bash

set -euo pipefail

print_header() {
    echo
    echo "================================"
    echo "$1"
    echo "================================"
}

system_info() {
    print_header "System Information"

    hostname
    cat /etc/os-release | grep PRETTY_NAME
}

uptime_info() {
    print_header "System Uptime"

    uptime
}

disk_usage() {
    print_header "Top Disk Usage"

    df -h | head -5
}

memory_usage() {
    print_header "Memory Usage"

    free -h
}

top_processes() {
    print_header "Top CPU Processes"

    ps -eo pid,ppid,cmd,%cpu --sort=-%cpu | head -6
}

main() {
    system_info
    uptime_info
    disk_usage
    memory_usage
    top_processes
}

main
```

### Example Output

```text
================================
System Information
================================

hostname
Ubuntu 24.04 LTS

================================
System Uptime
================================

up 3 hours

================================
Top Disk Usage
================================

Filesystem Size Used Avail Use%

================================
Memory Usage
================================

Mem: 7.5G

================================
Top CPU Processes
================================

PID CPU COMMAND
```

---

# Commands Used

```bash
chmod +x
./script.sh
df -h
free -h
hostname
uptime
ps
set -euo pipefail
local
function
```

---

# What I Learned

### 1. Functions Improve Reusability

Functions help avoid repeating code and make scripts easier to maintain.

---

### 2. Strict Mode Creates Safer Scripts

Using set -euo pipefail prevents silent failures and unexpected behavior.

---

### 3. Local Variables Prevent Conflicts

Local variables stay within function scope and reduce bugs in larger scripts.

---

# Why This Matters for DevOps

Functions and strict mode are commonly used in:

* Deployment scripts
* CI/CD pipelines
* Infrastructure automation
* Monitoring scripts
* Health checks
* Backup automation

Reusable and safe scripts are critical in production environments.

---

# Files Created

```text
functions.sh
disk_check.sh
strict_demo.sh
local_demo.sh
system_info.sh
```

---

# Screenshots

Add screenshots for:

* functions.sh output
* disk_check.sh output
* strict_demo.sh failure behavior
* local_demo.sh output
* system_info.sh report

