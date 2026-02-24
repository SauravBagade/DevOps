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
