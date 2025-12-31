<!-- ------------------------------------------------------------ -->
<!-- 🐳 DOCKER SERVICE DOCUMENTATION -->
<!-- ------------------------------------------------------------ -->

# 🐳 Docker Service Documentation

<p align="center">
  <img src="https://www.docker.com/wp-content/uploads/2022/03/Moby-logo.png" width="150" alt="Docker Logo" />
</p>

<p align="center">
  <b>Lightweight • Portable • Consistent • Scalable</b><br/>
  Simplify your development and deployment process with Docker — the world’s leading containerization platform.
</p>

---

## 📑 Table of Contents
- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Installation Steps](#installation-steps)
- [Docker Architecture Overview](#docker-architecture-overview)
- [Key Concepts](#-key-concepts)
- [Common Docker Commands](#common-docker-commands)
- [Dockerfile Explanation](#dockerfile-explanation)
- [Docker Network](#docker-network)
- [Docker Volume](#docker-volume)
- [Docker Compose File](#docker-compose-file)
- [Multi-Stage Dockerfile](#multi-stage-dockerfile)
- [Troubleshooting](#troubleshooting)
- [Best Practices](#best-practices)
- [References](#references)


---

## Introduction
Docker is an open-source platform that enables developers to automate the deployment of applications inside lightweight, portable containers.  
It ensures consistency across multiple environments — from development to production — by packaging code, runtime, libraries, and dependencies together.

**Key Benefits:**
- Faster application delivery  
- Consistent environment setup  
- Easy scalability and portability  

---

## Prerequisites
Before using Docker, ensure you have the following:
- **Operating System:** Windows 10/11, macOS, or any Linux distribution  
- **Memory:** Minimum 4 GB RAM  
- **Admin Rights:** To install Docker Engine  
- **Basic Knowledge:** Command-line usage  

---

## Installation Steps
- 🪟 Windows
1. Download **Docker Desktop** from [Docker Hub](https://www.docker.com/products/docker-desktop/).  
2. Run the installer and follow on-screen instructions.  
3. Verify installation:  
   ```bash
   docker --version
---

## Docker Architecture Overview

- Docker uses a client–server architecture:
- Docker Client: CLI tool that communicates with the daemon.
- Docker Daemon (dockerd): Manages images, containers, and volumes.
- Docker Images: Immutable templates used to create containers.
- Docker Containers: Running instances of images.
- Docker Registry: Stores Docker images (e.g., Docker Hub).

<p align="center"> <img src="https://techlearners.blog/wp-content/uploads/2025/06/Docker-Ecosystem.drawio.svg" width="600" radius=20 alt="Docker Architecture Diagram"/> </p>

---

## 🧱 Key Concepts

| **Concept** | **Description** |
|--------------|----------------|
| **Image** | A blueprint for creating containers. |
| **Container** | A lightweight, isolated runtime environment. |
| **Volume** | A mechanism for data persistence. |
| **Network** | Allows containers to communicate securely. |

---

## Common Docker Commands

### 🧱 Docker Image Commands

| **Command** | **Description** | **Example** |
|--------------|----------------|--------------|
| `docker pull <image>` | Download an image from Docker Hub. | `docker pull node:18` |
| `docker images` | List all downloaded images. | `docker images` |
| `docker rmi <image>` | Remove an image. | `docker rmi node:18` |
| `docker image inspect <image-id>` | Inspect detailed info about an image. | `docker image inspect node:18` |

---

### 📦 Docker Container Commands

| **Command** | **Description** | **Example** |
|--------------|----------------|--------------|
| `docker run <image>` | Create and start a new container. | `docker run node:18` |
| `docker run -idt <image>` | Run container continuously in background. | `docker run -idt node:18` |
| `docker ps` | List active containers. | `docker ps` |
| `docker ps -a` | List all containers (active + stopped). | `docker ps -a` |
| `docker rm <id>` | Remove a container. | `docker rm 8f9a1c3b2d` |
| `docker stop <id>` | Stop a running container. | `docker stop 8f9a1c3b2d` |
| `docker start <id>` | Start a stopped container. | `docker start 8f9a1c3b2d` |
| `docker restart <id>` | Restart a running container. | `docker restart 8f9a1c3b2d` |
| `docker logs <id>` | View log of container. | `docker log 8f9a1c3b2d` |
| `docker inspect <id>` | View container details (config, network, mounts, etc.). | `docker inspect 8f9a1c3b2d` |
| `docker exec -it <id> bash` | Access container terminal interactively. | `docker exec -it 8f9a1c3b2d bash` |
| `docker attach <id>` | Attach terminal to running container. | `docker attach 8f9a1c3b2d` |

---

### ⚙️ Common Docker Options (Flags)

| **Flag** | **Description** | **Example** |
|-----------|----------------|--------------|
| `-d` | Run container in detached (background) mode. | `docker run -d nginx` |
| `-p` | Map container port to host port. | `docker run -p 8080:80 nginx` |
| `-e` | Set environment variable inside container. | `docker run -e MYSQL_ROOT_PASSWORD=root mysql` |
| `-it` | Allocate a pseudo-TTY (interactive terminal). | `docker run -it ubuntu` |
| `-u` | Specify a username. | `docker exec -u root -it container bash` |
| `-p` | for password. | `docker exec -p practice c-id` |
| `-t` | to name image. | `docker build -t img_name .` |
| `-h` | Assign hostname to container. | `docker run -h mycontainer ubuntu` |
| `--name` | Assign a custom name to container. | `docker run --name myapp nginx` |
| `--force` | Forcefully remove running container/image. | `docker rm --force myapp` |
| `--driver` | Driver used when we create network want to to tell what kind of driver. | `docker network create --driver bridge network_name ` |

---

### 💡 Example: Running a Node.js Container

```bash
# Pull the official Node image
docker pull node:18

# Run Node container in detached mode with port mapping and a custom name
docker run -d -p 3000:3000 --name mynode node:18

# Access the container shell
docker exec -it mynode bash

```
---

## Dockerfile Explanation

### 🧩 1.  Definition
A **Dockerfile** is a text file that contains a set of instructions to build a Docker image automatically.  
It defines what goes inside the image — such as base OS, dependencies, application files, and startup commands.

---

### ⚙️ 2. Common Dockerfile Commands

| **Instruction** | **Description** | **Example** |
|------------------|-----------------|--------------|
| `FROM` | Specifies the base image to use. | `FROM node:18` |
| `WORKDIR` | Sets the working directory inside the container. | `WORKDIR /app` |
| `COPY` | Copies files/folders from host to container. | `COPY . .` |
| `RUN` | Executes commands during image build (e.g., install dependencies). | `RUN npm install` |
| `CMD` | Specifies default command to run when container starts . | `CMD ["node", "server.js"]` |
| `EXPOSE` | Informs Docker which port the container listens on. | `EXPOSE 3000` |
| `ENTRYPOINT` | Configures a container that will run as an executable. | `ENTRYPOINT ["npm", "start"]` |
| `ENV` | Sets environment variables inside the image. | `ENV NODE_ENV=production` |
| `LABEL` | Adds metadata to the image. | `LABEL version="1.0"` |
| `ADD` | Similar to COPY but can also extract `.tar` files or fetch URLs. | `ADD app.tar.gz /app` |
| `USER` | Sets the username or UID to use when running the image. | `USER node` |

NOTE: `CMD` can be overwrite during container running ||
      `ENTRYPOINT` cannot be overwrite

---

### 🧱 3. Example Dockerfile

```dockerfile
# Use an official Node.js image as the base
FROM node:18

# Set working directory
WORKDIR /app

# Copy package files and install dependencies
COPY package*.json ./
RUN npm install

# Copy project files into container
COPY . .

# Expose application port
EXPOSE 3000

# Command to run the application
CMD ["npm", "start"]
```

### 🧱 4. Build image

```bash
# Build Docker image ('.' means current directory)
docker build -t mynodeapp .

# Verify the image
docker images

# Run container from image
docker run -d -p 3000:3000 --name mynode mynodeapp

```
---

## Docker Network

### 🧩 1. Definition
A **Docker Network** allows containers to communicate with each other and with the host system securely.  
It provides isolated environments for containers, ensuring controlled communication and easy service discovery.  
Docker automatically manages networking so containers can interact using container names instead of IPs.

---

### ⚙️ 2. Common Docker Network Commands

| **Command** | **Description** | **Example** |
|--------------|----------------|--------------|
| `docker network ls` | List all existing Docker networks. | `docker network ls` |
| `docker network inspect <network>` | Show detailed info about a network. | `docker network inspect bridge` |
| `docker network create <network>` | Create a new custom network. | `docker network create mynetwork` |
| `docker network rm <network>` | Remove a specific network. | `docker network rm mynetwork` |
| `docker network connect <network> <container>` | Connect a container to a network. | `docker network connect mynetwork mycontainer` |
| `docker network disconnect <network> <container>` | Disconnect a container from a network. | `docker network disconnect mynetwork mycontainer` |

---

### 🧱 3. Example in Bash

```bash
# Step 1: Create a custom Docker network
docker network create mynetwork

# Step 2: Run a MySQL container on that network
docker run -d --name mysql-db --network mynetwork -e MYSQL_ROOT_PASSWORD=root mysql:latest

# Step 3: Run a Node.js app container on the same network
docker run -d --name node-app --network mynetwork -p 3000:3000 mynodeapp

# Step 4: Verify both containers are connected to the same network
docker network inspect mynetwork

```
---

## Docker Volume

### 🧩 1. Definition
A **Docker Volume** is a mechanism for **persisting data** generated by and used in Docker containers.  
When a container stops or is removed, its data inside the container is lost — but with **volumes**, data remains safe and reusable.  
Volumes are managed by Docker and can be easily shared between multiple containers.

---

### ⚙️ 2. Common Docker Volume Commands

| **Command** | **Description** | **Example** |
|--------------|----------------|--------------|
| `docker volume ls` | List all Docker volumes. | `docker volume ls` |
| `docker volume rm <volume>` | Remove a specific volume. | `docker volume rm myvolume` |
| `docker volume create <volume>` | Create a new volume. | `docker volume create myvolume` |
| `docker volume inspect <volume>` | View detailed information about a volume. | `docker volume inspect myvolume` |
| `docker volume prune` | Remove all unused volumes. | `docker volume prune` |

---

### 🧱 3. Example in Bash

```bash
# Step 1: Create a volume
docker volume create myvolume

# Step 2: Run a MySQL container using the created volume
docker run -d \
  --name mysql-db \
  -e MYSQL_ROOT_PASSWORD=root \
  -v myvolume:/var/lib/mysql \
  mysql:latest

# Step 3: Check the volume list
docker volume ls

# Step 4: Inspect volume details
docker volume inspect myvolume

# Step 5: Remove volume (only if not in use)
docker volume rm myvolume

```
---

## Docker Compose File

### 🧱 1. Definition
A **Docker Compose file** (`docker-compose.yml`) is a YAML configuration file that defines how multiple Docker containers work together in a single application.  
It allows you to define **services**, **networks**, and **volumes** in one place — making it easy to start, stop, and manage multi-container applications with a single command.

---

### ⚙️ 2. Common Docker Compose Commands

| **Command** | **Description** | **Example** |
|--------------|----------------|--------------|
| `docker compose up` | Build and start all services. | `docker compose up` |
| `docker compose up -d` | Run services in detached (background) mode. | `docker compose up -d` |
| `docker compose down` | Stop and remove all containers, networks, and volumes. | `docker compose down` |
| `docker compose ps` | List all running services. | `docker compose ps` |
| `docker compose build` | Build or rebuild services. | `docker compose build` |
| `docker compose logs` | View logs of all running services. | `docker compose logs` |
| `docker compose exec <service> <command>` | Execute a command in a running service container. | `docker compose exec app bash` |
| `docker compose stop` | Stop running containers without removing them. | `docker compose stop` |
| `docker compose restart` | Restart all services. | `docker compose restart` |

---

### 📜 3. Example `docker-compose.yml` File

```yaml
version: '3.8'

services:
  app:
    build: .
    container_name: mynodeapp
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
    depends_on:
      - db
    networks:
      - mynetwork

  db:
    image: mysql:latest
    container_name: mysql-db
    environment:
      - MYSQL_ROOT_PASSWORD=root
      - MYSQL_DATABASE=mydb
    volumes:
      - db_data:/var/lib/mysql
    networks:
      - mynetwork

volumes:
  db_data:

networks:
  mynetwork:
    driver: bridge

```

```bash
# Step 1: Start all containers (build if needed)
docker compose up -d

# Step 2: View running services
docker compose ps

# Step 3: Access container terminal
docker compose exec app bash

# Step 4: Stop and remove all containers, networks, and volumes
docker compose down

```

---
## Multi-Stage Dockerfile

### 🧩 1. Definition
A **Multi-Stage Dockerfile** is a powerful feature that allows you to use **multiple `FROM` instructions** in one Dockerfile.  
Each `FROM` starts a new build stage, letting you separate **build dependencies** from **runtime environment**.  
This reduces final image size and improves security by keeping only what’s needed to run your application.

---

### ⚙️ 2. Common Commands & Concepts

| **Command / Concept** | **Description** | **Example** |
|------------------------|----------------|--------------|
| `FROM` | Starts a new build stage. | `FROM node:18 AS builder` |
| `AS <name>` | Names a build stage for reference. | `FROM node:18 AS build` |
| `COPY --from=<name>` | Copies files from a previous stage. | `COPY --from=build /app/dist /app/dist` |
| `RUN` | Executes commands in the current stage. | `RUN npm install && npm run build` |
| `WORKDIR` | Sets working directory inside container. | `WORKDIR /app` |
| `CMD` | Defines the command to run at container start. | `CMD ["npm", "start"]` |

---

### 🧱 3. Example: Multi-Stage Dockerfile for Node.js App

```dockerfile
# ---------- Stage 1: Build ----------
FROM node:18 AS build

# Set working directory
WORKDIR /app

# Copy package files and install dependencies
COPY package*.json ./
RUN npm install

# Copy all source code and build the app
COPY . .
RUN npm run build

# ---------- Stage 2: Run ----------
FROM node:18-alpine

# Set working directory
WORKDIR /app

# Copy only build output and dependencies from build stage
COPY --from=build /app/dist ./dist
COPY --from=build /app/package*.json ./

# Install only production dependencies
RUN npm install --only=production

# Expose application port
EXPOSE 3000

# Run the application
CMD ["node", "dist/server.js"]

```
```bash
# Step 1: Build the image
docker build -t mynode-multistage .

# Step 2: Run the container
docker run -d -p 3000:3000 --name mynodeapp mynode-multistage

```

## Troubleshooting

| **Issue** | **Possible Fix** |
|------------|------------------|
| **Port already in use** | Stop conflicting process or change port mapping. |
| **Permission denied** | Run with `sudo` or add user to the `docker` group. |
| **Container won’t start** | Check logs using `docker logs <container_id>`. |

---

## Best Practices

- Use `.dockerignore` to reduce image size.  
- Use **multi-stage builds** for optimization.  
- Keep containers **stateless**.  
- Tag images with proper **version numbers**.  
- Regularly clean up unused images and containers.  

---

## References

- [📘 Official Docker Documentation](https://docs.docker.com/)  
- [🐳 Docker Hub](https://hub.docker.com/)  
- [📄 Dockerfile Best Practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)  
- [⚙️ Compose File Reference](https://docs.docker.com/compose/compose-file/)  

---

<p align="center">
  <b>💙 Built with Docker — Simplify. Ship. Run. 💙</b>
</p>



