# 🐳 Docker Documentation
 ---
## 1️⃣ Docker Introduction

### 🔹 What is Docker

**Docker** is an open-source platform that allows you to **build, package, ship, and run applications** in lightweight units called **containers**.
A container includes:

* Application code
* Runtime
* Libraries & dependencies

So the app runs **the same everywhere** (local, server, cloud).

👉 In short: **Docker = consistency + speed + portability**

---

### 🔹 What is Virtualization

**Virtualization** is a technology that lets you run **multiple operating systems** on a single physical machine using a **hypervisor**.

Each Virtual Machine (VM) has:

* Full OS
* Virtual hardware
* App + dependencies

👉 Heavy but strongly isolated.

---

### 🔹 Why Docker is Used

Docker is used because it solves real problems developers and DevOps teams face:

* ❌ “Works on my machine” problem → ✅ solved
* 🚀 Faster application deployment
* 📦 Lightweight compared to VMs
* 🔁 Easy scaling & rollback
* 🤝 Perfect for CI/CD pipelines

---

### 🔹 Virtualization vs Containers

| Feature        | Virtual Machines | Containers     |
| -------------- | ---------------- | -------------- |
| OS             | Full OS per VM   | Shares host OS |
| Boot Time      | Minutes          | Seconds        |
| Size           | GBs              | MBs            |
| Performance    | Slower           | Near-native    |
| Resource Usage | High             | Low            |
| Isolation      | Strong           | Process-level  |

👉 **Containers are not VMs** — they are processes isolated by the OS.

---

### 🔹 Docker Lifecycle

Docker follows a simple lifecycle:

1. **Build** – Create image from Dockerfile
2. **Pull** – Download image from registry
3. **Run** – Start container from image
4. **Stop** – Stop running container
5. **Remove** – Delete container/image

Flow:

```
Dockerfile → Image → Container → Stop → Remove
```

---

### 🔹 Docker vs Virtual Machine

| Aspect          | Docker     | Virtual Machine      |
| --------------- | ---------- | -------------------- |
| Architecture    | App + libs | App + libs + full OS |
| Speed           | Very fast  | Slow                 |
| Disk usage      | Small      | Large                |
| Scaling         | Easy       | Hard                 |
| DevOps friendly | ✅ Yes      | ❌ Less               |

👉 Docker uses **host kernel**, VM uses **guest OS**.

---

### 🔹 Docker Use Cases

#### ✅ DevOps

* CI/CD pipelines
* Infrastructure consistency
* Faster testing & deployments

#### ✅ Cloud

* Run containers on AWS, Azure, GCP
* Kubernetes orchestration
* Auto-scaling apps

#### ✅ Microservices

* One service = one container
* Independent deployment
* Easy rollback, fault isolation

---

### 🔹 Machine Virtualization vs Containers (Diagram – Explanation)

**Machine Virtualization**

```
Hardware
 └── Host OS
     └── Hypervisor
         ├── VM (OS + App)
         ├── VM (OS + App)
         └── VM (OS + App)
```

**Containers**

```
Hardware
 └── Host OS
     └── Docker Engine
         ├── Container (App)
         ├── Container (App)
         └── Container (App)
```

👉 Containers share **same OS kernel**, so they are **lighter & faster**.

---
![Image](https://assets.bytebytego.com/diagrams/0414-how-does-docker-work.png)

![Image](https://k21academy.com/wp-content/uploads/2020/05/2020-05-12-16_36_49-PowerPoint-Slide-Show-Azure_AZ104_M01_Compute_ed1-1.png)

![Image](https://www.slashroot.in/sites/default/files/docker%20client%20server%20architecture.PNG)

![Image](https://miro.medium.com/1%2AuuZ-h5EH76LOtJ614z-qDA.png)

## 2️⃣ Docker Architecture
### 🔹 Docker Engine

**Docker Engine** is the **core of Docker**.
It is responsible for:

* Building images
* Running containers
* Managing networks & volumes

Docker Engine = **Brain of Docker**

It has 3 main parts:

1. Docker Daemon
2. Docker REST API
3. Docker CLI

---

### 🔹 Docker Daemon (`dockerd`)

The **Docker Daemon** runs in the background on the host machine.

**Main responsibilities:**

* Listens for Docker API requests
* Builds Docker images
* Runs & manages containers
* Manages Docker objects (images, containers, networks, volumes)

👉 Without daemon, **Docker cannot work**.

**Reality:**
If `dockerd` is stopped → Docker commands will fail.

---

### 🔹 Docker CLI (Client)

**Docker CLI** is what **you interact with**.

Examples:

```bash
docker build
docker run
docker ps
docker pull
```

What CLI does:

* Takes user commands
* Converts them into API requests
* Sends them to Docker Daemon

👉 CLI **does not do real work** — daemon does.

---

### 🔹 Docker REST API

Docker uses a **REST API** to communicate internally.

Flow:

```
Docker CLI → REST API → Docker Daemon
```

Why REST API matters:

* Remote Docker management
* Automation tools (CI/CD)
* Kubernetes & cloud tools integration

👉 Even GUI tools talk to Docker via this API.

---

### 🔹 Docker Registry

A **Docker Registry** is a place to **store & distribute images**.

Types:

* Public Registry
* Private Registry

Most popular:

* **Docker Hub**

What registry does:

* Stores Docker images
* Allows image pull & push
* Version control via tags

Example:

```bash
docker pull nginx
docker push myimage:latest
```

---

### 🔹 Docker Hub (Registry Example)

**Docker Hub** provides:

* Official images (nginx, mysql, redis, ubuntu)
* Versioned tags
* Public & private repositories

👉 Default registry used when none is specified.

---

### 🔹 Complete Docker Architecture Flow

```
User
 └── Docker CLI
       └── Docker REST API
             └── Docker Daemon
                   ├── Images
                   ├── Containers
                   ├── Networks
                   └── Volumes
                         │
                         └── Docker Registry (Docker Hub)
```

---

## 3️⃣ Docker Core Concepts (Complete & Real Explanation)

---

### 🔹 1. Docker Image

### What is a Docker Image?

A **Docker Image** is a **read-only template** used to create containers.

It contains:

* Application code
* Runtime (Java, Python, Node, etc.)
* Libraries & dependencies
* OS base layer (Alpine, Ubuntu, etc.)

👉 Image = **Blueprint**

### Key Points

* Images are **immutable** (cannot change)
* Images are built from **Dockerfile**
* Images are stored in **registries**

### Example

```bash
docker pull nginx
docker images
```

### Image Naming Format

```
repository:tag
nginx:latest
```

---

### 🔹 2. Docker Container

### What is a Docker Container?

A **Docker Container** is a **running instance of an image**.

👉 Image = class
👉 Container = object

### Container Characteristics

* Lightweight
* Fast startup
* Isolated process
* Uses host OS kernel

### Lifecycle

```
Create → Start → Run → Stop → Delete
```

### Example

```bash
docker run -d -p 80:80 nginx
docker ps
```

### Reality

* Containers are **temporary**
* If container dies → data is lost (unless volumes used)

---

### 🔹 3. Dockerfile

### What is Dockerfile?

A **Dockerfile** is a **text file** with instructions to build an image.

### Common Instructions

| Instruction | Purpose          |
| ----------- | ---------------- |
| FROM        | Base image       |
| RUN         | Execute commands |
| COPY        | Copy files       |
| ADD         | Copy + extract   |
| WORKDIR     | Set working dir  |
| EXPOSE      | Port info        |
| CMD         | Default command  |
| ENTRYPOINT  | Fixed command    |

### Example Dockerfile

```dockerfile
FROM ubuntu:22.04
RUN apt update && apt install -y nginx
COPY index.html /var/www/html/
EXPOSE 80
CMD ["nginx","-g","daemon off;"]
```

### Build Image

```bash
docker build -t my-nginx .
```

👉 Dockerfile = **Automation + Reproducibility**

---

### 🔹 4. Docker Volumes

### What are Docker Volumes?

**Volumes** are used for **persistent data storage**.

Problem:

* Container deleted → data lost ❌

Solution:

* Use volumes ✅

### Types of Volumes

1. **Named Volume** (Recommended)
2. **Bind Mount**
3. **Anonymous Volume**

### Example

```bash
docker volume create mydata
docker run -v mydata:/data nginx
```

### Why Volumes Matter

* Data persistence
* Backup & restore
* Share data between containers

👉 Databases **must use volumes**.

---

### 🔹 5. Docker Networks

### What is Docker Networking?

Docker networking allows **containers to communicate** with:

* Other containers
* Host system
* External world

### Network Types

| Network | Use Case               |
| ------- | ---------------------- |
| bridge  | Default, single host   |
| host    | High performance       |
| none    | No networking          |
| overlay | Multi-host (Swarm/K8s) |
| macvlan | Real IP from LAN       |

### Example

```bash
docker network create mynet
docker run --network mynet nginx
```

### Reality

* Microservices **depend on networking**
* Wrong network = broken app

---

### 🔹 6. Docker Registry

### What is Docker Registry?

A **Docker Registry** stores Docker images.

Types:

* Public registry
* Private registry

Most popular:

* **Docker Hub**

### Registry Operations

```bash
docker login
docker push myimage:1.0
docker pull myimage:1.0
```

### Why Registry is Important

* CI/CD pipelines
* Image versioning
* Team collaboration
* Cloud deployments

---

### 🔹 Core Concept Relationship (Very Important)

```
Dockerfile → Image → Container
                    ↓
                 Volume
                    ↓
                 Network
                    ↓
                 Registry
```

---

## 4️⃣ Docker **ALL Commands with Examples**

---
### 🔹 1. Docker System & Info Commands

| Command                  | Example                  | Use                |
| ------------------------ | ------------------------ | ------------------ |
| `docker version`         | `docker version`         | Docker version     |
| `docker info`            | `docker info`            | System-wide info   |
| `docker system df`       | `docker system df`       | Disk usage         |
| `docker system prune`    | `docker system prune`    | Remove unused data |
| `docker system prune -a` | `docker system prune -a` | Clean everything   |
| `docker stats`           | `docker stats`           | CPU/RAM usage      |
| `docker events`          | `docker events`          | Real-time events   |

---

### 🔹 2. Docker Image Commands

| Command                | Example                        | Purpose        |
| ---------------------- | ------------------------------ | -------------- |
| `docker images`        | `docker images`                | List images    |
| `docker pull`          | `docker pull nginx`            | Download image |
| `docker push`          | `docker push myimg:1.0`        | Upload image   |
| `docker build`         | `docker build -t app:v1 .`     | Build image    |
| `docker image inspect` | `docker image inspect nginx`   | Image details  |
| `docker image history` | `docker image history nginx`   | Image layers   |
| `docker image rm`      | `docker image rm nginx`        | Remove image   |
| `docker image prune`   | `docker image prune`           | Remove unused  |
| `docker tag`           | `docker tag app:v1 app:latest` | Tag image      |
| `docker save`          | `docker save -o img.tar nginx` | Save image     |
| `docker load`          | `docker load -i img.tar`       | Load image     |

---

### 🔹 3. Docker Container – Run / Start / Stop

| Command             | Example                       | Use             |
| ------------------- | ----------------------------- | --------------- |
| `docker run`        | `docker run nginx`            | Run container   |
| `docker run -d`     | `docker run -d nginx`         | Detached        |
| `docker run -p`     | `docker run -p 80:80 nginx`   | Port map        |
| `docker run --name` | `docker run --name web nginx` | Name container  |
| `docker create`     | `docker create nginx`         | Create only     |
| `docker start`      | `docker start web`            | Start container |
| `docker stop`       | `docker stop web`             | Stop container  |
| `docker restart`    | `docker restart web`          | Restart         |
| `docker pause`      | `docker pause web`            | Pause           |
| `docker unpause`    | `docker unpause web`          | Resume          |

---

### 🔹 4. Docker Container – View & Inspect

| Command          | Example              | Use                |
| ---------------- | -------------------- | ------------------ |
| `docker ps`      | `docker ps`          | Running containers |
| `docker ps -a`   | `docker ps -a`       | All containers     |
| `docker inspect` | `docker inspect web` | Full details       |
| `docker logs`    | `docker logs web`    | Logs               |
| `docker logs -f` | `docker logs -f web` | Live logs          |
| `docker top`     | `docker top web`     | Processes          |
| `docker stats`   | `docker stats web`   | Resource usage     |

---

### 🔹 5. Docker Exec & Attach

| Command          | Example                    | Purpose         |
| ---------------- | -------------------------- | --------------- |
| `docker exec`    | `docker exec -it web bash` | Enter container |
| `docker exec sh` | `docker exec -it web sh`   | Alpine shell    |
| `docker attach`  | `docker attach web`        | Attach STDOUT   |
| `Ctrl + P + Q`   | —                          | Detach safely   |

👉 **Use `exec`, not `attach` in production**

---

### 🔹 6. Docker Remove & Cleanup

| Command                  | Example                  | Use              |
| ------------------------ | ------------------------ | ---------------- |
| `docker rm`              | `docker rm web`          | Remove container |
| `docker rm -f`           | `docker rm -f web`       | Force remove     |
| `docker container prune` | `docker container prune` | Remove stopped   |
| `docker image prune`     | `docker image prune`     | Remove images    |
| `docker volume prune`    | `docker volume prune`    | Remove volumes   |
| `docker network prune`   | `docker network prune`   | Remove networks  |

---

### 🔹 7. Docker Copy & Export

| Command         | Example                       | Use       |
| --------------- | ----------------------------- | --------- |
| `docker cp`     | `docker cp a.txt web:/tmp`    | Copy to   |
| `docker cp`     | `docker cp web:/tmp/a.txt .`  | Copy from |
| `docker export` | `docker export web > web.tar` | Export    |
| `docker import` | `docker import web.tar`       | Import    |

---

### 🔹 8. Docker Volume Commands

| Command                 | Example                         | Purpose      |
| ----------------------- | ------------------------------- | ------------ |
| `docker volume ls`      | `docker volume ls`              | List volumes |
| `docker volume create`  | `docker volume create data`     | Create       |
| `docker volume inspect` | `docker volume inspect data`    | Details      |
| `docker volume rm`      | `docker volume rm data`         | Remove       |
| `docker run -v`         | `docker run -v data:/app nginx` | Mount        |

---

### 🔹 9. Docker Network Commands

| Command                     | Example                               | Use           |
| --------------------------- | ------------------------------------- | ------------- |
| `docker network ls`         | `docker network ls`                   | List networks |
| `docker network create`     | `docker network create mynet`         | Create        |
| `docker network inspect`    | `docker network inspect mynet`        | Inspect       |
| `docker network connect`    | `docker network connect mynet web`    | Connect       |
| `docker network disconnect` | `docker network disconnect mynet web` | Disconnect    |
| `docker network rm`         | `docker network rm mynet`             | Remove        |

---

### 🔹 10. Docker Registry Commands

| Command         | Example               | Purpose      |
| --------------- | --------------------- | ------------ |
| `docker login`  | `docker login`        | Login        |
| `docker logout` | `docker logout`       | Logout       |
| `docker search` | `docker search redis` | Search image |
| `docker pull`   | `docker pull redis`   | Download     |
| `docker push`   | `docker push app:v1`  | Upload       |

Default registry: **Docker Hub**

---

### 🔹 11. Docker Context Commands

| Command                  | Example                       | Use     |
| ------------------------ | ----------------------------- | ------- |
| `docker context ls`      | `docker context ls`           | List    |
| `docker context create`  | `docker context create prod`  | Create  |
| `docker context use`     | `docker context use prod`     | Switch  |
| `docker context inspect` | `docker context inspect prod` | Inspect |

---

### 🔹 12. Docker Compose Commands

| Command                | Example                        | Use            |
| ---------------------- | ------------------------------ | -------------- |
| `docker compose up`    | `docker compose up`            | Start services |
| `docker compose up -d` | `docker compose up -d`         | Background     |
| `docker compose down`  | `docker compose down`          | Stop           |
| `docker compose ps`    | `docker compose ps`            | Status         |
| `docker compose logs`  | `docker compose logs`          | Logs           |
| `docker compose exec`  | `docker compose exec app bash` | Enter          |

---

## 5️⃣ Dockerfile – **Theory in Deep Detail**

> **Straight truth:**
> Dockerfile is the **MOST IMPORTANT** Docker topic.
> If Dockerfile is weak → images are bad → containers fail → production breaks.

---

### 🔹 What is a Dockerfile?

A **Dockerfile** is a **plain text file** that contains a **set of instructions** to automatically build a Docker image.

📌 Dockerfile tells Docker:

* Which OS to use
* What software to install
* Which files to copy
* How the container should start

👉 Dockerfile = **Recipe**
👉 Image = **Cooked food**
👉 Container = **Served plate**

---

### 🔹 Why Dockerfile is Required (Reality)

Without Dockerfile:

* Manual configuration ❌
* Not reproducible ❌
* CI/CD impossible ❌

With Dockerfile:

* Same image everywhere ✅
* Automated builds ✅
* Version controlled ✅

---

### 🔹 Dockerfile → Image → Container Flow

```
Dockerfile
   ↓ docker build
Docker Image
   ↓ docker run
Docker Container
```

---

### 🔹 Dockerfile Architecture (How it Works Internally)

* Docker reads Dockerfile **top to bottom**
* Each instruction creates a **new image layer**
* Layers are **cached**
* If a line changes → cache breaks from that line onward

👉 Poor Dockerfile = slow builds

---

### 🔹 Dockerfile Instructions (THEORY + PURPOSE)

### 1️⃣ `FROM` – Base Image (Mandatory)

Defines the base OS/image.

```dockerfile
FROM ubuntu:22.04
```

Rules:

* First instruction (except ARG)
* Can use minimal images (alpine)

Reality:

* Smaller base image = faster + secure

---

### 2️⃣ `LABEL` – Metadata

Adds information to image.

```dockerfile
LABEL maintainer="saurav"
LABEL env="production"
```

Used for:

* Ownership
* Version info
* Automation tools

---

### 3️⃣ `RUN` – Execute Commands

Runs commands during **image build time**.

```dockerfile
RUN apt update && apt install -y nginx
```

Best Practice:

```dockerfile
RUN apt update \
 && apt install -y nginx \
 && rm -rf /var/lib/apt/lists/*
```

Reality:

* Too many RUN = too many layers

---

### 4️⃣ `COPY` – Copy Files (Recommended)

Copies files from host to image.

```dockerfile
COPY app.py /app/
```

Why COPY over ADD?

* Simple
* Predictable
* Secure

---

### 5️⃣ `ADD` – Copy + Extra Features

```dockerfile
ADD app.tar.gz /app/
```

Extra features:

* Auto-extract `.tar`
* Download from URL (not recommended)

Reality:

* Use `COPY` unless ADD feature needed

---

### 6️⃣ `WORKDIR` – Working Directory

Sets default directory.

```dockerfile
WORKDIR /app
```

Avoid:

```dockerfile
RUN cd /app
```

---

### 7️⃣ `ENV` – Environment Variables

```dockerfile
ENV APP_ENV=prod
ENV PORT=8080
```

Used for:

* Configs
* Secrets (⚠ don’t hardcode passwords)

---

### 8️⃣ `ARG` – Build-Time Variables

```dockerfile
ARG VERSION=1.0
```

Difference:

| ARG            | ENV        |
| -------------- | ---------- |
| Build time     | Runtime    |
| Not persistent | Persistent |

---

### 9️⃣ `EXPOSE` – Port Documentation

```dockerfile
EXPOSE 80
```

Reality:

* Does NOT open port
* Only documentation

---

### 🔟 `CMD` – Default Command

```dockerfile
CMD ["nginx","-g","daemon off;"]
```

Rules:

* Only ONE CMD allowed
* Can be overridden

---

### 1️⃣1️⃣ `ENTRYPOINT` – Fixed Command

```dockerfile
ENTRYPOINT ["python","app.py"]
```

Difference:

| CMD          | ENTRYPOINT       |
| ------------ | ---------------- |
| Can override | Hard to override |
| Default      | Fixed            |

Best combo:

```dockerfile
ENTRYPOINT ["python","app.py"]
CMD ["--help"]
```

---

### 1️⃣2️⃣ `VOLUME` – Persistent Storage Hint

```dockerfile
VOLUME /data
```

Reality:

* Just a hint
* Real volumes created at runtime

---

### 1️⃣3️⃣ `USER` – Security

```dockerfile
USER appuser
```

Reality:

* Never run containers as root in prod

---

### 1️⃣4️⃣ `HEALTHCHECK` – Container Health

```dockerfile
HEALTHCHECK CMD curl -f http://localhost || exit 1
```

Used by:

* Docker
* Kubernetes
* Load balancers

---

### 1️⃣5️⃣ `ONBUILD` – Trigger Instructions

```dockerfile
ONBUILD COPY . /app
```

Used for:

* Base images
* Framework templates

---

### 🔹 Example: Real Production Dockerfile

```dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install --production

COPY . .

EXPOSE 3000

USER node

CMD ["node","server.js"]
```

---

## 6️⃣ Docker Image Management 

---

### 🔹 What is Docker Image Management?

**Docker Image Management** is the practice of:

* Creating images correctly
* Versioning & tagging images
* Storing images in registries
* Optimizing size & security
* Cleaning unused images

👉 Image management = **stable containers + faster CI/CD**

---

### 🔹 Docker Image Lifecycle

```
Dockerfile
   ↓ docker build
Docker Image
   ↓ docker tag
Docker Registry
   ↓ docker pull
Docker Container
```

Images move **between environments**:
Dev → Test → Staging → Production

---

### 🔹 Docker Image Layers (Core Concept)

Docker images are built using **layers**.

Each Dockerfile instruction:

* Creates **one read-only layer**
* Layers are cached
* Shared across images

Example:

```
Layer 1: Base OS
Layer 2: Install packages
Layer 3: Copy app code
Layer 4: CMD
```

👉 Change in one layer invalidates all layers below.

---

### 🔹 Image Immutability (Very Important)

Docker images are **immutable**:

* Once built → cannot be changed
* Any change = new image

Reality:

* Never modify running containers
* Always rebuild images

---

### 🔹 Image Naming & Tagging

### Image Name Format

```
registry/repository:tag
```

Examples:

```
nginx:1.25
myrepo/app:v1.0.3
```

### Tagging Strategy (REAL WORLD)

| Tag Type          | Use              |
| ----------------- | ---------------- |
| `latest`          | Dev/testing only |
| Version (`1.2.3`) | Production       |
| Commit SHA        | CI/CD            |
| Date tags         | Releases         |

👉 Production **should not use `latest`**

---

### 🔹 Image Build Strategies

### 1️⃣ Single-stage Build

```dockerfile
FROM node:18
COPY . .
RUN npm install
CMD ["node","app.js"]
```

❌ Results in:

* Large image
* Build tools inside prod image

---

### 2️⃣ Multi-stage Build (Best Practice)

```dockerfile
FROM node:18 AS build
WORKDIR /app
COPY . .
RUN npm install && npm run build

FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
```

✅ Benefits:

* Smaller image
* More secure
* Faster startup

---

### 🔹 Image Size Optimization

Common techniques:

* Use `alpine` images
* Remove package cache
* Combine RUN commands
* Multi-stage builds
* `.dockerignore`

Bad image:

* 1–2 GB ❌
  Good image:
* <200 MB ✅

---

### 🔹 Docker Image Registries

Images are stored in **registries**.

Types:

* Public registry
* Private registry
* Cloud registry

Default:

* **Docker Hub**

Reality:

* Every company uses **private registry**
* Public images are scanned before use

---

### 🔹 Image Pull & Push Theory

### Pull

```bash
docker pull nginx:1.25
```

* Downloads image layers
* Uses cache if layer exists

### Push

```bash
docker push myapp:1.0
```

* Uploads only changed layers
* Faster incremental pushes

---

### 🔹 Image Caching & CI/CD Impact

Docker cache:

* Speeds up builds
* Can cause bugs if misused

Best practice order:

```dockerfile
COPY package.json .
RUN npm install
COPY . .
```

👉 This allows dependency caching.

---

### 🔹 Image Security Management

Key points:

* Scan images for vulnerabilities
* Use trusted base images
* Avoid root user
* Update base images regularly

Reality:

* 90% vulnerabilities come from base image

---

### 🔹 Image Cleanup & Disk Management

Unused images cause:

* Disk full issues
* CI/CD failures

Cleanup methods:

* Remove dangling images
* Remove unused tags
* Scheduled prune jobs

Reality:

* CI servers need **regular cleanup**

---

### 🔹 Image Promotion Strategy (Prod Reality)

```
Build once
Tag many times
Promote across environments
```

Example:

```
myapp:1.0.0 → dev
myapp:1.0.0 → staging
myapp:1.0.0 → prod
```

👉 Same image everywhere = no surprises

---

## 7️⃣ Docker Container Management – **Theory (Deep & Real)**

---

### 🔹 What is Docker Container Management?

**Docker Container Management** means:

* Creating containers correctly
* Running them with proper configs
* Monitoring, restarting, and scaling
* Managing logs, resources, and failures
* Cleaning unused containers

👉 Good container management = **stable applications**

---

### 🔹 Container vs Image (Quick Reality)

| Image              | Container        |
| ------------------ | ---------------- |
| Blueprint          | Running instance |
| Read-only          | Read-write layer |
| Immutable          | Ephemeral        |
| Stored in registry | Lives on host    |

---

### 🔹 Docker Container Lifecycle (Important)

```
Create → Start → Run → Pause → Stop → Restart → Delete
```

Detailed:

1. `docker create`
2. `docker start`
3. `docker run` (create + start)
4. `docker stop`
5. `docker rm`

👉 Deleted container = data gone (unless volumes).

---

### 🔹 Container Creation Theory (`docker run`)

`docker run` combines:

* Image pull (if missing)
* Container create
* Network attach
* Volume mount
* Process start

Example concept:

```bash
docker run -d -p 80:80 --name web nginx
```

Behind the scenes:

* Creates writable layer
* Assigns IP
* Starts PID 1

---

### 🔹 PID 1 Problem (Advanced Reality)

Inside container:

* First process = **PID 1**
* If PID 1 dies → container exits
* PID 1 must handle signals

Reality:

* Poorly written apps crash containers
* Use proper init or signal handling

---

### 🔹 Foreground vs Background Containers

### Foreground

```bash
docker run nginx
```

* Attached to terminal
* Ctrl+C stops container

### Background (Detached)

```bash
docker run -d nginx
```

* Runs in background
* Needs logs to debug

Production uses **detached mode**.

---

### 🔹 Container Restart Policies

Containers **do not restart automatically** unless defined.

Restart policies:

| Policy           | Behavior                        |
| ---------------- | ------------------------------- |
| `no`             | Default                         |
| `always`         | Always restart                  |
| `on-failure`     | Restart on error                |
| `unless-stopped` | Restart unless manually stopped |

Used for:

* Self-healing apps
* Basic resilience

---

### 🔹 Container Resource Management

Containers share host resources.

### CPU

* CPU shares
* CPU quotas

### Memory

* Memory limits
* OOM killer

Reality:

* No limits = one container can kill host

---

### 🔹 Container Logs Management

Logs:

* STDOUT / STDERR
* Stored by Docker

Reality:

* Docker logs are **not permanent**
* Logs rotate
* Central logging needed in prod

---

### 🔹 Exec vs Attach (Very Important)

### `exec`

* Starts new process
* Safe
* Preferred

### `attach`

* Attaches to STDOUT
* Dangerous
* Can stop container

👉 **Always use `exec`**

---

### 🔹 Container Networking Theory

Each container:

* Gets virtual IP
* Communicates via Docker networks
* Uses port mapping for external access

Reality:

* Containers should talk by **service name**, not IP

---

### 🔹 Container Storage Theory

Containers use:

* Writable layer (temporary)
* Volumes (persistent)

Reality:

* Databases **must not** use container FS
* Volumes are mandatory

---

### 🔹 Health Checks & Monitoring

Health checks:

* Define container health
* Used by orchestrators

Unhealthy container:

* Still running
* But marked unhealthy

---

### 🔹 Container Scaling Reality

Standalone Docker:

* Manual scaling

Production:

* Use Docker Compose
* Use Kubernetes

---

### 🔹 Container Cleanup Strategy

Problems:

* Stopped containers
* Disk usage
* Resource leak

Solution:

* Regular cleanup
* Automated pruning

Reality:

* CI/CD agents die due to disk full

---

## 8️⃣ Docker Volumes & Storage

---

### 🔹 Why Docker Storage Exists

By default, containers use a **writable layer**:

* When container stops or is deleted → **data is lost**
* This is by design

👉 Docker storage solves:

* Data persistence
* Data sharing
* Backup & restore
* Performance isolation

---

### 🔹 Docker Storage Types (VERY IMPORTANT)

Docker provides **3 storage mechanisms**:

| Type                     | Persistent | Use Case             |
| ------------------------ | ---------- | -------------------- |
| Container writable layer | ❌ No       | Temporary files      |
| **Volumes**              | ✅ Yes      | Databases, prod data |
| **Bind Mounts**          | ✅ Yes      | Dev, config files    |

---

### 🔹 1️⃣ Container Writable Layer (Default)

### Theory

* Created when container starts
* Deleted when container is removed
* Slow & unsafe for data

```
Image (read-only)
 + Writable layer (container)
```

### Example

```bash
docker run -it ubuntu bash
echo "data" > file.txt
exit
docker rm <container>
```

❌ `file.txt` is gone

👉 **Never store important data here**

---

### 🔹 2️⃣ Docker Volumes (MOST IMPORTANT)

### What is a Docker Volume?

A **Docker Volume** is a **managed storage** area outside the container filesystem.

* Stored on host
* Managed by Docker
* Independent of container lifecycle

👉 Best option for **production**

---

### Volume Architecture

```
Host Machine
 └── /var/lib/docker/volumes/
       └── volume_name/_data
```

---

### Volume Lifecycle

```
Create → Attach → Use → Detach → Reuse → Delete
```

---

### Volume Commands (Examples)

#### Create Volume

```bash
docker volume create mydata
```

#### List Volumes

```bash
docker volume ls
```

#### Inspect Volume

```bash
docker volume inspect mydata
```

#### Remove Volume

```bash
docker volume rm mydata
```

---

### Using Volume with Container

```bash
docker run -d \
  --name db \
  -v mydata:/var/lib/mysql \
  mysql:8
```

✅ Data survives container deletion
✅ Safe for databases

---

### Volume Reuse Example

```bash
docker run -d --name db2 -v mydata:/var/lib/mysql mysql:8
```

👉 Same data reused

---

### 🔹 3️⃣ Bind Mounts

### What is a Bind Mount?

Bind mounts map a **host directory** directly into a container.

```bash
/host/path  →  /container/path
```

---

### Bind Mount Example

```bash
docker run -d \
  -v /home/user/app:/app \
  node:18
```

Used for:

* Development
* Live code reload
* Config files

---

### Bind Mount Problems (Reality)

❌ Depends on host path
❌ OS-specific
❌ Less secure
❌ Not portable

👉 **Avoid bind mounts in production**

---

### 🔹 Volume vs Bind Mount (EXAM + INTERVIEW)

| Feature           | Volume | Bind Mount |
| ----------------- | ------ | ---------- |
| Managed by Docker | ✅      | ❌          |
| Portable          | ✅      | ❌          |
| Secure            | ✅      | ❌          |
| Prod Ready        | ✅      | ❌          |
| Dev Friendly      | ⚠️     | ✅          |

---

### 🔹 Anonymous Volumes

### Theory

* Auto-created
* No name
* Hard to manage

```bash
docker run -v /data nginx
```

❌ Difficult cleanup
❌ Not recommended

---

### 🔹 Volume in Dockerfile (`VOLUME`)

```dockerfile
VOLUME /data
```

Reality:

* Just a **hint**
* Actual volume created at runtime
* Not enough for prod planning

---

### 🔹 Database + Volume (REAL WORLD EXAMPLE)

### ❌ Wrong (Data Loss)

```bash
docker run mysql
```

### ✅ Correct

```bash
docker volume create mysql_data

docker run -d \
  --name mysql \
  -e MYSQL_ROOT_PASSWORD=root \
  -v mysql_data:/var/lib/mysql \
  mysql:8
```

---

### 🔹 Backup & Restore Volumes

### Backup

```bash
docker run --rm \
  -v mysql_data:/data \
  -v $(pwd):/backup \
  ubuntu tar cvf /backup/backup.tar /data
```

### Restore

```bash
docker run --rm \
  -v mysql_data:/data \
  -v $(pwd):/backup \
  ubuntu tar xvf /backup/backup.tar -C /
```

---

### 🔹 Volume Cleanup (CRITICAL)

Unused volumes:

* Consume disk
* Kill CI/CD agents

Cleanup:

```bash
docker volume prune
```

Reality:

* Run cleanup regularly

---

### 🔹 Storage Driver (High-Level Theory)

Docker uses storage drivers:

* `overlay2` (most common)
* `aufs`, `devicemapper` (older)

Reality:

* Don’t change unless required
* Managed by Docker Engine

---

## 9️⃣ Docker Networking

---

### 🔹 What is Docker Networking?

**Docker Networking** enables:

* Container ↔ Container communication
* Container ↔ Host communication
* Container ↔ External world access

Docker creates **virtual networks** so containers can talk **securely and predictably**.

---

### 🔹 Why Docker Needs Networking

Without networking:

* Microservices can’t communicate
* Load balancers can’t route traffic
* Scaling is impossible

👉 Networking is the **backbone** of containerized apps.

---

### 🔹 Docker Networking Architecture (Concept)

```
Client / Browser
      ↓
 Host Port (80)
      ↓
 Docker Network
      ↓
 Container (nginx)
```

Each container:

* Gets a **virtual IP**
* Joins one or more Docker networks
* Uses **iptables / NAT** internally

---

### 🔹 Docker Network Drivers (VERY IMPORTANT)

Docker supports multiple **network drivers**:

| Driver      | Scope       | Use Case           |
| ----------- | ----------- | ------------------ |
| **bridge**  | Single host | Default, most apps |
| **host**    | Single host | High performance   |
| **none**    | Single host | Isolation          |
| **overlay** | Multi-host  | Swarm / K8s        |
| **macvlan** | LAN level   | Real IP needed     |

---

### 🔹 1️⃣ Bridge Network (DEFAULT & MOST USED)

### Theory

* Default network when Docker installs
* Containers get private IPs
* Uses NAT for external access

```
Container A ↔ Bridge ↔ Container B
                     ↕
                   Host
```

---

### Example: Default Bridge

```bash
docker run -d --name web1 nginx
docker run -d --name web2 nginx
```

❌ Containers **cannot resolve names** by default
They communicate via IP (bad practice).

---

### Custom Bridge Network (BEST PRACTICE)

```bash
docker network create mynet

docker run -d --name app --network mynet nginx
docker run -d --name db  --network mynet mysql:8
```

✅ Containers can talk using **names**:

```bash
ping db
```

👉 **Always use custom bridge networks**

---

### 🔹 2️⃣ Host Network

### Theory

* Container uses **host’s network stack**
* No isolation
* No port mapping needed

```
Container == Host Network
```

---

### Example

```bash
docker run --network host nginx
```

✅ Faster
❌ No isolation
❌ Port conflicts

👉 Use only when **performance is critical**

---

### 🔹 3️⃣ None Network

### Theory

* Container has **no network**
* Fully isolated

---

### Example

```bash
docker run --network none alpine
```

Used for:

* Batch jobs
* Security isolation
* Offline processing

---

### 🔹 4️⃣ Overlay Network (Multi-Host)

### Theory

* Used in **Docker Swarm / Kubernetes**
* Containers across hosts communicate
* Uses VXLAN

```
Host1 ── Overlay ── Host2
```

---

### Example (Concept)

```bash
docker network create -d overlay prod_net
```

👉 Rare in standalone Docker
👉 Common in orchestration

---

### 🔹 5️⃣ Macvlan Network

### Theory

* Container gets **real LAN IP**
* Appears as physical device

---

### Example (Concept)

```bash
docker network create -d macvlan \
  --subnet=192.168.1.0/24 \
  --gateway=192.168.1.1 \
  macvlan_net
```

Used when:

* Legacy apps
* Network appliances
* Monitoring tools

---

### 🔹 Port Mapping (CRITICAL CONCEPT)

### Theory

Containers listen on **internal ports**.
Host exposes them via **port mapping**.

```
Host:80 → Container:80
```

---

### Example

```bash
docker run -d -p 8080:80 nginx
```

* `8080` → host port
* `80` → container port

Access:

```
http://localhost:8080
```

---

### 🔹 Expose vs Publish (Interview Favorite)

| Instruction | Meaning             |
| ----------- | ------------------- |
| `EXPOSE 80` | Documentation only  |
| `-p 80:80`  | Actually opens port |

👉 `EXPOSE` **does not** publish ports

---

### 🔹 Container-to-Container Communication

### ❌ Bad Practice

```bash
ping 172.18.0.3
```

### ✅ Good Practice

```bash
ping db
```

Rules:

* Same network
* Use **container names**
* DNS handled by Docker

---

### 🔹 Multiple Networks per Container

### Theory

A container can join **multiple networks**.

---

### Example

```bash
docker network create frontend
docker network create backend

docker run -d --name api --network frontend nginx
docker network connect backend api
```

Use case:

* Frontend ↔ API ↔ Database
* Network isolation

---

### 🔹 Docker DNS (Internal)

Docker provides:

* Embedded DNS server
* Name resolution
* Automatic service discovery

Reality:

* Works only inside same network
* Replaces hardcoded IPs

---

### 🔹 Network Security (High Level)

Isolation via:

* Separate networks
* Firewall rules
* No direct host exposure

Reality:

* Networking = first security layer

---

## 🔟 Docker Compose

---

### 🔹 What is Docker Compose?

**Docker Compose** is a tool used to **define and run multi-container applications** using a single YAML file (`docker-compose.yml`).

Instead of running:

```bash
docker run ...
docker run ...
docker network ...
docker volume ...
```

You write **one file** and run:

```bash
docker compose up
```

👉 Compose = **Automation + Consistency**

---

### 🔹 Why Docker Compose is Needed (Reality)

Real applications are **not single containers**.

Example real app:

* Frontend (React)
* Backend (Node / Java)
* Database (MySQL)
* Cache (Redis)

Without Compose:

* Manual commands ❌
* Hard to reproduce ❌
* Human errors ❌

With Compose:

* One command start/stop ✅
* Same setup for everyone ✅
* Perfect for Dev & Test ✅

---

### 🔹 Docker Compose Architecture

```
docker-compose.yml
        ↓
 Docker Compose Engine
        ↓
 ┌───────────────┐
 │ Network       │
 │ Volumes       │
 │ Containers    │
 └───────────────┘
```

Compose automatically creates:

* Network
* Volumes
* Containers
* DNS entries

---

### 🔹 Docker Compose File (`docker-compose.yml`)

### Basic Structure

```yaml
version: "3.9"

services:
  service_name:
    image: image_name
    ports:
      - "host:container"
```

Main sections:

* `services` (mandatory)
* `volumes` (optional)
* `networks` (optional)

---

### 🔹 Key Docker Compose Concepts

### 1️⃣ Services

A **service** = one container definition.

```yaml
services:
  web:
    image: nginx
```

👉 One service can be scaled to many containers.

---

### 2️⃣ Networks (Auto-Created)

* Docker Compose creates a **default bridge network**
* All services can talk using **service names**

```bash
curl http://backend:3000
```

👉 No IPs, no port confusion.

---

### 3️⃣ Volumes (Persistence)

Used to persist data.

```yaml
volumes:
  db_data:
```

---

### 🔹 Example 1: Simple Web App (Nginx)

```yaml
version: "3.9"

services:
  web:
    image: nginx
    ports:
      - "8080:80"
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

### 🔹 Example 2: Web + Database (REAL WORLD)

```yaml
version: "3.9"

services:
  web:
    image: nginx
    ports:
      - "8080:80"
    depends_on:
      - db

  db:
    image: mysql:8
    environment:
      MYSQL_ROOT_PASSWORD: root
    volumes:
      - mysql_data:/var/lib/mysql

volumes:
  mysql_data:
```

### What happens:

* Network auto-created
* MySQL data persists
* Web waits for DB

---

### 🔹 `depends_on` (Important)

```yaml
depends_on:
  - db
```

Reality:

* Controls **start order**
* Does **NOT** wait for DB to be ready

👉 Healthchecks needed for real readiness.

---

### 🔹 Example 3: Backend + DB + Volume

```yaml
version: "3.9"

services:
  backend:
    build: .
    ports:
      - "3000:3000"
    depends_on:
      - db

  db:
    image: postgres:15
    environment:
      POSTGRES_PASSWORD: admin
    volumes:
      - pgdata:/var/lib/postgresql/data

volumes:
  pgdata:
```

---

### 🔹 Build with Docker Compose

```yaml
services:
  app:
    build:
      context: .
      dockerfile: Dockerfile
```

Run:

```bash
docker compose up --build
```

---

### 🔹 Environment Variables

### Inline

```yaml
environment:
  APP_ENV: production
```

### Using `.env` file (BEST PRACTICE)

```yaml
environment:
  - DB_USER=${DB_USER}
```

---

### 🔹 Scaling Services

```bash
docker compose up --scale web=3
```

Creates:

* web_1
* web_2
* web_3

👉 Used for load testing.

---

### 🔹 Docker Compose Lifecycle

| Command                  | Meaning        |
| ------------------------ | -------------- |
| `docker compose up`      | Create & start |
| `docker compose up -d`   | Background     |
| `docker compose ps`      | Status         |
| `docker compose logs`    | Logs           |
| `docker compose stop`    | Stop           |
| `docker compose down`    | Stop + remove  |
| `docker compose down -v` | Remove volumes |

---

### 🔹 Compose vs Docker Run (INTERVIEW)

| Docker Run       | Docker Compose   |
| ---------------- | ---------------- |
| Single container | Multi-container  |
| Manual           | Declarative      |
| Error-prone      | Reproducible     |
| Not scalable     | Scalable         |
| Poor for apps    | Perfect for apps |

---

### 🔹 What Docker Compose is NOT

❌ Not a production orchestrator
❌ Not auto-healing at scale
❌ Not replacement for Kubernetes

👉 Compose = **Dev / Test / Small prod**

---

## 1️⃣1️⃣ Docker Registry & Docker Hub

---

### 🔹 What is a Docker Registry?

A **Docker Registry** is a **storage system for Docker images**.

It allows you to:

* Store images
* Version images
* Share images
* Pull images to any server/cloud

👉 Registry = **Image warehouse**

---

### 🔹 Why Docker Registry is Required

Without registry:

* Images stay on one machine ❌
* No CI/CD ❌
* No cloud deployment ❌
* No scaling ❌

With registry:

* Build once, deploy anywhere ✅
* Version control for images ✅
* Team collaboration ✅

---

### 🔹 Types of Docker Registries

| Type             | Example           | Use Case      |
| ---------------- | ----------------- | ------------- |
| Public Registry  | Docker Hub        | Open images   |
| Private Registry | Company registry  | Secure images |
| Cloud Registry   | AWS / Azure / GCP | Production    |

---

### 🔹 Docker Hub (Most Popular Registry)

The default public registry is **Docker Hub**.

When you run:

```bash
docker pull nginx
```

Docker actually pulls from:

```
docker.io/library/nginx
```

👉 `docker.io` = Docker Hub

---

### 🔹 What Docker Hub Provides

Docker Hub offers:

* Public repositories (free)
* Private repositories (limited/free + paid)
* Official images
* Verified publisher images
* Image tags & versions

---

### 🔹 Docker Hub Image Types (IMPORTANT)

### 1️⃣ Official Images

Maintained by Docker or vendors.
Examples:

* nginx
* mysql
* redis
* ubuntu

✅ Secure
✅ Regular updates

---

### 2️⃣ Verified Publisher Images

Maintained by companies.
Examples:

* HashiCorp
* Elastic
* Bitnami

---

### 3️⃣ Community Images

Created by users.

⚠️ Risky
⚠️ Must scan before prod

---

### 🔹 Docker Registry Architecture

```
Developer
   ↓ docker push
Docker Registry
   ↓ docker pull
Servers / CI / Kubernetes
```

Registry stores:

* Image layers
* Metadata
* Tags

---

### 🔹 Image Push & Pull 

### Pull (Download)

```bash
docker pull nginx:1.25
```

What happens:

* Docker checks local cache
* Downloads missing layers
* Reuses existing layers

---

### Push (Upload)

```bash
docker push myapp:1.0
```

What happens:

* Only new layers uploaded
* Faster incremental push

👉 Efficient by design

---

### 🔹 Image Naming with Registry

Format:

```
registry/username/repository:tag
```

Example:

```
docker.io/saurav/app:1.0
```

---

### 🔹 Docker Login & Authentication

```bash
docker login
```

Stores credentials:

* `~/.docker/config.json`

Reality:

* CI/CD uses tokens, not passwords
* Never commit credentials

---

### 🔹 Public vs Private Repositories

| Feature    | Public | Private               |
| ---------- | ------ | --------------------- |
| Visibility | Anyone | Restricted            |
| Cost       | Free   | Free (limited) / Paid |
| Security   | Low    | High                  |
| Prod usage | ❌      | ✅                     |

👉 **Production images must be private**

---

### 🔹 Private Docker Registry (Self-Hosted)

You can run your own registry.

Concept:

```bash
docker run -d -p 5000:5000 registry:2
```

Used when:

* Security policies
* Air-gapped environments
* Compliance needs

---

### 🔹 Docker Registry in CI/CD (Reality)

Typical pipeline:

```
Code → Build Image → Scan → Push → Deploy
```

Registry is the **handoff point** between:

* Build stage
* Deploy stage

---

### 🔹 Image Versioning Strategy (Critical)

❌ Bad:

```
latest
```

✅ Good:

```
1.0.0
1.0.1
commit-sha
```

👉 Registry enables rollback.

---

### 🔹 Image Security in Registry

Best practices:

* Scan images
* Use trusted base images
* Delete unused tags
* Rotate credentials

Reality:

* Most vulnerabilities come from base images

---

## 1️⃣2️⃣ Docker Security

---

### 🔹 What is Docker Security?

**Docker Security** is the practice of protecting:

* Docker host
* Docker images
* Docker containers
* Docker registry
* Secrets & data

👉 Goal: **If a container is compromised, the host must survive**

---

### 🔹 Docker Security Layers (Big Picture)

Docker security works in **layers**:

```
Application Security
↓
Container Security
↓
Image Security
↓
Docker Engine Security
↓
Host OS Security
```

👉 Weakest layer breaks everything.

---

### 🔹 1️⃣ Container Isolation (Core Concept)

Docker uses **Linux kernel features**:

### 🔸 Namespaces

Provide isolation for:

* Process IDs (PID)
* Network
* Mounts
* Users

👉 One container **cannot see another container’s processes**

---

### 🔸 cgroups (Control Groups)

Limit resources:

* CPU
* Memory
* Disk I/O

👉 Prevents **resource abuse attacks**

---

### 🔸 Reality

❌ Containers are **not full VMs**
❌ Kernel is shared
👉 Kernel exploit = all containers at risk

---

### 🔹 2️⃣ Root vs Non-Root Containers (CRITICAL)

### ❌ Running as root (Very Dangerous)

```dockerfile
FROM ubuntu
CMD ["bash"]
```

If attacker escapes container → **host root access**.

---

### ✅ Running as non-root (Mandatory)

```dockerfile
RUN useradd appuser
USER appuser
```

👉 **Golden rule:**
**Never run containers as root in production**

---

### 🔹 3️⃣ Docker Image Security

### Image is your **attack surface**

Problems:

* Vulnerable packages
* Outdated OS
* Malware in base image

---

### Best Practices

✅ Use official images
✅ Use minimal images (alpine, slim)
✅ Update base images regularly
✅ Remove build tools

Example:

```dockerfile
FROM node:18-alpine
```

---

### 🔹 4️⃣ Image Source Trust

Image sources:

1. **Official images** (safe)
2. Verified publishers
3. Random community images ❌

👉 Always prefer official images from **Docker Hub**

---

### 🔹 5️⃣ Image Vulnerability Scanning 

What scanners detect:

* OS vulnerabilities (CVE)
* Library vulnerabilities
* Known exploits

Reality:

* 90% CVEs come from base image
* Scan before pushing to registry

---

### 🔹 6️⃣ Dockerfile Security Best Practices

### ❌ Bad Dockerfile

```dockerfile
FROM ubuntu
RUN apt install ssh
```

### ✅ Secure Dockerfile

```dockerfile
FROM ubuntu:22.04
RUN apt update && apt install -y curl \
 && rm -rf /var/lib/apt/lists/*
USER appuser
```

Rules:

* No secrets
* Fewer layers
* No unnecessary packages

---

### 🔹 7️⃣ Secrets Management (VERY IMPORTANT)

### ❌ NEVER DO THIS

```dockerfile
ENV DB_PASSWORD=admin123
```

### ✅ Correct Approaches

* Environment variables at runtime
* Docker Compose `.env`
* External secret managers

👉 **Secrets must never be baked into images**

---

### 🔹 8️⃣ Docker Daemon Security

### Docker Daemon = ROOT POWER

If someone controls `dockerd` → full host access.

Security rules:

* Never expose Docker socket publicly
* Restrict access to `/var/run/docker.sock`
* Use TLS for remote Docker

👉 Docker socket = **root access**

---

### 🔹 9️⃣ Network Security in Docker

Best practices:

* Use custom bridge networks
* Do not expose unnecessary ports
* Separate frontend & backend networks

❌ Bad:

```bash
-p 3306:3306   # Exposing database
```

✅ Good:

* DB only accessible internally

---

### 🔹 🔟 Volume & File System Security

Risks:

* Sensitive host paths mounted
* `/` mounted into container ❌

❌ Dangerous:

```bash
-v /:/host
```

✅ Safe:

* Mount only required directories
* Read-only mounts where possible

---

#### 🔹 1️⃣1️⃣ Runtime Security (Behavior)

Runtime threats:

* Crypto mining
* Reverse shells
* Privilege escalation

Indicators:

* High CPU usage
* Unknown processes
* Network anomalies

👉 Monitoring is required

---

### 🔹 1️⃣2️⃣ Docker Security in CI/CD

Secure pipeline:

```
Build → Scan → Push → Deploy
```

Rules:

* Scan images before push
* Reject vulnerable images
* Use signed images

---

## 1️⃣3️⃣ Docker Logs & Monitoring

---

### 🔹 What are Docker Logs?

**Docker logs** are the **stdout and stderr output** of the main process (PID 1) running inside a container.

Docker does **not invent logs**.
It only **collects what your app prints**.

👉 If your app doesn’t log → Docker can’t show anything.

---

### 🔹 Docker Logging Architecture (Concept)

```
Application
   ↓ stdout / stderr
Container
   ↓
Docker Logging Driver
   ↓
Local logs / Centralized system
```

---

### 🔹 Default Docker Logging Behavior

* Default logging driver: **json-file**
* Logs stored on host:

  ```
  /var/lib/docker/containers/<id>/<id>-json.log
  ```

Reality:

* Logs grow fast
* Can fill disk
* Need rotation or external logging

---

### 🔹 Basic Docker Logs Commands

### View Logs

```bash
docker logs <container>
```

### Follow Logs (Live)

```bash
docker logs -f <container>
```

### Last N Lines

```bash
docker logs --tail 100 <container>
```

### Logs with Timestamp

```bash
docker logs -t <container>
```

👉 First command to run when something breaks.

---

### 🔹 Foreground vs Background Logs

### Foreground Container

```bash
docker run nginx
```

* Logs printed directly
* Terminal attached

### Background Container

```bash
docker run -d nginx
docker logs nginx
```

👉 Production always uses **detached mode**

---

### 🔹 Important Reality: What Docker Logs Are NOT

❌ Not application log files
❌ Not structured by default
❌ Not permanent
❌ Not searchable at scale

👉 Docker logs are **temporary troubleshooting tools**

---

### 🔹 Logging Drivers (VERY IMPORTANT)

Docker supports **multiple logging drivers**:

| Driver      | Use Case        |
| ----------- | --------------- |
| `json-file` | Default, local  |
| `syslog`    | Linux syslog    |
| `journald`  | systemd systems |
| `fluentd`   | Central logging |
| `awslogs`   | AWS CloudWatch  |
| `none`      | Disable logs    |

---

### Set Logging Driver (Example)

```bash
docker run \
  --log-driver=json-file \
  --log-opt max-size=10m \
  --log-opt max-file=3 \
  nginx
```

👉 Prevents disk explosion

---

### 🔹 Log Rotation (CRITICAL)

### Problem

* Containers write logs endlessly
* Disk gets full
* CI/CD & servers crash

### Solution

```bash
--log-opt max-size=10m
--log-opt max-file=3
```

Reality:

* Log rotation is **mandatory in production**

---

### 🔹 Centralized Logging (Production Reality)

In real systems:

* Logs from many containers
* Logs from many servers

Architecture:

```
Containers
   ↓
Log Agent
   ↓
Central Log System
```

Benefits:

* Search
* Alerts
* Long-term storage
* Audit trails

👉 Docker logs alone are **not enough**

---

### 🔹 Docker Monitoring (Metrics)

Monitoring answers:

* Is container alive?
* How much CPU?
* How much memory?
* Is it leaking resources?

---

### 🔹 Basic Container Monitoring (Built-in)

### Live Resource Usage

```bash
docker stats
```

Shows:

* CPU %
* Memory usage
* Network I/O
* Block I/O

Example:

```bash
docker stats web db api
```

---

### 🔹 Container Inspect (Deep Debug)

```bash
docker inspect <container>
```

Used for:

* Restart policy
* Mounts
* Network config
* Health status

---

### 🔹 Health Checks & Monitoring

### Dockerfile Healthcheck

```dockerfile
HEALTHCHECK CMD curl -f http://localhost || exit 1
```

Result:

* `healthy`
* `unhealthy`

Reality:

* Container may run but be unusable
* Healthcheck exposes that state

---

### 🔹 Restart + Monitoring Relation

Restart policies:

```bash
--restart always
--restart on-failure
```

Monitoring tools rely on:

* Health status
* Exit codes
* Restart counts

---

### 🔹 What Docker Monitoring Does NOT Give

❌ Long-term metrics history
❌ Alerting
❌ Dashboards
❌ SLA visibility

👉 Docker monitoring is **basic**, not enterprise-grade

---

### 🔹 Production Monitoring Stack (Concept)

```
Containers
   ↓
Metrics Collector
   ↓
Monitoring System
   ↓
Alerts / Dashboards
```

Metrics tracked:

* CPU spikes
* Memory leaks
* Container restarts
* Disk usage

---

## 1️⃣4️⃣ Docker Troubleshooting

---

### 🔎 Docker Troubleshooting Mindset (VERY IMPORTANT)

**Always debug in this order:**

```
1. Is container running?
2. Check logs
3. Check ports
4. Check volumes
5. Check network
6. Check permissions
```

👉 Don’t guess. **Inspect.**

---

### ❌ Problem 1: Container Exits Immediately

### Symptom

```bash
docker ps
# container not listed
docker ps -a
# container exited
```

### Root Causes

* CMD / ENTRYPOINT finished
* App crashed
* Wrong command

### Fix

```bash
docker logs <container>
```

Example:

```bash
docker run ubuntu
```

Ubuntu exits because no long-running process.

✅ Correct:

```bash
docker run -it ubuntu bash
```

---

### ❌ Problem 2: `docker ps` shows container, but app not reachable

### Symptom

* Container running
* Browser shows *connection refused*

### Root Causes

* Port not exposed
* Wrong port mapping
* App listening on localhost

### Check

```bash
docker ps
```

### Fix

```bash
docker run -p 8080:80 nginx
```

👉 Rule:

```
HOST_PORT : CONTAINER_PORT
```

---

### ❌ Problem 3: `Error: bind: address already in use`

### Cause

* Host port already used

### Check

```bash
netstat -tuln | grep 80
```

### Fix

* Use different port

```bash
docker run -p 8081:80 nginx
```

* Or stop conflicting service

---

### ❌ Problem 4: Container runs but shows no logs

### Cause

* App logs to file instead of stdout

### Reality

Docker logs only capture:

* stdout
* stderr

### Fix (App Side)

❌ Wrong:

```text
logfile.log
```

✅ Correct:

```text
print / console.log
```

👉 **Log to stdout, not files**

---

### ❌ Problem 5: Permission Denied (Files / Volumes)

### Symptom

```text
permission denied
```

### Root Causes

* Container runs as non-root
* Host folder permissions wrong

### Check

```bash
docker inspect <container>
```

### Fix

```bash
chown -R 1000:1000 /host/path
```

or

```dockerfile
USER root
```

⚠️ Only for debugging, not production.

---

### ❌ Problem 6: Data Lost After Container Restart

### Cause

* No volume used
* Data stored in container FS

### Fix

```bash
docker volume create mydata

docker run -v mydata:/var/lib/mysql mysql
```

👉 **No volume = no data**

---

### ❌ Problem 7: Image Build Fails

### Symptom

```text
ERROR: failed to build
```

### Debug

```bash
docker build .
```

### Common Causes

* Wrong base image
* Missing package
* Network issues

### Fix

* Check exact failing layer
* Test commands manually
* Reduce layers

---

### ❌ Problem 8: Changes Not Reflected After Build

### Cause

* Docker cache

### Fix

```bash
docker build --no-cache .
```

Or reorder Dockerfile:

```dockerfile
COPY package.json .
RUN npm install
COPY . .
```

---

### ❌ Problem 9: Container Can’t Reach Another Container

### Cause

* Different networks
* Using IP instead of name

### Check

```bash
docker network ls
```

### Fix

```bash
docker network create mynet

docker run --network mynet --name app nginx
docker run --network mynet --name db mysql
```

Use:

```bash
ping db
```

---

### ❌ Problem 10: Docker Compose `depends_on` Not Working

### Reality

`depends_on` **only controls order**, not readiness.

### Fix

Use **healthchecks**.

```yaml
healthcheck:
  test: ["CMD", "mysqladmin", "ping", "-h", "localhost"]
  interval: 10s
```

---

### ❌ Problem 11: Disk Full on Server

### Cause

* Logs
* Old images
* Stopped containers
* Volumes

### Fix

```bash
docker system df
docker system prune -a
docker volume prune
```

👉 CI/CD servers die because of this.

---

### ❌ Problem 12: `permission denied while connecting to Docker daemon`

### Cause

* User not in docker group

### Fix

```bash
sudo usermod -aG docker $USER
newgrp docker
```

---

### ❌ Problem 13: Container Keeps Restarting

### Check

```bash
docker ps
docker logs <container>
```

### Causes

* App crash
* Wrong env vars
* Healthcheck failure

### Fix

* Fix app
* Fix config
* Remove restart policy during debug

---

### ❌ Problem 14: Docker Daemon Not Running

### Symptom

```text
Cannot connect to the Docker daemon
```

### Fix

```bash
systemctl start docker
systemctl status docker
```

---

### 🧠 Universal Docker Debug Commands (MEMORIZE)

```bash
docker ps -a
docker logs <container>
docker inspect <container>
docker exec -it <container> sh
docker stats
docker system df
```

---

### 🔥 Real-World Debug Flow (Follow This)

```
App down
 ↓
docker ps
 ↓
docker logs
 ↓
docker inspect
 ↓
docker exec
 ↓
Fix
```

---