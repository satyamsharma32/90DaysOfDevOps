# This is day 5 linux practice 
# Linux Troubleshooting Runbook

## Target Service / Process

**Service Selected:** SSH

**Purpose:**
SSH is used for remote login and server administration. This drill focuses on verifying the health and availability of the SSH service.

---

# Environment Basics

## Command

```bash
uname -a
```

### Observation

Verified Linux kernel version, hostname, and system architecture.

---

## Command

```bash
cat /etc/os-release
```

### Observation

Confirmed Ubuntu operating system version and distribution details.

---

# Filesystem Sanity

## Command

```bash
mkdir /tmp/runbook-demo
```

### Observation

Created a temporary directory for filesystem testing.

---

## Command

```bash
cp /etc/hosts /tmp/runbook-demo/hosts-copy
ls -l /tmp/runbook-demo
```

### Observation

Verified file copy operation and checked file permissions.

---

# Snapshot: CPU & Memory

## Command

```bash
top
```

### Observation

Checked overall CPU utilization, memory usage, and running processes.

---

## Command

```bash
free -h
```

### Observation

Verified available RAM and swap usage. No memory pressure observed.

---

# Snapshot: Disk & IO

## Command

```bash
df -h
```

### Observation

Checked disk space utilization across mounted filesystems.

---

## Command

```bash
du -sh /var/log
```

### Observation

Reviewed total size of system log files to ensure logs are not consuming excessive disk space.

---

# Snapshot: Network

## Command

```bash
ss -tulpn
```

### Observation

Verified listening ports and confirmed SSH service is listening on port 22.

---

## Command

```bash
curl -I http://localhost
```

### Observation

Tested service connectivity and verified successful response from the local host.

---

# Logs Reviewed

## Command

```bash
journalctl -u ssh -n 50
```

### Observation

Reviewed the last 50 SSH service log entries. No critical errors observed.

---

## Command

```bash
tail -n 50 /var/log/syslog
```

### Observation

Reviewed recent system log messages for warnings or failures related to SSH.

---

# Quick Findings

* SSH service is active and accessible.
* CPU and memory utilization are within normal limits.
* Disk space is sufficient.
* Network port 22 is listening correctly.
* No critical issues identified in recent logs.

---

# If This Worsens (Next Steps)

1. Restart the SSH service and verify connectivity again.

```bash
sudo systemctl restart ssh
```

2. Increase log analysis using detailed journal entries.

```bash
journalctl -u ssh -xe
```

3. Capture deeper process activity and resource consumption.

```bash
top
ps aux | grep ssh
```

