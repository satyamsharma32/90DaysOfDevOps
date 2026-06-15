
# Day 15 – Networking Concepts: DNS, IP, Subnets & Ports

## Objective

Understand the core networking concepts every DevOps Engineer should know, including DNS, IP addressing, subnetting, CIDR notation, and ports.

---

# Task 1: DNS – How Names Become IPs

## What Happens When You Type google.com in a Browser?

1. The browser checks its cache for the IP address.
2. If not found, the system queries a DNS server.
3. DNS resolves the domain name to an IP address.
4. The browser connects to that IP address and loads the website.

---

## Common DNS Record Types

### A Record

Maps a domain name to an IPv4 address.

### AAAA Record

Maps a domain name to an IPv6 address.

### CNAME Record

Maps one domain name to another domain name.

### MX Record

Specifies mail servers responsible for receiving emails.

### NS Record

Identifies the authoritative DNS servers for a domain.

---

## DNS Lookup

### Command

```bash
dig google.com
```

### Observation

* Identified the A record (IPv4 address).
* Observed the TTL (Time To Live) value returned by DNS.

---

# Task 2: IP Addressing

## What Is an IPv4 Address?

An IPv4 address is a unique 32-bit identifier assigned to a device on a network.

Example:

```text
192.168.1.10
```

It consists of four octets separated by dots.

---

## Public vs Private IP Addresses

### Public IP

Accessible over the internet.

Example:

```text
8.8.8.8
```

---

### Private IP

Used inside private networks and not directly reachable from the internet.

Example:

```text
192.168.1.100
```

---

## Private IP Address Ranges

### Class A

```text
10.0.0.0 – 10.255.255.255
```

### Class B

```text
172.16.0.0 – 172.31.255.255
```

### Class C

```text
192.168.0.0 – 192.168.255.255
```

---

## Identify Your IP Address

### Command

```bash
ip addr show
```

### Observation

Checked available network interfaces and identified private IP addresses assigned to the system.

---

# Task 3: CIDR & Subnetting

## What Does /24 Mean?

Example:

```text
192.168.1.0/24
```

The first 24 bits represent the network portion and the remaining 8 bits represent host addresses.

---

## Usable Hosts

### /24

```text
Total IPs = 256
Usable Hosts = 254
```

---

### /16

```text
Total IPs = 65,536
Usable Hosts = 65,534
```

---

### /28

```text
Total IPs = 16
Usable Hosts = 14
```

---

## Why Do We Subnet?

Subnetting helps:

* Organize networks efficiently.
* Reduce broadcast traffic.
* Improve security.
* Manage IP addresses effectively.

---

## CIDR Practice Table

| CIDR | Subnet Mask     | Total IPs | Usable Hosts |
| ---- | --------------- | --------- | ------------ |
| /24  | 255.255.255.0   | 256       | 254          |
| /16  | 255.255.0.0     | 65,536    | 65,534       |
| /28  | 255.255.255.240 | 16        | 14           |

---

# Task 4: Ports – The Doors to Services

## What Is a Port?

A port is a logical communication endpoint used by applications and services.

Ports allow multiple services to run on the same IP address.

---

## Common Ports

| Port  | Service |
| ----- | ------- |
| 22    | SSH     |
| 80    | HTTP    |
| 443   | HTTPS   |
| 53    | DNS     |
| 3306  | MySQL   |
| 6379  | Redis   |
| 27017 | MongoDB |

---

## Check Listening Ports

### Command

```bash
ss -tulpn
```

### Observation

Identified listening services and their associated ports.

Example:

```text
SSH listening on port 22
Docker listening on its configured port
```

---

# Task 5: Putting It Together

## Scenario 1

### Question

You run:

```bash
curl http://myapp.com:8080
```

What networking concepts are involved?

### Answer

* DNS resolves myapp.com to an IP address.
* TCP establishes a connection to port 8080.
* HTTP sends a request over the TCP connection.
* IP routing delivers packets between systems.

---

## Scenario 2

### Question

Your application cannot reach a database at:

```text
10.0.1.50:3306
```

What would you check first?

### Answer

1. Verify network connectivity using ping.
2. Check whether port 3306 is reachable.
3. Confirm the database service is running.
4. Verify firewall and security group rules.

---

# Commands Used

```bash
dig google.com
ip addr show
ss -tulpn
ping
curl
```

---

# What I Learned

### 1. DNS Converts Names to IP Addresses

Applications rely on DNS before communication can begin.

### 2. CIDR Defines Network Size

CIDR notation determines how many hosts can exist in a subnet.

### 3. Ports Identify Services

Different services listen on specific ports to receive network traffic.

---

# Why This Matters for DevOps

DevOps Engineers use these concepts daily when:

* Troubleshooting connectivity issues.
* Debugging application communication.
* Managing cloud networking.
* Configuring load balancers.
* Securing infrastructure using ports and firewalls.

Understanding DNS, IPs, subnets, and ports makes troubleshooting faster and more effective.

---

# Screenshots

Add screenshots for:

* dig google.com
* ip addr show
* ss -tulpn
* ping output
* curl output


