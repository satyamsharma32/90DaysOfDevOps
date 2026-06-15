# Day 20 – Bash Scripting Challenge: Log Analyzer and Report Generator

## Objective

Create a Bash script that analyzes log files, identifies errors and critical events, and generates a daily summary report.

---

# Problem Statement

System administrators often need to review large log files to identify:

* Error messages
* Failed operations
* Critical events
* Frequent issues

Manually reviewing logs is time-consuming.

The goal of this script is to automate log analysis and generate a concise report.

---

# Solution Overview

The script performs the following tasks:

1. Accepts a log file as input.
2. Validates the input file.
3. Counts ERROR and Failed entries.
4. Finds CRITICAL events with line numbers.
5. Displays the top 5 most common error messages.
6. Generates a daily report file.
7. Optionally archives processed logs.

---

# Script: log_analyzer.sh

```bash
#!/bin/bash

set -euo pipefail

LOG_FILE="${1:-}"

if [ -z "$LOG_FILE" ]; then
    echo "Usage: ./log_analyzer.sh <logfile>"
    exit 1
fi

if [ ! -f "$LOG_FILE" ]; then
    echo "Error: File does not exist."
    exit 1
fi

REPORT_FILE="log_report_$(date +%F).txt"

TOTAL_LINES=$(wc -l < "$LOG_FILE")

ERROR_COUNT=$(grep -Ei "ERROR|Failed" "$LOG_FILE" | wc -l)

CRITICAL_EVENTS=$(grep -n "CRITICAL" "$LOG_FILE" || true)

TOP_ERRORS=$(grep "ERROR" "$LOG_FILE" \
    | sed 's/.*ERROR[: ]*//' \
    | sort \
    | uniq -c \
    | sort -rn \
    | head -5)

echo "Total Errors Found: $ERROR_COUNT"

echo
echo "--- Critical Events ---"

grep -n "CRITICAL" "$LOG_FILE" || echo "No Critical Events Found"

cat > "$REPORT_FILE" << EOF
=================================
LOG ANALYSIS REPORT
=================================

Date of Analysis: $(date)

Log File: $LOG_FILE

Total Lines Processed: $TOTAL_LINES

Total Error Count: $ERROR_COUNT

---------------------------------
Top 5 Error Messages
---------------------------------

$TOP_ERRORS

---------------------------------
Critical Events
---------------------------------

$CRITICAL_EVENTS

EOF

echo
echo "Report Generated: $REPORT_FILE"

mkdir -p archive

mv "$LOG_FILE" archive/

echo "Log archived successfully."
```

---

# Task 1: Input Validation

## Validation Performed

### Check Argument

```bash
if [ -z "$LOG_FILE" ]
```

Purpose:

Ensures a log file path is provided.

---

### Check File Exists

```bash
if [ ! -f "$LOG_FILE" ]
```

Purpose:

Prevents processing a non-existent file.

---

# Task 2: Error Count

### Command Used

```bash
grep -Ei "ERROR|Failed" logfile.log
```

Purpose:

Searches for:

* ERROR
* Failed

Then counts matching lines.

---

# Task 3: Critical Events

### Command Used

```bash
grep -n "CRITICAL" logfile.log
```

Purpose:

Displays:

* Critical event
* Line number

Example:

```text
84: CRITICAL Disk space below threshold
217: CRITICAL Database connection lost
```

---

# Task 4: Top 5 Error Messages

### Commands Used

```bash
grep
sort
uniq -c
sort -rn
head -5
```

Purpose:

* Extract error messages
* Count occurrences
* Sort by frequency
* Display top 5

Example:

```text
45 Connection timed out
32 File not found
28 Permission denied
15 Disk I/O error
9 Out of memory
```

---

# Task 5: Summary Report

Generated file:

```text
log_report_YYYY-MM-DD.txt
```

Contents:

* Date of analysis
* Log filename
* Total lines
* Error count
* Top 5 errors
* Critical events

---

# Task 6: Archive Processed Logs

### Commands Used

```bash
mkdir -p archive
mv logfile.log archive/
```

Purpose:

Store processed logs separately.

Benefits:

* Prevent duplicate processing
* Keep working directory clean
* Maintain log history

---

# Example Execution

```bash
chmod +x log_analyzer.sh

./log_analyzer.sh application.log
```

---

# Example Output

```text
Total Errors Found: 28

--- Critical Events ---

84: CRITICAL Disk space below threshold

217: CRITICAL Database connection lost

Report Generated: log_report_2026-06-15.txt

Log archived successfully.
```

---

# What I Learned

### 1. Log Analysis Can Be Automated

Bash can quickly process thousands of log entries.

---

### 2. grep + sort + uniq Is Powerful

These commands help identify recurring issues.

---

### 3. Reports Improve Troubleshooting

Generating a summary report saves investigation time during incidents.

---

# Why This Matters for DevOps

In production environments DevOps engineers regularly:

* Analyze application logs
* Investigate outages
* Identify recurring failures
* Monitor system health
* Generate operational reports

Automating these tasks improves response time and reduces manual effort.

---

# Files Created

```text
log_analyzer.sh

day-20-solution.md

log_report_<date>.txt
```

---

# Screenshots

Add screenshots for:

* Script execution
* Error count output
* Critical events output
* Generated report file
* Archive directory

