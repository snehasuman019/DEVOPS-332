# Continuous Integration (CI) with GitHub Actions

---

# 1. Introduction to Continuous Integration (CI)

## What is Continuous Integration (CI)?

Continuous Integration (CI) is a DevOps practice where developers frequently merge code changes into a shared repository.

Whenever code is pushed:

- Build starts automatically
- Tests run automatically
- Code quality checks execute automatically
- Deployment can be triggered automatically

Goal:

> Detect and fix issues early in the development cycle.

---

# What is GitHub Actions?

GitHub Actions is GitHub's built-in CI/CD platform used to automate:

- Build processes
- Testing
- Deployment
- Security checks
- Docker image creation

GitHub Actions uses YAML workflow files.

---

# Why Use GitHub Actions?

Benefits:

- Built into GitHub
- Free for public repositories
- Supports CI/CD
- Large marketplace of reusable actions
- Easy integration with Docker, AWS, Azure, GCP

---

# Workflow Automation

Workflow automation means automatically executing predefined tasks when specific events occur.

Example:

```text
Developer Pushes Code
          ↓
GitHub Actions Triggered
          ↓
Build Application
          ↓
Run Tests
          ↓
Create Docker Image
          ↓
Deploy Application
```

---

# Workflow Directory Structure

GitHub Actions workflows are stored inside:

```text
.github/
└── workflows/
      ├── ci.yml
      ├── deploy.yml
      └── docker.yml
```

Example:

```text
project
│
├── src
├── pom.xml
│
└── .github
    └── workflows
        └── ci.yml
```

---

# Basic Workflow Structure

```yaml
name: Java CI

on:
  push:

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v4
```

---

# Key Components of GitHub Actions

GitHub Actions consists of:

1. Workflows
2. Jobs
3. Steps
4. Actions
5. Runners

---

# Workflows

A workflow is an automated process defined in a YAML file.

Example:

```yaml
name: Build Workflow
```

A workflow can contain:

- Multiple jobs
- Multiple steps
- Multiple actions

---

# Jobs

A workflow consists of one or more jobs.

Example:

```yaml
jobs:

  build:
    runs-on: ubuntu-latest

  test:
    runs-on: ubuntu-latest
```

Jobs run independently unless dependencies are specified.

---

# Steps

Each job contains multiple steps.

Example:

```yaml
steps:

  - name: Checkout Code

  - name: Build Project

  - name: Run Tests
```

---

# Actions

Actions are reusable tasks.

Example:

```yaml
uses: actions/checkout@v4
```

Popular actions:

- checkout
- setup-java
- setup-node
- upload-artifact
- docker-build-push

---

# Runners

A runner is a machine that executes workflows.

Types:

1. GitHub-hosted runners
2. Self-hosted runners

---

# Workflow Triggers

Triggers define when workflows run.

```yaml
on:
  push:
```

---

# Push Trigger

Runs workflow when code is pushed.

```yaml
on:
  push:
```

Example:

```bash
git push origin main
```

Workflow starts automatically.

---

# Pull Request Trigger

Runs when a pull request is created or updated.

```yaml
on:
  pull_request:
```

Use Case:

```text
Validate code before merging
```

---

# Schedule Trigger

Runs workflows at specific times.

Uses Cron syntax.

Example:

```yaml
on:
  schedule:
    - cron: "0 0 * * *"
```

Runs every day at midnight.

---

# Cron Format

```text
* * * * *
│ │ │ │ │
│ │ │ │ └── Day of Week
│ │ │ └──── Month
│ │ └────── Day
│ └──────── Hour
└────────── Minute
```

---

# Manual Workflow Trigger

Allows users to run workflows manually.

```yaml
on:
  workflow_dispatch:
```

GitHub UI:

```text
Actions
→ Select Workflow
→ Run Workflow
```

---

# Multiple Triggers

```yaml
on:
  push:
  pull_request:
  workflow_dispatch:
```

Workflow runs on all specified events.

---

# Jobs & Matrix Strategies

Matrix strategy allows running jobs on multiple environments.

---

## Example

```yaml
strategy:
  matrix:
    java-version: [17, 21]
```

Runs workflow twice:

```text
Java 17
Java 21
```

---

# Complete Matrix Example

```yaml
jobs:

  test:

    strategy:

      matrix:

        os: [ubuntu-latest, windows-latest]

    runs-on: ${{ matrix.os }}
```

Execution:

```text
Ubuntu Build
Windows Build
```

---

# Steps & Shell Commands

Shell commands are executed using:

```yaml
run:
```

Example:

```yaml
steps:

  - name: Print Message

    run: echo "Hello GitHub Actions"
```

---

# Multiple Commands

```yaml
run: |
  pwd
  ls
  echo "Build Started"
```

---

# Using Marketplace Actions

GitHub Marketplace provides pre-built actions.

Marketplace:

```text
https://github.com/marketplace/actions
```

Popular Actions:

- Checkout
- Setup Java
- Setup Node
- Docker Build
- AWS Deploy

---

# Example

```yaml
- uses: actions/checkout@v4
```

Downloads repository code.

---

# Language-Specific Actions

---

# Java

```yaml
- uses: actions/setup-java@v4

  with:
    distribution: temurin
    java-version: 17
```

---

# Node.js

```yaml
- uses: actions/setup-node@v4

  with:
    node-version: 20
```

---

# Python

```yaml
- uses: actions/setup-python@v5

  with:
    python-version: 3.11
```

---

# Using Caching for Faster Builds

Caching stores dependencies between workflow runs.

Benefits:

- Faster builds
- Reduced downloads
- Lower execution time

---

# Maven Cache Example

```yaml
- uses: actions/cache@v4

  with:
    path: ~/.m2

    key: maven-cache
```

---

# Node.js Cache Example

```yaml
- uses: actions/cache@v4

  with:
    path: node_modules

    key: node-cache
```

---

# Multi-Job Workflows

A workflow can contain multiple jobs.

Example:

```text
Build Job
     ↓
Test Job
     ↓
Deploy Job
```

---

# Job Dependency

```yaml
jobs:

  build:

  test:
    needs: build

  deploy:
    needs: test
```

Execution order:

```text
Build
 ↓
Test
 ↓
Deploy
```

---

# Example Multi-Job Workflow

```yaml
jobs:

  build:

    runs-on: ubuntu-latest

  test:

    needs: build

    runs-on: ubuntu-latest

  deploy:

    needs: test

    runs-on: ubuntu-latest
```

---

# Deploying Using GitHub Actions

GitHub Actions can deploy applications automatically.

Targets:

- Linux Servers
- AWS
- Azure
- Google Cloud
- Kubernetes
- Docker Swarm

---

# Deployment Workflow

```text
Push Code
    ↓
Build
    ↓
Test
    ↓
Docker Image
    ↓
Deployment
```

---

# GitHub-Hosted Runners

Managed by GitHub.

Example:

```yaml
runs-on: ubuntu-latest
```

Available runners:

```text
ubuntu-latest
windows-latest
macos-latest
```

---

# Advantages

- No setup required
- Fully managed
- Easy to use

---

# Self-Hosted Runners

Managed by the organization.

Installed on:

- Local Server
- VM
- Cloud Machine

Example:

```yaml
runs-on: self-hosted
```

---

# Advantages

- Full control
- Custom software
- More resources

---

# Runner Security & Management

Best Practices:

### Use Secrets

Never hardcode:

```yaml
password=admin123
```

Use:

```yaml
${{ secrets.PASSWORD }}
```

---

### Restrict Permissions

Use least privilege principle.

---

### Update Runners

Keep runners updated.

---

### Monitor Usage

Track workflow executions and logs.

---

# Docker & GitHub Actions

GitHub Actions can automatically:

- Build Docker images
- Push images
- Deploy containers

---

# Building Docker Images in CI

Example:

```yaml
- name: Build Docker Image

  run: docker build -t myapp .
```

---

# Docker Build Workflow

```yaml
jobs:

  build:

    runs-on: ubuntu-latest

    steps:

      - uses: actions/checkout@v4

      - run: docker build -t myapp .
```

---

# Pushing to Docker Hub

---

## Login

```yaml
- name: Login Docker Hub

  uses: docker/login-action@v3

  with:
    username: ${{ secrets.DOCKER_USERNAME }}

    password: ${{ secrets.DOCKER_PASSWORD }}
```

---

## Build and Push

```yaml
- name: Build Image

  run: docker build -t username/myapp .

- name: Push Image

  run: docker push username/myapp
```

---

# Complete Docker Hub Workflow

```yaml
name: Docker Build

on:
  push:

jobs:

  docker:

    runs-on: ubuntu-latest

    steps:

      - uses: actions/checkout@v4

      - uses: docker/login-action@v3

        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}

      - run: docker build -t username/myapp .

      - run: docker push username/myapp
```

---

# GitHub Container Registry (GHCR)

GitHub's built-in container registry.

Example Image:

```text
ghcr.io/username/app
```

---

# Login to GHCR

```yaml
- uses: docker/login-action@v3

  with:
    registry: ghcr.io

    username: ${{ github.actor }}

    password: ${{ secrets.GITHUB_TOKEN }}
```

---

# Build & Push to GHCR

```yaml
- run: docker build -t ghcr.io/user/app .

- run: docker push ghcr.io/user/app
```

---

# Deployments to Servers

Example:

```yaml
- name: Deploy

  uses: appleboy/ssh-action@v1

  with:
    host: ${{ secrets.SERVER_IP }}
    username: ubuntu
    key: ${{ secrets.SERVER_KEY }}

    script: |
      docker pull username/app
      docker restart app
```

---

# Deployments to AWS

Common Services:

- EC2
- ECS
- EKS
- Lambda

Workflow:

```text
Push Code
    ↓
Build
    ↓
Docker Image
    ↓
Push to ECR
    ↓
Deploy to ECS
```

---

# Deployments to Kubernetes

Workflow:

```text
Build Image
     ↓
Push Registry
     ↓
kubectl apply
```

Example:

```yaml
run: kubectl apply -f deployment.yaml
```

---

# Complete CI/CD Pipeline

```text
Developer Pushes Code
          ↓
GitHub Actions Triggered
          ↓
Checkout Repository
          ↓
Install Dependencies
          ↓
Compile Code
          ↓
Run Tests
          ↓
Build Docker Image
          ↓
Push Image
          ↓
Deploy Application
          ↓
Production Ready
```

---

# Common GitHub Actions Commands

## View Workflows

```text
GitHub Repository
→ Actions Tab
```

---

## Re-run Workflow

```text
Actions
→ Select Workflow
→ Re-run Jobs
```

---

## Cancel Workflow

```text
Actions
→ Cancel Workflow
```

---

# Viva Questions

## What is Continuous Integration?

A practice of automatically building and testing code whenever changes are committed.

---

## What is GitHub Actions?

GitHub's built-in CI/CD automation platform.

---

## Where are workflows stored?

```text
.github/workflows/
```

---

## What is a Workflow?

A YAML file defining automation tasks.

---

## What is a Job?

A collection of steps executed on a runner.

---

## What is a Step?

An individual task within a job.

---

## What is an Action?

Reusable automation component.

---

## What is a Runner?

A machine that executes GitHub Actions workflows.

---

## Difference Between GitHub-Hosted and Self-Hosted Runners?

GitHub-hosted → Managed by GitHub.

Self-hosted → Managed by organization.

---

## What is workflow_dispatch?

A manual workflow trigger.

---

## What is Matrix Strategy?

Runs jobs across multiple operating systems or language versions.

---

## How to Store Passwords Securely?

Using GitHub Secrets.

---

## How to Build Docker Images in GitHub Actions?

```yaml
docker build -t app .
```

---

## What is GHCR?

GitHub Container Registry used to store Docker images.

---

## How to Deploy Using GitHub Actions?

Use deployment actions such as SSH, AWS Actions, Kubernetes Actions, etc.

---

# End of Notes