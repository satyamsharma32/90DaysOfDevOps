# Day 33 - Docker Compose: Multi-Container Basics

## Objective

Today's goal was to understand Docker Compose and manage multi-container applications using a single YAML configuration file.

By the end of this task, I learned:

* What Docker Compose is
* Why Docker Compose is useful
* How to create docker-compose.yml files
* How multiple containers communicate automatically
* Managing volumes and networks using Compose
* Using environment variables in Compose
* Common Docker Compose commands

---

# What is Docker Compose?

Docker Compose is a tool used to define and run multi-container Docker applications.

Instead of running multiple docker commands manually, we define all services inside a YAML file.

Example:

Without Compose:

```bash
docker run mysql
docker run wordpress
docker network create my-network
docker volume create mysql-data
```

With Compose:

```bash
docker compose up
```

Everything is created automatically.

---

# Why Use Docker Compose?

Benefits:

* Easier container management
* Infrastructure as Code
* Automatic networking
* Automatic volume creation
* Simplified deployments
* Easy scaling

---

# Task 1: Verify Docker Compose

## Check Compose Version

```bash
docker compose version
```

Example Output:

```text
Docker Compose version v2.x.x
```

---

# Task 2: First Docker Compose File

## Project Structure

```text
compose-basics/
└── docker-compose.yml
```

---

## docker-compose.yml

```yaml
services:
  nginx:
    image: nginx
    ports:
      - "8080:80"
```

---

## Start Services

```bash
docker compose up
```

Output:

```text
Creating network
Creating container
Starting nginx
```

---

## Access Browser

```text
http://localhost:8080
```

Nginx welcome page should appear.

---

## Stop and Remove Everything

```bash
docker compose down
```

Observation:

* Container removed
* Network removed

---

# Task 3: WordPress + MySQL Setup

## Architecture

```text
WordPress Container
         |
         |
         v
MySQL Container
         |
         |
         v
Docker Volume
```

---

## docker-compose.yml

```yaml
services:

  db:
    image: mysql:8
    container_name: mysql-db

    environment:
      MYSQL_ROOT_PASSWORD: rootpassword
      MYSQL_DATABASE: wordpressdb
      MYSQL_USER: wordpressuser
      MYSQL_PASSWORD: wordpresspass

    volumes:
      - mysql_data:/var/lib/mysql

  wordpress:
    image: wordpress
    container_name: wordpress-app

    ports:
      - "8080:80"

    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wordpressuser
      WORDPRESS_DB_PASSWORD: wordpresspass
      WORDPRESS_DB_NAME: wordpressdb

    depends_on:
      - db

volumes:
  mysql_data:
```

---

# Start Application

```bash
docker compose up -d
```

Verify:

```bash
docker ps
```

Expected Containers:

```text
mysql-db
wordpress-app
```

---

# Access WordPress

Open:

```text
http://localhost:8080
```

Complete WordPress installation.

---

# Data Persistence Verification

Stop application:

```bash
docker compose down
```

Start again:

```bash
docker compose up -d
```

Observation:

WordPress configuration and database data remain intact.

Reason:

MySQL data is stored in a Docker Volume.

---

# How WordPress Connects to MySQL

In Compose:

```yaml
WORDPRESS_DB_HOST: db
```

Why does this work?

Docker Compose automatically creates:

* A network
* Internal DNS

The service name:

```text
db
```

automatically resolves to the MySQL container IP.

No manual networking required.

---

# Task 4: Common Docker Compose Commands

---

## Start Services

```bash
docker compose up
```

---

## Start in Detached Mode

```bash
docker compose up -d
```

Runs containers in background.

---

## View Running Services

```bash
docker compose ps
```

---

## View All Logs

```bash
docker compose logs
```

---

## Follow Logs

```bash
docker compose logs -f
```

---

## Logs of Specific Service

```bash
docker compose logs wordpress
```

or

```bash
docker compose logs db
```

---

## Stop Services

```bash
docker compose stop
```

Containers stop but remain available.

---

## Start Stopped Services

```bash
docker compose start
```

---

## Restart Services

```bash
docker compose restart
```

---

## Remove Containers and Networks

```bash
docker compose down
```

Removes:

* Containers
* Networks

Keeps volumes.

---

## Remove Everything Including Volumes

```bash
docker compose down -v
```

Removes:

* Containers
* Networks
* Volumes

Warning:

Database data will be lost.

---

## Rebuild Images

```bash
docker compose up --build
```

Useful after Dockerfile changes.

---

# Task 5: Environment Variables

---

# Direct Variables in Compose

Example:

```yaml
environment:
  MYSQL_ROOT_PASSWORD: rootpassword
  MYSQL_DATABASE: appdb
```

Works but not ideal.

Passwords become visible inside the compose file.

---

# Using a .env File

Create:

```text
.env
```

Contents:

```env
MYSQL_ROOT_PASSWORD=rootpassword
MYSQL_DATABASE=appdb
MYSQL_USER=appuser
MYSQL_PASSWORD=apppassword
```

---

## Reference Variables

docker-compose.yml

```yaml
services:

  db:
    image: mysql

    environment:
      MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
      MYSQL_DATABASE: ${MYSQL_DATABASE}
      MYSQL_USER: ${MYSQL_USER}
      MYSQL_PASSWORD: ${MYSQL_PASSWORD}
```

---

## Start Compose

```bash
docker compose up -d
```

Docker automatically loads values from:

```text
.env
```

---

# Verify Environment Variables

Inspect Container:

```bash
docker inspect mysql-db
```

Or:

```bash
docker exec -it mysql-db env
```

Example Output:

```text
MYSQL_DATABASE=appdb
MYSQL_USER=appuser
```

---

# Docker Compose Workflow

```text
docker-compose.yml
         |
         v
docker compose up
         |
         v
Networks Created
Volumes Created
Containers Created
Services Connected
```

---

# Advantages of Docker Compose

* Single YAML file
* Reproducible environments
* Easy deployments
* Automatic networking
* Automatic DNS resolution
* Simplified development workflow
* Infrastructure as Code approach

---

# Key Learnings

* Docker Compose manages multi-container applications.
* All services are defined inside docker-compose.yml.
* Docker Compose automatically creates networks.
* Services communicate using service names.
* Volumes provide persistent storage.
* Environment variables improve configuration management.
* docker compose up starts the application stack.
* docker compose down removes containers and networks.
* Docker Compose greatly simplifies development and testing environments.
* Compose is commonly used in DevOps projects before moving applications to Kubernetes.

