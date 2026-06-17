# Shell Scripting Cheat Sheet

## 1. Basics

### Shebang

```bash
#!/bin/bash
```

Defines which interpreter should execute the script.

Example:

```bash
#!/bin/bash
echo "Hello DevOps"
```

---

### Running a Script

Make executable:

```bash
chmod +x script.sh
```

Run:

```bash
./script.sh
```

Run without execute permission:

```bash
bash script.sh
```

---

### Comments

Single-line comment:

```bash
# This is a comment
```

Inline comment:

```bash
echo "Hello" # Print message
```

---

### Variables

Declare variable:

```bash
NAME="user1"
```

Use variable:

```bash
echo $NAME
echo "$NAME"
```

Single quotes:

```bash
echo '$NAME'
```

Output:

```text
$NAME
```

Double quotes:

```bash
echo "$NAME"
```

Output:

```text
user1
```

---

### Reading User Input

```bash
read -p "Enter Name: " NAME

echo "Hello $NAME"
```

---

### Command Line Arguments

```bash
$0   # Script name
$1   # First argument
$2   # Second argument
$#   # Number of arguments
$@   # All arguments
$?   # Exit status of last command
```

Example:

```bash
./demo.sh DevOps Linux
```

---

# 2. Operators and Conditionals

## String Comparisons

```bash
[ "$A" = "$B" ]
[ "$A" != "$B" ]
[ -z "$VAR" ]
[ -n "$VAR" ]
```

---

## Integer Comparisons

```bash
[ "$A" -eq "$B" ]
[ "$A" -ne "$B" ]
[ "$A" -lt "$B" ]
[ "$A" -gt "$B" ]
[ "$A" -le "$B" ]
[ "$A" -ge "$B" ]
```

---

## File Test Operators

```bash
-f file.txt
-d directory
-e file
-r file
-w file
-x file
-s file
```

---

## If Else

```bash
if [ "$NUM" -gt 0 ]; then
    echo "Positive"
elif [ "$NUM" -lt 0 ]; then
    echo "Negative"
else
    echo "Zero"
fi
```

---

## Logical Operators

```bash
&&
||
!
```

Example:

```bash
mkdir test && cd test
```

---

## Case Statement

```bash
case $CHOICE in
    start)
        echo "Starting"
        ;;
    stop)
        echo "Stopping"
        ;;
    *)
        echo "Invalid Option"
        ;;
esac
```

---

# 3. Loops

## For Loop

List-based:

```bash
for fruit in apple mango banana
do
    echo $fruit
done
```

C-style:

```bash
for ((i=1;i<=5;i++))
do
    echo $i
done
```

---

## While Loop

```bash
COUNT=1

while [ $COUNT -le 5 ]
do
    echo $COUNT
    ((COUNT++))
done
```

---

## Until Loop

```bash
COUNT=1

until [ $COUNT -gt 5 ]
do
    echo $COUNT
    ((COUNT++))
done
```

---

## Loop Control

Break:

```bash
break
```

Continue:

```bash
continue
```

---

## Loop Over Files

```bash
for file in *.log
do
    echo $file
done
```

---

## Loop Over Command Output

```bash
cat users.txt | while read line
do
    echo $line
done
```

---

# 4. Functions

## Define Function

```bash
greet() {
    echo "Hello DevOps"
}
```

---

## Call Function

```bash
greet
```

---

## Function Arguments

```bash
greet() {
    echo "Hello $1"
}

greet user1
```

---

## Return Values

Using return:

```bash
return 0
```

Using echo:

```bash
add() {
    echo $(( $1 + $2 ))
}
```

---

## Local Variables

```bash
demo() {
    local NAME="DevOps"
    echo $NAME
}
```

---

# 5. Text Processing Commands

## grep

```bash
grep error app.log
grep -i error app.log
grep -r error .
grep -c error app.log
grep -n error app.log
grep -v error app.log
grep -E "ERROR|FAILED" app.log
```

---

## awk

Print column:

```bash
awk '{print $1}'
```

Custom delimiter:

```bash
awk -F: '{print $1}' /etc/passwd
```

BEGIN / END:

```bash
awk 'BEGIN{print "Start"} {print $1} END{print "End"}'
```

---

## sed

Replace text:

```bash
sed 's/nginx/apache/'
```

Delete line:

```bash
sed '2d' file.txt
```

Edit file:

```bash
sed -i 's/old/new/g' file.txt
```

---

## cut

```bash
cut -d: -f1 /etc/passwd
```

---

## sort

```bash
sort file.txt
sort -n file.txt
sort -r file.txt
sort -u file.txt
```

---

## uniq

```bash
uniq file.txt
uniq -c file.txt
```

---

## tr

Uppercase:

```bash
tr 'a-z' 'A-Z'
```

Delete characters:

```bash
tr -d ','
```

---

## wc

```bash
wc file.txt
wc -l file.txt
wc -w file.txt
wc -c file.txt
```

---

## head / tail

```bash
head -5 file.txt
tail -5 file.txt
tail -f app.log
```

---

# 6. Useful DevOps One-Liners

### Find files older than 7 days

```bash
find /tmp -type f -mtime +7
```

### Count lines in log files

```bash
wc -l *.log
```

### Replace text in multiple files

```bash
sed -i 's/old/new/g' *.conf
```

### Check if service is running

```bash
systemctl is-active ssh
```

### Monitor disk usage

```bash
df -h
```

### Parse JSON

```bash
cat data.json | jq .
```

### Tail logs and filter errors

```bash
tail -f app.log | grep ERROR
```

---

# 7. Error Handling and Debugging

## Exit Codes

Success:

```bash
exit 0
```

Failure:

```bash
exit 1
```

Check last command:

```bash
echo $?
```

---

## set -e

Exit immediately if a command fails.

```bash
set -e
```

---

## set -u

Treat undefined variables as errors.

```bash
set -u
```

---

## set -o pipefail

Catch failures inside pipelines.

```bash
set -o pipefail
```

---

## set -x

Debug mode.

```bash
set -x
```

Shows every command before execution.

---

## Trap

Run cleanup before exit.

```bash
cleanup() {
    rm -f /tmp/testfile
}

trap cleanup EXIT
```

---

# DevOps Commands I Use Most

```bash
grep
awk
sed
systemctl
journalctl
tail -f
find
df -h
free -h
ss -tulpn
```

These commands are commonly used during production troubleshooting, log analysis, monitoring, and automation.
