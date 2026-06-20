# Day 30 - Docker Images & Container Lifecycle

## Objective

Today's goal was to understand:

* Docker Images
* Image Layers
* Container Lifecycle
* Working with Running Containers
* Docker Cleanup Commands

---

# What is a Docker Image?

A Docker Image is a read-only template used to create containers.

It contains:

* Application code
* Dependencies
* Libraries
* Runtime
* Configuration

A container is simply a running instance of an image.

### Relationship

```text
Dockerfile → Docker Image → Docker Container
```

Example:

```bash
docker run nginx
```

Docker uses the nginx image and creates a running container from it.

---

# Pulling Images

## Pull Nginx Image

```bash
docker pull nginx
```

## Pull Ubuntu Image

```bash
docker pull ubuntu
```

## Pull Alpine Image

```bash
docker pull alpine
```

---

# List Images

```bash
docker images
```

Example Output:

```text
REPOSITORY   TAG       IMAGE ID       SIZE
nginx        latest    abc123         192MB
ubuntu       latest    def456         78MB
alpine       latest    ghi789         8MB
```

---

# Ubuntu vs Alpine

| Ubuntu                 | Alpine                         |
| ---------------------- | ------------------------------ |
| Larger image size      | Very small image size          |
| More packages included | Minimal packages               |
| Easier for beginners   | Lightweight and fast           |
| Good for development   | Good for production containers |

### Why is Alpine Smaller?

Alpine Linux is designed to be lightweight.

It contains:

* Minimal packages
* Smaller libraries
* Less disk usage

This results in:

* Faster downloads
* Faster container startup
* Lower storage usage

---

# Inspecting an Image

```bash
docker image inspect nginx
```

Information Available:

* Image ID
* Creation Date
* Architecture
* Environment Variables
* Layers
* Tags

---

# Remove an Image

```bash
docker rmi alpine
```

Removes the image if no container is using it.

---

# Docker Image Layers

Check image history:

```bash
docker image history nginx
```

Example Output:

```text
IMAGE          CREATED       SIZE
layer1         2 weeks ago   120MB
layer2         2 weeks ago   50MB
layer3         2 weeks ago   0B
layer4         2 weeks ago   20MB
```

---

# What are Layers?

A Docker image is built using multiple layers.

Each Dockerfile instruction creates a new layer.

Example:

```dockerfile
FROM ubuntu
RUN apt update
RUN apt install nginx
COPY . /app
```

Each instruction above creates a separate layer.

---

# Why Docker Uses Layers

Benefits:

* Faster image builds
* Layer reuse
* Less storage consumption
* Efficient image downloads

Docker only downloads missing layers instead of the entire image.

---

# Container Lifecycle

A container goes through several states.

```text
Created
   ↓
Running
   ↓
Paused
   ↓
Running
   ↓
Stopped
   ↓
Removed
```

---

# Create Container Without Starting

```bash
docker create --name my-nginx nginx
```

Check:

```bash
docker ps -a
```

Status:

```text
Created
```

---

# Start Container

```bash
docker start my-nginx
```

Status:

```text
Up
```

---

# Pause Container

```bash
docker pause my-nginx
```

Status:

```text
Paused
```

---

# Unpause Container

```bash
docker unpause my-nginx
```

Status:

```text
Up
```

---

# Stop Container

```bash
docker stop my-nginx
```

Status:

```text
Exited
```

---

# Restart Container

```bash
docker restart my-nginx
```

Status:

```text
Up
```

---

# Kill Container

```bash
docker kill my-nginx
```

Immediately stops the container without graceful shutdown.

---

# Remove Container

```bash
docker rm my-nginx
```

Status:

Container removed.

---

# Working with Running Containers

## Run Nginx in Detached Mode

```bash
docker run -d --name nginx-server -p 8080:80 nginx
```

### Explanation

* -d → Run in background
* --name → Custom container name
* -p → Port mapping

Access:

```text
http://localhost:8080
```

---

# View Logs

```bash
docker logs nginx-server
```

Shows container logs.

---

# View Logs in Real Time

```bash
docker logs -f nginx-server
```

Displays logs continuously.

Press:

```text
Ctrl + C
```

to exit.

---

# Enter Running Container

```bash
docker exec -it nginx-server bash
```

Explore filesystem:

```bash
pwd
ls
cd /usr/share/nginx/html
ls
```

---

# Run Single Command Inside Container

```bash
docker exec nginx-server hostname
```

Runs a command without entering the container.

---

# Inspect Container

```bash
docker inspect nginx-server
```

Useful Information:

* Container ID
* IP Address
* Port Mapping
* Mounts
* Network Configuration

Find IP Address:

```bash
docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' nginx-server
```

---

# Cleanup Commands

## Stop All Running Containers

```bash
docker stop $(docker ps -q)
```

---

## Remove All Stopped Containers

```bash
docker container prune
```

---

## Remove Unused Images

```bash
docker image prune
```

---

## Remove Everything Unused

```bash
docker system prune
```

---

# Check Docker Disk Usage

```bash
docker system df
```

Shows:

* Images size
* Containers size
* Volumes size
* Cache usage

---

# Key Learnings

* Docker Images are templates used to create containers.
* Containers are running instances of images.
* Docker images are built using layers.
* Layers improve caching and storage efficiency.
* Containers have a lifecycle: Create → Run → Pause → Stop → Remove.
* Docker provides commands for logs, inspection, and cleanup.
* Alpine is much smaller than Ubuntu because it contains only essential packages.

