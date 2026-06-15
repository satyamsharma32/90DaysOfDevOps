# Day 14 – Networking Fundamentals & Hands-on Checks

## Objective

Learn basic networking concepts and practice common troubleshooting commands used by DevOps Engineers.

---

# Quick Concepts

## OSI Model (Layers 1–7)

### Layer 1 – Physical

* Physical cables, switches, and network hardware.
* Responsible for transmitting bits.

### Layer 2 – Data Link

* MAC addresses and switching.
* Responsible for communication within the same network.

### Layer 3 – Network

* IP addressing and routing.
* Responsible for packet delivery between networks.

### Layer 4 – Transport

* TCP and UDP protocols.
* Responsible for reliable or fast communication.

### Layer 5 – Session

* Establishes and manages sessions between applications.

### Layer 6 – Presentation

* Data encryption, compression, and formatting.

### Layer 7 – Application

* User-facing protocols like HTTP, HTTPS, DNS, SSH.

---

## TCP/IP Model

### Link Layer

* Physical and Data Link functionality.

### Internet Layer

* IP addressing and routing.

### Transport Layer

* TCP and UDP communication.

### Application Layer

* HTTP, HTTPS, DNS, SSH, FTP.

## Real Example

```text
curl https://example.com

Application Layer (HTTPS)
        ↓
Transport Layer (TCP)
        ↓
Internet Layer (IP)
        ↓
Link Layer (Ethernet/Wi-Fi)
```

---

# Target Host

Target selected for testing:

```text
google.com
```

---

# Identity Check

## Command

```bash
hostname -I
```

### Observation

Displayed the IP address assigned to the system.

---

# Reachability Test

## Command

```bash
ping google.com
```

### Observation

Verified connectivity to the target host and checked packet loss and latency.

---

# Path Check

## Command

```bash
traceroute google.com
```

or

```bash
tracepath google.com
```

### Observation

Displayed the network path taken to reach the destination.

---

# Open Ports Check

## Command

```bash
ss -tulpn
```

### Observation

Listed listening services and their associated ports.

Example:

```text
SSH listening on port 22
```

---

# DNS Resolution Check

## Command

```bash
nslookup google.com
```

or

```bash
dig google.com
```

### Observation

Successfully resolved the domain name into an IP address.

---

# HTTP Connectivity Check

## Command

```bash
curl -I https://google.com
```

### Observation

Received HTTP response headers and verified status code.

---

# Connection Snapshot

## Command

```bash
netstat -an | head
```

### Observation

Displayed active and listening network connections.

---

# Mini Task – Port Probe

## Identify Listening Port

Using:

```bash
ss -tulpn
```

Example service:

```text
SSH running on port 22
```

---

## Test Port Reachability

### Command

```bash
nc -zv localhost 22
```

### Observation

Successfully connected to the listening port.

---

## Interpretation

Port is reachable from the local system.

If unreachable:

### Next Checks

```bash
systemctl status ssh
```

```bash
journalctl -u ssh -n 20
```

```bash
sudo ufw status
```

---

# Reflection

## Which command gives the fastest signal when something is broken?

```bash
ping
```

Reason:

Quickly verifies basic network connectivity.

---

## What layer would you inspect if DNS fails?

### Application Layer

Commands:

```bash
nslookup
```

```bash
dig
```

---

## What layer would you inspect if HTTP 500 appears?

### Application Layer

Reason:

HTTP 500 indicates an application or web server issue rather than a network problem.

---

## Two Follow-Up Checks During a Real Incident

### Check Service Status

```bash
systemctl status nginx
```

Purpose:

Verify whether the application service is running.

---

### Review Logs

```bash
journalctl -u nginx -n 50
```

Purpose:

Identify application or service-related errors.

---

# Commands Used

```bash
hostname -I
ping
traceroute
tracepath
ss -tulpn
nslookup
dig
curl -I
netstat -an
nc -zv
```

---

# What I Learned

### 1. Networking Troubleshooting Starts with Connectivity

Use ping and traceroute to verify communication paths.

### 2. DNS Resolution Is Critical

If DNS fails, applications may appear unavailable even though servers are healthy.

### 3. Ports and Services Must Be Verified Together

A running service must also be listening on the expected port.

---

# Why This Matters for DevOps

DevOps engineers use these commands daily to:

* Troubleshoot connectivity issues.
* Verify service availability.
* Investigate DNS failures.
* Debug application access problems.
* Identify network bottlenecks quickly.

---

# Screenshots

Add screenshots for:

* hostname -I
* ping output
* traceroute output
* ss -tulpn output
* nslookup or dig output
* curl -I output
* nc -zv output

