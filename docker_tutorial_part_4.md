# Docker Tutorial – Part 4: Dockerfile, Docker Compose & Multi-Container Applications

---

## 📝 Dockerfile – Build Custom Images

### What is a Dockerfile?
A Dockerfile is a script containing instructions to build a Docker image layer-by-layer.

### Basic Dockerfile Example:
```Dockerfile
# Use a base image
FROM ubuntu:20.04

# Add metadata
LABEL maintainer="you@example.com"

# Update and install packages
RUN apt-get update && apt-get install -y nginx

# Copy files
COPY index.html /var/www/html/

# Set working directory
WORKDIR /var/www/html

# Expose port
EXPOSE 80

# Default command
CMD ["nginx", "-g", "daemon off;"]
```

### Build and Run:
```bash
docker build -t custom-nginx .
docker run -d -p 8080:80 custom-nginx
```

---

## 🔁 Multi-Stage Builds (Advanced Dockerfile)
Reduce image size by separating build and runtime stages.

```Dockerfile
# Build stage
FROM golang:1.20 as builder
WORKDIR /app
COPY . .
RUN go build -o myapp

# Runtime stage
FROM alpine:latest
COPY --from=builder /app/myapp /usr/local/bin/myapp
ENTRYPOINT ["myapp"]
```

---

## 🧩 Docker Compose – Multi-Container Apps

### What is Docker Compose?
Tool to define and run multi-container applications using a YAML file (`docker-compose.yml`).

### Example:
```yaml
version: '3.8'
services:
  web:
    image: nginx
    ports:
      - "8080:80"
  app:
    build: ./app
    volumes:
      - .:/app
    depends_on:
      - db
  db:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: rootpass
      MYSQL_DATABASE: mydb
```

### Usage:
```bash
docker-compose up -d            # Start all services
docker-compose down             # Stop and remove containers, networks
```

### Compose File Features:
- `depends_on`: Set container startup order
- `volumes`: Map local dirs into containers
- `ports`: Expose container ports
- `build`: Build from local Dockerfile

---

## 📦 Compose Commands
```bash
docker-compose build            # Build services

# Run service command
docker-compose run web bash

# View logs
docker-compose logs

# Restart
docker-compose restart
```

---

## 🔥 Real-world Example – Flask + Redis

**docker-compose.yml**
```yaml
version: '3'
services:
  web:
    build: .
    ports:
      - "5000:5000"
  redis:
    image: redis
```

**Dockerfile**
```Dockerfile
FROM python:3.8-slim
WORKDIR /app
COPY . .
RUN pip install flask redis
CMD ["python", "app.py"]
```

**app.py**
```python
from flask import Flask
from redis import Redis
app = Flask(__name__)
redis = Redis(host='redis', port=6379)

@app.route('/')
def hello():
    count = redis.incr('hits')
    return f'Hello! This page has been visited {count} times.'

if __name__ == '__main__':
    app.run(host='0.0.0.0')
```

### Run It:
```bash
docker-compose up --build
```
Visit: [http://localhost:5000](http://localhost:5000)

---

> ✅ In [Docker Tutorial – Part 5](./docker_tutorial_part5.md), we'll cover Docker volumes, backup & restore, and production best practices.
