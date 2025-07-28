# 🐳 Docker Interview Cheat Sheet (One-Pager)

---

## ✅ Basic Concepts

| Term              | Description                                      |
|-------------------|--------------------------------------------------|
| **Docker**        | Tool to run apps in isolated containers          |
| **Image**         | Read-only template for containers                |
| **Container**     | Running instance of an image                     |
| **Dockerfile**    | Instructions to build an image                   |
| **Volume**        | Persistent storage for containers                |
| **Registry**      | Stores/publishes images (e.g., Docker Hub)       |
| **Docker Compose**| Tool to define multi-container applications      |

---

## 🧱 Dockerfile Key Instructions

| Instruction   | Purpose                          |
|---------------|----------------------------------|
| `FROM`        | Base image                       |
| `COPY`        | Copy files into image            |
| `RUN`         | Execute commands during build    |
| `CMD`         | Default command when container runs |
| `ENTRYPOINT`  | Main command, can't be overridden easily |
| `EXPOSE`      | Declares the port used           |
| `WORKDIR`     | Set working directory            |
| `ENV`         | Set environment variables        |

---

## 💻 Common Docker Commands

```bash
# List all containers
docker ps -a

# Run container in detached mode with port mapping
docker run -d -p 8080:80 nginx

# Build image from Dockerfile
docker build -t myapp .

# Stop and remove container
docker stop <id> && docker rm <id>

# Access container shell
docker exec -it <container_id> bash

# View container logs
docker logs <container_id>

# Remove all containers
docker rm $(docker ps -aq)
```

---

## 📦 Volumes & Mounts

```bash
# Create named volume
docker volume create myvol

# Use named volume
docker run -v myvol:/data alpine

# Bind mount local directory
docker run -v $(pwd)/code:/app myapp
```

---

## 🧬 Docker Compose

**docker-compose.yml**
```yaml
version: "3"
services:
  web:
    image: nginx
    ports:
      - "8080:80"
  db:
    image: postgres
    environment:
      POSTGRES_PASSWORD: secret
```

```bash
docker-compose up -d     # Start services
docker-compose down      # Stop and remove containers
```

---

## 🚀 Optimization Tips

- Use **multi-stage builds** to reduce image size
- Use **.dockerignore** to exclude unnecessary files
- Use **Alpine base images** for smaller size
- Clean up cache in RUN:
  ```Dockerfile
  RUN apt-get update && apt-get install -y tool && rm -rf /var/lib/apt/lists/*
  ```

---

## 🔐 Security Tips

- Run containers as **non-root** users
- Scan images with `docker scan` or **Trivy**
- Don’t store secrets in images; use **Docker secrets**, Vault, etc.
- Limit privileges with `--read-only`, `--cap-drop`, etc.

---

## 🧠 Advanced Concepts

| Concept         | Explanation                                        |
|------------------|----------------------------------------------------|
| **Cgroups**      | Resource limiting (CPU, memory)                    |
| **Namespaces**   | Isolation of containers (PID, net, etc.)           |
| **ENTRYPOINT vs CMD** | ENTRYPOINT = fixed command, CMD = default args |
| **Docker Swarm** | Native clustering/orchestration                    |
| **Healthcheck**  | Monitor container health status                    |

---

## 📄 Sample Dockerfile

```Dockerfile
FROM openjdk:17-alpine
COPY target/app.jar app.jar
ENTRYPOINT ["java", "-jar", "/app.jar"]
```

---