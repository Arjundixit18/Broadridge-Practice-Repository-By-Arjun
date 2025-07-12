# 🐳 Docker - DevOps Practice by Arjun Dixit

Welcome to the **Docker module** of my Broadridge Practice Repository. This folder contains everything I’ve learned and practiced on Docker – from basic to advanced – with real-world examples, use-cases, and CLI workflows.

---

## 📁 Topics Covered

| Section                        | Description                                                                 |
|-------------------------------|-----------------------------------------------------------------------------|
| 🔹 Part 1: Introduction        | What is Docker? Architecture, Installation, CLI setup                      |
| 🔹 Part 2: Container Lifecycle | Create, Start, Stop, Pause, Attach, Exec, Remove                           |
| 🔹 Part 3: Images & Filesystem | Docker images, layered filesystem, networking, `diff`, `commit`, `save`    |
| 🔹 Part 4: Dockerfile & Compose| Writing Dockerfiles, multi-stage builds, Docker Compose, multi-container   |
| 🔹 Part 5: Volumes & Best Practices | Persistent storage, backup/restore, `.dockerignore`, security         |

---

## 🚀 Commands Covered (Examples)

```bash
docker run -it ubuntu

docker ps -a
docker exec -it <container-id> /bin/bash
docker build -t myimage .
docker-compose up -d
docker volume create myvol
docker stats
docker logs <container-id>
```

---

## 🧱 Real-World Concepts Practiced
- 🧩 Multi-container apps using Docker Compose
- ⚙️ Persistent storage using named volumes
- 📦 Application packaging with Dockerfiles
- 🌐 Custom bridge networks for internal container communication
- 📥 File transfer using `docker cp`
- 📉 Monitoring container health and performance
- 🛠️ Building production-grade images with Alpine
- 🔄 Container backups with `export`, `import`, `save`, `load`

---

## 🧰 Tools Used
- Docker Engine
- Docker Compose
- BusyBox (for lightweight containers)
- Jenkins (deployed via Docker)
- Nginx, MySQL, Ubuntu, Redis (as containerized services)

---

## 📸 Sneak Peek

![Docker CLI](https://miro.medium.com/v2/resize:fit:1200/format:webp/1*QQGTfSm-xeAjVXa74Fk6mQ.png)

---

## 📚 References & Practice Links
- 🔗 [DevOpsSchool Docker Tutorials](https://www.devopsschool.com/tutorial/docker/)
- 🔗 [Docker CLI Reference](https://docs.docker.com/engine/reference/commandline/docker/)
- 🔗 [Play with Docker (Free Lab)](https://labs.play-with-docker.com/)

---

## 🧑‍💻 Maintained By
**Arjun Dixit**
> Documenting my full Docker journey for DevOps mastery 💪🐳

📧 arjundixit.dev@gmail.com  
🔗 [GitHub](https://github.com/arjundixit18) | [LinkedIn](https://www.linkedin.com/in/arjundixit18)

---

> 🔄 Updates will be continuously added as I dive deeper into Docker networking, image optimization, and orchestration tools like Kubernetes.
