# Docker Cheat Sheet

## Container Commands

| Command                             | Description                    |
| ----------------------------------- | ------------------------------ |
| docker run -it ubuntu bash          | Start container interactively  |
| docker run -d nginx                 | Run container in detached mode |
| docker ps                           | List running containers        |
| docker ps -a                        | List all containers            |
| docker stop <container_id>          | Stop container                 |
| docker start <container_id>         | Start container                |
| docker restart <container_id>       | Restart container              |
| docker rm <container_id>            | Remove container               |
| docker exec -it <container_id> bash | Access running container       |
| docker logs <container_id>          | View container logs            |

---

## Image Commands

| Command                               | Description    |
| ------------------------------------- | -------------- |
| docker images                         | List images    |
| docker pull nginx                     | Download image |
| docker build -t myapp:v1 .            | Build image    |
| docker tag myapp:v1 username/myapp:v1 | Tag image      |
| docker push username/myapp:v1         | Push image     |
| docker rmi <image_id>                 | Remove image   |

---

## Volume Commands

| Command                        | Description    |
| ------------------------------ | -------------- |
| docker volume create myvolume  | Create volume  |
| docker volume ls               | List volumes   |
| docker volume inspect myvolume | Inspect volume |
| docker volume rm myvolume      | Remove volume  |

---

## Network Commands

| Command                                         | Description       |
| ----------------------------------------------- | ----------------- |
| docker network create mynetwork                 | Create network    |
| docker network ls                               | List networks     |
| docker network inspect mynetwork                | Inspect network   |
| docker network connect mynetwork container_name | Connect container |

---

## Docker Compose Commands

| Command                | Description      |
| ---------------------- | ---------------- |
| docker compose up -d   | Start services   |
| docker compose down    | Stop services    |
| docker compose ps      | List services    |
| docker compose logs    | View logs        |
| docker compose build   | Build services   |
| docker compose restart | Restart services |

---

## Cleanup Commands

| Command                | Description                    |
| ---------------------- | ------------------------------ |
| docker system df       | Check Docker disk usage        |
| docker container prune | Remove stopped containers      |
| docker image prune     | Remove unused images           |
| docker volume prune    | Remove unused volumes          |
| docker network prune   | Remove unused networks         |
| docker system prune -a | Remove unused Docker resources |

---

## Dockerfile Instructions

| Instruction | Purpose                        |
| ----------- | ------------------------------ |
| FROM        | Base image                     |
| RUN         | Execute command during build   |
| COPY        | Copy files into image          |
| ADD         | Copy files and URLs            |
| WORKDIR     | Set working directory          |
| EXPOSE      | Document container port        |
| ENV         | Define environment variable    |
| CMD         | Default command                |
| ENTRYPOINT  | Fixed executable               |
| USER        | Run container as specific user |

---

## Common Port Mapping

docker run -p 8080:80 nginx

Meaning:

* Host Port = 8080
* Container Port = 80


