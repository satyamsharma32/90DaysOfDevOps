# Day 16 – Shell Scripting Basics

## Objective

Learn the fundamentals of shell scripting including shebang, variables, user input, and if-else conditions.

---

# Task 1: Your First Script

## File: hello.sh

### Script

```bash
#!/bin/bash

echo "Hello, DevOps!"
```

### Make Executable

```bash
chmod +x hello.sh
```

### Run Script

```bash
./hello.sh
```

### Output

```text
Hello, DevOps!
```

### What Happens If Shebang Is Removed?

The shebang (`#!/bin/bash`) tells Linux which interpreter should execute the script.

Without a shebang:

* The script may still work if executed using `bash hello.sh`.
* Running `./hello.sh` may fail or use a different shell depending on the environment.

---

# Task 2: Variables

## File: variables.sh

### Script

```bash
#!/bin/bash

NAME="Shubham"
ROLE="DevOps Engineer"

echo "Hello, I am $NAME and I am a $ROLE"
```

### Run Script

```bash
chmod +x variables.sh
./variables.sh
```

### Output

```text
Hello, I am Shubham and I am a DevOps Engineer
```

### Single Quotes vs Double Quotes

#### Double Quotes

```bash
echo "My name is $NAME"
```

Output:

```text
My name is Shubham
```

Variables are expanded.

---

#### Single Quotes

```bash
echo 'My name is $NAME'
```

Output:

```text
My name is $NAME
```

Variables are not expanded.

---

# Task 3: User Input with read

## File: greet.sh

### Script

```bash
#!/bin/bash

read -p "Enter your name: " NAME
read -p "Enter your favourite tool: " TOOL

echo "Hello $NAME, your favourite tool is $TOOL"
```

### Run Script

```bash
chmod +x greet.sh
./greet.sh
```

### Example Output

```text
Enter your name: Shubham
Enter your favourite tool: Docker

Hello Shubham, your favourite tool is Docker
```

---

# Task 4: If-Else Conditions

## File: check_number.sh

### Script

```bash
#!/bin/bash

read -p "Enter a number: " NUM

if [ $NUM -gt 0 ]; then
    echo "Positive Number"
elif [ $NUM -lt 0 ]; then
    echo "Negative Number"
else
    echo "Zero"
fi
```

### Example Output

```text
Enter a number: 10
Positive Number
```

---

## File: file_check.sh

### Script

```bash
#!/bin/bash

read -p "Enter filename: " FILE

if [ -f "$FILE" ]; then
    echo "File exists"
else
    echo "File does not exist"
fi
```

### Example Output

```text
Enter filename: notes.txt
File exists
```

---

# Task 5: Combine It All

## File: server_check.sh

### Script

```bash
#!/bin/bash

SERVICE="ssh"

read -p "Do you want to check the status? (y/n): " CHOICE

if [ "$CHOICE" = "y" ]; then

    if systemctl is-active --quiet $SERVICE; then
        echo "$SERVICE service is active"
    else
        echo "$SERVICE service is not active"
    fi

elif [ "$CHOICE" = "n" ]; then
    echo "Skipped."

else
    echo "Invalid input."
fi
```

### Run Script

```bash
chmod +x server_check.sh
./server_check.sh
```

### Example Output

```text
Do you want to check the status? (y/n): y
ssh service is active
```

---

# Commands Used

```bash
chmod +x
./script.sh
echo
read
if
elif
else
systemctl is-active
```

---

# What I Learned

### 1. Shebang Defines the Interpreter

The shebang tells Linux which shell should execute the script.

---

### 2. Variables Make Scripts Dynamic

Variables allow values to be stored and reused throughout the script.

---

### 3. Conditions Add Decision Making

If-else statements allow scripts to perform different actions based on user input or system conditions.

---

# Why This Matters for DevOps

Shell scripting is one of the most important DevOps skills because it helps automate:

* Server administration
* Deployment tasks
* Health checks
* Log monitoring
* Backup operations
* Infrastructure maintenance

Almost every DevOps tool eventually executes shell commands behind the scenes.

---

# Files Created

```text
hello.sh
variables.sh
greet.sh
check_number.sh
file_check.sh
server_check.sh
```

---

# Screenshots

Add screenshots for:

* hello.sh execution
* variables.sh output
* greet.sh output
* check_number.sh output
* file_check.sh output
* server_check.sh output

