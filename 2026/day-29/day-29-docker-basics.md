# Day 29 - Introduction to Docker

## What is Docker?

Docker is a containerization platform that allows developers to package applications along with their dependencies and run them consistently across different environments.

Docker solves the common problem of:

> "It works on my machine but not on another machine."

By using containers, applications can run the same way on a developer's laptop, test server, and production server.

---

# What is a Container?

A container is a lightweight, isolated environment where an application runs.

A container includes:

* Application code
* Required libraries
* Dependencies
* Runtime environment

Containers share the host operating system kernel, making them fast and efficient.

### Container Creation Flow

Dockerfile → Docker Image → Docker Container

* **Dockerfile**: Instructions to build an image.
* **Docker Image**: Read-only template containing application and dependencies.
* **Docker Container**: Running instance of a Docker image.

---

# Why Do We Need Containers?

Without containers:

* Applications may behave differently on different systems.
* Dependency conflicts occur.
* Deployment becomes difficult.

With containers:

* Consistent environments
* Faster deployments
* Easy scalability
* Better resource utilization
* Portable across systems

---

# Containers vs Virtual Machines

| Feature        | Container             | Virtual Machine      |
| -------------- | --------------------- | -------------------- |
| OS             | Shares Host OS Kernel | Has its Own Guest OS |
| Startup Time   | Seconds               | Minutes              |
| Resource Usage | Lightweight           | Heavy                |
| Performance    | Faster                | Slower               |
| Storage        | Smaller               | Larger               |
| Isolation      | Process Level         | Hardware Level       |
| Portability    | High                  | Moderate             |

### In Simple Words

A Virtual Machine uses a Hypervisor and runs a complete operating system for each VM. Because every VM has its own OS, it consumes more RAM, CPU, and storage.

Containers do not require a separate operating system. They share the host OS kernel, making them lightweight, faster, and more efficient.

---

# Docker Architecture

Docker follows a Client-Server Architecture.

Components:

1. Docker Client
2. Docker Daemon
3. Docker Registry
4. Docker Images
5. Docker Containers

## Docker Client

The Docker Client is the command-line interface (CLI) used by users.

Example:

```bash
docker run nginx
docker ps
docker images
```

The client sends commands to the Docker Daemon.

## Docker Daemon

The Docker Daemon (dockerd) is the background service responsible for:

* Building images
* Running containers
* Managing networks
* Managing volumes

## Docker Registry

A Docker Registry stores Docker Images.

Example:

* Docker Hub

The daemon pulls images from registries when needed.

## Docker Images

Docker Images are read-only templates used to create containers.

Example:

```bash
nginx
ubuntu
mysql
```

## Docker Containers

Containers are running instances of Docker Images.

Example:

```bash
docker run nginx
```

This command creates and starts an Nginx container from the nginx image.

---

# Docker Architecture Diagram

```text
+-------------------+
|   Docker Client   |
| (docker commands) |
+---------+---------+
          |
          v
+-------------------+
|   Docker Daemon   |
|     (dockerd)     |
+----+---------+----+
     |         |
     |         |
     v         v
+---------+ +-----------+
| Images  | | Containers|
+---------+ +-----------+
     |
     v
+-------------------+
|   Docker Hub      |
|   (Registry)      |
+-------------------+
```

Flow:

1. User runs a Docker command.
2. Docker Client sends request to Docker Daemon.
3. Docker Daemon checks for required image.
4. If image is not available locally, it pulls from Docker Hub.
5. Docker Daemon creates and runs the container.

---

# Docker Installation Verification

```bash
docker --version
docker version
docker info
```

---

# Running Hello World Container

```bash
docker run hello-world
```

This command:

1. Checks for the hello-world image locally.
2. Downloads it from Docker Hub if not present.
3. Creates a container.
4. Runs the container.
5. Displays a success message.

---

# Useful Docker Commands

## Run Nginx Container

```bash
docker run -d -p 8080:80 --name my-nginx nginx
```

## Run Ubuntu Container

```bash
docker run -it ubuntu bash
```

## List Running Containers

```bash
docker ps
```

## List All Containers

```bash
docker ps -a
```

## Stop a Container

```bash
docker stop my-nginx
```

## Remove a Container

```bash
docker rm my-nginx
```

## View Logs

```bash
docker logs my-nginx
```

## Execute Command Inside Container

```bash
docker exec -it my-nginx bash
```

---

# Difference Between Interactive and Detached Mode

### Interactive Mode

```bash
docker run -it ubuntu bash
```

* Opens terminal inside container.
* User can interact directly.

### Detached Mode

```bash
docker run -d nginx
```

* Container runs in background.
* Terminal remains free for other commands.

---

# Key Learnings

* Docker is a containerization platform.
* Containers are lightweight and fast.
* Dockerfile → Image → Container.
* Containers share the host OS kernel.
* Virtual Machines require a separate Guest OS.
* Docker uses Client, Daemon, Images, Containers, and Registry.
* Docker Hub stores Docker images.
* Containers can run in interactive or detached mode.

