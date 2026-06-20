# Day 31 - Dockerfile: Build Your Own Images

## Objective

Today's goal was to learn how to create custom Docker Images using Dockerfiles.

By the end of this task, I understood:

* What a Dockerfile is
* How to build custom Docker images
* Common Dockerfile instructions
* Difference between CMD and ENTRYPOINT
* Building a simple web application image
* Using .dockerignore
* Docker build cache and optimization

---

# What is a Dockerfile?

A Dockerfile is a text file containing instructions used to build a Docker image.

Instead of manually creating containers and installing software every time, we define the entire setup in a Dockerfile.

Docker then creates the image automatically.

### Build Flow

```text
Dockerfile → Docker Image → Docker Container
```

---

# Task 1: My First Dockerfile

## Dockerfile

```dockerfile
FROM ubuntu

RUN apt-get update && apt-get install -y curl

CMD ["echo", "Hello from my custom image!"]
```

### Explanation

### FROM

```dockerfile
FROM ubuntu
```

Uses Ubuntu as the base image.

### RUN

```dockerfile
RUN apt-get update && apt-get install -y curl
```

Executes commands during image build.

Installs curl inside the image.

### CMD

```dockerfile
CMD ["echo", "Hello from my custom image!"]
```

Default command executed when the container starts.

---

## Build the Image

```bash
docker build -t my-ubuntu:v1 .
```

### Verify Image

```bash
docker images
```

---

## Run the Container

```bash
docker run my-ubuntu:v1
```

Expected Output:

```text
Hello from my custom image!
```

---

# Task 2: Dockerfile Instructions

## Example Dockerfile

```dockerfile
FROM ubuntu

RUN apt-get update && apt-get install -y curl

WORKDIR /app

COPY sample.txt .

EXPOSE 8080

CMD ["bash"]
```

---

## Dockerfile Instructions Explained

### FROM

Defines the base image.

```dockerfile
FROM ubuntu
```

---

### RUN

Executes commands during image build.

```dockerfile
RUN apt-get update
```

---

### COPY

Copies files from host machine into image.

```dockerfile
COPY sample.txt .
```

---

### WORKDIR

Sets the working directory.

```dockerfile
WORKDIR /app
```

Equivalent to:

```bash
cd /app
```

inside the container.

---

### EXPOSE

Documents which port the application uses.

```dockerfile
EXPOSE 8080
```

---

### CMD

Default command executed when container starts.

```dockerfile
CMD ["bash"]
```

---

# Task 3: CMD vs ENTRYPOINT

---

## CMD Example

Dockerfile:

```dockerfile
FROM ubuntu

CMD ["echo", "hello"]
```

Build:

```bash
docker build -t cmd-demo .
```

Run:

```bash
docker run cmd-demo
```

Output:

```text
hello
```

Run with custom command:

```bash
docker run cmd-demo ls
```

Output:

```text
CMD gets replaced by ls
```

---

## ENTRYPOINT Example

Dockerfile:

```dockerfile
FROM ubuntu

ENTRYPOINT ["echo"]
```

Build:

```bash
docker build -t entry-demo .
```

Run:

```bash
docker run entry-demo hello
```

Output:

```text
hello
```

Run:

```bash
docker run entry-demo Dockerfile
```

Output:

```text
Dockerfile
```

ENTRYPOINT remains fixed and arguments are appended.

---

# CMD vs ENTRYPOINT

| CMD                        | ENTRYPOINT                |
| -------------------------- | ------------------------- |
| Default command            | Fixed command             |
| Can be overridden          | Harder to override        |
| Used for optional defaults | Used for main application |

### When to Use CMD

Use CMD when users may want to run different commands.

Example:

```dockerfile
CMD ["bash"]
```

---

### When to Use ENTRYPOINT

Use ENTRYPOINT when the container should always execute a specific program.

Example:

```dockerfile
ENTRYPOINT ["nginx"]
```

---

# Task 4: Build a Simple Web App Image

## Create index.html

```html
<!DOCTYPE html>
<html>
<head>
<title>My Website</title>
</head>
<body>
<h1>Hello from Docker!</h1>
</body>
</html>
```

---

## Dockerfile

```dockerfile
FROM nginx:alpine

COPY index.html /usr/share/nginx/html/index.html
```

---

## Build Image

```bash
docker build -t my-website:v1 .
```

---

## Run Container

```bash
docker run -d -p 8080:80 --name website my-website:v1
```

---

## Verify

Open browser:

```text
http://localhost:8080
```

Expected Output:

```text
Hello from Docker!
```

---

# Task 5: .dockerignore

## Example File

```text
node_modules
.git
*.md
.env
```

---

## Why Use .dockerignore?

Benefits:

* Smaller build context
* Faster image builds
* Improved security
* Reduced image size

Files matching these patterns are not sent to Docker during build.

---

# Task 6: Build Optimization

## First Build

```bash
docker build -t cache-demo .
```

Docker builds all layers.

---

## Second Build

Run build again:

```bash
docker build -t cache-demo .
```

Docker reuses existing layers from cache.

Build becomes much faster.

---

## Why Layer Order Matters

Bad Example:

```dockerfile
COPY . .

RUN npm install
```

Any code change invalidates cache.

Docker must reinstall all dependencies.

---

## Better Example

```dockerfile
COPY package.json .

RUN npm install

COPY . .
```

Benefits:

* Dependency layer stays cached.
* Faster builds.
* Less resource usage.

---

# Docker Build Cache

Docker stores previously built layers.

When rebuilding:

* Unchanged layers are reused.
* Changed layers are rebuilt.

This significantly reduces build time.

---

# Key Learnings

* Dockerfiles automate image creation.
* FROM specifies the base image.
* RUN executes commands during build.
* COPY transfers files into images.
* WORKDIR sets the working directory.
* EXPOSE documents application ports.
* CMD defines the default command.
* ENTRYPOINT defines the main executable.
* .dockerignore reduces build context size.
* Docker layers improve build performance through caching.
* Proper Dockerfile ordering improves build speed.
* Dockerfile → Image → Container is the standard workflow.

