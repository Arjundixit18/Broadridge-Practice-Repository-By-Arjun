# Docker Tutorial – Part 1: Introduction, Architecture, Installation

---


## 🐳 What is Docker?
Docker is an open-source **container management platform** that simplifies the process of developing, shipping, and running applications. It packages applications into lightweight, portable containers.

- **Docker Editions**:
  - **Community Edition (CE)**: Free, open-source version.
  - **Enterprise Edition (EE)**: Paid, enterprise-grade version with additional features and support.

- **Written in**: Go Programming Language

---

## 📦 What is a Container?
Containers are lightweight environments that package software and all its dependencies so it can run reliably from one computing environment to another.

- **Key Traits**:
  - Lightweight & fast
  - Isolated in user space
  - Use namespaces (NS) from kernel:
    - MNT (Mount Namespace)
    - PMAP (Process Mapping)
    - NET (Network Namespace)

- **Powered by**: Docker Engine (which interacts with Linux kernel namespaces)

- **Other Container Runtime Tools**: 
  - [CRI-O](https://cri-o.io/)
  - [containerd](https://containerd.io/)
  - [Podman](https://podman.io/)
  - [LXC](https://linuxcontainers.org/)
  - Full list: https://www.devopsschool.com/blog/list-of-top-container-runtime-interface-projects/

---

## ⚙️ Docker Architecture

```text
You ---> Docker Client ---> Docker Daemon (REST API) ---> containerd ---> Linux Kernel (Namespaces)
```

- **Docker Client**: CLI tool (`docker`) to interact with daemon
- **Docker Daemon**: Background service that manages images, containers, networks, etc.
- **containerd**: Core container runtime
- **Namespaces**: Kernel-level isolation for each container

---

## 🧩 Components of Docker

### 1. Docker Engine
  - Core engine that powers Docker

### 2. Docker Image
  - A read-only template used to create containers
  - Includes root filesystem, app binaries, libraries, etc.
  - Used by `docker run` to spin up containers

### 3. Docker Container
  - A running instance of a Docker image

### 4. Docker Registry
  - Stores Docker images
  - Public: Docker Hub, Google Registry, AWS ECR
  - Private: JFrog Artifactory, Sonatype Nexus, self-hosted Docker registry

---

## 🛠️ How to Install Docker on RHEL/CentOS 7

1. Install dependencies:
```bash
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
```

2. Add Docker repository:
```bash
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

3. (Optional) Enable EPEL repository:
```bash
sudo yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
```

4. Enable RHEL extras:
```bash
sudo yum-config-manager --enable rhui-REGION-rhel-server-extras
```

5. Install Docker:
```bash
sudo yum install -y docker-ce
```

6. Start and enable Docker:
```bash
sudo systemctl enable docker
sudo systemctl start docker
```

7. Verify installation:
```bash
docker -v
docker info
docker version
```

---

## 👤 Docker and User Permissions
- Docker requires root by default.
- To allow a normal user to use Docker:
```bash
sudo usermod -aG docker <username>
newgrp docker
```

---

## 📋 Useful Docker Commands (System Level)

```bash
ps -eaf | grep docker     # Check if Docker is running
which docker              # Docker path
sudo systemctl status docker
sudo systemctl restart docker
```

---

> ✅ Continue to [Docker Tutorial – Part 2](./docker_tutorial_part2.md) for hands-on commands, container workflows, and lifecycle operations.
