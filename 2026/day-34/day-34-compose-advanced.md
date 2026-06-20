# Day 34 - Docker Compose: Real-World Multi-Container Apps

## Objective

Today's goal was to build a production-like multi-container application using Docker Compose.

The stack consists of:

* Web Application (Python Flask)
* PostgreSQL Database
* Redis Cache

By the end of this task, I learned:

* Multi-service Compose architecture
* Healthchecks
* Service dependencies
* Restart policies
* Custom Dockerfiles
* Named networks and volumes
* Scaling limitations

---

# Application Architecture

```text
                +----------------+
                | Flask Web App  |
                +-------+--------+
                        |
         +--------------+--------------+
         |                             |
         v                             v
+----------------+         +----------------+
| PostgreSQL DB  |         | Redis Cache    |
+----------------+         +----------------+
         |
         v
+----------------+
| Docker Volume  |
+----------------+
```

---

# Project Structure

```text
app-stack/

├── app.py
├── requirements.txt
├── Dockerfile
└── docker-compose.yml
```

---

# Task 1: Build Your Own App Stack

## Flask Application

### app.py

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return "Hello from Flask App running in Docker Compose!"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

---

## requirements.txt

```text
flask
psycopg2-binary
redis
```

---

## Dockerfile

```dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 5000

CMD ["python", "app.py"]
```

---

# Docker Compose File

## docker-compose.yml

```yaml
services:

  app:
    build: .
    container_name: flask-app

    ports:
      - "5000:5000"

    depends_on:
      postgres:
        condition: service_healthy

    networks:
      - app-network

  postgres:
    image: postgres

    container_name: postgres-db

    environment:
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: password
      POSTGRES_DB: mydb

    restart: always

    volumes:
      - postgres-data:/var/lib/postgresql/data

    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U admin"]
      interval: 10s
      timeout: 5s
      retries: 5

    networks:
      - app-network

  redis:
    image: redis

    container_name: redis-cache

    networks:
      - app-network

volumes:
  postgres-data:

networks:
  app-network:
```

---

# Start Application

```bash
docker compose up -d
```

Verify:

```bash
docker compose ps
```

Expected:

```text
flask-app
postgres-db
redis-cache
```

---

# Access Application

Open browser:

```text
http://localhost:5000
```

Output:

```text
Hello from Flask App running in Docker Compose!
```

---

# Task 2: depends_on & Healthchecks

## Why depends_on?

Without depends_on:

```text
App starts immediately
Database still starting
Connection fails
```

---

## depends_on Example

```yaml
depends_on:
  postgres:
    condition: service_healthy
```

This ensures:

```text
Database Healthy
        ↓
Application Starts
```

---

# Database Healthcheck

```yaml
healthcheck:
  test: ["CMD-SHELL", "pg_isready -U admin"]
  interval: 10s
  timeout: 5s
  retries: 5
```

---

## Verification

Stop everything:

```bash
docker compose down
```

Start again:

```bash
docker compose up -d
```

Observation:

* Database starts first
* Healthcheck passes
* App starts afterward

---

# Task 3: Restart Policies

Restart policies automatically recover containers.

---

## restart: always

```yaml
restart: always
```

Behavior:

* Restarts if container crashes
* Restarts after Docker daemon restart
* Restarts after server reboot

Example:

```bash
docker kill postgres-db
```

Result:

```text
Docker automatically recreates it
```

---

## restart: on-failure

```yaml
restart: on-failure
```

Behavior:

* Restarts only when container exits with error
* Does not restart after manual stop

---

# Restart Policy Comparison

| Policy         | Behavior                        |
| -------------- | ------------------------------- |
| no             | Never restart                   |
| always         | Always restart                  |
| unless-stopped | Restart unless manually stopped |
| on-failure     | Restart only after failure      |

---

# When to Use Each

### always

Best for:

* Databases
* Production applications

---

### on-failure

Best for:

* Batch jobs
* Scheduled tasks

---

### unless-stopped

Best for:

* Long-running services

---

# Task 4: Custom Dockerfiles in Compose

Instead of:

```yaml
image: my-app
```

Use:

```yaml
build: .
```

Compose automatically builds the image.

---

# Rebuild After Code Change

Modify:

```python
return "Docker Compose Rebuild Test"
```

Rebuild:

```bash
docker compose up --build -d
```

This command:

```text
Build Image
      ↓
Replace Container
      ↓
Start Updated App
```

---

# Task 5: Named Networks & Volumes

---

# Named Volume

```yaml
volumes:
  postgres-data:
```

Benefits:

* Persistent database storage
* Survives container deletion

---

# Named Network

```yaml
networks:
  app-network:
```

Benefits:

* Better isolation
* Easier troubleshooting
* Clear architecture

---

# Labels

Labels provide metadata.

```yaml
labels:
  project: docker-compose-demo
  environment: dev
```

Useful for:

* Monitoring
* Logging
* Container management

---

# Inspect Labels

```bash
docker inspect flask-app
```

---

# Task 6: Scaling

Scale application:

```bash
docker compose up -d --scale app=3
```

Verify:

```bash
docker ps
```

Expected:

```text
app-1
app-2
app-3
```

---

# What Breaks?

Problem:

```yaml
ports:
  - "5000:5000"
```

All three containers want:

```text
Host Port 5000
```

Only one container can bind to a host port.

Result:

```text
Port conflict
```

---

# Why Scaling Doesn't Work Well With Port Mapping

Each replica needs:

```text
Container Port 5000
```

But the host only has:

```text
One Port 5000
```

Available.

---

# Real Production Solution

Instead of exposing every app:

```text
User
  |
  v
Load Balancer
(Nginx / HAProxy)
  |
  +---- App 1
  |
  +---- App 2
  |
  +---- App 3
```

The load balancer distributes traffic.

This is how scaling works in Kubernetes and production systems.

---

# Useful Commands

## Start Services

```bash
docker compose up -d
```

---

## Stop Services

```bash
docker compose stop
```

---

## Remove Everything

```bash
docker compose down
```

---

## Rebuild Images

```bash
docker compose up --build -d
```

---

## View Logs

```bash
docker compose logs
```

---

## Follow Logs

```bash
docker compose logs -f
```

---

## View Running Containers

```bash
docker compose ps
```

---

# Key Learnings

* Docker Compose can manage complete application stacks.
* depends_on controls startup order.
* Healthchecks ensure services are truly ready.
* Restart policies improve reliability.
* build: allows Compose to build custom Dockerfiles.
* Named volumes provide persistence.
* Named networks improve communication and organization.
* Labels help manage containers.
* Scaling multiple replicas introduces port conflicts.
* Production environments use load balancers instead of direct port mappings.
* This architecture closely resembles real-world DevOps deployments.

