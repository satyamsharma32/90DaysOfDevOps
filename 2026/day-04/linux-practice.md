# Day 04 linux practice 
# Linux Practice Notes

## Process Checks

### Command 1

```bash
ps aux | head
```

### Observation

Used to check currently running processes in the Linux system.

---

### Command 2

```bash
pgrep ssh
```

### Observation

Used to find the process ID of the SSH service.

---

## Service Checks

### Command 3

```bash
systemctl status ssh
```

### Observation

Used to verify whether the SSH service is active and running.

---

### Command 4

```bash
systemctl list-units --type=service --state=running
```

### Observation

Used to list all active running services in the system.

---

## Log Checks

### Command 5

```bash
journalctl -u ssh --no-pager | tail -n 10
```

### Observation

Used to inspect recent logs related to the SSH service.

---

### Command 6

```bash
tail -n 20 /var/log/syslog
```

### Observation

Used to check the latest system log entries.

---

# Mini Troubleshooting Steps

## Step 1

```bash
pgrep ssh
```

Verified whether the SSH process was running.

---

## Step 2

```bash
systemctl status ssh
```

Checked the SSH service status and health.

---

## Step 3

```bash
journalctl -u ssh --no-pager | tail -n 10
```

Reviewed recent SSH logs for errors or warnings.

---

## Result

SSH service was running successfully without major issues.

