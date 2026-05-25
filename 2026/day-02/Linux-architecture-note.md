# Day 2 of linux learning

# Linux Architecture Notes

## Introduction

Linux is an operating system that manages:
- Hardware
- Memory
- Processes
- Applications
- Networking

Linux acts as a bridge between software and hardware.

---

# Core Components of Linux

Linux mainly consists of:

1. Kernel
2. User Space
3. Init/systemd

---

# 1. Kernel

The kernel is the core part of Linux.

It directly communicates with hardware and manages system resources.

## Responsibilities of Kernel

- Process management
- Memory management
- Device management
- File system management
- Networking
- Security

## Example

When we open a browser:
- Kernel allocates memory
- Gives CPU time
- Accesses disk
- Uses network hardware

Without the kernel, applications cannot communicate with hardware.

---

# 2. User Space

User space is where applications run.

Examples:
- Bash
- Docker
- VS Code
- Nginx
- Chrome

Applications use system calls to communicate with the kernel.

# 3. Init/systemd

After Linux boots:
- Kernel starts the first process

That process is:
bash
systemd

Its PID is:
bash
PID 1

Check using:
bash
ps -p 1


# What systemd Does

systemd is responsible for:
- Starting services
- Managing background processes
- Restarting failed services
- Boot management
- Logging
- Monitoring services

## Why systemd Matters

systemd helps DevOps engineers:
- Manage servers
- Troubleshoot applications
- Restart crashed services
- Monitor system health


# Process Management

Linux manages processes using Process IDs (PID).

Each running program gets:
- CPU time
- Memory
- System resources

Linux can:
- Start processes
- Stop processes
- Pause processes
- Restart processes

Every process has a unique PID (Process ID).


## Running State
The process is actively using CPU resources.

## Sleeping State
The process is waiting for input/output operations or resources.

## Stopped State
The process is paused manually or by system signals.

## Zombie State
The process has completed execution but still exists in the process table until the parent process reads its exit status.


# Daily Linux Commands

## 1. View Running Processes
bash
ps aux

## 2. Real-Time Process Monitoring
bash
top


## 3. Check Service Status
bash
systemctl status nginx


## 4. View System Logs
bash
journalctl -xe


## 5. Kill a Process
bash
kill PID


# Summary

- Kernel is the heart of Linux
- User space runs applications
- systemd manages services and boot process
- Linux manages processes using PID
- Process states help understand system behavior
- Linux commands are important for daily troubleshooting
- Linux knowledge is essential for DevOps engineers
