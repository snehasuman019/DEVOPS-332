#  Day 06 — Container Images & Layers, Image Registries & Image Distribution

## Container Image

A **Container Image** is an immutable (unchangeable) blueprint used to create containers.

It contains everything required to run an application:

- Base Operating System  
- Application Code  
- Runtime Environment  
- Libraries and Dependencies  
- Environment Configurations  

Once an image is created, it does not change.  
If updates are needed, a **new image version is built.**

##  Characteristics of Container Image

- Immutable in nature  
- Portable across environments  
- Enables consistent deployments  
- Version controlled  
- Supports microservices architecture  

## Image Layers

Container images are built in **multiple layers.**

Each instruction in a Dockerfile such as:

- `FROM`
- `COPY`
- `RUN`
- `ADD`
- `CMD`

creates a **new layer.**

These layers are **stacked together** to form the final container image.

### Types of Layers

#### Read-Only Layers

These include:
- Base OS  
- Libraries  
- Dependencies  
- Application binaries  
They cannot be modified once the image is built.

####  Writable Layer (Container Layer)

When a container starts:
- A temporary writable layer is added on top  
- All runtime changes happen here  
- Changes are lost when container is removed 

### Image Layer Architecture

graph TD
A[Writable Container Layer]
B[Application Layer]
C[Dependency Layer]
D[Runtime Layer]
E[Base OS Layer]
A --> B --> C --> D --> E

### Benefits of Image Layers

Faster image build using caching
Reduced storage usage
Efficient image distribution
Easy updates and rollback
Layer reuse across multiple images

## Image Registry

An Image Registry is a centralized repository used to:
Store container images
Manage image versions
Distribute images across environments
It ensures consistent deployment across development, testing, and production.

## Why Image Registry is Needed
### Without Registry:
Each system builds images independently
High inconsistency across environments
Manual dependency installation
No version control
Slow deployments

### With Registry:

Build once → Deploy everywhere
Faster deployments
Version controlled environments
Easy rollback capability
Automation support

## Real World Analogy

GitHub → stores source code
Maven Central → stores Java libraries
Image Registry → stores container images

## Public Image Registry

Public registries allow open access to container images.

### Characteristics

Images are publicly visible
Anyone can pull images
Often free to use
Used for base images and open-source applications

#### Examples

Docker Hub
GitHub Container Registry (Public Images)

## Private Image Registry

Private registries restrict access using authentication and authorization.

### Characteristics

Secure and controlled access
Used in enterprise environments
Stores proprietary applications
Integrated with IAM and RBAC

#### Examples

AWS Elastic Container Registry (ECR)
Azure Container Registry (ACR)
GitHub Container Registry (Private)
On-premise private registry

## Image Naming Convention

Container images follow a standard naming format:
<registry>/<namespace>/<image>:<tag>

#### 📌 Example
docker.io/sneha/webapp:v1
Component	Meaning
Registry	Location of image
Namespace	User or organization
Image	Application name
Tag	Version or label

## Tags and Versioning
Tags help identify different versions of the same image.

### Tag	Purpose
latest	Default version
v1, v2	Version based releases
prod	Production ready
dev	Development build

### Versioning enables:

Rollback capability
Controlled deployments
Release tracking

## Image Distribution Process

Image distribution refers to how container images move from developers to production systems.
🔄 Distribution Flow
⬆️ Push Operation

Push operation uploads image layers from local system to registry.

### Features

Requires authentication
Only new layers are uploaded
Faster transfer due to layer caching

#### ⬇️ Pull Operation

Pull operation downloads image layers from registry.

#### Features

Downloads only missing layers
Uses caching mechanism
Faster deployment

### Role of Image Registry in CI/CD Pipeline

#### In modern DevOps pipelines:

Developer commits code to Git
CI system builds container image
Image is pushed to registry
CD system pulls image
Application is deployed automatically
The registry acts as a bridge between CI and CD stages.