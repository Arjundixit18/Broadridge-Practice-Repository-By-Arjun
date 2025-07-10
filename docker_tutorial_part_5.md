# Docker Tutorial – Part 5: Volumes, Backups, and Production Practices

---

## 💾 Docker Volumes – Persistent Storage

### Why Volumes?
Containers are ephemeral—once removed, all data is lost. **Volumes** help persist data independent of container lifecycle.

### Types of Storage:
| Type         | Mounted From         | Use Case                    |
|--------------|----------------------|-----------------------------|
| Volume       | Docker-managed       | Recommended for most uses  |
| Bind Mount   | Host filesystem path | Tight host-container sync  |
| tmpfs        | RAM (Linux only)     | Non-persistent temp storage|

---

## 📦 Using Volumes

### Create and Use:
```bash
# Create volume
docker volume create myvol

# Run with volume
docker run -d --name web -v myvol:/usr/share/nginx/html nginx
```

### List and Inspect:
```bash
docker volume ls
docker volume inspect myvol
```

### Remove Volumes:
```bash
docker volume rm myvol
```

---

## 🔗 Bind Mounts Example
```bash
docker run -d -v /home/user/data:/data ubuntu
```
- Left: host path
- Right: container path

---

## 🧰 Backup & Restore Docker Volumes

### Backup Volume to Host:
```bash
docker run --rm -v myvol:/data -v $(pwd):/backup busybox tar czf /backup/backup.tar.gz /data
```

### Restore Volume from Backup:
```bash
docker run --rm -v myvol:/data -v $(pwd):/backup busybox tar xzf /backup/backup.tar.gz -C /
```

---

## 🔐 Production Practices for Docker

### 1. Use Official or Trusted Images
- From verified publishers or build your own

### 2. Minimal Base Images
- Use `alpine`, `debian:slim`, etc. to reduce attack surface

### 3. Use `.dockerignore`
```dockerignore
node_modules
.git
*.log
```

### 4. Resource Limits
```bash
# Limit memory and CPU
docker run -m 512m --cpus="1.0" myapp
```

### 5. Set Non-Root User in Dockerfile
```Dockerfile
RUN adduser -D myuser
USER myuser
```

### 6. Secrets Management (Don’t hardcode!)
Use environment variables or secret management tools (Vault, AWS Secrets Manager)

### 7. Logging & Monitoring
Use:
- `docker logs`
- `docker stats`
- Centralized log aggregation (e.g., ELK, Promtail)

### 8. Health Checks
```Dockerfile
HEALTHCHECK CMD curl --fail http://localhost:8080 || exit 1
```

---

## 📎 Clean Up Unused Resources
```bash
# Remove unused containers, networks, images, volumes
docker system prune -a
```
> Use with caution ⚠️ – this deletes stopped containers, dangling images, and volumes.

---

## 🔚 Wrapping Up

You now have a **complete end-to-end Docker workflow**:
- Build images
- Run containers
- Network them
- Persist and back up data
- Prepare for production

✅ Next step? Learn Kubernetes or Docker Swarm for orchestration!

---

> 📁 [Back to Docker Tutorial – Part 1](./docker_tutorial_part1.md)
> 
> 🚀 Thank you for following this Docker series!
