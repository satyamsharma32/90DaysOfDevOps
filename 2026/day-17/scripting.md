# Day 17 – Shell Scripting: Loops, Arguments & Error Handling

## Objective

Learn how to use loops, command-line arguments, package installation automation, and basic error handling in shell scripting.

---

# Task 1: For Loop

## File: for_loop.sh

### Script

```bash
#!/bin/bash

for FRUIT in Apple Banana Mango Orange Grapes
do
    echo "$FRUIT"
done
```

### Output

```text
Apple
Banana
Mango
Orange
Grapes
```

---

## File: count.sh

### Script

```bash
#!/bin/bash

for NUM in {1..10}
do
    echo "$NUM"
done
```

### Output

```text
1
2
3
4
5
6
7
8
9
10
```

---

# Task 2: While Loop

## File: countdown.sh

### Script

```bash
#!/bin/bash

read -p "Enter a number: " NUM

while [ $NUM -ge 0 ]
do
    echo "$NUM"
    NUM=$((NUM-1))
done

echo "Done!"
```

### Example Output

```text
Enter a number: 5
5
4
3
2
1
0
Done!
```

---

# Task 3: Command-Line Arguments

## File: greet.sh

### Script

```bash
#!/bin/bash

if [ $# -eq 0 ]
then
    echo "Usage: ./greet.sh <name>"
else
    echo "Hello, $1!"
fi
```

### Example

```bash
./greet.sh Shubham
```

### Output

```text
Hello, Shubham!
```

---

## File: args_demo.sh

### Script

```bash
#!/bin/bash

echo "Script Name: $0"
echo "Total Arguments: $#"
echo "All Arguments: $@"
```

### Example

```bash
./args_demo.sh docker kubernetes linux
```

### Output

```text
Script Name: ./args_demo.sh
Total Arguments: 3
All Arguments: docker kubernetes linux
```

---

# Task 4: Install Packages via Script

## File: install_packages.sh

### Script

```bash
#!/bin/bash

if [ "$EUID" -ne 0 ]
then
    echo "Please run this script as root."
    exit 1
fi

PACKAGES=("nginx" "curl" "wget")

for PACKAGE in "${PACKAGES[@]}"
do

    if dpkg -s "$PACKAGE" >/dev/null 2>&1
    then
        echo "$PACKAGE is already installed."
    else
        echo "Installing $PACKAGE ..."
        apt update
        apt install -y "$PACKAGE"
    fi

done
```

### Example Output

```text
nginx is already installed.
curl is already installed.
Installing wget ...
```

---

# Task 5: Error Handling

## File: safe_script.sh

### Script

```bash
#!/bin/bash

set -e

mkdir /tmp/devops-test || echo "Directory already exists"

cd /tmp/devops-test || {
    echo "Failed to enter directory"
    exit 1
}

touch test-file.txt

echo "Script completed successfully."
```

### Example Output

```text
Directory already exists
Script completed successfully.
```

---

# Commands Used

```bash
chmod +x
./script.sh
for
while
$1
$#
$@
dpkg -s
apt install
set -e
mkdir
touch
```

---

# What I Learned

### 1. Loops Help Automate Repetitive Tasks

Using for and while loops allows scripts to perform actions multiple times without repeating code.

---

### 2. Command-Line Arguments Make Scripts Flexible

Arguments like $1, $#, and $@ allow users to provide input directly when running a script.

---

### 3. Error Handling Makes Scripts Safer

Using set -e and conditional checks prevents scripts from continuing after failures.

---

# Why This Matters for DevOps

Shell scripting is heavily used in DevOps for:

* Server provisioning
* Package installation
* Health checks
* Backup automation
* Deployment pipelines
* Monitoring and maintenance tasks

Understanding loops, arguments, and error handling helps create reliable automation scripts used in real production environments.

---

# Files Created

```text
for_loop.sh
count.sh
countdown.sh
greet.sh
args_demo.sh
install_packages.sh
safe_script.sh
```

---

# Screenshots

Add screenshots for:

* for_loop.sh execution
* count.sh execution
* countdown.sh output
* greet.sh output
* args_demo.sh output
* install_packages.sh output
* safe_script.sh output

