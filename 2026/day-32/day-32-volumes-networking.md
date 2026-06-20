# Day 32 - Docker Volumes & Networking

## Objective

Today's goal was to understand:

* Why containers lose data
* How Docker Volumes provide persistence
* Difference between Named Volumes and Bind Mounts
* Docker Networking Basics
* Container-to-Container Communication
* Custom Bridge Networks

---

# Understanding the Problem

Containers are ephemeral.

This means:

* Containers can be created and destroyed easily.
* Any data stored inside a container is lost when the container is removed.

Example:

```text
Container Removed
        ↓
Data Removed
```

This creates a problem for databases and applications that need persistent storage.

Docker Volumes solve this problem.

---

# Task 1: Data Loss Without Volumes

## Run PostgreSQL Container

```bash
docker run -d \
--name postgres-db \
-e POSTGRES_PASSWORD=password \
postgres
```

Verify:

```bash
docker ps
```

---

## Enter Container

```bash
docker exec -it postgres-db bash
```

Connect to PostgreSQL:

```bash
psql -U postgres
```

---

## Create Sample Data

```sql
CREATE TABLE employees(
id INT,
name VARCHAR(50)
);

INSERT INTO employees VALUES (1,'John');

SELECT * FROM employees;
```

Output:

```text
 id | name
----+------
 1  | John
```

---

## Remove Container

```bash
docker stop postgres-db
docker rm postgres-db
```

---

## Run New Container

```bash
docker run -d \
--name postgres-db-new \
-e POSTGRES_PASSWORD=password \
postgres
```

Check database again.

Observation:

```text
Table does not exist.
```

### Why?

Because the database files were stored inside the container.

When the container was removed, the data was removed as well.

---

# Task 2: Named Volumes

## Create Volume

```bash
docker volume create postgres-data
```

Verify:

```bash
docker volume ls
```

---

## Run Database With Volume

```bash
docker run -d \
--name postgres-db \
-e POSTGRES_PASSWORD=password \
-v postgres-data:/var/lib/postgresql/data \
postgres
```

---

## Create Data

```sql
CREATE TABLE employees(
id INT,
name VARCHAR(50)
);

INSERT INTO employees VALUES (1,'John');
```

---

## Remove Container

```bash
docker stop postgres-db
docker rm postgres-db
```

---

## Create New Container Using Same Volume

```bash
docker run -d \
--name postgres-db-new \
-e POSTGRES_PASSWORD=password \
-v postgres-data:/var/lib/postgresql/data \
postgres
```

---

## Verify Data

```sql
SELECT * FROM employees;
```

Output:

```text
 id | name
----+------
 1  | John
```

### Observation

Data still exists.

Reason:

The data is stored in the Docker Volume, not inside the container.

---

## Inspect Volume

```bash
docker volume inspect postgres-data
```

Useful Information:

* Mountpoint
* Driver
* Creation Date

---

# What is a Docker Volume?

A Docker Volume is a persistent storage location managed by Docker.

Benefits:

* Data survives container deletion
* Easy backup and restore
* Better performance
* Recommended for databases

---

# Task 3: Bind Mounts

## Create Host Directory

```bash
mkdir website
cd website
```

---

## Create HTML File

```html
<!DOCTYPE html>
<html>
<head>
<title>Docker Volume Demo</title>
</head>
<body>
<h1>Hello from Host Machine</h1>
</body>
</html>
```

Save as:

```text
index.html
```

---

## Run Nginx With Bind Mount

```bash
docker run -d \
--name nginx-bind \
-p 8080:80 \
-v $(pwd):/usr/share/nginx/html \
nginx
```

---

## Access Browser

```text
http://localhost:8080
```

Output:

```text
Hello from Host Machine
```

---

## Modify index.html

Change:

```html
<h1>Hello from Docker Bind Mount</h1>
```

Refresh browser.

Observation:

Changes appear immediately.

No container rebuild required.

---

# Named Volume vs Bind Mount

| Named Volume               | Bind Mount              |
| -------------------------- | ----------------------- |
| Managed by Docker          | Managed by Host OS      |
| Stored in Docker directory | Stored anywhere on host |
| Better for databases       | Better for source code  |
| More portable              | Host dependent          |
| Recommended for production | Common in development   |

---

# Task 4: Docker Networking Basics

## List Networks

```bash
docker network ls
```

Example Output:

```text
bridge
host
none
```

---

# Default Bridge Network

Inspect:

```bash
docker network inspect bridge
```

Shows:

* Subnet
* Gateway
* Connected Containers

---

# Run Two Containers

```bash
docker run -dit --name container1 ubuntu
docker run -dit --name container2 ubuntu
```

---

## Find Container IP

```bash
docker inspect container1
docker inspect container2
```

Example:

```text
container1 = 172.17.0.2
container2 = 172.17.0.3
```

---

## Ping Using IP

```bash
docker exec -it container1 bash
```

```bash
ping 172.17.0.3
```

Result:

```text
Success
```

---

## Ping Using Name

```bash
ping container2
```

Result:

```text
Fails
```

### Why?

Default bridge network does not automatically provide DNS-based name resolution.

---

# Task 5: Custom Bridge Network

## Create Network

```bash
docker network create my-app-net
```

Verify:

```bash
docker network ls
```

---

## Run Containers

```bash
docker run -dit \
--network my-app-net \
--name app1 \
ubuntu
```

```bash
docker run -dit \
--network my-app-net \
--name app2 \
ubuntu
```

---

## Test Communication

Enter app1:

```bash
docker exec -it app1 bash
```

Ping app2:

```bash
ping app2
```

Result:

```text
Success
```

---

# Why Custom Networks Work

Custom bridge networks include Docker DNS.

Docker automatically resolves:

```text
app1
app2
database
backend
frontend
```

into container IP addresses.

This allows containers to communicate using names instead of IP addresses.

Benefits:

* Easier configuration
* Better scalability
* Dynamic IP management

---

# Task 6: Database + Application Together

## Create Network

```bash
docker network create app-network
```

---

## Create Volume

```bash
docker volume create mysql-data
```

---

## Run MySQL Container

```bash
docker run -d \
--name mysql-db \
--network app-network \
-v mysql-data:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD=password \
mysql
```

---

## Run Ubuntu Container

```bash
docker run -dit \
--name app-container \
--network app-network \
ubuntu
```

---

## Verify Connectivity

Enter App Container:

```bash
docker exec -it app-container bash
```

Ping Database:

```bash
ping mysql-db
```

Output:

```text
Success
```

Observation:

The application container can reach the database using the container name.

No IP address required.

---

# Real-World Example

In production:

```text
Frontend Container
        |
        |
        v
Backend Container
        |
        |
        v
MySQL/Postgres Container
```

All containers communicate using a custom Docker network.

Database data is stored in Docker Volumes.

This ensures:

* Persistent data
* Easy communication
* Better scalability

---

# Useful Commands

## List Volumes

```bash
docker volume ls
```

---

## Inspect Volume

```bash
docker volume inspect volume-name
```

---

## List Networks

```bash
docker network ls
```

---

## Inspect Network

```bash
docker network inspect network-name
```

---

## Remove Volume

```bash
docker volume rm volume-name
```

---

## Remove Network

```bash
docker network rm network-name
```

---

# Key Learnings

* Containers are ephemeral and lose data when removed.
* Docker Volumes provide persistent storage.
* Named Volumes are managed by Docker.
* Bind Mounts connect host directories to containers.
* The default bridge network allows IP-based communication.
* Custom bridge networks provide DNS-based name resolution.
* Containers on the same custom network can communicate using container names.
* Databases should store data in volumes.
* Applications and databases typically communicate through custom Docker networks.
* Volumes + Networking are essential concepts in real-world Docker deployments.

