# 📅 Day 02 — DevOps Tools, Agile vs DevOps, Continuous Integration & Continuous Deployment

## Introduction to DevOps Tools

DevOps tools are software applications that help automate different stages of the DevOps lifecycle such as development, integration, testing, deployment, monitoring, and infrastructure management.

These tools help teams to:

- Deliver software faster  
- Reduce manual errors  
- Improve collaboration  
- Increase system reliability  
- Enable automation  

##  Major DevOps Tools

###  Git (Version Control System)

Git is a distributed version control system used to track changes in source code during software development.

It allows multiple developers to work on the same project efficiently.

####  Features of Git

- Tracks history of code changes  
- Supports branching and merging  
- Enables team collaboration  
- Helps revert to previous versions  
- Distributed architecture  

#### Common Git Commands

git init
git clone <repository-link>
git add .
git commit -m "message"
git push
git pull
git status
git log
git branch
git checkout
git merge



### Jenkins (Continuous Integration & Deployment Tool)

Jenkins is an open-source automation server used to automate build, testing, and deployment processes.

#### Features of Jenkins

Automates software build process
Detects bugs early
Plugin-based architecture
Pipeline creation support
Integration with Git, Docker, Kubernetes

### Docker (Containerization Platform)

Docker is a platform that packages applications and their dependencies into containers.
This ensures applications run consistently across different environments.

#### Features of Docker

Lightweight virtualization
Faster deployment
Environment consistency
Efficient resource utilization
Easy scalability

### Kubernetes (Container Orchestration Tool)

Kubernetes is used to deploy, manage, and scale containerized applications automatically.

#### Features of Kubernetes

Auto scaling
Load balancing
Self-healing containers
Rolling updates
Service discovery

### Monitoring Tools (Prometheus & Grafana)

Monitoring tools help track performance and health of systems and applications.

#### Purpose

Monitor CPU, memory, network usage
Visualize metrics through dashboards
Detect failures early
Improve reliability

### Agile vs DevOps

Agile and DevOps both aim to improve software delivery but differ in scope.

Feature	Agile	DevOps
Focus	Development process	Development + Operations
Goal	Faster feature delivery	Faster reliable releases
Team	Mostly developers	Developers + Operations
Automation	Limited	Extensive
Lifecycle	Iterative	Continuous
#### Relationship

DevOps extends Agile practices by including deployment, infrastructure management, and monitoring.

### Continuous Integration (CI)

Continuous Integration is a practice where developers frequently integrate code changes into a shared repository.

Each integration triggers:

Automated build
Automated testing
Code quality analysis
This helps detect bugs early and improves software quality.

#### Benefits of Continuous Integration

Early bug detection
Reduced integration conflicts
Faster development cycle
Improved collaboration
Better code quality

#### Continuous Integration Workflow
graph LR
A[Developer Writes Code] --> B[Push to Git Repository]
B --> C[Automated Build]
C --> D[Automated Testing]
D --> E[Feedback to Developer]


### Continuous Deployment (CD)

Continuous Deployment automatically releases application updates to production after successful testing.

#### Benefits of Continuous Deployment

Faster software delivery
Reduced manual work
Lower deployment risk
Immediate feedback
Improved customer satisfaction

🔁 CI/CD Pipeline Overview
graph LR
A[Code Commit] --> B[Build]
B --> C[Test]
C --> D[Deploy]
D --> E[Monitor]
