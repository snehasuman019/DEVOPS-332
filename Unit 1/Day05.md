#  Day 05 — Control Groups (cgroups) for Resource Limits

##  Introduction to Control Groups (cgroups)

Control Groups, commonly known as **cgroups**, are a Linux kernel feature used to **limit, control, and monitor system resources** used by processes or groups of processes.

In container environments, cgroups play a very important role in ensuring that **each container gets fair and controlled access to system resources** such as CPU, memory, disk I/O, and network bandwidth.

cgroups help maintain **system stability, performance, and scalability** in modern DevOps infrastructures.

##  Why cgroups are Needed

Without cgroups:
- One container can consume all CPU or memory  
- Other containers may slow down or crash  
- System performance becomes unstable  
- Resource starvation can occur  

With cgroups:
- Resources are distributed fairly  
- Containers run efficiently  
- System remains stable  
- Performance improves  

## Functions of cgroups

- Limit resource usage  
- Prioritize resource allocation  
- Monitor resource consumption  
- Isolate workloads  
- Prevent system overload  

##  How cgroups Work
cgroups organize processes into hierarchical groups.

Each group can have defined limits for:

- CPU  
- Memory  
- Disk I/O  
- Network  

When a container runs, the container runtime assigns that container to a specific cgroup where its resource limits are enforced.

## cgroups Hierarchy Representation

graph TD
Root --> GroupA
Root --> GroupB
GroupA --> Container1
GroupA --> Container2
GroupB --> Container3

## Types of Resources Controlled by cgroups
### CPU Control
#### cgroups can:
Limit CPU usage percentage
Assign CPU shares
Pin containers to specific CPU cores
This ensures that no single container monopolizes the CPU.

### Memory Control

#### cgroups allow:
Setting maximum memory limits
Preventing excessive memory consumption
Triggering Out Of Memory (OOM) handling
This prevents system crashes due to memory exhaustion.

### Disk I/O Control

#### cgroups can:

Limit read/write speed
Control disk access priority
This helps maintain consistent disk performance.

### Network Bandwidth Control

#### cgroups can:

Limit network traffic
Control bandwidth usage
This ensures fair network usage among containers.

## cgroups in Docker

Docker uses cgroups internally to apply resource limits on containers.

#### Example Docker Commands for Resource Limits
docker run -d --memory="512m" nginx
docker run -d --cpus="1.5" nginx
docker stats

### Benefits of cgroups in DevOps
Prevents resource starvation
Improves system reliability
Enables workload prioritization
Supports multi-tenant environments
Enhances container performance
Helps in auto-scaling strategies
Enables efficient infrastructure utilization

## Relationship Between Namespaces and cgroups
Feature	Namespaces	cgroups
Purpose	Resource Isolation	Resource Limiting
Focus	Visibility	Usage Control
Example	Separate Network	CPU Limit
Role in Containers	Environment Isolation	Resource Management

Both work together to provide complete container isolation and control.