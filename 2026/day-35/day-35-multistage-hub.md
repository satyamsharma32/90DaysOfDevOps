# Day 35 - Multi-Stage Builds & Docker Hub

## Objective

Today's goal was to learn:

* Why large Docker images are a problem
* How Multi-Stage Builds reduce image size
* How to push images to Docker Hub
* Docker image versioning and tags
* Docker image security and optimization best practices

---

# Why Image Size Matters

Large Docker images cause:

* Slower builds
* Slower deployments
* Higher storage usage
* Increased network transfer time
* Larger attack surface

In production environments, smaller images are preferred.

---

# Task 1: Single-Stage Build

## Simple Node.js Application

### app.js

```javascript id="qskkl5"
console.log("Hello from Docker!");
```

---

## Single-Stage Dockerfile

```dockerfile id="fgj23n"
FROM node:22

WORKDIR /app

COPY app.js .

CMD ["node", "app.js"]
```

---

## Build Image

```bash id="6ynr9e"
docker build -t node-single:v1 .
```

---

## Check Image Size

```bash id="66e0s4"
docker images
```

Example:

```text id="o1whw6"
REPOSITORY      TAG     SIZE
node-single     v1      1.1GB
```

Observation:

The image includes:

* Node runtime
* Package manager
* Build tools
* Development dependencies

Many of these are not required to run the application.

---

# Task 2: Multi-Stage Build

## What is a Multi-Stage Build?

A Multi-Stage Build uses multiple FROM statements.

One stage builds the application.

Another stage creates a lightweight runtime image.

Only the required files are copied into the final image.

---

## Multi-Stage Dockerfile

```dockerfile id="q75bjy"
# Build Stage

FROM node:22 AS builder

WORKDIR /app

COPY app.js .

# Runtime Stage

FROM alpine:3.22

WORKDIR /app

COPY --from=builder /app/app.js .

RUN apk add --no-cache nodejs

CMD ["node", "app.js"]
```

---

## Build Image

```bash id="p8xfm6"
docker build -t node-multistage:v1 .
```

---

## Compare Sizes

```bash id="md4cth"
docker images
```

Example:

```text id="8cw17r"
REPOSITORY         TAG      SIZE
node-single        v1       1.1GB
node-multistage    v1       70MB
```

---

# Why is Multi-Stage Smaller?

The final image contains only:

* Application files
* Runtime dependencies

It does not include:

* Build tools
* Package managers
* Temporary files
* Source code not needed at runtime

Benefits:

* Smaller size
* Faster deployments
* Better security
* Lower storage usage

---

# Multi-Stage Build Flow

```text id="h0n9iv"
Build Stage
      |
      v
Compile Application
      |
      v
Copy Artifact
      |
      v
Minimal Runtime Image
```

---

# Task 3: Push Image to Docker Hub

## Create Docker Hub Account

Create a free account on Docker Hub.

---

## Login

```bash id="j2t7o6"
docker login
```

Enter:

```text id="v6d7nd"
Docker Hub Username
Docker Hub Password
```

---

## Verify Login

```bash id="mlad6n"
docker info
```

---

## Tag Image

Syntax:

```bash id="ng4nml"
docker tag local-image username/image-name:tag
```

Example:

```bash id="egsvhx"
docker tag node-multistage:v1 yourusername/node-demo:v1
```

---

## Push Image

```bash id="gjdqwv"
docker push yourusername/node-demo:v1
```

Output:

```text id="n7z3up"
Pushed successfully
```

---

# Verify Upload

Visit:

```text id="mcbmfh"
https://hub.docker.com
```

Check repository:

```text id="4qgkqv"
yourusername/node-demo
```

Verify image appears.

---

# Pull Image Again

Remove local image:

```bash id="rh4r9v"
docker rmi yourusername/node-demo:v1
```

Pull from Docker Hub:

```bash id="lf5dbn"
docker pull yourusername/node-demo:v1
```

Run:

```bash id="jkq0j4"
docker run yourusername/node-demo:v1
```

Expected Output:

```text id="v2nbg4"
Hello from Docker!
```

---

# Task 4: Docker Hub Repository

## Repository Description

Example:

```text id="80mfqb"
Simple Node.js application demonstrating Docker Multi-Stage Builds.
```

A good description helps other users understand the image.

---

# Docker Image Tags

Examples:

```text id="y8thqv"
v1
v2
1.0.0
latest
production
development
```

Tags represent image versions.

---

## Pull Latest Tag

```bash id="o7b4od"
docker pull yourusername/node-demo:latest
```

Pulls:

```text id="ntxvme"
Most recent default version
```

---

## Pull Specific Tag

```bash id="2j08af"
docker pull yourusername/node-demo:v1
```

Pulls:

```text id="mqw5r5"
Exactly version v1
```

---

# Why Avoid latest in Production?

Bad Practice:

```dockerfile id="ik1m0f"
FROM node:latest
```

Problem:

```text id="0n6g8o"
Image changes unexpectedly
```

Deployment may behave differently.

---

## Better Practice

```dockerfile id="b9lhxm"
FROM node:22.18-alpine
```

Benefits:

* Predictable builds
* Consistent deployments

---

# Task 5: Docker Image Best Practices

---

# Use Minimal Base Images

Compare:

```dockerfile id="9eih4s"
FROM ubuntu
```

vs

```dockerfile id="q8bwzl"
FROM alpine
```

Example Sizes:

```text id="fd0q5u"
Ubuntu = 78MB+
Alpine = 8MB+
```

Benefits:

* Smaller images
* Faster pulls
* Better security

---

# Run as Non-Root User

Bad:

```dockerfile id="2rkxgg"
USER root
```

Root has full privileges.

---

## Better

```dockerfile id="74f67t"
RUN adduser -D appuser

USER appuser
```

Benefits:

* Improved security
* Reduced risk

---

# Combine RUN Commands

Bad:

```dockerfile id="3pt5y8"
RUN apk update

RUN apk add nodejs

RUN apk add npm
```

Creates multiple layers.

---

## Better

```dockerfile id="4y9c5h"
RUN apk update && \
    apk add --no-cache nodejs npm
```

Benefits:

* Fewer layers
* Smaller images

---

# Use Specific Tags

Bad:

```dockerfile id="5w6r8q"
FROM nginx:latest
```

---

## Better

```dockerfile id="8nmzcu"
FROM nginx:1.29-alpine
```

Benefits:

* Predictable deployments
* Stable builds

---

# Before and After Optimization

Example:

| Build Type             | Image Size |
| ---------------------- | ---------- |
| Single Stage           | 1.1GB      |
| Multi-Stage            | 70MB       |
| Optimized Alpine Build | 45MB       |

Observation:

Optimization significantly reduces image size.

---

# Multi-Stage Build Benefits

* Smaller images
* Faster deployments
* Better security
* Less storage usage
* Cleaner Dockerfiles
* Production-ready builds

---

# Useful Commands

## Build Image

```bash id="3v86yo"
docker build -t myimage:v1 .
```

---

## View Images

```bash id="rvrv41"
docker images
```

---

## Login to Docker Hub

```bash id="9jv3s0"
docker login
```

---

## Tag Image

```bash id="m6qah6"
docker tag image username/image:v1
```

---

## Push Image

```bash id="awitmn"
docker push username/image:v1
```

---

## Pull Image

```bash id="bhm5kz"
docker pull username/image:v1
```

---

## Run Image

```bash id="eclv81"
docker run username/image:v1
```

---

# Key Learnings

* Large Docker images slow down deployments and consume more resources.
* Multi-Stage Builds separate build and runtime environments.
* Only required artifacts are copied to the final image.
* Docker Hub is used to store and distribute Docker images.
* Image tags provide version control.
* Avoid using latest in production environments.
* Alpine images are significantly smaller than Ubuntu images.
* Running containers as non-root improves security.
* Combining RUN commands reduces image layers.
* Multi-Stage Builds are a common production and interview topic.

