# Microservices with Docker Compose

---

# 1. Microservices Architecture

## What is Microservices Architecture?

Microservices Architecture is a software development approach where an application is divided into multiple small, independent services.

Each service:

- Performs a specific business function.
- Runs independently.
- Communicates through APIs.
- Can be developed, deployed, and scaled separately.

### Example

Food Delivery Application:

- User Service
- Restaurant Service
- Order Service
- Payment Service
- Notification Service

Each service runs independently and communicates via REST APIs.

---

# Need for Microservices

Traditional applications become difficult to manage as they grow.

Problems:

- Large codebase
- Slow deployment
- Difficult maintenance
- Entire application affected by a single failure
- Hard to scale individual components

Microservices solve these issues by splitting the application into smaller services.

---

# Monolithic vs Microservices

## Monolithic Architecture

A monolithic application is built as a single unit.

### Structure

```
Application
├── User Module
├── Product Module
├── Order Module
├── Payment Module
└── Database
```

### Advantages

- Easy to develop initially
- Simple deployment
- Easier debugging for small applications

### Disadvantages

- Difficult to scale
- Large codebase
- Slow deployment
- Entire application failure possible

---

## Microservices Architecture

### Structure

```
User Service
Order Service
Payment Service
Notification Service

Each service has:
- Own codebase
- Own deployment
- Own database (optional)
```

### Advantages

- Independent deployment
- Better scalability
- Faster development
- Fault isolation
- Technology flexibility

### Disadvantages

- Complex communication
- More infrastructure management
- Monitoring becomes difficult

---

# Advantages of Microservices

---

## 1. Scalability

Only the required service can be scaled.

### Example

Food Delivery App:

During lunch time:

- Order Service → High traffic
- Payment Service → Normal traffic

Scale only Order Service.

```
Order Service: 5 Containers
Payment Service: 1 Container
```

Benefits:

- Reduced cost
- Better resource utilization

---

## 2. Isolation

Failure of one service does not affect others.

### Example

Payment Service crashes

Still working:

- User Service
- Restaurant Service
- Order Service

System remains partially operational.

---

## 3. Agility

Teams can work independently.

### Example

Team A → User Service

Team B → Payment Service

Team C → Order Service

Benefits:

- Faster development
- Faster deployment
- Independent updates

---

## 4. API Gateway

API Gateway acts as a single entry point for clients.

### Without API Gateway

```
Client
 ├── User Service
 ├── Order Service
 ├── Payment Service
 └── Notification Service
```

### With API Gateway

```
Client
   |
API Gateway
   |
---------------------------------
|       |       |       |
User   Order  Payment Notify
```

Benefits:

- Centralized routing
- Authentication
- Rate limiting
- Load balancing

Popular API Gateways:

- Nginx
- Kong
- Traefik
- Spring Cloud Gateway

---

# Docker Compose

---

## What is Docker Compose?

Docker Compose is a tool used to define and run multi-container Docker applications.

Instead of running multiple docker commands manually, all configurations are written in a YAML file.

File Name:

```bash
docker-compose.yml
```

---

# YAML Structure

Basic Structure:

```yaml
version: '3'

services:
  service1:
    image: nginx

  service2:
    image: mysql
```

Main Components:

- version
- services
- volumes
- networks

---

# Writing docker-compose.yml

Example:

```yaml
version: '3.8'

services:
  web:
    image: nginx

  db:
    image: mysql
```

Run:

```bash
docker compose up
```

Stop:

```bash
docker compose down
```

---

# Version

Defines Docker Compose specification version.

Example:

```yaml
version: '3.8'
```

Common Versions:

- 3
- 3.7
- 3.8
- Latest Compose specification

---

# Services

Services define containers.

Example:

```yaml
services:

  frontend:
    image: nginx

  backend:
    image: node

  database:
    image: mysql
```

Each service creates a separate container.

---

# Volumes

Volumes provide persistent storage.

Without volume:

Container deleted → Data lost

With volume:

Container deleted → Data remains

Example:

```yaml
services:
  mysql:
    image: mysql

    volumes:
      - mysql-data:/var/lib/mysql

volumes:
  mysql-data:
```

---

# Networks

Networks enable communication between containers.

Example:

```yaml
services:

  frontend:
    networks:
      - appnet

  backend:
    networks:
      - appnet

networks:
  appnet:
```

Containers can communicate using service names.

Example:

```bash
http://backend:5000
```

---

# Environment Variables

Used to store configuration values.

Example:

```yaml
services:

  mysql:
    image: mysql

    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: mydb
```

Equivalent Docker Command:

```bash
docker run -e MYSQL_ROOT_PASSWORD=root mysql
```

---

# Secrets and Configs

---

## Secrets

Used to store sensitive information.

Examples:

- Passwords
- API Keys
- Tokens

Example:

```yaml
secrets:
  db_password:
    file: ./password.txt
```

Use inside service:

```yaml
services:
  mysql:
    secrets:
      - db_password
```

---

## Configs

Used for non-sensitive configuration files.

Examples:

- Nginx Config
- Application Config

```yaml
configs:
  app_config:
    file: ./config.yml
```

---

# Build vs Image Fields

---

## Image

Uses an already built image.

```yaml
services:
  web:
    image: nginx
```

Docker pulls image from Docker Hub.

---

## Build

Builds image from Dockerfile.

```yaml
services:
  backend:
    build: .
```

Docker Compose executes:

```bash
docker build .
```

---

### Build Example

```yaml
services:

  backend:
    build:
      context: .
      dockerfile: Dockerfile
```

---

# Service Dependency Ordering

Used when one service depends on another.

Example:

Backend depends on Database.

```yaml
services:

  backend:
    depends_on:
      - database

  database:
    image: postgres
```

Docker starts:

1. database
2. backend

---

# Use Case Deployments

---

# 1. Database + Backend + Frontend

Architecture:

```
Frontend
    |
Backend API
    |
Database
```

Compose File:

```yaml
version: '3.8'

services:

  frontend:
    image: nginx

  backend:
    build: ./backend

  database:
    image: mysql
```

Run:

```bash
docker compose up
```

---

# 2. WordPress + MySQL

Architecture:

```
WordPress
    |
MySQL
```

docker-compose.yml

```yaml
version: '3.8'

services:

  wordpress:
    image: wordpress

    ports:
      - "8080:80"

    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: root
      WORDPRESS_DB_PASSWORD: root

  db:
    image: mysql

    environment:
      MYSQL_ROOT_PASSWORD: root
```

Run:

```bash
docker compose up -d
```

Access:

```
http://localhost:8080
```

---

# 3. Node.js + MongoDB

Architecture:

```
Node.js App
      |
MongoDB
```

Compose File:

```yaml
version: '3.8'

services:

  app:
    build: .

    ports:
      - "3000:3000"

    depends_on:
      - mongo

  mongo:
    image: mongo

    ports:
      - "27017:27017"
```

Run:

```bash
docker compose up
```

---

# 4. Spring Boot + PostgreSQL

Architecture:

```
Spring Boot
      |
PostgreSQL
```

docker-compose.yml

```yaml
version: '3.8'

services:

  app:
    build: .

    ports:
      - "8080:8080"

    depends_on:
      - postgres

  postgres:
    image: postgres

    environment:
      POSTGRES_DB: mydb
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: admin
```

Run:

```bash
docker compose up
```

---

# Important Docker Compose Commands

## Start Containers

```bash
docker compose up
```

---

## Start in Background

```bash
docker compose up -d
```

---

## Stop Containers

```bash
docker compose down
```

---

## View Running Containers

```bash
docker ps
```

---

## View Logs

```bash
docker compose logs
```

---

## Rebuild Services

```bash
docker compose up --build
```

---

## Restart Services

```bash
docker compose restart
```

---

# Viva Questions

### What is Microservices Architecture?

An architecture where an application is divided into small independent services communicating through APIs.

---

### Difference between Monolithic and Microservices?

Monolithic = Single large application.

Microservices = Multiple independent services.

---

### What is Docker Compose?

A tool used to define and manage multi-container Docker applications using a YAML file.

---

### What is docker-compose.yml?

Configuration file containing services, volumes, networks, environment variables, etc.

---

### What is a Volume?

Persistent storage used to retain data even after containers are removed.

---

### What is a Network in Docker Compose?

A communication layer allowing containers to interact using service names.

---

### Difference Between Build and Image?

Build → Creates image using Dockerfile.

Image → Uses existing image from registry.

---

### What is depends_on?

Defines service startup dependency ordering.

---

### What is API Gateway?

A single entry point that routes requests to appropriate microservices.

---

### Why use Microservices?

- Scalability
- Isolation
- Agility
- Independent deployment
- Better fault tolerance

---
# End of Notes