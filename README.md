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
- [Dockerfile Explanation](#-dockerfile-explanation)
- [Docker Compose Overview](#-docker-compose-overview)
- [Managing Containers and Images](#-managing-containers-and-images)
- [Networking in Docker](#-networking-in-docker)
- [Data Persistence](#-data-persistence)
- [Troubleshooting](#-troubleshooting)
- [Best Practices](#-best-practices)
- [References](#-references)

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
| `docker stop <id>` | Stop a running container. | `docker stop 8f9a1c3b2d` |
| `docker start <id>` | Start a stopped container. | `docker start 8f9a1c3b2d` |
| `docker restart <id>` | Restart a running container. | `docker restart 8f9a1c3b2d` |
| `docker rm <id>` | Remove a container. | `docker rm 8f9a1c3b2d` |
| `docker exec -it <id> bash` | Access container terminal interactively. | `docker exec -it 8f9a1c3b2d bash` |
| `docker inspect <id>` | View container details (config, network, mounts, etc.). | `docker inspect 8f9a1c3b2d` |
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
| `-h` | Assign hostname to container. | `docker run -h mycontainer ubuntu` |
| `--name` | Assign a custom name to container. | `docker run --name myapp nginx` |
| `--force` | Forcefully remove running container/image. | `docker rm --force myapp` |

---

### 💡 Example: Running a Node.js Container

```bash
# Pull the official Node image
docker pull node:18

# Run Node container in detached mode with port mapping and a custom name
docker run -d -p 3000:3000 --name mynode node:18

# Access the container shell
docker exec -it mynode bash


