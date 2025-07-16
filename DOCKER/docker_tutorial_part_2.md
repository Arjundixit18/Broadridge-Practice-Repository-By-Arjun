# Docker Tutorial – Part 2: Container Lifecycle, Commands, and Access

---

## 🚀 Docker Workflow

### General Flow:
```text
Human → Docker Client → Docker Daemon
            ↓
    Checks for Image in Local Repository
        ↓     ↘
      Yes     No → Pull from Docker Registry
        ↓
    Create & Start Container
```

---

## 🔁 Container Lifecycle

### Stages:
```text
create → start → stop → restart → pause → unpause → kill → remove
```

### Commands:
```bash
docker create jenkins              # Create a container from image

# Start/Stop/Restart
docker start <container-id>
docker stop <container-id>
docker restart <container-id>

docker pause <container-id>       # Pause container
docker unpause <container-id>     # Resume it

docker kill <container-id>        # Force-stop the container

docker rm <container-id>          # Remove a stopped container
```

---

## 🧠 `docker run` Explained

### Default Run:
```bash
docker run ubuntu
```
#### Internally Does:
```text
pull → create → start → becomes container (PID 1 active)
```

### Detached Mode:
```bash
docker run -d jenkins
```
> Runs in background (detached), returns container ID.

---

## 📂 Container Access and Networking

### View Running Containers:
```bash
docker ps
```

### Access a Container:
#### 1. Exec Way (Preferred):
```bash
docker exec -it <container-id> /bin/bash
```
- `-it`: interactive terminal

#### 2. Attach Way:
```bash
docker attach <container-id>
```
> This attaches to the main process (PID 1).

---

## 🌐 Expose Container via Web (HTTP Access)

### Expose Jenkins on port 8080:
```bash
docker run -d -p 8080:8080 jenkins
```

### Find Container IP:
```bash
docker inspect <container-id> | grep -i ip
```

### Test Access:
```bash
curl http://<container-ip>:8080
```

---

## 📋 Examples with Commands

```bash
# Pull image
$ docker pull jenkins

# Create and Start
$ docker create jenkins
$ docker start <container-id>

# Inspect container
$ docker inspect <container-id> | grep -i ip

# Execute commands inside
$ docker exec <container-id> ls /
$ docker exec <container-id> df -kh
$ docker exec <container-id> ps -eaf

# File interaction
$ docker exec <container-id> touch /opt/devops.txt
$ docker cp <container-id>:/opt/devops.txt .  # Copy from container
$ docker cp devops.txt <container-id>:/opt/   # Copy to container

# Logs
$ docker logs <container-id>
$ docker stats
$ docker events
```

---

## 🔎 Docker Container Rules

- A container is considered **running** as long as its **PID 1** is active.
- Unlike VMs where PID 1 is usually `systemd`, containers can run any binary (e.g., bash, java) as PID 1.

---

> ✅ Continue to [Docker Tutorial – Part 3](./docker_tutorial_part3.md) for image management, file system differences, and Docker networking.
