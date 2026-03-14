#  Day 04 — Container Runtime, Process Isolation & Namespaces

##  Introduction

Containers are lightweight environments used to run applications in isolation.  
To understand how containers actually work, it is important to learn about:

- Container Runtime  
- Process Isolation  
- Namespaces  

These concepts form the **core foundation of container technology.**

##  Container Runtime

A **Container Runtime** is software responsible for running containers on a host system.

It manages the complete lifecycle of a container such as:

- Pulling container images  
- Creating containers  
- Starting and stopping containers  
- Managing container resources  

### Responsibilities of Container Runtime

- Image management  
- Container execution  
- Resource allocation  
- Security enforcement  
- Networking setup  
- Storage management  

###  Examples of Container Runtimes

- Docker Engine  
- containerd  
- CRI-O  
- runc  

###  Container Runtime Workflow

graph LR
A[Pull Image] --> B[Create Container]
B --> C[Allocate Resources]
C --> D[Start Container Process]
D --> E[Monitor Execution]
E --> F[Stop / Remove Container]

## Process Isolation in Containers

Process isolation ensures that applications running inside a container cannot interfere with processes running on the host or other containers.

Each container runs as an independent environment even though it shares the same host operating system kernel.

### Why Process Isolation is Important

Prevents system conflicts
Improves security
Ensures application stability
Allows multiple applications to run safely on same machine

### How Isolation is Achieved

Isolation in containers is achieved using Linux Kernel features such as Namespaces and Control Groups (cgroups).

# Namespaces

Namespaces are a Linux kernel feature that provides isolation of system resources for processes.

Each container gets its own namespace which makes it appear as if it is running on a separate system.

## Types of Namespaces
 #### PID Namespace
Isolates process IDs
Each container has its own process tree
Processes inside container cannot see host processes

#### Network Namespace
Provides separate network interfaces
Each container gets its own IP address
Enables container networking

#### Mount Namespace
Isolates filesystem mount points
Containers can have their own filesystem structure

#### UTS Namespace
Allows containers to have their own hostname

#### IPC Namespace
Isolates inter-process communication resources

#### User Namespace
Maps container users to different host users
Improves security

### Namespace Isolation Diagram
graph TD
HostKernel --> Container1
HostKernel --> Container2
Container1 --> PID1
Container1 --> NET1
Container1 --> MOUNT1
Container2 --> PID2
Container2 --> NET2
Container2 --> MOUNT2


### Benefits of Container Runtime

Efficient container lifecycle management
Faster container startup
Improved resource utilization
Enhanced security
Automation support

### Benefits of Process Isolation

Prevents interference between applications
Increases system reliability
Enables safe multi-tenant environments
Improves performance

### Benefits of Namespaces

Strong process and resource isolation
Independent networking and filesystem
Better container security
Enables scalable infrastructure

## Basic Commands Related to Containers
docker run nginx
docker ps
docker stop <container-id>
docker rm <container-id>
docker inspect <container-id>