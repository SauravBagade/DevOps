# 🐳 1️⃣ Docker Introduction 

This chapter builds a complete conceptual foundation of Docker.
After finishing this section, you should clearly understand:

* What Docker really is
* How it differs from virtualization
* Why it became industry standard
* How containers work at OS level
* Where Docker fits in modern DevOps

---

## 1.1 What is Docker

![Image](https://assets.bytebytego.com/diagrams/0414-how-does-docker-work.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2Amq2QpIZUnfmnDPn47spI4A.jpeg)

![Image](https://miro.medium.com/1%2ApvBxLhlnJ7w9FKPUpJfXkw.jpeg)

![Image](https://www.researchgate.net/publication/396790138/figure/fig2/AS%3A11431281688182742%401761190859381/Dockers-filesystem-architecture-it-relies-on-layered-images-which-are-read-only-a.png)

Docker is a container platform developed by Docker, Inc. that enables applications to run inside isolated environments called containers.

### Simple Definition

Docker packages an application along with:

* Runtime
* System libraries
* Dependencies
* Configuration

Into a standardized unit called an **image**.

From that image, Docker creates a **container**, which is the running process.

---

### What a Container Actually Is

A container is:

* A Linux process
* Running with isolation
* Using namespaces
* Controlled by cgroups
* Sharing the host kernel

This is critical to understand:

> A container is NOT a virtual machine.
> It is an isolated process group on the host OS.

---

### Why This Design Matters

Because containers:

* Start in seconds
* Use minimal memory
* Scale quickly
* Share common OS resources efficiently

---

## 1.2 What is Virtualization

Virtualization allows multiple logical systems to run on one physical machine.

There are two main approaches.

---

### 1️⃣ Hardware-Level Virtualization (Virtual Machines)

Used by:

* VMware
* Microsoft (Hyper-V)
* Oracle Corporation (VirtualBox)

Architecture:

```text
Hardware
 → Hypervisor
   → Guest OS
     → Application
```

Each VM contains:

* Full operating system
* Separate kernel
* Dedicated memory allocation
* System services

### Advantages

* Strong isolation
* Can run different operating systems
* Mature enterprise support

### Disadvantages

* Heavy resource usage
* Slow startup
* High storage requirements

---

### 2️⃣ OS-Level Virtualization (Containers)

Architecture:

```text
Hardware
 → Host OS
   → Docker Engine
     → Containers
```

Containers:

* Share the host OS kernel
* Isolate processes using kernel features
* Require fewer resources
* Start instantly

---

### Key Architectural Difference

Virtual Machines virtualize hardware.
Docker isolates processes.

That is the core difference.

---

## 1.3 Why Docker is Used

Before Docker, developers faced major problems.

### Common Issues

* Application works locally but fails on server
* Dependency conflicts
* Library version mismatch
* Manual environment setup
* Difficult scaling
* Configuration drift

Example:

Developer uses Node 18
Production server has Node 16
Application crashes

Docker eliminates this by packaging everything inside the image.

---

### Major Benefits

1. Environment consistency
2. Fast deployment
3. Portability across platforms
4. Simplified CI/CD
5. Microservices enablement
6. Cloud-ready architecture

---

### Real-World Deployment Flow

```text
Developer writes Dockerfile
 → Build Image
   → Push to Registry
     → Pull on Server
       → Run Container
```

The same image runs everywhere.

---

## 1.4 Virtualization vs Containers

![Image](https://akfpartners.com//uploads/blog/VM_Image.PNG)

![Image](https://raw.githubusercontent.com/collabnix/dockerlabs/master/beginners/docker/images/vm-docker5.png)

![Image](https://www.researchgate.net/publication/364684487/figure/fig5/AS%3A11431281390116518%401745245064959/Resource-utilization-comparison-chart-a-CPU-utilization-vs-number-of-VMs-b-RAM.tif)

![Image](https://www.researchgate.net/publication/341907958/figure/fig2/AS%3A898684774526984%401591274555152/CPU-Comparison-of-Docker-and-Virtual-Machine.png)

| Feature        | Virtual Machine | Docker Container |
| -------------- | --------------- | ---------------- |
| OS             | Full Guest OS   | Shared Host OS   |
| Kernel         | Separate        | Shared           |
| Boot Time      | Minutes         | Seconds          |
| Size           | GBs             | MBs              |
| Isolation      | Hardware-level  | Process-level    |
| Resource Usage | High            | Low              |

---

### Performance Comparison

Containers perform near native speed because:

* No OS boot
* No hardware emulation
* Lightweight filesystem
* Direct kernel interaction

---

## 1.5 Docker Lifecycle

Docker follows a defined lifecycle.

```text
Dockerfile
 → docker build
   → Image
     → docker run
       → Container
         → docker stop
           → docker rm
```

---

### Container States

* Created
* Running
* Paused
* Restarting
* Stopped
* Dead

Containers are designed to be replaceable, not manually repaired.

---

## 1.6 Docker vs Virtual Machine (Internal View)

### Virtual Machine

* Runs full OS
* Requires hypervisor
* High overhead
* Slower scaling

### Docker

* Runs isolated process
* Shares kernel
* Lightweight
* Fast scaling

VMs are ideal when:

* Running different operating systems

Containers are ideal when:

* Running multiple services efficiently on same OS

---

## 1.7 Docker Use Cases

Docker is widely used with:

* Kubernetes
* Amazon Web Services
* Microsoft Azure
* Google Cloud

---

### Microservices Architecture

Each service:

* Runs in separate container
* Has isolated dependencies
* Can scale independently
* Can deploy independently

---

### CI/CD Pipeline Integration

```text
Git Push
 → CI builds Docker Image
   → Run automated tests
     → Push image to registry
       → Deploy automatically
```

Docker ensures reproducibility.

---

## 1.8 Machine Virtualization vs Containers

![Image](https://www.sei.cmu.edu/media/images/multicorevirtualization_firesmith__figure2_0918.original.png)

![Image](https://ars.els-cdn.com/content/image/3-s2.0-B9780128204887000268-gr003.jpg)

![Image](https://www.netapp.com/media/container-vs-vm-inline1_tcm19-82163.png?v=85344)

![Image](https://media2.dev.to/dynamic/image/width%3D1600%2Cheight%3D900%2Cfit%3Dcover%2Cgravity%3Dauto%2Cformat%3Dauto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F9zk0491ay21mp2tyea79.png)

### VM Stack

```text
Hardware
 → Hypervisor
   → Guest OS
     → Applications
```

### Container Stack

```text
Hardware
 → Host OS
   → Docker Engine
     → Containers
```

Containers eliminate guest OS overhead.

---

## 1.9 Evolution of Containers

| Year   | Technology   |
| ------ | ------------ |
| 1979   | chroot       |
| 2008   | LXC          |
| 2013   | Docker       |
| Modern | OCI Standard |

Docker later aligned with standards from:

Open Container Initiative

This ensures:

* Portability
* Runtime compatibility
* Vendor neutrality

---

## 1.10 Docker in Modern DevOps (2026 Landscape)

Modern infrastructure stack:

```text
Docker
 → Kubernetes
   → Cloud Provider
     → Monitoring
       → Automation
```

Docker plays a central role in:

* Cloud-native apps
* Platform engineering
* Infrastructure as Code
* GitOps
* Edge computing
* AI workloads

---
# 2️⃣ Docker Architecture

This section explains **how Docker works internally** — from the moment you type a command to when a container starts running.

After this section, you should clearly understand:

* How Docker components interact
* What happens when you run `docker run`
* Role of `dockerd`, containerd, and runc
* How Docker communicates with the Linux kernel
* How images are pulled and containers are created

---

## 2.1 Docker Engine

![Image](https://docs.docker.com/get-started/images/docker-architecture.webp)

![Image](https://miro.medium.com/1%2AGoZ56yZNpG_VnGGvqhYlCQ.png)

![Image](https://www.docker.com/app/uploads/2021/10/Docker-Website-2018-Diagrams-071918-V5_a-Docker-Engine-page-first-panel.png)

![Image](https://www.dclessons.com/uploads/2019/08/Docker-2.3.png)

Docker Engine is the core runtime that builds, runs, and manages containers.

It follows a **client-server architecture**.

Docker Engine consists of:

1. Docker CLI (Client)
2. Docker Daemon (`dockerd`)
3. REST API

---

### High-Level Architecture Flow

```text
User
 → Docker CLI
   → Docker REST API
     → Docker Daemon
       → containerd
         → runc
           → Linux Kernel
             → Container Process
```

Each layer has a specific responsibility.

---

## 2.2 Docker Daemon (`dockerd`)

The Docker daemon is the main background service.

It is responsible for:

* Managing images
* Creating and running containers
* Handling networking
* Managing volumes
* Communicating with registries
* Applying resource limits
* Logging configuration

It listens for requests through:

* Unix socket (`/var/run/docker.sock`)
* TCP socket (if configured)

---

### What Happens Internally

When you run:

```bash
docker ps
```

The CLI sends a request to the daemon.
The daemon queries its internal container database and returns the result.

The daemon does the real work.
The CLI is just a request sender.

---

## 2.3 Docker CLI (Client)

The Docker CLI is the command-line interface.

Examples:

```bash
docker build
docker run
docker stop
docker images
```

The CLI:

* Parses user commands
* Converts them into API requests
* Sends them to the daemon

Important:

The CLI does not create containers directly.

---

### Remote Docker

You can configure CLI to talk to a remote Docker daemon using:

```bash
docker -H tcp://server-ip:2375 ps
```

This makes Docker usable across remote servers.

---

## 2.4 Docker REST API

Docker exposes a REST API.

The CLI communicates with `dockerd` using this API.

This allows:

* Automation scripts
* CI/CD integration
* Platform tools
* Third-party orchestration

Tools like:

* Kubernetes
* Jenkins

Interact with Docker using APIs.

---

## 2.5 Docker Registry

A registry stores Docker images.

Most commonly used:

Docker Hub

There are two types:

1. Public registry
2. Private registry

---

### Registry Architecture

A registry stores:

* Image layers
* Image manifest
* Tags

When you push an image:

```bash
docker push myapp:v1
```

Docker:

1. Checks existing layers
2. Uploads only missing layers
3. Updates image manifest

Layer reuse reduces bandwidth usage.

---

## 2.6 Docker Hub

Docker Hub is the default public registry provided by
Docker, Inc..

If you run:

```bash
docker pull nginx
```

Docker automatically pulls from Docker Hub unless another registry is specified.

---

### Image Types on Docker Hub

* Official images
* Verified publisher images
* Community images

---

## 2.7 containerd & runc

![Image](https://www.researchgate.net/publication/333235708/figure/fig1/AS%3A760874507722754%401558418027301/Docker-container-architecture.ppm)

![Image](https://devoriales.com/static/post_images/high-level-container-architecture.png)

![Image](https://miro.medium.com/1%2AxvSX9Hk1gmsKV7tDMuO5hw.jpeg)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2ALQis_Wh44VXQkiW87hhsAw.png)

Docker does not directly talk to the Linux kernel.

It delegates work to lower-level runtimes.

---

### containerd

containerd is responsible for:

* Managing container lifecycle
* Handling image pulls
* Snapshot management
* Storage handling

It acts as a container supervisor.

Docker uses containerd internally.

---

### runc

runc is a lightweight runtime that:

* Creates namespaces
* Applies cgroups
* Sets up root filesystem
* Launches the container process

runc directly interacts with the Linux kernel.

---

## 2.8 OCI (Open Container Initiative)

Open Container Initiative defines open standards for:

* Container image format
* Runtime specification

This ensures:

* Vendor neutrality
* Runtime compatibility
* Image portability

Because of OCI:

* Docker images work with Kubernetes
* containerd works independently
* Other runtimes can run same images

---

## 2.9 Complete Docker Architecture Flow

Let’s break down the full execution path of:

```bash
docker run nginx
```

### Step 1 – CLI Request

CLI sends API request to Docker daemon.

---

### Step 2 – Image Check

Daemon checks local image store.

If not found:

* Pulls from registry
* Downloads layers
* Verifies checksum

---

### Step 3 – containerd Setup

containerd:

* Creates container metadata
* Prepares snapshot
* Mounts layered filesystem

---

### Step 4 – runc Execution

runc:

* Creates Linux namespaces
* Applies resource limits
* Sets root filesystem
* Executes main process

---

### Step 5 – Kernel Enforcement

Linux kernel enforces:

* Process isolation
* CPU limits
* Memory limits
* Network isolation

Container is now running.

---

## 2.10 How Docker Runs a Container Internally

Full internal chain:

```text
docker run nginx
 → CLI sends API request
   → dockerd processes request
     → containerd prepares container
       → runc configures isolation
         → Kernel starts process
           → Container is active
```

Important understanding:

The container is just a process created with isolation rules.

---

# 🔎 Internal Layer Responsibilities

| Component  | Responsibility               |
| ---------- | ---------------------------- |
| CLI        | Accepts user input           |
| REST API   | Communication layer          |
| dockerd    | Orchestration & management   |
| containerd | Container lifecycle          |
| runc       | Runtime execution            |
| Kernel     | Isolation & resource control |

---
# 3️⃣ Docker Core Concepts (Full Deep Documentation – 2026)

This section explains the core building blocks of Docker in complete detail.

After this section, you should clearly understand:

* What an image really is internally
* How layers work and why they matter
* What a container truly represents
* How storage, networking, and registry connect together
* Why immutability is critical in production

---

# 3.1 Docker Image

![Image](https://i.sstatic.net/fotPN.jpg)

![Image](https://miro.medium.com/0%2AqcB7YXqasZYLwMYc.jpg)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2ABCaWeTzJkH0ry4m_DX2gLQ.png)

![Image](https://i.sstatic.net/6EKSp.jpg)

## What is a Docker Image?

A Docker image is a **read-only layered filesystem** used to create containers.

It includes:

* Base operating system layer
* Application runtime
* Libraries
* Dependencies
* Configuration
* Application code

An image does not run.
It is only a template.

---

## Internal Structure of an Image

Every image consists of multiple layers stacked on top of each other.

Example Dockerfile:

```dockerfile
FROM ubuntu:22.04
RUN apt update
RUN apt install nginx
COPY index.html /var/www/html/
```

Docker creates:

1. Ubuntu base layer
2. Update layer
3. Nginx install layer
4. File copy layer

Each instruction creates a new layer.

---

## How Layers Work

Layers are:

* Immutable (read-only)
* Cached
* Reusable
* Shared across images

If two images use the same base image:

Docker stores that layer only once on disk.

This improves:

* Storage efficiency
* Build speed
* Network transfer efficiency

---

## Layer Caching Mechanism

When building:

```bash
docker build -t myapp .
```

Docker:

1. Reads Dockerfile
2. Executes instructions sequentially
3. Caches each layer

If no change occurs in a step:

* Docker reuses cached layer
* Skips rebuilding

If a step changes:

* That layer and all following layers rebuild

This is why instruction order matters.

---

## Copy-on-Write Mechanism

Image layers are read-only.

When a container modifies a file:

* Docker copies that file into writable layer
* Modification happens there
* Base image remains unchanged

This is called Copy-on-Write.

---

## Why Image Immutability Matters

Images never change after build.

If update is needed:

* Modify Dockerfile
* Rebuild image
* Redeploy container

This ensures:

* Reproducibility
* Version control
* Easy rollback
* CI/CD compatibility

---

# 3.2 Docker Container

![Image](https://assets.bytebytego.com/diagrams/0414-how-does-docker-work.png)

![Image](https://docs.docker.com/engine/storage/drivers/images/container-layers.webp)

![Image](https://cdn.bunny.pictures/images/what-is-a-linux-namespace-and-container-isolation.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2Away9ZDlcgOKvaB8k7jaOAA.png)

## What is a Container?

A container is:

> A running instance of an image with an additional writable layer.

Technically:

* It is a Linux process
* Running inside isolated namespaces
* Controlled by cgroups
* Using image as root filesystem

---

## What Happens When You Run:

```bash
docker run nginx
```

Step-by-step:

1. Check image locally
2. Pull from registry if missing
3. Create container metadata
4. Add writable layer
5. Configure networking
6. Apply CPU & memory limits
7. Start main process

That main process becomes PID 1 inside container.

---

## Container Isolation Details

Docker uses Linux kernel features.

### Namespaces

Provide isolation for:

* Process IDs
* Network stack
* Filesystem mount points
* Hostname
* User IDs
* IPC

Each container believes it is running alone.

---

### Control Groups (cgroups)

Limit:

* CPU usage
* Memory usage
* Disk I/O
* Network bandwidth

This prevents resource exhaustion.

---

## Writable Layer

When container runs:

* Image layers remain read-only
* Docker adds writable layer

If container is deleted:

* Writable layer is removed
* Changes disappear

Unless volumes are used.

---

# 3.3 Dockerfile

A Dockerfile is a build instruction file used to create images.

Example:

```dockerfile
FROM node:18
WORKDIR /app
COPY package.json .
RUN npm install
COPY . .
CMD ["node", "server.js"]
```

---

## Dockerfile Build Flow

```text
Dockerfile
 → docker build
   → Image
     → docker run
       → Container
```

Each instruction:

* Executes sequentially
* Creates a new layer
* Uses caching

---

## Why Dockerfile Order Matters

Example:

Bad order:

```dockerfile
COPY . .
RUN npm install
```

Any code change breaks cache.

Better order:

```dockerfile
COPY package.json .
RUN npm install
COPY . .
```

Now dependency install is cached unless package.json changes.

---

# 3.4 Docker Volumes

Containers are temporary by design.

Data inside writable layer disappears when container is removed.

Volumes solve this.

---

## Storage Types

1. Writable layer (temporary)
2. Named volumes (persistent)
3. Bind mounts (host directory mapping)

---

## Named Volume Example

```bash
docker volume create mydata
docker run -v mydata:/var/lib/mysql mysql
```

Now:

* Database data persists
* Container can be recreated safely

---

## Volume Lifecycle

Volumes:

* Exist independently
* Must be deleted manually
* Survive container deletion

---

# 3.5 Docker Networks

Docker creates virtual networks.

Default network: bridge.

Each container gets:

* Virtual Ethernet interface
* IP address
* Internal DNS entry

---

## Communication Types

1. Container → Container
2. Host → Container
3. Container → Internet
4. External → Container

---

## Port Publishing

Example:

```bash
docker run -p 8080:80 nginx
```

Host port 8080 forwards to container port 80.

Docker configures NAT rules internally.

---

# 3.6 Docker Registry

Registry stores images.

Common example:

Docker Hub

---

## Registry Components

* Repository
* Tags
* Layers
* Manifest

---

## Push Process

```bash
docker push myapp:v1
```

Docker:

1. Compares local layers
2. Uploads missing layers only
3. Updates manifest

Efficient and bandwidth-friendly.

---

# 3.7 Core Concept Relationship

![Image](https://almablog-media.s3.ap-south-1.amazonaws.com/docker_architecture_d8ec8e9cb8.png)

![Image](https://media2.dev.to/dynamic/image/width%3D1000%2Cheight%3D500%2Cfit%3Dcover%2Cgravity%3Dauto%2Cformat%3Dauto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fdyzwicbhbr3mq76prwwm.png)

![Image](https://cdn.prod.website-files.com/68232df8de1a79da2c32a09e/68473e91a43921d3d4ed0bbe_66fdaea48c5da47d9f4bca52_66fdae9fcd8243eb5249bacf_Docker%252520Daemon%252520Architecture%252520-%252520Diagram%2525202.png)

![Image](https://media.licdn.com/dms/image/v2/D5612AQELIQ0xTBQVAA/article-cover_image-shrink_720_1280/article-cover_image-shrink_720_1280/0/1731916055174?e=2147483647\&t=fdeFfIHwmzQB4sU38MDYfBeKPaz7JexgaQpjS3T5QXg\&v=beta)

Full relationship:

```text
Dockerfile
 → Image (Layered, Immutable)
   → Container (Runtime + Writable Layer)
     → Uses Volume (Persistent Storage)
     → Uses Network (Communication)
       → Stored in Registry
         → Managed by Docker Engine
```

Everything connects through the image.

---

# 3.8 Image Immutability Concept

Never modify container manually in production.

Wrong:

```bash
docker exec -it container bash
apt install something
```

Correct:

* Update Dockerfile
* Rebuild image
* Redeploy

This ensures consistent deployments.

---

# 3.9 Container Runtime Lifecycle

States:

* Created
* Running
* Paused
* Restarting
* Stopped
* Dead

Lifecycle commands:

```bash
docker create
docker start
docker stop
docker rm
```

Best practice:

Containers should be replaceable, not repaired.

---
# 4️⃣ Docker Commands 

This section covers Docker commands from:

* Basic usage
* Intermediate options
* Advanced runtime flags
* Production-level usage patterns
* Troubleshooting usage

Commands are grouped exactly as per your index.

---

# 4.1 Docker System & Info Commands

These commands help inspect Docker environment and overall system state.

---

## 🔹 `docker version`

Shows Docker client and server versions.

```bash
docker version
```

Displays:

* Client version
* Server version
* API version
* Go version

Useful for debugging compatibility issues.

---

## 🔹 `docker info`

Shows detailed system-wide information.

```bash
docker info
```

Displays:

* Storage driver (overlay2, etc.)
* Number of containers
* Number of images
* Logging driver
* Cgroup version
* Rootless mode status

Production use:

Check storage driver performance and resource configuration.

---

## 🔹 `docker system df`

Shows disk usage.

```bash
docker system df
```

Useful to identify:

* Image space usage
* Volume size
* Build cache size

---

## 🔹 `docker system prune`

Removes unused data.

```bash
docker system prune
```

Options:

```bash
docker system prune -a
docker system prune --volumes
```

Production caution:

Never run blindly in production — may delete unused images.

---

# 4.2 Docker Image Commands

Manage images.

---

## 🔹 `docker images`

List images.

```bash
docker images
```

Filters:

```bash
docker images -f dangling=true
```

---

## 🔹 `docker pull`

Download image.

```bash
docker pull nginx
docker pull nginx:1.25
```

Pull from custom registry:

```bash
docker pull myregistry.com/app:v1
```

---

## 🔹 `docker build`

Build image from Dockerfile.

```bash
docker build -t myapp .
```

Important flags:

```bash
docker build -t myapp:v1 -f Dockerfile.prod .
docker build --no-cache -t myapp .
docker build --build-arg ENV=prod .
```

---

## 🔹 `docker tag`

Tag image.

```bash
docker tag myapp:v1 username/myapp:v1
```

Used before pushing.

---

## 🔹 `docker push`

Push image to registry.

```bash
docker push username/myapp:v1
```

Only missing layers are uploaded.

---

## 🔹 `docker rmi`

Remove image.

```bash
docker rmi myapp:v1
```

Force remove:

```bash
docker rmi -f image_id
```

---

# 4.3 Docker Container Commands

Manage container lifecycle.

---

## 🔹 `docker run`

Most important command.

```bash
docker run nginx
```

Run in detached mode:

```bash
docker run -d nginx
```

Port mapping:

```bash
docker run -p 8080:80 nginx
```

Environment variable:

```bash
docker run -e ENV=prod nginx
```

Volume mount:

```bash
docker run -v mydata:/data nginx
```

Resource limits:

```bash
docker run --memory=512m --cpus=1 nginx
```

Restart policy:

```bash
docker run --restart=always nginx
```

---

## 🔹 `docker ps`

List running containers.

```bash
docker ps
docker ps -a
```

---

## 🔹 `docker stop`

Gracefully stop container.

```bash
docker stop container_id
```

---

## 🔹 `docker start`

Start stopped container.

```bash
docker start container_id
```

---

## 🔹 `docker restart`

Restart container.

```bash
docker restart container_id
```

---

## 🔹 `docker rm`

Remove container.

```bash
docker rm container_id
```

Force remove:

```bash
docker rm -f container_id
```

---

# 4.4 Docker Inspect, Logs & Stats

---

## 🔹 `docker inspect`

View container or image metadata.

```bash
docker inspect container_id
```

Useful to check:

* IP address
* Mounts
* Network
* Resource limits

---

## 🔹 `docker logs`

View logs.

```bash
docker logs container_id
docker logs -f container_id
docker logs --tail 100 container_id
```

---

## 🔹 `docker stats`

Live resource usage.

```bash
docker stats
```

Shows:

* CPU usage
* Memory usage
* Network I/O
* Block I/O

---

# 4.5 Docker Exec & Attach

---

## 🔹 `docker exec`

Run command inside running container.

```bash
docker exec -it container_id bash
```

Production debugging tool.

---

## 🔹 `docker attach`

Attach to container STDIN/STDOUT.

```bash
docker attach container_id
```

Use carefully — can interrupt process.

---

# 4.6 Docker Remove & Cleanup

---

Remove stopped containers:

```bash
docker container prune
```

Remove unused images:

```bash
docker image prune
```

Remove unused volumes:

```bash
docker volume prune
```

---

# 4.7 Docker Copy & Export

---

## 🔹 `docker cp`

Copy files.

```bash
docker cp file.txt container_id:/app/
```

---

## 🔹 `docker export`

Export container filesystem.

```bash
docker export container_id > container.tar
```

---

## 🔹 `docker import`

Import image from tar.

```bash
docker import container.tar newimage
```

---

# 4.8 Docker Volume Commands

Create volume:

```bash
docker volume create mydata
```

List volumes:

```bash
docker volume ls
```

Inspect volume:

```bash
docker volume inspect mydata
```

Remove volume:

```bash
docker volume rm mydata
```

---

# 4.9 Docker Network Commands

List networks:

```bash
docker network ls
```

Create network:

```bash
docker network create mynet
```

Connect container to network:

```bash
docker network connect mynet container_id
```

Inspect network:

```bash
docker network inspect mynet
```

---

# 4.10 Docker Registry Commands

Login:

```bash
docker login
```

Logout:

```bash
docker logout
```

Search image:

```bash
docker search nginx
```

---

# 4.11 Docker Context Commands

List contexts:

```bash
docker context ls
```

Create context:

```bash
docker context create mycontext
```

Use context:

```bash
docker context use mycontext
```

---

# 4.12 Docker Compose Commands

Start services:

```bash
docker compose up
```

Detached:

```bash
docker compose up -d
```

Stop services:

```bash
docker compose down
```

Rebuild:

```bash
docker compose up --build
```

---

# 4.13 Docker Buildx Commands

Create builder:

```bash
docker buildx create --use
```

Build multi-platform:

```bash
docker buildx build --platform linux/amd64,linux/arm64 .
```

---

# 4.14 Docker Swarm Commands

Initialize swarm:

```bash
docker swarm init
```

Create service:

```bash
docker service create nginx
```

List services:

```bash
docker service ls
```

---
# 5️⃣ Dockerfile 

This section explains Dockerfile in complete depth.

After finishing this chapter, you should clearly understand:

* How Docker builds images internally
* How layers and caching work
* How to write production-grade Dockerfiles
* How to optimize image size
* How to secure builds
* How to avoid common mistakes

---

# 5.1 What is Dockerfile

A Dockerfile is a text file that contains step-by-step instructions to build a Docker image.

It defines:

* Base image
* Application dependencies
* Runtime configuration
* Startup command

Example:

```dockerfile
FROM node:18
WORKDIR /app
COPY package.json .
RUN npm install
COPY . .
CMD ["node", "server.js"]
```

When you run:

```bash
docker build -t myapp .
```

Docker reads this file and creates a layered image.

---

# 5.2 Dockerfile → Image → Container Flow

```text
Dockerfile
 → docker build
   → Image (Immutable)
     → docker run
       → Container (Runtime Instance)
```

Important understanding:

* Dockerfile is the build blueprint
* Image is the build artifact
* Container is the runtime process

Never modify running container directly.
Always update Dockerfile and rebuild.

---

# 5.3 Dockerfile Layers & Cache (Deep Understanding)

![Image](https://depot.dev/images/docker-cache-image3.png)

![Image](https://i.sstatic.net/fotPN.jpg)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2AM22nNEt4gVL8Sv5qlXHVAA.png)

![Image](https://depot.dev/images/docker-cache-across-builds.webp)

Each Dockerfile instruction creates a new image layer.

Example:

```dockerfile
FROM ubuntu:22.04
RUN apt update
RUN apt install nginx
COPY index.html /var/www/html/
```

Layers created:

1. Ubuntu base layer
2. Update layer
3. Nginx install layer
4. File copy layer

---

## Cache Mechanism

Docker builds layers sequentially.

If nothing changes in a step:

* Docker reuses cached layer
* Skips rebuilding

If one instruction changes:

* That layer and all following layers rebuild

---

## Why Order Matters

Bad:

```dockerfile
COPY . .
RUN npm install
```

Any code change invalidates cache.

Better:

```dockerfile
COPY package.json .
RUN npm install
COPY . .
```

Now dependency installation is cached unless package.json changes.

---

# 5.4 Dockerfile Instructions (Complete Explanation)

---

## 🔹 FROM

Defines base image.

```dockerfile
FROM ubuntu:22.04
```

Best Practice:

* Use specific versions
* Avoid `latest` in production

---

## 🔹 LABEL

Adds metadata.

```dockerfile
LABEL maintainer="team@example.com"
```

Used for:

* Version tracking
* Ownership
* Documentation

---

## 🔹 RUN

Executes commands during build.

```dockerfile
RUN apt update && apt install -y nginx
```

Best Practice:

Combine commands to reduce layers:

```dockerfile
RUN apt update && apt install -y nginx && rm -rf /var/lib/apt/lists/*
```

---

## 🔹 COPY vs ADD

COPY (recommended):

```dockerfile
COPY app.py /app/
```

ADD (extra features like extracting tar):

```dockerfile
ADD archive.tar.gz /app/
```

Best Practice:

Prefer COPY unless ADD feature is needed.

---

## 🔹 WORKDIR

Sets working directory.

```dockerfile
WORKDIR /app
```

All following commands run in this directory.

---

## 🔹 ENV vs ARG

ENV (available at runtime):

```dockerfile
ENV NODE_ENV=production
```

ARG (only during build):

```dockerfile
ARG VERSION=1.0
```

Difference:

* ARG disappears after build
* ENV stays inside container

---

## 🔹 EXPOSE

Documents container port.

```dockerfile
EXPOSE 3000
```

Does not publish port automatically.

---

## 🔹 CMD

Default runtime command.

```dockerfile
CMD ["node", "server.js"]
```

Can be overridden during docker run.

---

## 🔹 ENTRYPOINT

Defines fixed startup command.

```dockerfile
ENTRYPOINT ["nginx"]
```

Difference from CMD:

* ENTRYPOINT always runs
* CMD provides default arguments

---

## 🔹 VOLUME

Creates mount point.

```dockerfile
VOLUME /data
```

Used for persistent storage.

---

## 🔹 USER

Specifies user.

```dockerfile
USER node
```

Security best practice:

Avoid running as root.

---

## 🔹 HEALTHCHECK

Defines container health check.

```dockerfile
HEALTHCHECK CMD curl --fail http://localhost:3000 || exit 1
```

Allows orchestration systems to monitor health.

---

## 🔹 ONBUILD

Trigger instruction when used as base image.

```dockerfile
ONBUILD COPY . /app
```

Used for parent images.

---

# 5.5 Production Dockerfile Example (Node.js)

```dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package.json package-lock.json ./

RUN npm ci --only=production

COPY . .

USER node

EXPOSE 3000

CMD ["node", "server.js"]
```

Why this is good:

* Uses lightweight alpine base
* Uses npm ci for reproducibility
* Runs as non-root
* Separates dependency layer

---

# 5.6 Multi-Stage Builds

![Image](https://labs.iximiuz.com/content/files/tutorials/docker-multi-stage-builds/__static__/multi-stage-build.png)

![Image](https://depot.dev/images/docker-multi-stage-builds-image3.webp)

![Image](https://cdn.prod.website-files.com/68232df8de1a79da2c32a09e/68473e96bab1a481e47a648c_66fdaf3d58acc627f76db63a_66fdaf35614e560cc54df420_Docker%252520Multi-Stage%252520Builds%252520-%252520Image%252520Size%252520Diagram.png)

Multi-stage builds reduce image size.

Example:

```dockerfile
FROM node:18 AS builder
WORKDIR /app
COPY . .
RUN npm install && npm run build

FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
```

Benefits:

* Smaller final image
* No build tools in production
* Better security

---

# 5.7 Dockerfile Anti-Patterns

❌ Using `latest` tag
❌ Running as root
❌ Installing unnecessary packages
❌ Large base images
❌ Copying entire context unnecessarily
❌ Ignoring .dockerignore

---

# 5.8 Secure Dockerfile Practices

* Use minimal base image
* Run as non-root user
* Remove package caches
* Use multi-stage builds
* Scan images for vulnerabilities
* Avoid secrets in Dockerfile

Never hardcode:

```dockerfile
ENV PASSWORD=secret
```

Use runtime environment variables instead.

---

# 5.9 Dockerfile Performance Optimization

* Order instructions for cache efficiency
* Reduce number of layers
* Use alpine or slim images
* Remove unnecessary files
* Use multi-stage builds

---

# 5.10 .dockerignore Best Practices

.dockerignore prevents unnecessary files from being sent to build context.

Example:

```
node_modules
.git
Dockerfile
*.log
```

Benefits:

* Faster build
* Smaller context size
* Better security

---
# 6️⃣ Docker BuildKit

BuildKit is the modern image builder used by Docker.
It replaces the legacy builder with:

* Faster builds
* Parallel execution
* Advanced caching
* Secure secret handling
* Multi-platform builds
* CI/CD optimization

After this section, you should clearly understand:

* Why BuildKit exists
* How it works internally
* How to use advanced build features
* How to optimize builds for production

---

# 6.1 What is BuildKit

BuildKit is the next-generation build engine integrated into Docker.

It improves:

* Performance
* Security
* Cache control
* Flexibility

BuildKit uses a dependency-based execution model rather than strict sequential execution.

This means independent build steps can run in parallel.

---

## Why BuildKit Matters

Traditional builder:

* Executes instructions line by line
* Limited cache control
* No secret-safe builds
* Slower performance

BuildKit:

* Detects independent stages
* Runs steps in parallel
* Supports advanced mount types
* Supports remote cache

---

# 6.2 Why BuildKit Replaced Legacy Builder

Problems with legacy builder:

* Inefficient cache invalidation
* Sequential build execution
* Secrets stored in image layers
* Limited multi-platform support

BuildKit solves these.

It provides:

* Directed acyclic graph (DAG) execution
* Secure mounts
* Inline caching
* Exportable cache

---

# 6.3 Enable BuildKit

Temporary enable:

```bash
DOCKER_BUILDKIT=1 docker build .
```

Permanent enable (Linux):

```bash
export DOCKER_BUILDKIT=1
```

Docker 23+ enables BuildKit by default.

Check builder:

```bash
docker buildx ls
```

---

# 6.4 BuildKit Architecture

![Image](https://depot.dev/images/buildkit-in-depth-image3.webp)

![Image](https://container-registry.com/posts/productivity-lift-buildkit-cli-for-kubectl/workflow-with-buildkit-cli-for-kubectl.svg)

![Image](https://www.docker.com/app/uploads/2022/04/image10-906x1024.png)

![Image](https://www.docker.com/app/uploads/2022/04/image11-1110x858.png)

BuildKit uses:

* Frontend (Dockerfile parser)
* LLB (Low-Level Build) definition
* Solver (execution engine)
* Cache exporter/importer

Execution Flow:

```text
Dockerfile
 → Converted to LLB
   → Build graph generated
     → Parallel execution
       → Final image output
```

---

# 6.5 Parallel Build Execution

If multiple stages do not depend on each other, BuildKit runs them simultaneously.

Example:

```dockerfile
FROM node:18 AS frontend
RUN npm install

FROM python:3.11 AS backend
RUN pip install flask
```

These stages can build in parallel.

This reduces build time significantly.

---

# 6.6 Secret Mounting (`--mount=type=secret`)

Old approach (unsafe):

```dockerfile
ENV PASSWORD=mysecret
```

Secret gets stored in image layer.

BuildKit approach:

```dockerfile
RUN --mount=type=secret,id=mysecret \
    cat /run/secrets/mysecret
```

Build command:

```bash
docker build --secret id=mysecret,src=secret.txt .
```

Secret:

* Not stored in final image
* Not visible in layer history
* Available only during build

This is production-safe.

---

# 6.7 SSH Mount (`--mount=type=ssh`)

Used when accessing private Git repositories during build.

Example:

```dockerfile
RUN --mount=type=ssh git clone git@github.com:private/repo.git
```

Build command:

```bash
docker build --ssh default .
```

SSH key:

* Not stored in image
* Used temporarily during build

---

# 6.8 Cache Mount (`--mount=type=cache`)

Used to cache dependencies between builds.

Example for Node:

```dockerfile
RUN --mount=type=cache,target=/root/.npm \
    npm install
```

Example for Python:

```dockerfile
RUN --mount=type=cache,target=/root/.cache/pip \
    pip install -r requirements.txt
```

Benefits:

* Faster rebuilds
* Reduced network usage
* Persistent build cache

---

# 6.9 Inline Cache

Inline cache allows image to carry cache metadata.

Build:

```bash
docker build --build-arg BUILDKIT_INLINE_CACHE=1 -t myapp .
```

Push image.

Later builds can reuse cache from registry.

Used heavily in CI/CD pipelines.

---

# 6.10 Remote Cache Export / Import

Export cache:

```bash
docker buildx build \
  --cache-to=type=registry,ref=myapp:buildcache \
  --cache-from=type=registry,ref=myapp:buildcache .
```

This enables:

* CI systems to share cache
* Faster builds across environments

Very useful in large teams.

---

# 6.11 Multi-Platform Builds (buildx)

Build for multiple architectures:

```bash
docker buildx build \
  --platform linux/amd64,linux/arm64 \
  -t myapp:latest \
  --push .
```

Supported architectures:

* AMD64
* ARM64
* ARMv7

Essential for:

* Apple Silicon
* Cloud ARM servers
* Edge devices

---

# 6.12 Advanced Build Optimizations

1. Use multi-stage builds
2. Order instructions for caching
3. Use slim/alpine base images
4. Use cache mounts
5. Remove build dependencies in final stage
6. Use parallel build stages

---

# 6.13 BuildKit in CI/CD

BuildKit is heavily used in:

* GitHub Actions
* GitLab CI
* Jenkins
* Kubernetes build pipelines

Benefits in CI:

* Faster builds
* Cache reuse
* Secure secret handling
* Multi-architecture support

---

# 6.14 BuildKit Security Benefits

BuildKit improves security by:

* Preventing secrets from leaking
* Avoiding layer exposure
* Enabling reproducible builds
* Supporting minimal images

It aligns with OCI standards defined by:

Open Container Initiative

---

# 7️⃣ Docker Image Management 

Docker images are the **core artifact** in container-based systems.
Everything in production — deployments, rollbacks, scaling, CI/CD — depends on how well images are built, tagged, stored, secured, and promoted.

This section covers image management from beginner to enterprise-level practices.

---

# 7.1 What is Image Management

Image management refers to the complete lifecycle control of Docker images:

* Building
* Tagging
* Storing
* Securing
* Optimizing
* Promoting
* Cleaning

In production environments, image management directly affects:

* Deployment stability
* Security posture
* Storage efficiency
* CI/CD speed
* Rollback capability

---

### Why Image Management Is Critical

Poor image management leads to:

* Bloated images
* Security vulnerabilities
* Broken deployments
* Storage waste
* Inconsistent environments

Good image management ensures:

* Reproducibility
* Version traceability
* Secure builds
* Clean registry structure

---

# 7.2 Docker Image Lifecycle

![Image](https://media2.dev.to/dynamic/image/width%3D800%2Cheight%3D%2Cfit%3Dscale-down%2Cgravity%3Dauto%2Cformat%3Dauto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F7298dbklbkky66pmpu4d.png)

![Image](https://media2.dev.to/dynamic/image/width%3D1000%2Cheight%3D500%2Cfit%3Dcover%2Cgravity%3Dauto%2Cformat%3Dauto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fdyzwicbhbr3mq76prwwm.png)

![Image](https://learn.microsoft.com/en-us/dotnet/architecture/microservices/container-docker-introduction/media/docker-containers-images-registries/taxonomy-of-docker-terms-and-concepts.png)

![Image](https://user-images.githubusercontent.com/1712635/38696268-8c40bc06-3e43-11e8-8e79-e904ba5ed26b.png)

The Docker image lifecycle typically follows:

```text
Code
 → Dockerfile
   → Build Image
     → Tag Image
       → Push to Registry
         → Pull in Environment
           → Run Container
             → Promote or Deprecate
               → Cleanup
```

---

### Detailed Lifecycle Stages

### 1️⃣ Build

```bash
docker build -t myapp:1.0 .
```

Creates immutable image.

---

### 2️⃣ Tag

```bash
docker tag myapp:1.0 myregistry/myapp:1.0
```

Adds repository reference.

---

### 3️⃣ Push

```bash
docker push myregistry/myapp:1.0
```

Uploads layers to registry.

---

### 4️⃣ Pull

```bash
docker pull myregistry/myapp:1.0
```

Downloads layers in target environment.

---

### 5️⃣ Deploy

```bash
docker run myregistry/myapp:1.0
```

Container runs using image.

---

### 6️⃣ Promote or Remove

Image either:

* Moves to higher environment
* Gets deprecated
* Gets deleted

---

# 7.3 Image Layers & Immutability

## Image Layers

Each Dockerfile instruction creates a layer.

Layers are:

* Read-only
* Cached
* Reusable
* Content-addressable

Docker stores layers using SHA256 digests.

Example layer ID:

```
sha256:abc123...
```

---

## Immutability Principle

Once built, image cannot change.

If change is required:

* Update Dockerfile
* Rebuild image
* Deploy new version

Never modify container directly.

---

### Why Immutability Matters

* Enables consistent deployments
* Makes rollback simple
* Prevents configuration drift
* Supports GitOps workflows

---

# 7.4 Image Naming & Tagging Strategy

Image naming format:

```
registry/repository:tag
```

Example:

```
myregistry.com/backend:v1.2.3
```

---

## Tagging Best Practices

### ❌ Avoid:

```
myapp:latest
```

Because:

* Not predictable
* Breaks rollback
* Hard to trace

---

### ✅ Recommended Strategies

### Semantic Versioning

```
v1.0.0
v1.0.1
v2.1.3
```

---

### Git Commit Based

```
myapp:commit-8f4d3a
```

---

### Environment Tags

```
myapp:dev
myapp:qa
myapp:prod
```

Better practice:

Use immutable version tags + environment mapping.

---

# 7.5 Single-Stage vs Multi-Stage Builds

## Single-Stage Build

All build tools remain in final image.

Example:

```dockerfile
FROM node:18
RUN npm install
COPY . .
CMD ["node", "server.js"]
```

Problem:

* Larger image
* Includes build dependencies

---

## Multi-Stage Build

![Image](https://depot.dev/images/docker-multi-stage-builds-image3.webp)

![Image](https://labs.iximiuz.com/content/files/tutorials/docker-multi-stage-builds/__static__/multi-stage-build.png)

![Image](https://depot.dev/images/docker-multi-stage-builds-image4.webp)

![Image](https://media2.dev.to/dynamic/image/width%3D800%2Cheight%3D%2Cfit%3Dscale-down%2Cgravity%3Dauto%2Cformat%3Dauto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fd97mifvnbylgfverzea2.png)

Example:

```dockerfile
FROM node:18 AS builder
WORKDIR /app
COPY . .
RUN npm install && npm run build

FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
```

Benefits:

* Smaller image
* No build tools in final image
* Better security
* Faster deployment

---

# 7.6 Image Size Optimization

Large images cause:

* Slow pulls
* Higher storage costs
* Slower deployments

---

## Optimization Techniques

### 1️⃣ Use Minimal Base Image

Instead of:

```
ubuntu
```

Use:

```
alpine
debian:slim
distroless
```

---

### 2️⃣ Combine RUN Commands

Instead of:

```dockerfile
RUN apt update
RUN apt install nginx
```

Use:

```dockerfile
RUN apt update && apt install -y nginx && rm -rf /var/lib/apt/lists/*
```

---

### 3️⃣ Use Multi-Stage Builds

Remove build dependencies from final image.

---

### 4️⃣ Remove Unnecessary Files

Use `.dockerignore`:

```
.git
node_modules
*.log
```

---

### 5️⃣ Analyze Image Size

```bash
docker history myapp
```

---

# 7.7 Image Caching & CI/CD

Build caching speeds up pipelines.

BuildKit supports:

* Inline cache
* Remote cache export/import

Example:

```bash
docker build --build-arg BUILDKIT_INLINE_CACHE=1 -t myapp .
```

CI best practice:

* Use shared registry cache
* Cache dependency layers
* Separate dependency copy step

---

### CI Pipeline Flow

```text
Code Commit
 → Build Image
   → Use Cache
     → Run Tests
       → Push Versioned Image
```

Faster builds = faster delivery.

---

# 7.8 Image Security Basics

Security starts at image build.

---

## 1️⃣ Use Trusted Base Images

Prefer:

* Official images from Docker Hub

Avoid random community images in production.

---

## 2️⃣ Scan Images

Use tools:

* Docker Scout
* Trivy
* Clair

Check:

* CVEs
* Outdated packages
* Vulnerable dependencies

---

## 3️⃣ Avoid Secrets in Image

Never hardcode:

```dockerfile
ENV PASSWORD=secret
```

Use runtime environment variables.

---

## 4️⃣ Use Non-Root User

```dockerfile
USER node
```

Reduces risk of container breakout.

---

# 7.9 Image Cleanup & Disk Management

Over time, images accumulate.

Check disk usage:

```bash
docker system df
```

Remove unused images:

```bash
docker image prune
docker image prune -a
```

Remove dangling images:

```bash
docker images -f dangling=true
```

---

## Production Cleanup Strategy

* Keep only last N versions
* Automate cleanup using cron
* Apply registry retention policies

---

# 7.10 Image Promotion Strategy (Dev → QA → Prod)

Never rebuild image per environment.

Instead:

1️⃣ Build once
2️⃣ Test in Dev
3️⃣ Promote same image to QA
4️⃣ Promote same image to Prod

Promotion methods:

* Retag image
* Use registry repository promotion
* Use immutable version tags

Example:

```bash
docker tag myapp:1.0 myapp:prod
docker push myapp:prod
```

---

## Why This Matters

Ensures:

* Same binary across environments
* No hidden differences
* Easier debugging

---

# 7.11 Multi-Architecture Images (ARM64 / AMD64)

Modern systems use:

* AMD64 (x86 servers)
* ARM64 (Apple Silicon, AWS Graviton)

Build multi-arch image:

```bash
docker buildx build \
  --platform linux/amd64,linux/arm64 \
  -t myapp:latest \
  --push .
```

Docker creates manifest list.

When pulling:

Docker automatically selects correct architecture.

---

## Why Multi-Arch Matters

* Cloud ARM adoption
* Edge computing
* Cost optimization
* Cross-platform development

---
# 8️⃣ Docker Container Management (Full Deep Documentation – 2026)

Containers are the **runtime layer** of Docker.
Images are build artifacts — containers are live processes.

This section explains container lifecycle, runtime behavior, performance control, logging, scaling, and production best practices.

After this chapter, you should clearly understand:

* What happens when a container starts
* How to manage container lifecycle properly
* Resource control (CPU, memory, OOM)
* Restart policies
* Logging strategy
* Health checks
* Rootless containers
* Production cleanup and scaling

---

# 8.1 What is Container Management

Container management means controlling:

* Creation
* Execution
* Resource allocation
* Monitoring
* Restart behavior
* Removal
* Scaling

In production, container management directly impacts:

* Application uptime
* System stability
* Resource efficiency
* Fault tolerance

---

# 8.2 Container vs Image (Runtime Perspective)

| Image              | Container            |
| ------------------ | -------------------- |
| Read-only          | Writable layer added |
| Template           | Running instance     |
| Immutable          | Ephemeral            |
| Stored in registry | Runs on host         |

Image is passive.
Container is active.

When you run:

```bash id="w89p4a"
docker run nginx
```

Docker:

1. Creates container metadata
2. Adds writable layer
3. Configures networking
4. Applies resource limits
5. Starts process

---

# 8.3 Container Lifecycle

Container states:

* Created
* Running
* Paused
* Restarting
* Exited
* Dead

Lifecycle flow:

```bash id="2bhlcb"
docker create
docker start
docker stop
docker rm
```

---

## Lifecycle Commands

Create container without starting:

```bash id="5ov5i6"
docker create nginx
```

Start container:

```bash id="33v3j2"
docker start container_id
```

Stop container:

```bash id="c8t0tt"
docker stop container_id
```

Remove container:

```bash id="s0j3pq"
docker rm container_id
```

Force remove:

```bash id="nhg8zi"
docker rm -f container_id
```

---

# 8.4 `docker run` Internals

![Image](https://learn.microsoft.com/en-us/dotnet/architecture/microservices/docker-application-development-process/media/docker-app-development-workflow/life-cycle-containerized-apps-docker-cli.png)

![Image](https://miro.medium.com/1%2AuuZ-h5EH76LOtJ614z-qDA.png)

![Image](https://miro.medium.com/1%2Avca4e-SjpzSL5H401p4LCg.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2Ap2T79jQpvRm1b06dv4tbzA.jpeg)

`docker run` performs multiple actions:

```text id="hch2m0"
Check image
 → Pull if missing
   → Create container
     → Add writable layer
       → Setup network
         → Apply cgroups
           → Start process
```

It is equivalent to:

```bash id="imq3zc"
docker create
docker start
```

---

# 8.5 PID 1 Problem

Inside a container:

* The main process becomes PID 1
* PID 1 behaves differently in Linux

Issues:

* Does not handle signals properly
* Does not reap zombie processes

Example problem:

App does not shut down gracefully when container stops.

---

## Solution

Use:

* Proper init system (like `tini`)
* Or write signal-handling logic in application

Example:

```dockerfile id="qeg3f5"
ENTRYPOINT ["tini", "--"]
```

---

# 8.6 Foreground vs Background Containers

Foreground:

```bash id="66cy68"
docker run nginx
```

Blocks terminal.

Detached mode:

```bash id="b3uc91"
docker run -d nginx
```

Runs in background.

---

# 8.7 Restart Policies

Restart policies improve fault tolerance.

Options:

```bash id="g1lru6"
docker run --restart=always nginx
```

Available policies:

* no
* on-failure
* always
* unless-stopped

Production recommendation:

Use `unless-stopped` for long-running services.

---

# 8.8 Resource Management (CPU, Memory)

Containers share host resources.

Without limits, one container can consume all memory.

---

## Limit Memory

```bash id="l3ggs0"
docker run --memory=512m nginx
```

Limit swap:

```bash id="r9vjjk"
docker run --memory=512m --memory-swap=512m nginx
```

---

## Limit CPU

```bash id="0ns78r"
docker run --cpus=1 nginx
```

Or:

```bash id="iyhtwj"
docker run --cpu-shares=512 nginx
```

---

## OOM Behavior

If memory limit exceeded:

* Container is killed
* OOM event recorded

Check OOM:

```bash id="azk01j"
docker inspect container_id
```

---

# 8.9 Logs Management

Containers log to STDOUT/STDERR.

View logs:

```bash id="sxz36l"
docker logs container_id
docker logs -f container_id
```

---

## Logging Drivers

Docker supports:

* json-file (default)
* syslog
* journald
* fluentd
* gelf

Check logging driver:

```bash id="wrif45"
docker info
```

---

## Log Rotation

Prevent disk overflow:

```bash id="j6zx3k"
--log-opt max-size=10m
--log-opt max-file=3
```

Example:

```bash id="5w3qhv"
docker run --log-opt max-size=10m nginx
```

---

# 8.10 Exec vs Attach

Exec:

```bash id="hm8v09"
docker exec -it container_id bash
```

Creates new process inside container.

Attach:

```bash id="q7u9kl"
docker attach container_id
```

Connects to main process.

Use `exec` for debugging.

---

# 8.11 Container Networking Basics

Each container:

* Gets IP address
* Gets network namespace
* Can connect to other containers

List networks:

```bash id="xv9s61"
docker network ls
```

---

# 8.12 Container Storage & Volumes

Writable layer is temporary.

Use volumes for persistent data:

```bash id="zve1gr"
docker run -v mydata:/data nginx
```

Without volume:

* Data deleted when container removed

---

# 8.13 Health Checks & Monitoring

Define health check in Dockerfile:

```dockerfile id="3hnhc2"
HEALTHCHECK CMD curl --fail http://localhost:3000 || exit 1
```

Check status:

```bash id="x7d8ye"
docker ps
```

Shows:

* healthy
* unhealthy

Used by orchestration tools like
Kubernetes

---

# 8.14 Scaling Containers

Manual scaling:

```bash id="48y3cd"
docker run -d nginx
docker run -d nginx
```

Better approach:

Use orchestration:

* Docker Compose
* Docker Swarm
* Kubernetes

---

# 8.15 Cleanup Strategy

List stopped containers:

```bash id="rmc6az"
docker ps -a
```

Remove unused:

```bash id="rts24q"
docker container prune
```

Remove unused volumes:

```bash id="xpkf4i"
docker volume prune
```

Production recommendation:

* Automate cleanup
* Monitor disk usage
* Use retention policy

---

# 8.16 Rootless Containers

Rootless mode runs Docker without root privileges.

Benefits:

* Improved security
* Reduced attack surface

Check rootless:

```bash id="nwhv2t"
docker info
```

Look for:

```text id="0ov5zi"
rootless: true
```

Rootless reduces risk of host compromise.

---
# 9️⃣ Docker Volumes & Storage 

Storage is one of the most misunderstood areas in Docker.

Containers are **ephemeral by design**, but real applications require **persistent data**.

This section explains:

* How Docker storage works internally
* Writable layer behavior
* Volume types
* Bind mounts
* Storage drivers
* Overlay2 internals
* Performance considerations
* Backup & cleanup strategies

After this section, you should clearly understand how Docker handles data at filesystem level.

---

# 9.1 Why Docker Storage Exists

By default:

* Containers are temporary
* Writable layer is deleted when container is removed

Example:

```bash
docker run -it ubuntu bash
```

Create file:

```bash
touch test.txt
```

Exit and remove container:

```bash
docker rm container_id
```

File is gone.

That is expected behavior.

Containers are designed to be:

* Disposable
* Replaceable
* Stateless

But applications like:

* Databases
* File uploads
* Logs
* Application state

Need persistent storage.

That is why Docker storage mechanisms exist.

---

# 9.2 Docker Storage Types

Docker provides three main storage types:

1️⃣ Writable layer
2️⃣ Volumes
3️⃣ Bind mounts

---

# 9.3 Container Writable Layer

![Image](https://docs.docker.com/engine/storage/drivers/images/container-layers.webp)

![Image](https://i.sstatic.net/6EKSp.jpg)

![Image](https://static.packt-cdn.com/products/9781788992329/graphics/assets/5c8fd414-799b-43e3-9623-0dcbdabfe7ff.png)

![Image](https://cdn.hashnode.com/res/hashnode/image/upload/v1641655045270/xbtF0ib56.jpeg)

When a container starts:

* Image layers remain read-only
* Docker adds a writable layer on top

All changes go to this layer.

This uses **Copy-on-Write (CoW)**.

---

## How Copy-on-Write Works

If container modifies a file:

* Docker copies file from lower layer
* Modification happens in writable layer

Base image remains unchanged.

---

## Limitations of Writable Layer

* Slower performance than volumes
* Deleted when container removed
* Not suitable for databases

Writable layer should not store persistent production data.

---

# 9.4 Docker Volumes

Volumes are Docker-managed persistent storage.

Create volume:

```bash
docker volume create mydata
```

Use volume:

```bash
docker run -v mydata:/var/lib/mysql mysql
```

Now:

* Data stored outside container
* Survives container deletion

---

## Where Volumes Are Stored

On Linux:

```text
/var/lib/docker/volumes/
```

Docker manages this directory.

---

## Why Volumes Are Better

* Higher performance
* Not tied to container lifecycle
* Managed by Docker
* Easy backup

---

# 9.5 Volume Lifecycle

Volume lifecycle is independent.

Check volumes:

```bash
docker volume ls
```

Inspect volume:

```bash
docker volume inspect mydata
```

Remove volume:

```bash
docker volume rm mydata
```

Remove unused volumes:

```bash
docker volume prune
```

---

# 9.6 Volume Commands

Create:

```bash
docker volume create myvolume
```

Use:

```bash
docker run -v myvolume:/data nginx
```

Remove:

```bash
docker volume rm myvolume
```

Inspect:

```bash
docker volume inspect myvolume
```

---

# 9.7 Bind Mounts

Bind mounts connect a host directory to container.

Example:

```bash
docker run -v /home/user/app:/app nginx
```

This maps:

Host → Container

---

## When to Use Bind Mounts

* Development environment
* Live code changes
* Debugging
* Local file sharing

---

## Risk of Bind Mounts

* Container can modify host files
* Security concerns
* Less portable

Volumes are safer for production.

---

# 9.8 Volume vs Bind Mount

| Feature            | Volume      | Bind Mount |
| ------------------ | ----------- | ---------- |
| Managed by Docker  | Yes         | No         |
| Performance        | High        | High       |
| Host Path Required | No          | Yes        |
| Production Use     | Recommended | Limited    |
| Portability        | High        | Low        |

---

# 9.9 Anonymous Volumes

Created automatically if:

```dockerfile
VOLUME /data
```

Or:

```bash
docker run -v /data nginx
```

Docker generates random volume name.

Anonymous volumes:

* Harder to manage
* May accumulate unused volumes

Better to use named volumes.

---

# 9.10 Volumes in Dockerfile

```dockerfile
VOLUME /data
```

This:

* Marks directory as mount point
* Signals container expects persistent storage

But volume still created at runtime.

---

# 9.11 Database + Volume Example

Run MySQL:

```bash
docker run -d \
  -v mysqldata:/var/lib/mysql \
  -e MYSQL_ROOT_PASSWORD=secret \
  mysql
```

Now:

* Data persists
* Container restart does not lose data

If container deleted:

* Volume remains
* Data safe

---

# 9.12 Volume Backup & Restore

Backup:

```bash
docker run --rm \
  -v mysqldata:/data \
  -v $(pwd):/backup \
  ubuntu tar czf /backup/backup.tar.gz /data
```

Restore:

```bash
docker run --rm \
  -v mysqldata:/data \
  -v $(pwd):/backup \
  ubuntu tar xzf /backup/backup.tar.gz -C /
```

Important in production:

* Regular volume backups
* Disaster recovery planning

---

# 9.13 Volume Cleanup

Over time volumes accumulate.

Check disk usage:

```bash
docker system df
```

Remove unused:

```bash
docker volume prune
```

Production best practice:

* Automate cleanup
* Monitor disk usage
* Apply retention policy

---

# 9.14 Storage Drivers

Docker uses storage drivers to manage layered filesystem.

Common drivers:

* overlay2 (default Linux)
* aufs (legacy)
* devicemapper (legacy)
* btrfs
* zfs

Check storage driver:

```bash
docker info
```

Look for:

```text
Storage Driver: overlay2
```

---

# 9.15 Overlay2 Deep Explanation

![Image](https://www.pedroalonso.net/blog/docker-introduction/docker-architecture.svg)

![Image](https://www.grant.pizza/overlay/stacked.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2AXSt_nEKizz9xW-58mRXZkA.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1276/1%2AiS3p2S0KR9SbIiADgxooPA.jpeg)

Overlay2 is the default storage driver for modern Linux.

It uses Linux OverlayFS.

---

## How overlay2 Works

It merges:

* Lower directories (image layers)
* Upper directory (writable layer)
* Work directory

Into unified filesystem.

---

### Structure Example

```text
lowerdir = image layers
upperdir = container writable layer
merged   = container filesystem
```

---

## Why overlay2 Is Preferred

* Stable
* High performance
* Efficient copy-on-write
* Native Linux support

---

# 9.16 Storage Driver Performance Comparison

| Driver       | Performance | Status       |
| ------------ | ----------- | ------------ |
| overlay2     | High        | Recommended  |
| aufs         | Medium      | Deprecated   |
| devicemapper | Low         | Legacy       |
| btrfs        | Medium      | Advanced use |
| zfs          | High        | Advanced use |

---

## Performance Best Practices

* Use overlay2
* Store databases in volumes
* Avoid heavy writes in writable layer
* Monitor disk usage
* Use SSD storage in production

---
# 🔟 Docker Networking 

Networking allows containers to:

* Communicate with each other
* Communicate with the host
* Communicate with external systems
* Be exposed to users

Docker networking is built on Linux networking primitives:

* Network namespaces
* Virtual Ethernet (veth) pairs
* Linux bridges
* iptables (NAT rules)

After this section, you should clearly understand:

* Docker networking architecture
* How bridge networking works internally
* Host mode vs bridge mode
* Overlay networking
* Macvlan
* Port publishing internals
* Docker DNS
* Network isolation
* Performance tuning

---

# 10.1 What is Docker Networking

Docker networking provides isolation and connectivity for containers.

Each container:

* Gets its own network namespace
* Gets its own IP address
* Has its own routing table
* Has its own network interfaces

Containers do NOT share host network stack (unless using host mode).

---

# 10.2 Docker Networking Architecture

![Image](https://blogs.cisco.com/gcs/ciscoblogs/1/2022/08/docker-bridge-1-768x478.jpeg)

![Image](https://miro.medium.com/0%2A79XBxOj0cC0EBsh9.jpg)

![Image](https://miro.medium.com/1%2AsA4-8pVmrdeKCa9HZxbAJQ.png)

![Image](https://www.docker.com/app/uploads/2022/12/networking-drivers-use-cases-3.png)

Default Docker network flow:

```text
Container
 → veth pair
   → Linux bridge (docker0)
     → Host network interface
       → External network
```

---

## Key Components

### 1️⃣ Network Namespace

Each container has its own isolated network stack.

### 2️⃣ veth Pair

Virtual Ethernet cable connecting container to host.

### 3️⃣ Linux Bridge (docker0)

Acts like a virtual switch.

### 4️⃣ iptables

Handles NAT and port forwarding.

---

# 10.3 Network Drivers

Docker supports multiple network drivers:

* Bridge
* Host
* None
* Overlay
* Macvlan

---

## 🔹 Bridge (Default)

Used when you run:

```bash
docker run nginx
```

Docker connects container to default bridge network.

Check networks:

```bash
docker network ls
```

Inspect bridge:

```bash
docker network inspect bridge
```

---

### How Bridge Works

1. Container gets IP (e.g., 172.17.0.x)
2. Connected via veth pair
3. Bridge routes traffic
4. iptables handles NAT

---

## 🔹 Host Mode

Run container in host network:

```bash
docker run --network host nginx
```

Characteristics:

* No network isolation
* Container shares host IP
* Faster networking
* Less secure

Used for:

* High-performance workloads
* Monitoring agents

---

## 🔹 None Driver

Disable networking:

```bash
docker run --network none nginx
```

Container has:

* No network interface
* No external communication

Used for:

* Security-sensitive tasks
* Offline processing

---

## 🔹 Overlay Network

![Image](https://miro.medium.com/0%2A-Si1piI584OyYZuA)

![Image](https://blog.octo.com/how-does-it-work-docker-part-2-swarm-networking/bridge-overlay.webp)

![Image](https://assets.community.aws/a/2nsPnQjIN4BiCiLhglxGjuvKLlr/1_jR.webp?imgSize=1200x724)

![Image](https://eu-images.contentstack.com/v3/assets/bltde8121fc52c5c8f3/blt9e491bcdfb8c7cdd/6835618c989ea43e0c537e67/Diagram-2.jpg)

Overlay network connects containers across multiple hosts.

Used with:

* Docker Swarm
* Kubernetes

Creates virtual network spanning hosts.

Encapsulates traffic using VXLAN.

---

## 🔹 Macvlan

Macvlan assigns real MAC address to container.

Container appears as physical device on network.

Example:

```bash
docker network create -d macvlan ...
```

Used when:

* Containers must appear as real devices
* Legacy systems require direct IP

---

# 10.4 Port Mapping

Expose container port to host.

Example:

```bash
docker run -p 8080:80 nginx
```

Meaning:

Host port 8080 → Container port 80

---

## Internally

Docker adds iptables rule:

```text
Host:8080 → ContainerIP:80
```

This uses NAT.

---

## Publishing Multiple Ports

```bash
docker run -p 8080:80 -p 8443:443 nginx
```

---

# 10.5 EXPOSE vs Publish

Dockerfile:

```dockerfile
EXPOSE 3000
```

This:

* Documents port
* Does NOT open port

Actual publishing happens at runtime:

```bash
docker run -p 3000:3000 myapp
```

---

# 10.6 Container-to-Container Communication

Containers in same network:

* Can communicate using container name
* Docker provides internal DNS

Example:

```bash
docker network create mynet
docker run -d --name app --network mynet myapp
docker run -d --name db --network mynet mysql
```

Inside app container:

```bash
ping db
```

Works because Docker DNS resolves container name.

---

# 10.7 Multiple Networks per Container

A container can connect to multiple networks.

Example:

```bash
docker network connect mynet container_id
```

Useful for:

* Backend network
* Frontend network
* Monitoring network

---

# 10.8 Docker DNS

Docker runs embedded DNS server.

Features:

* Resolves container names
* Resolves service names
* Handles dynamic container IP changes

No need to manage `/etc/hosts`.

---

# 10.9 Network Security Basics

Isolation is provided by:

* Network namespaces
* Separate bridges
* iptables filtering

Security best practices:

* Use custom bridge networks
* Avoid default bridge in production
* Avoid host network unless required
* Restrict exposed ports
* Use firewalls

---

# 10.10 Network Performance Considerations

Bridge network:

* Slight overhead due to NAT

Host network:

* Faster
* No NAT overhead

Overlay network:

* Extra VXLAN encapsulation
* Slight performance overhead

Macvlan:

* Near-native performance
* Complex configuration

---

## Performance Best Practices

* Use host mode for high-performance workloads
* Avoid unnecessary port publishing
* Use dedicated networks for isolation
* Monitor network usage with:

```bash
docker stats
```

---
# 1️⃣1️⃣ Docker Compose

Docker Compose is used to define and run **multi-container applications** using a single configuration file.

Instead of running multiple `docker run` commands manually, Compose allows you to define everything in a YAML file and manage the entire application stack as one unit.

After this section, you should clearly understand:

* What Docker Compose is
* Why it is required
* Compose architecture
* docker-compose.yml structure
* Services, networks, and volumes
* Scaling services
* Environment management
* Production considerations

---

# 11.1 What is Docker Compose

Docker Compose is a tool that allows you to define a multi-container application using a YAML file and manage it with a single command.

Instead of:

```bash
docker run -d --name db mysql
docker run -d --name app --link db myapp
```

You define:

```yaml
services:
  db:
    image: mysql
  app:
    image: myapp
```

And start everything with:

```bash
docker compose up
```

Compose simplifies application orchestration on a single host.

---

# 11.2 Why Docker Compose is Needed

In real applications, you rarely run just one container.

Typical stack:

* Backend service
* Database
* Cache
* Message queue
* Reverse proxy

Managing all of these manually is complex.

Compose provides:

* Centralized configuration
* Service dependency management
* Shared networking
* Persistent volume definitions
* Easier scaling

---

# 11.3 Docker Compose Architecture

![Image](https://docs.docker.com/compose/images/compose-application.webp)

![Image](https://media2.dev.to/dynamic/image/width%3D1000%2Cheight%3D420%2Cfit%3Dcover%2Cgravity%3Dauto%2Cformat%3Dauto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F3jdqbz263qx7iufkm63b.png)

![Image](https://accesto.com/blog/static/da655bd4bde7fe34eee74d8e5c6bf1b1/3e2b5/docker-networks-split.jpg)

![Image](https://raw.githubusercontent.com/docker/libnetwork/master/docs/cnm-model.jpg)

Compose architecture:

```text
docker-compose.yml
   ↓
Docker CLI (compose)
   ↓
Docker Engine
   ↓
Multiple Containers
```

Key characteristics:

* All services share a default network
* Each service gets DNS-based name resolution
* Volumes are automatically created if defined

---

# 11.4 docker-compose.yml Structure

Basic structure:

```yaml
version: "3.9"

services:
  service_name:
    image: image_name
    ports:
      - "8080:80"
    environment:
      - ENV=production
    volumes:
      - myvolume:/data
    depends_on:
      - db

volumes:
  myvolume:

networks:
  mynetwork:
```

---

## Main Sections

* `services` → Defines containers
* `volumes` → Defines persistent storage
* `networks` → Defines custom networks

---

# 11.5 Services, Networks & Volumes

## Services

Each service represents a container.

Example:

```yaml
services:
  web:
    image: nginx
  db:
    image: mysql
```

Compose automatically creates:

* Default network
* DNS entries

Web can access database using hostname:

```
db
```

---

## Volumes

Define persistent storage:

```yaml
volumes:
  dbdata:
```

Attach to service:

```yaml
services:
  db:
    image: mysql
    volumes:
      - dbdata:/var/lib/mysql
```

Volume survives container deletion.

---

## Networks

Define custom network:

```yaml
networks:
  backend:
```

Attach service:

```yaml
services:
  app:
    networks:
      - backend
```

Useful for isolation between frontend and backend.

---

# 11.6 Compose Examples (Full Application)

Example: Node app + MySQL

```yaml
version: "3.9"

services:
  app:
    build: .
    ports:
      - "3000:3000"
    depends_on:
      - db

  db:
    image: mysql:8
    environment:
      MYSQL_ROOT_PASSWORD: secret
    volumes:
      - dbdata:/var/lib/mysql

volumes:
  dbdata:
```

Run:

```bash
docker compose up -d
```

Stop:

```bash
docker compose down
```

---

# 11.7 depends_on & Healthchecks

`depends_on` controls startup order.

Example:

```yaml
depends_on:
  - db
```

Important:

It ensures container starts first, but does NOT guarantee database is ready.

Better approach:

Use healthcheck.

```yaml
services:
  db:
    image: mysql
    healthcheck:
      test: ["CMD", "mysqladmin", "ping"]
      interval: 10s
      retries: 5
```

Now Compose waits for healthy state (Compose v2 behavior).

---

# 11.8 Environment Variables

You can define environment variables in three ways:

### 1️⃣ Inline

```yaml
environment:
  - NODE_ENV=production
```

### 2️⃣ Key-Value Format

```yaml
environment:
  NODE_ENV: production
```

### 3️⃣ .env File

Create `.env` file:

```
NODE_ENV=production
```

Compose automatically loads it.

Best practice:

Do not store secrets directly in YAML.

---

# 11.9 Scaling Services

Scale service:

```bash
docker compose up --scale app=3
```

This runs 3 instances of app.

Compose automatically:

* Assigns different container names
* Shares network
* Supports load balancing internally

---

# 11.10 Docker Compose Lifecycle

Start services:

```bash
docker compose up
```

Detached:

```bash
docker compose up -d
```

Stop services:

```bash
docker compose stop
```

Remove services:

```bash
docker compose down
```

Rebuild services:

```bash
docker compose up --build
```

View logs:

```bash
docker compose logs -f
```

---

# 11.11 Docker Run vs Docker Compose

| Feature         | docker run    | Docker Compose  |
| --------------- | ------------- | --------------- |
| Multi-container | Manual        | Automatic       |
| Networking      | Manual config | Auto-created    |
| Volume setup    | Manual        | Defined in YAML |
| Scaling         | Manual        | Built-in        |
| Reproducibility | Low           | High            |

Compose is better for:

* Development
* Integration testing
* Multi-service stacks

---

# 11.12 Compose in Production

Compose is suitable for:

* Development
* Small deployments
* Single-node environments

For large-scale production:

Use orchestration tools like:

* Kubernetes

However, Compose can still be used in:

* Small production systems
* Internal tools
* Edge deployments

---
# 1️⃣2️⃣ Docker Context 

Docker Context allows you to manage **multiple Docker environments** (local, remote servers, cloud endpoints) from a single Docker CLI.

Instead of manually SSH-ing into servers and running Docker commands, you can switch contexts and run commands directly from your machine.

After this section, you should clearly understand:

* What Docker Context is
* Why it is needed
* How it works internally
* SSH-based remote management
* Cloud integrations
* Multi-environment workflows
* Security considerations

---

# 12.1 What is Docker Context

A Docker Context is a configuration that defines:

* Docker endpoint (local or remote)
* TLS configuration
* Authentication method
* Orchestration backend (optional)

By default, Docker uses:

```bash
docker context ls
```

You’ll see:

```text
NAME        DESCRIPTION                               DOCKER ENDPOINT
default *   Current DOCKER_HOST based configuration   unix:///var/run/docker.sock
```

The `default` context points to your local Docker Engine.

---

# 12.2 Why Docker Context is Needed

In real-world DevOps environments, you may have:

* Local development Docker
* Staging server Docker
* Production server Docker
* Cloud Docker environments

Without context, you must:

* SSH into server
* Run Docker commands manually
* Exit session

With context, you can:

* Switch environment instantly
* Deploy remotely from local machine
* Maintain multi-environment workflow

---

# 12.3 Local vs Remote Context

## Local Context

Default setup:

```text
unix:///var/run/docker.sock
```

This communicates with local Docker daemon.

---

## Remote Context (TCP Endpoint)

Example endpoint:

```text
tcp://192.168.1.10:2376
```

Requires:

* TLS certificates
* Secure configuration

---

# 12.4 Context with SSH

Most secure and common approach.

Create SSH context:

```bash
docker context create prod-server \
  --docker "host=ssh://user@192.168.1.50"
```

Verify:

```bash
docker context ls
```

Switch context:

```bash
docker context use prod-server
```

Now this runs on remote server:

```bash
docker ps
```

No need to SSH manually.

---

## How SSH Context Works Internally

Flow:

```text
Docker CLI
  → SSH tunnel
    → Remote Docker daemon
```

Docker uses SSH to securely forward commands to remote Docker Engine.

---

# 12.5 Context with Cloud

Docker Context can integrate with cloud providers and remote environments.

For example:

* Remote VMs
* Cloud-based Docker endpoints
* Managed container services

Context stores credentials and endpoint configuration.

This allows centralized management of distributed Docker systems.

---

# 12.6 Switching Contexts

List contexts:

```bash
docker context ls
```

Switch:

```bash
docker context use staging
```

Return to local:

```bash
docker context use default
```

Check current:

```bash
docker context show
```

---

# 12.7 Managing Multiple Environments

Example setup:

```text
default     → Local development
staging     → QA server
production  → Production server
```

Workflow:

```text
Build image locally
 → Switch to staging
   → Deploy
 → Test
 → Switch to production
   → Deploy same image
```

No need for manual SSH sessions.

---

# 12.8 Use Case: Remote Production Server Deployment

Example scenario:

You build locally:

```bash
docker build -t myapp:1.0 .
```

Switch to production context:

```bash
docker context use production
```

Deploy:

```bash
docker run -d -p 80:3000 myapp:1.0
```

Docker executes this command on remote production host.

---

# 12.9 Security Considerations for Context

Using remote Docker access improperly can expose your host.

Security best practices:

### 1️⃣ Use SSH instead of open TCP

Avoid exposing:

```text
tcp://0.0.0.0:2375
```

This is insecure.

---

### 2️⃣ Use Key-Based Authentication

Avoid password-based SSH.

Use:

```bash
ssh-keygen
```

---

### 3️⃣ Limit Docker Group Access

Users in `docker` group can control host.

Be cautious with permissions.

---

### 4️⃣ Protect Docker Socket

File:

```text
/var/run/docker.sock
```

If compromised, attacker controls entire host.

---

# Internal Understanding of Docker Context

Docker stores contexts under:

```text
~/.docker/contexts/
```

Each context includes:

* Metadata
* Endpoint config
* TLS info (if configured)

Context does not copy images automatically.

If deploying remotely:

* Image must exist on remote host
* Or be pulled from registry

---

# Production Workflow with Registry + Context

Recommended approach:

```text
Build image locally
 → Push to registry
   → Switch context
     → Pull image
       → Deploy container
```

This ensures:

* Clean deployment
* No image transfer issues
* Version traceability

---

# Common Mistakes

❌ Running production commands in wrong context
❌ Forgetting to switch back to default
❌ Exposing insecure TCP Docker daemon
❌ Not using registry for deployment

---
# 1️⃣3️⃣ Docker Performance Tuning 

Performance tuning in Docker is about:

* Efficient resource usage
* Faster builds
* Lower image pull time
* Reduced storage overhead
* Stable production systems

Containers share host resources.
If not configured properly, performance issues can occur quickly.

This section covers:

* CPU optimization
* Memory control
* Storage driver performance
* Logging impact
* Network tuning
* Image layer optimization
* Build optimization
* Disk monitoring
* Cleanup automation
* Production checklist

---

# 13.1 Performance Optimization Mindset

Before tuning, understand:

Containers are not VMs.

They share:

* Host CPU
* Host memory
* Host kernel
* Host disk

Poor tuning can cause:

* CPU starvation
* Memory OOM kills
* Disk full errors
* Slow container startup
* High build times

Performance tuning must focus on:

* Resource isolation
* Storage efficiency
* Network optimization
* Build speed

---

# 13.2 Storage Driver Performance

Check storage driver:

```bash id="v3h9gt"
docker info
```

Look for:

```text id="kth2t5"
Storage Driver: overlay2
```

---

## overlay2 (Recommended)

Overlay2 uses Linux OverlayFS.

Advantages:

* High performance
* Efficient copy-on-write
* Stable for production
* Native kernel support

Avoid legacy drivers like:

* devicemapper (loop-lvm mode slow)
* aufs (deprecated)

---

## Storage Best Practices

* Use SSD in production
* Store database data in volumes
* Avoid heavy writes in writable layer
* Clean unused images regularly

---

# 13.3 Overlay2 Deep Explanation

![Image](https://blog.wohin.me/posts/docker-advanced-02/5B04F93F4FF2A8BA4731AA154A9D1AA4.png)

![Image](https://tuxera.com/app/uploads/2025/05/tuxera_overlayFS_graphic_01_290223.jpg)

![Image](https://docs.docker.com/engine/storage/drivers/images/overlay_constructs.webp)

![Image](https://docs.docker.com/engine/storage/drivers/images/sharing-layers.webp)

Overlay2 works by merging:

```text id="8nxh9f"
Lower layers (image layers)
Upper layer (container writable)
Merged view (container filesystem)
```

When file is modified:

* Copied from lower to upper
* Change happens in upper

Too many small file changes:

* Can reduce performance
* Increase inode usage

Databases should always use volumes.

---

# 13.4 CPU & Memory Resource Limits Best Practices

Without limits, one container can consume entire host resources.

---

## CPU Limits

Limit CPU cores:

```bash id="ylo8mx"
docker run --cpus=2 myapp
```

Or use CPU shares:

```bash id="u5osmn"
docker run --cpu-shares=512 myapp
```

Use case:

* Multi-tenant servers
* Microservices with defined limits

---

## Memory Limits

Limit memory:

```bash id="a7xt8c"
docker run --memory=512m myapp
```

Set swap limit:

```bash id="8bovt3"
docker run --memory=512m --memory-swap=512m myapp
```

---

## Why Memory Limits Matter

If not limited:

* Container may consume all RAM
* Host may crash
* OOM killer may terminate critical processes

Check OOM status:

```bash id="mn3rce"
docker inspect container_id
```

---

# 13.5 Logging Driver Impact on Performance

Default logging driver:

```text id="mqybwr"
json-file
```

Problems:

* Logs stored in large JSON files
* Can fill disk
* Slows system

---

## Configure Log Rotation

Example:

```bash id="p6kj9l"
docker run \
  --log-opt max-size=10m \
  --log-opt max-file=3 \
  nginx
```

---

## Centralized Logging

Use logging drivers like:

* syslog
* fluentd
* gelf

Prevents disk overload.

---

# 13.6 Image Layer Optimization

Poorly structured Dockerfiles increase:

* Image size
* Pull time
* Startup delay

---

## Optimization Rules

1️⃣ Use minimal base image
2️⃣ Combine RUN commands
3️⃣ Remove build dependencies
4️⃣ Use multi-stage builds
5️⃣ Clean package cache

Example:

```dockerfile id="2vlc4g"
RUN apt update && \
    apt install -y nginx && \
    rm -rf /var/lib/apt/lists/*
```

---

## Analyze Image Layers

```bash id="uzh4fi"
docker history myapp
```

Shows layer sizes.

---

# 13.7 Build Optimization Strategies

Modern builds use BuildKit.

Enable:

```bash id="x3mxdr"
DOCKER_BUILDKIT=1 docker build .
```

Use:

* Cache mounts
* Secret mounts
* Parallel builds

Build caching reduces CI pipeline time significantly.

---

# 13.8 Network Performance Tuning

Default bridge network uses NAT.

Performance impact:

* Slight overhead

Host network:

```bash id="zqiwdu"
docker run --network host myapp
```

Benefits:

* No NAT
* Better performance

Overlay networks:

* Extra VXLAN encapsulation
* Slight overhead in multi-host setups

For high-throughput apps:

* Use host mode carefully
* Optimize kernel network settings

---

# 13.9 Disk Usage Monitoring

Check Docker disk usage:

```bash id="yqrmqv"
docker system df
```

Check container size:

```bash id="m8h4xg"
docker ps -s
```

Large writable layers indicate:

* Poor storage practices
* Missing volumes

---

# 13.10 Disk Cleanup Automation

Manual cleanup:

```bash id="b8c6ay"
docker system prune -a
```

Automate using cron:

```bash id="wd92an"
0 3 * * 0 docker system prune -f
```

Production best practice:

* Keep only recent image versions
* Use registry retention policy
* Monitor disk space alerts

---

# 13.11 Production Performance Checklist

Before deploying to production:

✔ Use overlay2 storage driver
✔ Use volumes for databases
✔ Limit CPU and memory
✔ Configure log rotation
✔ Use multi-stage builds
✔ Avoid large base images
✔ Monitor disk usage
✔ Enable BuildKit
✔ Use health checks
✔ Avoid excessive container restarts

---

# Performance Issues & Root Causes

| Issue                  | Possible Cause             |
| ---------------------- | -------------------------- |
| Slow container startup | Large image size           |
| High disk usage        | Log files or unused images |
| OOM kills              | No memory limits           |
| Slow builds            | No cache usage             |
| Network latency        | Overlay overhead           |
| High I/O               | Heavy writable layer usage |

---
# 1️⃣4️⃣ Docker Backup & Disaster Recovery

(Full Deep Documentation – 2026 Production Standard)

Containers are disposable.
Data is not.

In production systems, losing container data can mean:

* Database corruption
* Application downtime
* Customer impact
* Compliance violations

This section explains:

* Why backup matters in container systems
* Volume backup strategies
* Registry backup
* Image export
* Full recovery workflow
* Disaster recovery architecture patterns
* Backup testing strategy

---

# 14.1 Why Backup is Critical in Containers

Containers are:

* Ephemeral
* Replaceable
* Stateless (ideally)

But real applications store:

* Databases
* File uploads
* Application state
* Logs
* Configuration

These are usually stored in:

* Docker volumes
* Bind mounts
* External storage

If the host fails and volumes are not backed up → data loss.

---

## What Needs Backup in Docker?

1️⃣ Named volumes
2️⃣ Database data
3️⃣ Private registry
4️⃣ Custom images
5️⃣ Configuration files
6️⃣ Compose files

Not required to backup:

* Running containers
* Temporary writable layers

Containers can be recreated.
Data cannot.

---

# 14.2 Volume Backup Automation

Volumes are the most critical backup target.

---

## Manual Volume Backup

Example: Backup MySQL volume

```bash id="m3rptf"
docker run --rm \
  -v mysqldata:/data \
  -v $(pwd):/backup \
  ubuntu tar czf /backup/mysqldata.tar.gz /data
```

Explanation:

* Mount volume into temporary container
* Compress volume data
* Store backup on host

---

## Restore Volume

```bash id="3s8l4x"
docker run --rm \
  -v mysqldata:/data \
  -v $(pwd):/backup \
  ubuntu tar xzf /backup/mysqldata.tar.gz -C /
```

---

## Production Backup Strategy

✔ Schedule backups (cron)
✔ Store backups off-host (cloud storage)
✔ Encrypt backups
✔ Keep retention policy (e.g., 30 days)

Example cron job:

```bash id="g6vuyk"
0 2 * * * /usr/local/bin/docker-volume-backup.sh
```

---

# 14.3 Registry Backup Strategy

If using private registry:

Example registry container:

```bash id="yoq7nt"
docker run -d -p 5000:5000 --name registry registry:2
```

Registry stores images in:

```text id="gh2wbe"
/var/lib/registry
```

This directory must be backed up.

---

## Backup Registry Volume

```bash id="6c6kfa"
docker run --rm \
  -v registrydata:/data \
  -v $(pwd):/backup \
  ubuntu tar czf /backup/registry.tar.gz /data
```

If registry is lost without backup:

* All stored images lost
* Deployment pipelines break

---

# 14.4 Image Backup & Export

If you need offline image backup:

Export image:

```bash id="kht1yo"
docker save myapp:1.0 -o myapp.tar
```

Load image:

```bash id="3z2z9o"
docker load -i myapp.tar
```

Use case:

* Air-gapped environments
* Offline disaster recovery
* Regulatory compliance

---

# 14.5 Container Restore Strategy

Containers themselves should not be backed up.

Instead:

* Store Dockerfile
* Store docker-compose.yml
* Store environment configuration
* Backup volumes

Recreate container:

```bash id="k0uz8f"
docker compose up -d
```

This ensures clean and reproducible restoration.

---

# 14.6 Database Container Recovery

Databases require special handling.

Example: MySQL

Best practice:

1️⃣ Stop database container
2️⃣ Backup volume
3️⃣ Verify backup
4️⃣ Restart container

In production:

* Use logical backup (mysqldump)
* Use volume snapshot
* Or use cloud-managed database backups

Never rely only on writable layer.

---

# 14.7 Production Recovery Workflow

Example disaster scenario:

Host crashed.

Recovery steps:

1️⃣ Provision new host
2️⃣ Install Docker
3️⃣ Restore volumes
4️⃣ Pull images from registry
5️⃣ Deploy using Compose
6️⃣ Verify health checks

Workflow:

```text id="v7tmcz"
New Host
 → Install Docker
   → Restore volume data
     → Pull image
       → docker compose up
         → Application restored
```

---

# 14.8 Disaster Recovery Architecture Pattern

![Image](https://www.researchgate.net/publication/370682380/figure/fig2/AS%3A11431281157565057%401683838515941/Docker-disaster-recovery-process_Q320.jpg)

![Image](https://d2908q01vomqb2.cloudfront.net/fc074d501302eb2b93e2554793fcaf50b3bf7291/2021/04/23/Figure-2.-Backup-and-restore-DR-strategy.png)

![Image](https://global.discourse-cdn.com/docker/original/3X/f/3/f3120c0828bb80b3d1ba42073429fe79392207d2.png)

![Image](https://hewlettpackard.github.io/Docker-Synergy/assets/img/load-balancers.cc05ac82.png)

Production-level DR design includes:

✔ Offsite backups
✔ Registry replication
✔ Automated restore scripts
✔ Infrastructure as Code
✔ Health monitoring

---

## Recommended DR Pattern

```text id="9z6tyv"
Primary Host
 → Volume Backup (daily)
 → Registry Backup
 → Offsite Storage

If failure:
 → Provision new host
 → Restore data
 → Redeploy containers
```

---

# 14.9 Backup Testing Strategy

A backup is useless if not tested.

Best practices:

✔ Perform restore test monthly
✔ Verify database integrity
✔ Validate application startup
✔ Simulate failure scenario

Example test:

```text id="5trnqg"
Create new VM
 → Restore backup
   → Deploy containers
     → Run application tests
```

---

# What NOT to Do

❌ Do not rely only on container restart
❌ Do not store data in writable layer
❌ Do not skip registry backup
❌ Do not ignore offsite storage
❌ Do not assume cloud provider handles everything

---

# Enterprise-Level Best Practices

* Use cloud block storage snapshots
* Use managed database backups
* Replicate private registry
* Use infrastructure automation (Terraform, Ansible)
* Store Compose files in Git
* Use immutable image promotion

---
# 1️⃣5️⃣ Docker Security

(Full Deep Documentation – 2026 Production Standard)

Docker security is a **layered model**.
Security must be applied at:

* Host level
* Docker daemon level
* Image level
* Container runtime level
* Network level
* CI/CD pipeline level

Containers share the host kernel.
If security is weak, a container breakout can compromise the entire host.

This section explains security in deep production detail.

---

# 15.1 What is Docker Security

Docker security is the practice of protecting:

* Host system
* Container runtime
* Images
* Secrets
* Network traffic
* CI/CD pipelines

Security in Docker is based on Linux kernel isolation mechanisms:

* Namespaces
* cgroups
* Capabilities
* Seccomp
* AppArmor / SELinux

---

# 15.2 Security Layers in Docker

![Image](https://www.researchgate.net/publication/353162654/figure/fig2/AS%3A1045045734014976%401626169727373/Docker-layered-architecture-and-hypervisor-vs-container-virtualization-abstraction.ppm)

![Image](https://www.cavirin.com/images/blog/Screen-Shot-2018-01-30-at-1.45.14-PM.png)

![Image](https://miro.medium.com/1%2AoQBStcYmbbtP5n58I1Lb_A.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1086/0%2AQ9RrGw34n1zk9mUh.png)

Security layers:

```text
Host OS
 → Docker Daemon
   → Container Runtime
     → Image Security
       → Application Security
```

Security must be enforced at every layer.

---

# 15.3 Namespaces & cgroups

These are Linux kernel features that isolate containers.

---

## Namespaces (Isolation)

Namespaces isolate:

* PID (process IDs)
* NET (network)
* MNT (filesystem mounts)
* IPC (inter-process communication)
* UTS (hostname)
* USER (user IDs)

Each container believes it is running alone.

---

## cgroups (Resource Control)

Control:

* CPU usage
* Memory limits
* Disk I/O
* Network bandwidth

Without cgroups, a container could exhaust system resources.

---

# 15.4 Root vs Non-Root Containers

By default, containers run as root inside the container.

Even though it's container root, it still has high privileges.

Bad practice:

```dockerfile
FROM ubuntu
CMD ["bash"]
```

Better practice:

```dockerfile
FROM node:18-alpine
USER node
```

Running as non-root reduces risk of container escape.

---

# 15.5 Rootless Docker Mode

Rootless mode runs Docker daemon without root privileges.

Check:

```bash
docker info
```

Look for:

```
rootless: true
```

---

## Benefits

* Reduced attack surface
* Limits privilege escalation
* Safer for development environments

---

# 15.6 How to Enable Rootless Docker

On Linux:

```bash
dockerd-rootless-setuptool.sh install
```

Start rootless daemon:

```bash
systemctl --user start docker
```

Now Docker runs without root access.

---

# 15.7 Rootless Limitations

Rootless mode:

* Cannot bind to privileged ports (<1024)
* Limited network features
* Some storage drivers restricted

Best for:

* Development
* Multi-user environments

Production servers may still require root daemon with hardened configuration.

---

# 15.8 When to Use Rootless

Use rootless when:

* Running Docker in shared servers
* Developer machines
* CI environments
* Testing setups

Avoid if:

* You require advanced networking
* You require kernel-level features

---

# 15.9 Image Security & Scanning

Images are common attack vectors.

Always:

✔ Use official base images from Docker Hub
✔ Pin specific versions
✔ Scan for vulnerabilities

Example scanning tools:

* Docker Scout
* Trivy
* Clair

Scan example (conceptual):

```bash
docker scout cves myapp
```

---

## Avoid These Mistakes

❌ Using `latest` tag
❌ Installing unnecessary packages
❌ Leaving package cache
❌ Storing secrets in image

---

# 15.10 Secrets Management

Never store secrets in:

```dockerfile
ENV PASSWORD=secret
```

Better approaches:

* Runtime environment variables
* Secret files mounted at runtime
* BuildKit secret mounts
* Orchestration-level secrets

In orchestration systems like Kubernetes, use native secret objects.

---

# 15.11 Docker Daemon Security

The Docker daemon controls the entire host.

If compromised → full host compromise.

---

## Protect Docker Socket

File:

```
/var/run/docker.sock
```

Anyone with access can control host.

Do not mount it inside containers unless absolutely required.

---

## Secure Remote Access

Avoid exposing:

```
tcp://0.0.0.0:2375
```

Use:

* TLS
* SSH-based Docker context

---

# 15.12 Runtime Security

Runtime security protects containers during execution.

---

## Drop Capabilities

Containers have Linux capabilities.

Remove unnecessary ones:

```bash
docker run --cap-drop ALL myapp
```

Add only required capabilities.

---

## Read-Only Filesystem

Run container as read-only:

```bash
docker run --read-only myapp
```

Prevents modification of root filesystem.

---

## Resource Limits

Always define:

```bash
docker run --memory=512m --cpus=1 myapp
```

Prevents denial-of-service risk.

---

## Seccomp Profiles

Docker uses default seccomp profile to restrict syscalls.

You can define custom profile:

```bash
docker run --security-opt seccomp=profile.json myapp
```

Restricts dangerous system calls.

---

# 15.13 Security in CI/CD

Security must be integrated into pipeline.

CI/CD best practices:

✔ Scan images before push
✔ Use immutable tags
✔ Use private registry
✔ Sign images
✔ Restrict registry access
✔ Use automated vulnerability alerts

---

## Secure Image Promotion Workflow

```text
Build Image
 → Scan for CVEs
   → Sign Image
     → Push to Registry
       → Promote to Production
```

---

# Common Security Risks

| Risk                | Cause                 |
| ------------------- | --------------------- |
| Container breakout  | Running as root       |
| Host compromise     | Exposed Docker socket |
| Secret leak         | Hardcoded credentials |
| Resource exhaustion | No limits set         |
| Vulnerable packages | Outdated base image   |

---
# 1️⃣6️⃣ Docker Registry & Docker Hub

(Full Deep Documentation – 2026 Production Standard)

Docker Registry is where images are stored, versioned, and distributed.

Without a registry:

* CI/CD pipelines break
* Multi-environment deployments fail
* Teams cannot share images
* Rollbacks become difficult

This section explains:

* What a Docker registry is
* Why it is required
* Types of registries
* Docker Hub deep overview
* Push/pull workflow
* Authentication
* Private registry setup
* Image versioning strategy
* Enterprise registry architecture
* Security best practices

---

# 16.1 What is Docker Registry

A Docker Registry is a storage and distribution system for container images.

It stores:

* Image layers
* Image manifests
* Metadata
* Tags

Images are pulled from registry when running containers.

Example:

```bash
docker pull nginx
```

This pulls from default public registry:

Docker Hub

---

## Registry Components

```text
Repository
 → Tags
   → Manifest
     → Layers
```

---

# 16.2 Why Registry is Required

In real environments:

* Developers build images
* CI builds images
* QA tests images
* Production deploys images

All environments must use the same image artifact.

Registry ensures:

✔ Central image storage
✔ Version control
✔ Multi-host deployment
✔ Rollback capability
✔ CI/CD integration

---

# 16.3 Types of Registries

## 1️⃣ Public Registry

Example:

* Docker Hub

Accessible globally.

---

## 2️⃣ Private Cloud Registry

Examples:

* AWS ECR
* Azure Container Registry
* Google Artifact Registry

Used in cloud-native deployments.

---

## 3️⃣ Self-Hosted Registry

Run your own registry container:

```bash
docker run -d -p 5000:5000 --name registry registry:2
```

Used for:

* Internal enterprise networks
* Air-gapped environments
* Compliance requirements

---

# 16.4 Docker Hub Overview

![Image](https://www.docker.com/app/uploads/2022/06/docker-dashboard-local-images-1.png)

![Image](https://docker-docs.uclv.cu/docker-hub/images/repo-create-details.png)

![Image](https://docs.docker.com/scout/images/dd-image-view.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2AgsbWLsArBhLNEdhueFPWxg.png)

Docker Hub provides:

* Public image hosting
* Official images
* Verified publisher images
* Community images
* Free & paid plans

---

## Image Categories

### Official Images

Maintained by Docker and trusted vendors.

Example:

```bash
docker pull nginx
docker pull mysql
```

---

### Verified Publisher Images

Maintained by trusted companies.

---

### Community Images

Uploaded by users.

Use caution in production.

---

# 16.5 Push & Pull Workflow

## Pull Image

```bash
docker pull nginx:1.25
```

Process:

1️⃣ Check local cache
2️⃣ Download missing layers
3️⃣ Verify layer digest
4️⃣ Store locally

---

## Push Image

First tag image:

```bash
docker tag myapp:1.0 username/myapp:1.0
```

Login:

```bash
docker login
```

Push:

```bash
docker push username/myapp:1.0
```

Docker only uploads missing layers.

---

# 16.6 Image Naming with Registry

Image format:

```text
registry/repository:tag
```

Examples:

```text
docker.io/nginx:latest
myregistry.com/backend:v1.2.0
123456789.dkr.ecr.us-east-1.amazonaws.com/app:prod
```

If no registry specified → defaults to Docker Hub.

---

# 16.7 Authentication & Login

Login:

```bash
docker login
```

Stores credentials in:

```text
~/.docker/config.json
```

Logout:

```bash
docker logout
```

For CI/CD:

* Use access tokens
* Avoid plain passwords

---

# 16.8 Public vs Private Repositories

| Feature    | Public         | Private    |
| ---------- | -------------- | ---------- |
| Visibility | Anyone         | Restricted |
| Security   | Lower          | Higher     |
| Cost       | Free (limited) | Paid       |
| Use Case   | Open-source    | Enterprise |

Production systems should use private repositories.

---

# 16.9 Private Registry (Self-Hosted)

Run registry container:

```bash
docker run -d \
  -p 5000:5000 \
  --name registry \
  registry:2
```

Push image:

```bash
docker tag myapp:1.0 localhost:5000/myapp:1.0
docker push localhost:5000/myapp:1.0
```

---

## Production Enhancements

✔ Enable TLS
✔ Add authentication
✔ Use reverse proxy
✔ Configure storage backend
✔ Backup registry data

Registry data stored in:

```text
/var/lib/registry
```

Must be backed up.

---

# 16.10 Registry in CI/CD

Typical CI pipeline:

```text
Code Commit
 → Build Image
   → Scan Image
     → Tag Version
       → Push to Registry
         → Deploy from Registry
```

Registry becomes:

Single source of truth for images.

---

# 16.11 Image Versioning Strategy

Avoid:

```text
latest
```

Recommended:

✔ Semantic versioning (v1.2.3)
✔ Git commit hash
✔ Build number

Example:

```bash
docker build -t myapp:1.2.0 .
docker push myapp:1.2.0
```

---

# 16.12 Enterprise Registry Concepts

Enterprise registries provide:

* Role-based access control
* Image signing
* Vulnerability scanning
* Replication
* High availability
* Audit logging

Common enterprise features:

✔ Registry replication across regions
✔ Automated retention policies
✔ Fine-grained access control

---

# 16.13 Registry Security Best Practices

✔ Use HTTPS/TLS
✔ Use authentication tokens
✔ Restrict repository access
✔ Scan images before push
✔ Enable audit logging
✔ Apply retention policies
✔ Disable anonymous pull (if private)

---

# Registry High Availability Pattern

![Image](https://www.researchgate.net/publication/308050257/figure/fig1/AS%3A433709594746881%401480415833510/High-level-overview-of-Docker-architecture.png)

![Image](https://cdn-dynmedia-1.microsoft.com/is/image/microsoftcorp/container-registry_value_3?fit=constrain\&op_usm=1.5%2C0.65%2C15%2C0\&qlt=100\&resMode=sharp2\&wid=1454)

![Image](https://learn.microsoft.com/en-us/dotnet/architecture/microservices/container-docker-introduction/media/docker-containers-images-registries/taxonomy-of-docker-terms-and-concepts.png)

![Image](https://docs.opensvc.com/2.1/_images/docker.enterprise.architecture.png)

Enterprise pattern:

```text
Load Balancer
 → Multiple Registry Nodes
   → Shared Storage (S3/NFS)
```

Ensures:

* High availability
* Fault tolerance
* Scalable image distribution

---

# Common Registry Issues

| Problem            | Cause               |
| ------------------ | ------------------- |
| Image pull slow    | Large image size    |
| Unauthorized error | Invalid login       |
| Push denied        | Permission issue    |
| Disk full          | No retention policy |
| Corrupt image      | Interrupted push    |

---
# 1️⃣7️⃣ Docker Enterprise Concepts

(Full Deep Documentation – 2026 Enterprise Standard)

Enterprise container environments require more than just running containers.

They require:

* Governance
* Access control
* Compliance
* Audit logging
* Secure image lifecycle
* Centralized management
* High availability
* Policy enforcement

This section explains Docker in enterprise environments and how large organizations operate container platforms securely and at scale.

---

# 17.1 Docker CE vs Docker EE

Docker has historically been available in different editions.

## Docker CE (Community Edition)

* Free and open-source
* Suitable for developers and small environments
* Community support
* Basic features

## Docker EE (Enterprise Edition)

Docker EE was designed for enterprise environments with:

* Commercial support
* Security features
* RBAC
* Certified integrations
* Enterprise registry
* Compliance tooling

Docker Enterprise was later acquired by:

Mirantis

Now known as:

Mirantis Kubernetes Engine

---

# 17.2 Mirantis Docker Enterprise

Mirantis provides enterprise container solutions including:

* Enterprise container runtime
* Integrated registry
* Kubernetes orchestration
* Centralized management
* Security scanning
* Governance tools

Enterprise container platforms now heavily integrate with:

Kubernetes

---

# 17.3 Enterprise Registry

Enterprise registries provide advanced capabilities beyond basic image storage.

Features include:

* Role-based access control
* Image signing
* Image scanning
* Geo-replication
* High availability
* Immutable tags
* Audit logs
* Retention policies

Enterprise registries may include:

* Harbor
* Cloud-native registries
* Mirantis Secure Registry

Registry becomes the **single source of truth** for all container artifacts.

---

# 17.4 Role-Based Access Control (RBAC)

In enterprise environments, not everyone should have full Docker access.

RBAC defines:

* Who can build images
* Who can push images
* Who can deploy containers
* Who can manage infrastructure

---

## Why RBAC Is Critical

If a user can:

```bash id="m1qz9u"
docker run -v /:/host ubuntu
```

They can compromise the entire host.

RBAC ensures:

* Principle of least privilege
* Controlled deployment pipelines
* Environment segregation

---

# 17.5 Audit Logging

Enterprise systems require traceability.

Audit logging tracks:

* Who pushed image
* Who pulled image
* Who deleted repository
* Who modified configuration

Audit logs are essential for:

* Compliance (SOC2, ISO, HIPAA)
* Security investigations
* Incident response

---

# 17.6 Enterprise Image Governance

Image governance ensures:

* Approved base images
* Approved versions
* No vulnerable packages
* Signed artifacts
* Version traceability

---

## Governance Workflow

```text id="e4i8nt"
Developer builds image
 → Image scanned
   → Approved if no critical CVEs
     → Signed
       → Pushed to production registry
```

Unapproved images should not reach production.

---

# 17.7 Compliance & Security Policies

Enterprise container environments must follow:

* Security standards
* Regulatory requirements
* Internal IT policies

Common compliance requirements:

* Encrypted image storage
* Access logging
* Data retention policies
* Secure image promotion workflow
* Secret management
* Runtime monitoring

---

# Enterprise Container Architecture

![Image](https://www.researchgate.net/publication/221276496/figure/fig4/AS%3A669977342378007%401536746454999/Micro-container-architecture.jpg)

![Image](https://civo-com-assets.ams3.digitaloceanspaces.com/content_images/2015.blog.png?1671109414=)

![Image](https://www.stonebranch.com/fileadmin/_processed_/1/e/csm_2025-03-blog-container-orchestration-diagram_1054b47dc8.jpg)

![Image](https://www.techtarget.com/rms/onlineImages/itops-container_strategy_mobile.jpg)

Typical enterprise setup:

```text id="r8r8pl"
Developers
 → CI/CD
   → Image Scan
     → Enterprise Registry
       → Kubernetes Cluster
         → Production Deployment
           → Monitoring & Audit
```

Everything is controlled, logged, and secured.

---

# Enterprise Best Practices

✔ Separate dev / staging / prod registries
✔ Use immutable image tags
✔ Enforce vulnerability scanning
✔ Restrict Docker socket access
✔ Integrate with identity providers (LDAP, SSO)
✔ Enable image signing
✔ Use private networking
✔ Maintain backup strategy

---

# Enterprise Risks Without Governance

| Risk                  | Impact               |
| --------------------- | -------------------- |
| Unscanned images      | Security breach      |
| No RBAC               | Insider misuse       |
| No audit logs         | No traceability      |
| No version control    | Broken rollback      |
| Public registry usage | Supply chain attacks |

---

# Modern Enterprise Direction (2026)

Enterprise container platforms increasingly rely on:

* Container registries with built-in scanning
* GitOps workflows
* Policy enforcement
* Zero-trust networking
* Runtime security monitoring
* Kubernetes-native orchestration

Docker remains foundational, but orchestration is commonly handled by:

Kubernetes

---
# 1️⃣7️⃣ Docker Enterprise Concepts

(Full Deep Documentation – 2026 Enterprise Standard)

Enterprise container environments require more than just running containers.

They require:

* Governance
* Access control
* Compliance
* Audit logging
* Secure image lifecycle
* Centralized management
* High availability
* Policy enforcement

This section explains Docker in enterprise environments and how large organizations operate container platforms securely and at scale.

---

# 17.1 Docker CE vs Docker EE

Docker has historically been available in different editions.

## Docker CE (Community Edition)

* Free and open-source
* Suitable for developers and small environments
* Community support
* Basic features

## Docker EE (Enterprise Edition)

Docker EE was designed for enterprise environments with:

* Commercial support
* Security features
* RBAC
* Certified integrations
* Enterprise registry
* Compliance tooling

Docker Enterprise was later acquired by:

Mirantis

Now known as:

Mirantis Kubernetes Engine

---

# 17.2 Mirantis Docker Enterprise

Mirantis provides enterprise container solutions including:

* Enterprise container runtime
* Integrated registry
* Kubernetes orchestration
* Centralized management
* Security scanning
* Governance tools

Enterprise container platforms now heavily integrate with:

Kubernetes

---

# 17.3 Enterprise Registry

Enterprise registries provide advanced capabilities beyond basic image storage.

Features include:

* Role-based access control
* Image signing
* Image scanning
* Geo-replication
* High availability
* Immutable tags
* Audit logs
* Retention policies

Enterprise registries may include:

* Harbor
* Cloud-native registries
* Mirantis Secure Registry

Registry becomes the **single source of truth** for all container artifacts.

---

# 17.4 Role-Based Access Control (RBAC)

In enterprise environments, not everyone should have full Docker access.

RBAC defines:

* Who can build images
* Who can push images
* Who can deploy containers
* Who can manage infrastructure

---

## Why RBAC Is Critical

If a user can:

```bash id="m1qz9u"
docker run -v /:/host ubuntu
```

They can compromise the entire host.

RBAC ensures:

* Principle of least privilege
* Controlled deployment pipelines
* Environment segregation

---

# 17.5 Audit Logging

Enterprise systems require traceability.

Audit logging tracks:

* Who pushed image
* Who pulled image
* Who deleted repository
* Who modified configuration

Audit logs are essential for:

* Compliance (SOC2, ISO, HIPAA)
* Security investigations
* Incident response

---

# 17.6 Enterprise Image Governance

Image governance ensures:

* Approved base images
* Approved versions
* No vulnerable packages
* Signed artifacts
* Version traceability

---

## Governance Workflow

```text id="e4i8nt"
Developer builds image
 → Image scanned
   → Approved if no critical CVEs
     → Signed
       → Pushed to production registry
```

Unapproved images should not reach production.

---

# 17.7 Compliance & Security Policies

Enterprise container environments must follow:

* Security standards
* Regulatory requirements
* Internal IT policies

Common compliance requirements:

* Encrypted image storage
* Access logging
* Data retention policies
* Secure image promotion workflow
* Secret management
* Runtime monitoring

---

# Enterprise Container Architecture

![Image](https://www.researchgate.net/publication/221276496/figure/fig4/AS%3A669977342378007%401536746454999/Micro-container-architecture.jpg)

![Image](https://civo-com-assets.ams3.digitaloceanspaces.com/content_images/2015.blog.png?1671109414=)

![Image](https://www.stonebranch.com/fileadmin/_processed_/1/e/csm_2025-03-blog-container-orchestration-diagram_1054b47dc8.jpg)

![Image](https://www.techtarget.com/rms/onlineImages/itops-container_strategy_mobile.jpg)

Typical enterprise setup:

```text id="r8r8pl"
Developers
 → CI/CD
   → Image Scan
     → Enterprise Registry
       → Kubernetes Cluster
         → Production Deployment
           → Monitoring & Audit
```

Everything is controlled, logged, and secured.

---

# Enterprise Best Practices

✔ Separate dev / staging / prod registries
✔ Use immutable image tags
✔ Enforce vulnerability scanning
✔ Restrict Docker socket access
✔ Integrate with identity providers (LDAP, SSO)
✔ Enable image signing
✔ Use private networking
✔ Maintain backup strategy

---

# Enterprise Risks Without Governance

| Risk                  | Impact               |
| --------------------- | -------------------- |
| Unscanned images      | Security breach      |
| No RBAC               | Insider misuse       |
| No audit logs         | No traceability      |
| No version control    | Broken rollback      |
| Public registry usage | Supply chain attacks |

---

# Modern Enterprise Direction 

Enterprise container platforms increasingly rely on:

* Container registries with built-in scanning
* GitOps workflows
* Policy enforcement
* Zero-trust networking
* Runtime security monitoring
* Kubernetes-native orchestration

Docker remains foundational, but orchestration is commonly handled by:

Kubernetes

---
# 1️⃣9️⃣ Docker Troubleshooting

(Full Deep Documentation – 2026 Production Debugging Guide)

Docker troubleshooting is not about memorizing commands.

It is about:

* Systematic debugging
* Understanding container internals
* Identifying root cause
* Fixing without breaking production

This section covers:

* Troubleshooting mindset
* Common real-world issues
* Debug commands
* Networking failures
* Storage failures
* Build failures
* Restart loops
* Disk full errors
* Daemon errors
* Complete debug workflow

---

# 19.1 Troubleshooting Mindset

Before running commands, ask:

1️⃣ Is the container running?
2️⃣ Is the application inside running?
3️⃣ Are ports exposed correctly?
4️⃣ Are volumes mounted correctly?
5️⃣ Are resource limits exceeded?
6️⃣ Is Docker daemon healthy?

Never guess. Always verify.

---

# 19.2 Containers Exiting Immediately

Problem:

```bash id="wplm8y"
docker ps -a
```

Shows:

```text id="k5h9zv"
Exited (1)
```

---

## Possible Causes

* Application crashed
* CMD/ENTRYPOINT wrong
* Missing environment variables
* Permission issues

---

## Debug Steps

1️⃣ Check logs:

```bash id="bz0v6p"
docker logs container_id
```

2️⃣ Inspect exit code:

```bash id="8bt6f6"
docker inspect container_id
```

Look for:

```text id="sn2y4u"
"ExitCode": 1
```

3️⃣ Run container interactively:

```bash id="1ifp4p"
docker run -it image_name bash
```

---

# 19.3 Port Binding Issues

Error:

```text id="43q4j7"
port is already allocated
```

Cause:

* Port already in use

Check:

```bash id="i2c8p0"
netstat -tulnp
```

Or:

```bash id="q33o3s"
docker ps
```

Fix:

* Use different port
* Stop conflicting container

---

# 19.4 Logs Not Showing

Possible reasons:

* Wrong logging driver
* Application not logging to STDOUT
* Log rotation misconfigured

Check logging driver:

```bash id="7b3q0k"
docker info
```

Check container config:

```bash id="q4f6i8"
docker inspect container_id
```

---

# 19.5 Permission Denied Errors

Common error:

```text id="z3y6i1"
permission denied
```

Causes:

* Wrong volume permissions
* Running as non-root
* SELinux restrictions

---

## Fix Volume Permission

```bash id="9pt8no"
chown -R 1000:1000 directory
```

Or modify Dockerfile:

```dockerfile id="x6z7h3"
USER root
```

Better: fix file permissions properly.

---

# 19.6 Data Loss Issues

Cause:

* Using writable layer instead of volume

Check mounts:

```bash id="l8o6ps"
docker inspect container_id
```

Look under:

```text id="m5d3te"
"Mounts"
```

If no volume defined → data lost when container removed.

Solution:

Use named volumes.

---

# 19.7 Image Build Failures

Common causes:

* Syntax errors
* Missing dependencies
* Cache corruption
* Network timeout

Run without cache:

```bash id="g1m3pr"
docker build --no-cache .
```

Enable BuildKit debug:

```bash id="v4e8dk"
DOCKER_BUILDKIT=1 docker build --progress=plain .
```

---

# 19.8 Docker Cache Problems

Symptoms:

* Changes not reflected
* Old files persist

Solution:

```bash id="5sv9km"
docker builder prune
```

Or:

```bash id="n7s6ka"
docker build --no-cache .
```

---

# 19.9 Networking Issues

Symptoms:

* Cannot reach container
* Container cannot reach internet
* Service-to-service communication fails

---

## Debug Steps

1️⃣ Check container IP:

```bash id="r6d8la"
docker inspect container_id
```

2️⃣ Check network:

```bash id="z9p4yo"
docker network inspect bridge
```

3️⃣ Test inside container:

```bash id="d0l3xc"
docker exec -it container_id ping google.com
```

If no internet:

* DNS misconfigured
* Firewall rules blocking
* iptables issue

---

# 19.10 Docker Compose Issues

Common problems:

* Service not starting
* Environment variables missing
* Dependency not ready

Check logs:

```bash id="p1d8mc"
docker compose logs
```

Rebuild:

```bash id="b8f3tv"
docker compose up --build
```

Remove and recreate:

```bash id="e6m9qp"
docker compose down -v
docker compose up -d
```

---

# 19.11 Disk Full Errors

Error:

```text id="t9c5ov"
no space left on device
```

Check disk usage:

```bash id="u6y2nf"
df -h
```

Check Docker disk usage:

```bash id="l3e5zc"
docker system df
```

Cleanup:

```bash id="r0v7bn"
docker system prune -a
docker volume prune
```

Check logs directory:

```text id="v1n6wd"
/var/lib/docker/containers/
```

---

# 19.12 Docker Daemon Errors

Check daemon status:

```bash id="c9k8sd"
systemctl status docker
```

View logs:

```bash id="w3p2af"
journalctl -u docker
```

Restart daemon:

```bash id="f8t6gy"
systemctl restart docker
```

If daemon fails:

* Corrupted storage driver
* Disk full
* Config error in daemon.json

---

# 19.13 Universal Debug Commands

Most useful commands:

```bash id="y5z8rk"
docker ps -a
docker logs container_id
docker inspect container_id
docker stats
docker system df
docker info
```

These solve 80% of Docker issues.

---

# 19.14 Real-World Debug Flow

![Image](https://miro.medium.com/v2/da%3Atrue/resize%3Afit%3A1056/1%2APf8Y1uhAN0RHy1sqG_qz5A.gif)

![Image](https://cdn.prod.website-files.com/63f6813a0731b486f86573a1/679a9a6e371cd74e2cff11a5_debugging-main.png)

![Image](https://ik.imagekit.io/upgrad1/abroad-images/imageCompo/images/1718085389438_Untitled_design_2024_06_11T112543_1_H4Q7A9.webp?pr-true=)

![Image](https://www.atatus.com/blog/content/images/2023/06/complete-docker-container-lifecycle.png)

Production debug workflow:

```text id="w4p9kn"
Issue detected
 → Check container status
   → Check logs
     → Check resource usage
       → Check network
         → Check storage
           → Check daemon
```

---

# Advanced Debug Techniques

### Enter container namespace

```bash id="e9n6ha"
docker exec -it container_id sh
```

### Inspect network namespace

```bash id="r4y8oz"
ip addr
```

### Inspect resource usage

```bash id="z0p3vd"
docker stats
```

### Analyze image layers

```bash id="h2q6cm"
docker history image_name
```

---

# Common Root Causes Summary

| Symptom            | Likely Cause       |
| ------------------ | ------------------ |
| Container restarts | App crash          |
| High CPU           | Infinite loop      |
| High memory        | Memory leak        |
| No response        | Port not published |
| Data missing       | No volume          |
| Build slow         | No cache           |
| Pull slow          | Large image        |
| Daemon crash       | Disk full          |

---

# Production Troubleshooting Checklist

✔ Always check logs first
✔ Always check resource limits
✔ Always verify volume mounts
✔ Always confirm port mapping
✔ Avoid manual container modification
✔ Use versioned images
✔ Monitor disk usage regularly
✔ Use centralized logging

---

You now have a **complete 1–19 Docker documentation structure** covering:

* Foundations
* Architecture
* Core Concepts
* Commands
* Dockerfile
* BuildKit
* Image Management
* Container Management
* Storage
* Networking
* Compose
* Context
* Performance
* Backup
* Security
* Registry
* Enterprise
* Monitoring
* Troubleshooting

---


