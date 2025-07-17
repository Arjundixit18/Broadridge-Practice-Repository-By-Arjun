# Docker Tutorial – Part 3: Images, File System, Networking, and Advanced Commands

---


## 📦 Docker Images – Behind the Scenes

### What is an Image?
- A **Docker image** is a layered, read-only template used to create containers.
- Contains:
  - Application code
  - Dependencies
  - OS files (rootfs)

### Command:
```bash
docker images           # List available images
docker pull nginx       # Download image from registry
docker rmi nginx        # Remove image
```

### Image Lifecycle:
```text
Dockerfile → docker build → Docker image → docker run → Container
```

---

## 🧱 Docker File System (UnionFS)

### Layered Architecture:
Docker images use **Union File System** (UnionFS):
- Each image consists of **multiple layers**.
- Layers are immutable (read-only).
- A container adds a **read-write layer** on top.

### View Differences:
```bash
docker diff <container-id>     # Shows file changes in container vs original image
```

### Save and Load:
```bash
docker save -o nginx.tar nginx       # Save image to file
docker load -i nginx.tar             # Load image from file
```

### Export and Import:
```bash
docker export <container-id> > ubuntu.tar
cat ubuntu.tar | docker import - ubuntu:restored
```

---

## 🔄 Image & Container Utilities

### Rename:
```bash
docker rename <container-id> new_name
```

### Commit Container to Image:
```bash
docker commit <container-id> mynewimage:v1
```

### View History:
```bash
docker history <image-name>
```

---

## 🌐 Docker Networking Basics

### Default Networks:
```bash
docker network ls
```
- **bridge** – Default for containers on same host
- **host** – Uses host's network stack
- **none** – No networking

### Inspect Network:
```bash
docker network inspect bridge
```

### Run with Custom Port:
```bash
docker run -d -p 5000:80 nginx
```

### Communication Between Containers:
1. Create user-defined bridge:
```bash
docker network create mynet
```
2. Run containers in same network:
```bash
docker run -d --network=mynet --name app1 nginx
```
3. Then access `app1` from any container on `mynet` by its name.

---

## 🔍 Monitoring, Debugging & Logs

### Logs:
```bash
docker logs <container-id>
watch docker logs <container-id>
```

### Real-Time Stats:
```bash
docker stats
```

### Container Top (Processes):
```bash
docker top <container-id>
```

### Real-Time Docker Events:
```bash
docker events
```

---

## 📥 File Copy Between Host and Container

```bash
# Copy file from container to host
docker cp <container-id>:/opt/devops.txt .

# Copy file from host to container
docker cp devops.txt <container-id>:/opt/
```

---

> ✅ Continue to [Docker Tutorial – Part 4](./docker_tutorial_part4.md) for Dockerfiles, Docker Compose, and real-world application deployments.
