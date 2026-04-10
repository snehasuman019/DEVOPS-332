# 📅 Day 07 (17-03-2026) — Introduction to Docker, Architecture, Daemon & CLI

---

## 🌟 Introduction to Docker

Docker is an **open-source containerization platform** used to build, package, ship, and run applications inside containers.

It helps developers and DevOps engineers ensure that applications run **consistently across different environments** such as development, testing, staging, and production.

Docker simplifies:

- Application deployment  
- Environment setup  
- Dependency management  
- Infrastructure automation  

---

## 🗂 Docker Hub — Centralized Repository for Docker Images

Docker Hub is a **centralized image registry** where container images are stored, shared, and distributed.

It plays a very important role in DevOps pipelines.

### ⭐ Features

- Supports **public and private repositories**  
- Provides **official images** (Ubuntu, Nginx, Node, MySQL etc.)  
- Supports **automated builds from GitHub / Git repos**  
- Enables **image versioning and tagging**  
- Allows teams to **share images globally**  

### 🎯 Importance in DevOps

- Enables **Build Once → Deploy Anywhere**  
- Supports CI/CD automation  
- Ensures consistent environments  
- Reduces manual configuration  
- Improves deployment speed  

---

## 🧩 Key Components of Docker

---

### 🔹 Docker Client (Docker CLI)

Docker Client is the command-line interface used by users to interact with Docker.

Users execute Docker commands through CLI which are sent to Docker Daemon.

#### ✅ Examples


docker pull nginx
docker run ubuntu
docker ps
docker stop <container-id>

### 🔹 Docker Daemon (dockerd)

Docker Daemon is a **background service** that manages all Docker objects such as:

- Docker Images  
- Containers  
- Networks  
- Volumes  

It listens for Docker API requests from the Docker Client and performs operations like building images, running containers, and managing resources.

#### ⭐ Responsibilities of Docker Daemon

- Pulling and pushing images  
- Creating and managing containers  
- Handling container networking  
- Managing storage volumes  
- Monitoring container execution  
- Enforcing security and resource limits  

---

### 🔹 Docker Images

Docker Images are **read-only templates** used to create containers.

They contain everything needed to run an application:

- Base Operating System  
- Application Code  
- Dependencies and Libraries  
- Runtime Environment  
- Configuration Files  

Images are built in **layers**, which helps in faster builds and efficient storage.

---

### 🔹 Containers

Containers are **running instances of Docker images** where applications are actually executed.

#### ⭐ Characteristics of Containers

- Lightweight  
- Fast startup time  
- Portable across environments  
- Isolated execution environment  
- Efficient resource usage  

---

### 🔹 Docker Registry (Docker Hub)

Docker Registry is a centralized storage system used to:

- Store Docker images  
- Manage image versions  
- Distribute images across environments  

Example Registries:

- Docker Hub  
- AWS Elastic Container Registry (ECR)  
- Azure Container Registry (ACR)  
- GitHub Container Registry (GHCR)  

---

## 🏗 Docker Architecture

Docker follows a **Client–Server Architecture**.

- User interacts with Docker Client  
- Docker Client sends commands to Docker Daemon  
- Docker Daemon manages images and containers  
- Images are stored and retrieved from Docker Registry  

---

### 🔄 Docker Architecture Flowchart

graph LR
User --> DockerCLI
DockerCLI --> DockerDaemon
DockerDaemon --> DockerImages
DockerDaemon --> Containers
DockerDaemon --> DockerRegistry

## 🔁 Docker Lifecycle

Docker workflow consists of three major stages:

### 🧱 Build

- Dockerfile is used to create a Docker image  
- Application code, dependencies, and runtime are packaged  
- Image layers are created step-by-step  
- Image becomes ready for distribution  

---

### 🚚 Ship

- Docker image is pushed to Docker Hub or a private registry  
- Image can be shared across teams and environments  
- Enables **Build Once → Deploy Anywhere** strategy  

---

### ▶️ Run

- Container is created from Docker image  
- Application starts executing inside isolated environment  
- Resources such as CPU, memory, and network are allocated  

---

## 📊 Container States

Containers move through different states during their lifecycle.

| State   | Meaning |
|--------|---------|
| Created | Container is initialized but not started |
| Running | Container is actively executing |
| Paused  | Container execution is temporarily suspended |
| Stopped | Container execution is terminated |

---

## ⚡ Why Docker is Faster than Virtual Machines

- Containers **share the host OS kernel**  
- No need to boot a separate **guest operating system**  
- Requires **less CPU and memory resources**  
- Faster startup time (seconds compared to minutes in VMs)  
- Lightweight virtualization improves performance  

---

## 💻 Basic Docker Commands


docker pull ubuntu          # Download ubuntu image from Docker Hub
docker images               # List all downloaded images
docker run ubuntu           # Run container from ubuntu image
docker ps                   # Show running containers
docker ps -a                # Show all containers
docker stop <container-id>  # Stop running container
docker rm <container-id>    # Remove container
docker rmi ubuntu           # Remove image

## 🎯 Benefits of Docker in DevOps

- Provides **consistent environments** across development, testing, staging, and production  
- Enables **Build Once → Deploy Anywhere** strategy  
- Supports **faster and automated deployments**  
- Improves **resource utilization** due to lightweight containers  
- Reduces **infrastructure setup time**  
- Eliminates “**works on my machine**” issues  
- Supports **microservices architecture** for scalable applications  
- Simplifies **Continuous Integration and Continuous Deployment (CI/CD)** pipelines  
- Enables **easy rollback and version control** of application environments  
- Improves **system scalability and high availability**  
- Enhances **developer productivity and team collaboration**  
- Reduces **operational and maintenance costs**  