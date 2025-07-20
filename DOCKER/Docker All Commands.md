# 🐳 Docker All Commands – Cheat Sheet by Arjun Dixit

This markdown file contains **every essential Docker command** from beginner to advanced, with **syntax, purpose, and examples**. It's your ultimate one-stop guide for all Docker CLI operations.

---

## 📦 1. Docker Installation & Setup
```bash
# Verify Docker installation
docker --version

# Start Docker daemon (Linux)
sudo systemctl start docker

# Enable Docker to start on boot
sudo systemctl enable docker
```

---

## 🚀 2. Docker Images
```bash
# List all images
docker images

# Pull an image from Docker Hub
docker pull ubuntu:latest

# Remove an image
docker rmi <image-id>

# Build image from Dockerfile
docker build -t myapp:1.0 .

# Tag an image for push
docker tag myapp:1.0 myusername/myapp:1.0

# Push image to Docker Hub
docker push myusername/myapp:1.0

# Save image as tar
docker save -o myimage.tar myapp:1.0

# Load image from tar
docker load -i myimage.tar
```

---

## 🧱 3. Docker Containers
```bash
# Run a container (interactive)
docker run -it ubuntu

# Run in detached mode
docker run -d nginx

# Name the container
docker run --name mynginx -d nginx

# Run with a port mapping
docker run -d -p 8080:80 nginx

# List running containers
docker ps

# List all containers (including stopped)
docker ps -a

# Stop, start, and restart a container
docker stop <container-id>
docker start <container-id>
docker restart <container-id>

# Remove a container
docker rm <container-id>

# Remove all containers
docker rm $(docker ps -aq)
```

---

## 🛠️ 4. Container Management
```bash
# View container logs
docker logs <container-id>

# Get detailed info about a container
docker inspect <container-id>

# Access shell inside a running container
docker exec -it <container-id> /bin/bash

# Pause and unpause a container
docker pause <container-id>
docker unpause <container-id>

# Copy files between host and container
docker cp file.txt <container-id>:/file.txt
docker cp <container-id>:/file.txt ./file.txt
```

---

## 📂 5. Volumes & Mounts
```bash
# Create a named volume
docker volume create mydata

# List volumes
docker volume ls

# Use a volume in a container
docker run -v mydata:/data ubuntu

# Inspect volume metadata
docker volume inspect mydata

# Remove a volume
docker volume rm mydata

# Mount local host directory (bind mount)
docker run -v $(pwd):/app ubuntu
```

---

## 🌐 6. Networking
```bash
# List Docker networks
docker network ls

# Create a custom bridge network
docker network create mynet

# Run container on custom network
docker run --network=mynet nginx

# Inspect a network
docker network inspect mynet

# Connect/disconnect container to/from network
docker network connect mynet <container-id>
docker network disconnect mynet <container-id>
```

---

## 🧰 7. Docker System & Cleanup
```bash
# Show system-wide info
docker info

# Show disk usage summary
docker system df

# Prune unused containers, images, and networks
docker system prune -a

# Clean volumes only
docker volume prune

# Remove all images
docker rmi $(docker images -q)
```

---

## 📄 8. Dockerfile Instructions (Bonus)
```Dockerfile
FROM ubuntu:20.04
WORKDIR /app
COPY . .
RUN apt update && apt install -y python3
CMD ["python3", "app.py"]
```

---

## ⚙️ 9. Docker Compose
```bash
# Start services from docker-compose.yml
docker-compose up -d

# Stop services
docker-compose down

# View running services
docker-compose ps

# Build services from scratch
docker-compose build
```

---

## 📦 10. Backup & Restore
```bash
# Export container state
docker export <container-id> > container_backup.tar

# Import container state
docker import container_backup.tar mycontainer
```

---

## 💡 Additional Commands (Advanced)
```bash
# Monitor container resource usage
docker stats

# Show changes in container filesystem
docker diff <container-id>

# Commit changes to a new image
docker commit <container-id> mycustomimage
```

---

## ✅ Summary Table
| Command Category    | Key Command Example                          |
|---------------------|----------------------------------------------|
| Container Lifecycle | `docker run`, `docker ps`, `docker rm`       |
| Image Handling      | `docker pull`, `docker build`, `docker push` |
| Volumes             | `docker volume create`, `docker volume ls`   |
| Networks            | `docker network create`, `docker inspect`    |
| System Maintenance  | `docker system prune`, `docker stats`        |

---

## 👨‍💻 Maintained by Arjun Dixit
> Docker mastery from scratch to production with real CLI workflows.

🔗 [GitHub](https://github.com/arjundixit18) | 📧 arjundixit.dev@gmail.com

---

> 🧠 Tip: Practice commands on [Play with Docker](https://labs.play-with-docker.com/) for a free online playground.
