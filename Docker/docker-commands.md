# 🐳 1️⃣ Docker Root Level Commands

---

# 🔹 `docker version`

## ✅ Use

Check Docker Client & Server version compatibility.

## 📌 Syntax

```bash
docker version
```

## 💻 Example

```bash
docker version
```

## 🏭 Production Use Case

* Debug client-server mismatch
* Check API version before automation scripts
* Validate remote Docker engine compatibility

---

# 🔹 `docker info`

## ✅ Use

Displays full system-wide Docker configuration.

## 📌 Syntax

```bash
docker info
```

## 💻 Example

```bash
docker info
```

## 🏭 Shows

* Storage driver (overlay2)
* Running containers
* Logging driver
* Cgroup version
* Swarm status
* CPU & Memory limits

## 🏭 Production Use Case

Used during:

* Performance troubleshooting
* Storage debugging
* Swarm cluster validation

---

# 🔹 `docker login`

## ✅ Use

Authenticate with Docker registry (Docker Hub / Private Registry).

## 📌 Syntax

```bash
docker login [registry-url]
```

## 💻 Example (Docker Hub)

```bash
docker login
```

## 💻 Example (Private Registry)

```bash
docker login registry.company.com
```

## 🏭 Production Use Case

Used in:

* CI/CD pipelines
* GitHub Actions
* Jenkins deployment stages

---

# 🔹 `docker logout`

## ✅ Use

Remove stored registry credentials.

```bash
docker logout
```

---

# 🔹 `docker search`

## ✅ Use

Search images on Docker Hub.

```bash
docker search nginx
```

---

# 🔹 `docker pull`

## ✅ Use

Download image from registry.

## 📌 Syntax

```bash
docker pull IMAGE[:TAG]
```

## 💻 Example

```bash
docker pull nginx
docker pull ubuntu:22.04
```

## 🏭 Production Use

Pull specific version to avoid “latest” instability.

---

# 🔹 `docker push`

## ✅ Use

Upload image to registry.

```bash
docker push myrepo/app:1.0
```

## 🏭 Production

Used after CI build stage.

---

# 🔹 `docker tag`

## ✅ Use

Create new tag for image.

```bash
docker tag myapp:latest myrepo/myapp:v1
```

---

# 🔹 `docker build`

## ✅ Use

Build image from Dockerfile.

## 📌 Syntax

```bash
docker build -t name:tag PATH
```

## 💻 Example

```bash
docker build -t myapp:1.0 .
```

## 🏭 Production

Used in CI/CD pipelines with:

```bash
docker build --no-cache -t myapp:prod .
```

---

# 🔹 `docker run`

## ✅ Use

Create + Start container.

## 📌 Syntax

```bash
docker run [OPTIONS] IMAGE
```

## 💻 Basic Example

```bash
docker run nginx
```

## 💻 Detached Mode

```bash
docker run -d nginx
```

## 💻 Port Mapping

```bash
docker run -d -p 8080:80 nginx
```

## 💻 Resource Limit

```bash
docker run -d --memory="512m" --cpus="1.5" nginx
```

## 🏭 Production Best Practice

Always use:

* `--restart=always`
* Specific version tag
* Resource limits

---

# 🔹 `docker create`

## ✅ Use

Create container but do NOT start.

```bash
docker create nginx
```

---

# 🔹 `docker start`

```bash
docker start container_id
```

---

# 🔹 `docker stop`

Graceful stop (SIGTERM).

```bash
docker stop container_id
```

---

# 🔹 `docker restart`

```bash
docker restart container_id
```

---

# 🔹 `docker kill`

Force stop (SIGKILL).

```bash
docker kill container_id
```

---

# 🔹 `docker wait`

Wait until container stops.

```bash
docker wait container_id
```

Used in automation scripts.

---

# 🔹 `docker ps`

List running containers.

```bash
docker ps
docker ps -a
```

---

# 🔹 `docker top`

Show running processes inside container.

```bash
docker top container_id
```

---

# 🔹 `docker logs`

View container logs.

```bash
docker logs container_id
docker logs -f container_id
docker logs --since 10m container_id
```

---

# 🔹 `docker stats`

Live resource monitoring.

```bash
docker stats
```

---

# 🔹 `docker inspect`

Full JSON metadata.

```bash
docker inspect container_id
```

Filter example:

```bash
docker inspect -f '{{.State.Status}}' container_id
```

---

# 🔹 `docker attach`

Attach STDIN to running container.

```bash
docker attach container_id
```

⚠️ Ctrl+P Ctrl+Q to detach.

---

# 🔹 `docker exec`

Run command inside container.

```bash
docker exec -it container_id bash
```

Production debugging command.

---

# 🔹 `docker pause` / `docker unpause`

Freeze container.

```bash
docker pause container_id
docker unpause container_id
```

---

# 🔹 `docker update`

Update resource limits.

```bash
docker update --memory 1g container_id
```

---

# 🔹 `docker rename`

```bash
docker rename old_name new_name
```

---

# 🔹 `docker cp`

Copy file between host & container.

```bash
docker cp file.txt container_id:/app/
docker cp container_id:/app/file.txt .
```

---

# 🔹 `docker diff`

Show changed files in container.

```bash
docker diff container_id
```

---

# 🔹 `docker port`

Check port mapping.

```bash
docker port container_id
```

---

# 🔹 `docker events`

Real-time Docker events.

```bash
docker events
```

Used for monitoring systems.

---

# 🔹 `docker export`

Export container filesystem.

```bash
docker export container_id -o container.tar
```

---

# 🔹 `docker import`

Import tar as image.

```bash
docker import container.tar myimage:1.0
```

---

# 🔹 `docker save`

Save image as tar.

```bash
docker save -o myimage.tar myimage:1.0
```

---

# 🔹 `docker load`

Load image from tar.

```bash
docker load -i myimage.tar
```

---

# 🔹 `docker context`

Manage remote Docker environments.

```bash
docker context ls
docker context use mycontext
```

---

# 🔹 `docker system`

System management.

```bash
docker system df
docker system prune
```

---

# 🔹 `docker help`

Show help.

```bash
docker help
docker run --help
```

---
# 🐳 2️⃣ Docker Container Subcommands 

> Namespace version of root container commands
> Used in scripting, automation, enterprise environments

---

# 🔹 `docker container create`

## ✅ Use

Create a container but do NOT start it.

## 📌 Syntax

```bash
docker container create [OPTIONS] IMAGE [COMMAND]
```

## 💻 Example

```bash
docker container create --name mynginx -p 8080:80 nginx
```

## 🏭 Production Use

* Pre-create containers before orchestration
* Used in CI test setups
* Used when separating creation and start phases

---

# 🔹 `docker container start`

## ✅ Use

Start one or more stopped containers.

```bash
docker container start mynginx
```

Multiple:

```bash
docker container start c1 c2 c3
```

---

# 🔹 `docker container stop`

## ✅ Use

Gracefully stop container (SIGTERM → SIGKILL after timeout).

```bash
docker container stop mynginx
```

Custom timeout:

```bash
docker container stop -t 30 mynginx
```

---

# 🔹 `docker container restart`

## ✅ Use

Restart running container.

```bash
docker container restart mynginx
```

---

# 🔹 `docker container kill`

## ✅ Use

Force stop container (SIGKILL).

```bash
docker container kill mynginx
```

Custom signal:

```bash
docker container kill --signal=SIGINT mynginx
```

---

# 🔹 `docker container wait`

## ✅ Use

Block until container stops.

```bash
docker container wait mynginx
```

### 🏭 Automation Example

```bash
docker container wait mynginx && echo "Container finished"
```

---

# 🔹 `docker container rm`

## ✅ Use

Remove stopped container.

```bash
docker container rm mynginx
```

Force remove:

```bash
docker container rm -f mynginx
```

Remove multiple:

```bash
docker container rm c1 c2 c3
```

---

# 🔹 `docker container prune`

## ✅ Use

Remove ALL stopped containers.

```bash
docker container prune
```

Force:

```bash
docker container prune -f
```

🏭 Used in disk cleanup jobs.

---

# 🔹 `docker container ls`

## ✅ Use

List containers.

```bash
docker container ls
```

Show all:

```bash
docker container ls -a
```

Filter example:

```bash
docker container ls --filter "status=running"
```

---

# 🔹 `docker container inspect`

## ✅ Use

Show detailed JSON metadata.

```bash
docker container inspect mynginx
```

Format output:

```bash
docker container inspect -f '{{.State.Status}}' mynginx
```

Production monitoring usage.

---

# 🔹 `docker container logs`

## ✅ Use

Show container logs.

```bash
docker container logs mynginx
```

Follow:

```bash
docker container logs -f mynginx
```

Last 50 lines:

```bash
docker container logs --tail 50 mynginx
```

Time filter:

```bash
docker container logs --since 10m mynginx
```

---

# 🔹 `docker container stats`

## ✅ Use

Live CPU & memory monitoring.

```bash
docker container stats
```

Specific container:

```bash
docker container stats mynginx
```

No streaming:

```bash
docker container stats --no-stream
```

---

# 🔹 `docker container top`

## ✅ Use

Show running processes inside container.

```bash
docker container top mynginx
```

---

# 🔹 `docker container attach`

## ✅ Use

Attach terminal to running container.

```bash
docker container attach mynginx
```

Detach safely:

```
Ctrl + P + Q
```

---

# 🔹 `docker container exec`

## ✅ Use

Run command inside running container.

```bash
docker container exec -it mynginx bash
```

Run single command:

```bash
docker container exec mynginx ls /usr/share/nginx/html
```

Production debugging tool.

---

# 🔹 `docker container pause`

## ✅ Use

Freeze container processes (cgroups freeze).

```bash
docker container pause mynginx
```

---

# 🔹 `docker container unpause`

```bash
docker container unpause mynginx
```

---

# 🔹 `docker container update`

## ✅ Use

Update container resource limits dynamically.

```bash
docker container update --memory 1g mynginx
```

Update CPU:

```bash
docker container update --cpus 2 mynginx
```

Production scaling adjustment.

---

# 🔹 `docker container rename`

```bash
docker container rename mynginx newnginx
```

---

# 🔹 `docker container cp`

## ✅ Use

Copy files between host & container.

Host → Container:

```bash
docker container cp file.txt mynginx:/app/
```

Container → Host:

```bash
docker container cp mynginx:/app/file.txt .
```

---

# 🔹 `docker container diff`

## ✅ Use

Show filesystem changes.

```bash
docker container diff mynginx
```

Shows:

* A = Added
* C = Changed
* D = Deleted

Used in debugging unexpected file modifications.

---

# 🔹 `docker container port`

## ✅ Use

List mapped ports.

```bash
docker container port mynginx
```

---

# ✅ Container Namespace Section Completed

This covers ALL:

* Lifecycle management
* Monitoring
* Debugging
* Resource updates
* File operations
* Cleanup
* Automation usage

---
# 🐳 3️⃣ Docker Image Subcommands 

> Used for image lifecycle management, optimization, CI/CD pipelines, air-gapped environments, and production deployments.

---

# 🔹 `docker image build`

## ✅ Use

Build image from Dockerfile (namespace version of `docker build`).

## 📌 Syntax

```bash
docker image build [OPTIONS] PATH
```

## 💻 Basic Example

```bash
docker image build -t myapp:1.0 .
```

## 💻 Build with specific Dockerfile

```bash
docker image build -f Dockerfile.prod -t myapp:prod .
```

## 💻 Build without cache

```bash
docker image build --no-cache -t myapp:latest .
```

## 🏭 Production Use

* CI/CD pipelines
* Multi-stage builds
* Controlled production tagging
* Immutable infrastructure pattern

---

# 🔹 `docker image pull`

## ✅ Use

Download image from registry.

## 📌 Syntax

```bash
docker image pull IMAGE[:TAG]
```

## 💻 Example

```bash
docker image pull nginx
docker image pull ubuntu:22.04
```

## 💻 Pull from private registry

```bash
docker image pull registry.company.com/app:1.0
```

## 🏭 Best Practice

Always specify version tag (avoid `latest` in production).

---

# 🔹 `docker image push`

## ✅ Use

Upload image to registry.

```bash
docker image push myrepo/myapp:1.0
```

Push all tags:

```bash
docker image push --all-tags myrepo/myapp
```

🏭 Used after successful CI build stage.

---

# 🔹 `docker image ls`

## ✅ Use

List available images.

```bash
docker image ls
```

Show all (including intermediate):

```bash
docker image ls -a
```

Filter:

```bash
docker image ls --filter dangling=true
```

Format:

```bash
docker image ls --format "{{.Repository}}:{{.Tag}}"
```

---

# 🔹 `docker image inspect`

## ✅ Use

Display detailed JSON metadata.

```bash
docker image inspect nginx
```

Specific field:

```bash
docker image inspect -f '{{.Config.Entrypoint}}' nginx
```

🏭 Used to:

* Check environment variables
* Check exposed ports
* Verify entrypoint

---

# 🔹 `docker image history`

## ✅ Use

Show image layer history.

```bash
docker image history nginx
```

No truncation:

```bash
docker image history --no-trunc nginx
```

🏭 Used for:

* Layer size optimization
* Security auditing
* Detecting unnecessary layers

---

# 🔹 `docker image rm`

## ✅ Use

Remove one or more images.

```bash
docker image rm nginx
```

Remove multiple:

```bash
docker image rm img1 img2
```

Force remove:

```bash
docker image rm -f nginx
```

🏭 Used during disk cleanup automation.

---

# 🔹 `docker image prune`

## ✅ Use

Remove unused images.

```bash
docker image prune
```

Remove all unused:

```bash
docker image prune -a
```

With filter:

```bash
docker image prune --filter "until=24h"
```

🏭 Used in production maintenance jobs.

---

# 🔹 `docker image save`

## ✅ Use

Save image to tar archive (air-gapped systems).

```bash
docker image save -o myimage.tar myapp:1.0
```

Save multiple:

```bash
docker image save -o images.tar img1 img2
```

🏭 Used for:

* Offline environments
* Secure environments without internet

---

# 🔹 `docker image load`

## ✅ Use

Load image from tar archive.

```bash
docker image load -i myimage.tar
```

---

# 🔹 `docker image import`

## ✅ Use

Create image from tar file (filesystem only).

```bash
docker image import container.tar myimage:1.0
```

With metadata:

```bash
docker image import --change "ENV APP=prod" container.tar myimage:1.0
```

⚠ Difference:

* `load` preserves layers
* `import` creates single-layer image

---

# 🔹 `docker image tag`

## ✅ Use

Create new tag reference.

```bash
docker image tag myapp:latest myrepo/myapp:v1
```

Tag for private registry:

```bash
docker image tag myapp:1.0 registry.company.com/myapp:1.0
```

🏭 Used before pushing to registry.

---

# ✅ Image Namespace Section Completed

Covers:

* Build lifecycle
* Registry operations
* Optimization
* Cleanup

---

# 🐳 4️⃣ Docker Volume Commands 

> Volumes are used for **persistent storage** outside container lifecycle.
> Used in databases, logs, production applications, and stateful workloads.

---

# 🔹 `docker volume create`

## ✅ Use

Create a new named volume.

## 📌 Syntax

```bash
docker volume create [OPTIONS] VOLUME_NAME
```

## 💻 Basic Example

```bash
docker volume create mydata
```

## 💻 Create with driver

```bash
docker volume create --driver local myvolume
```

## 💻 Create with options

```bash
docker volume create \
  --driver local \
  --opt type=none \
  --opt device=/data \
  --opt o=bind \
  mybindvolume
```

## 🏭 Production Use

* Database storage (MySQL, PostgreSQL)
* Persistent logs
* Shared data between containers
* Bind mounts for legacy apps

---

# 🔹 `docker volume ls`

## ✅ Use

List all volumes.

```bash
docker volume ls
```

Filter:

```bash
docker volume ls --filter dangling=true
```

Format:

```bash
docker volume ls --format "{{.Name}}"
```

---

# 🔹 `docker volume inspect`

## ✅ Use

Show detailed metadata of a volume.

```bash
docker volume inspect mydata
```

Output shows:

* Mountpoint path
* Driver
* Labels
* Scope

Specific field:

```bash
docker volume inspect -f '{{.Mountpoint}}' mydata
```

🏭 Used for debugging storage location.

---

# 🔹 `docker volume rm`

## ✅ Use

Remove one or more volumes.

```bash
docker volume rm mydata
```

Remove multiple:

```bash
docker volume rm v1 v2 v3
```

Force remove:

```bash
docker volume rm -f mydata
```

⚠ Cannot remove volume attached to running container unless forced.

---

# 🔹 `docker volume prune`

## ✅ Use

Remove ALL unused volumes.

```bash
docker volume prune
```

Force:

```bash
docker volume prune -f
```

With filter:

```bash
docker volume prune --filter "label!=keep"
```

🏭 Production Use
Used in disk cleanup automation to prevent storage overflow.

---

# 🔥 Real Production Example

## Run database with persistent volume

```bash
docker volume create mysql_data

docker run -d \
  --name mysql-db \
  -e MYSQL_ROOT_PASSWORD=secret \
  -v mysql_data:/var/lib/mysql \
  mysql:8.0
```

If container is removed:

```bash
docker rm -f mysql-db
```

Data still exists in:

```bash
docker volume inspect mysql_data
```

---

# 🔥 Bind Mount vs Named Volume Example

## Bind Mount

```bash
docker run -v /host/data:/app/data nginx
```

## Named Volume

```bash
docker run -v myvolume:/app/data nginx
```

---

# 🏭 Enterprise Best Practices

* Never store DB data inside container filesystem
* Always use named volumes for portability
* Use labels to manage production volumes
* Regularly prune unused volumes
* Monitor disk usage using:

```bash
docker system df
```

---

# ✅ Volume Section Completed

Covered:

* Create
* List
* Inspect
* Remove
* Prune
* Production database example
* Bind mount comparison

---

# 🐳 5️⃣ Docker Network Commands 

> Docker networking allows containers to communicate
> Used for microservices, service discovery, isolation, production clusters.

---

# 🔹 `docker network create`

## ✅ Use

Create a new network.

## 📌 Syntax

```bash id="6gtr2a"
docker network create [OPTIONS] NETWORK_NAME
```

## 💻 Basic Example (Bridge Network)

```bash id="4uv1dj"
docker network create mybridge
```

## 💻 Custom Subnet

```bash id="ph5u0v"
docker network create \
  --subnet 192.168.10.0/24 \
  mycustomnet
```

## 💻 Create Overlay Network (Swarm)

```bash id="7l7qsn"
docker network create \
  --driver overlay \
  myoverlay
```

## 🏭 Production Use

* Microservices communication
* Service isolation
* Multi-container apps

---

# 🔹 `docker network ls`

## ✅ Use

List networks.

```bash id="wq6r3g"
docker network ls
```

Filter:

```bash id="r6rqgk"
docker network ls --filter driver=bridge
```

---

# 🔹 `docker network inspect`

## ✅ Use

Display detailed network information.

```bash id="a5qlhz"
docker network inspect mybridge
```

Shows:

* Subnet
* Gateway
* Connected containers
* Driver type

Specific field:

```bash id="4jtrjw"
docker network inspect -f '{{.IPAM.Config}}' mybridge
```

---

# 🔹 `docker network connect`

## ✅ Use

Attach running container to network.

```bash id="b3p9d2"
docker network connect mybridge mycontainer
```

With specific IP:

```bash id="c5u21k"
docker network connect --ip 192.168.10.10 mycustomnet mycontainer
```

---

# 🔹 `docker network disconnect`

## ✅ Use

Remove container from network.

```bash id="u7nfd8"
docker network disconnect mybridge mycontainer
```

Force:

```bash id="g4ksjz"
docker network disconnect -f mybridge mycontainer
```

---

# 🔹 `docker network rm`

## ✅ Use

Remove network.

```bash id="jqv9et"
docker network rm mybridge
```

Remove multiple:

```bash id="6o9shw"
docker network rm net1 net2
```

⚠ Cannot remove network with active containers attached.

---

# 🔹 `docker network prune`

## ✅ Use

Remove unused networks.

```bash id="crl8vy"
docker network prune
```

Force:

```bash id="8l7n8v"
docker network prune -f
```

Filter:

```bash id="7mpkq1"
docker network prune --filter "until=24h"
```

---

# 🔥 Real Production Example

## Step 1 – Create Network

```bash id="xk7s9c"
docker network create appnet
```

## Step 2 – Run Backend

```bash id="oqv9dn"
docker run -d --name backend \
  --network appnet \
  nginx
```

## Step 3 – Run Frontend

```bash id="5nb9od"
docker run -d --name frontend \
  --network appnet \
  nginx
```

Now:

```bash id="b3oqv9"
docker exec -it frontend ping backend
```

Containers communicate via name (DNS resolution built-in).

---

# 🔥 Network Drivers Overview

Default drivers:

* bridge (default single host)
* host
* none
* overlay (Swarm multi-host)
* macvlan

Example host network:

```bash id="4lmvcn"
docker run --network host nginx
```

---

# 🏭 Enterprise Best Practices

* Always create custom bridge network (avoid default bridge)
* Use overlay for multi-node Swarm
* Use separate networks for:

  * frontend
  * backend
  * database
* Restrict exposure using internal networks
* Inspect networking issues using:

```bash id="0s8du9"
docker network inspect
```

---

# 🔥 Debugging Networking Issues

Check container IP:

```bash id="bgt5q2"
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' container
```

Check open ports:

```bash id="p9tw5x"
docker port container
```

Live events:

```bash id="5nd8rz"
docker events
```

---

# ✅ Network Section Completed

Covered:

* Create
* List
* Inspect
* Connect
* Disconnect
* Remove
* Prune
* Drivers
* Production microservice example
* Debugging

---

# 🐳 6️⃣ Docker System Commands 

> Used for disk management, cleanup, monitoring, and system-wide debugging.
> Very important in production servers to prevent disk full & resource issues.

---

# 🔹 `docker system df`

## ✅ Use

Show Docker disk usage.

## 📌 Syntax

```bash id="7kq2lm"
docker system df [OPTIONS]
```

## 💻 Basic Example

```bash id="m8x4sp"
docker system df
```

Output shows:

* Images size
* Containers size
* Volumes size
* Build cache size

## 💻 Verbose Mode

```bash id="h1vd9k"
docker system df -v
```

Shows detailed per-image and per-volume usage.

---

## 🏭 Production Use Case

When server disk is full:

```bash id="6m4pzk"
df -h
docker system df
```

Identify large images or unused volumes.

---

# 🔹 `docker system prune`

## ✅ Use

Remove unused data:

* Stopped containers
* Unused networks
* Dangling images
* Build cache

## 📌 Syntax

```bash id="u7mxqp"
docker system prune [OPTIONS]
```

## 💻 Basic Example

```bash id="0d6tqa"
docker system prune
```

## 💻 Force without confirmation

```bash id="n9x1lu"
docker system prune -f
```

## 💻 Remove ALL unused images

```bash id="s5y7eh"
docker system prune -a
```

## 💻 Remove volumes also

```bash id="w1ptzk"
docker system prune -a --volumes
```

---

## 🏭 Production Maintenance Script

```bash id="1zj8c4"
docker system prune -a -f --volumes
```

⚠ Use carefully in production.

---

# 🔹 `docker system events`

## ✅ Use

Stream real-time Docker daemon events.

## 📌 Syntax

```bash id="9l5vts"
docker system events
```

## 💻 Filter by container

```bash id="jv4d8y"
docker system events --filter container=mynginx
```

## 💻 Filter by event type

```bash id="7s3kfp"
docker system events --filter event=start
```

---

## 🏭 Production Use

* Monitoring automation
* Security auditing
* Trigger external scripts
* Incident debugging

Example:

```bash id="z2w8qf"
docker system events --since 10m
```

---

# 🔹 `docker system info`

⚠ Alias of:

```bash id="3v8l5p"
docker info
```

Shows:

* Storage driver
* CPU/memory
* Swarm status
* Logging driver
* Cgroup version

Used in:

* Troubleshooting
* Compatibility verification
* System diagnostics

---

# 🔥 Real Production Debug Workflow

## 🟥 Problem: Disk Full

```bash id="z8s0cl"
docker system df
docker image ls
docker volume ls
docker system prune -a
```

---

## 🟥 Problem: Too Many Build Cache Files

```bash id="8m5u2n"
docker builder prune
```

---

## 🟥 Problem: Unknown Container Crash

```bash id="2m0gdf"
docker system events
docker logs container
docker inspect container
```

---

# 🏭 Enterprise Best Practices

* Schedule weekly prune job (controlled)
* Monitor `/var/lib/docker` size
* Use `docker system df -v` regularly
* Avoid uncontrolled `-a --volumes` in production
* Use centralized logging

---

# ✅ Docker System Section Completed

Covered:

* Disk usage inspection
* Cleanup commands
* Real-time event monitoring
* Production troubleshooting
* Maintenance best practices

---

# 🐳 7️⃣ Docker Builder 

> BuildKit is the modern build engine used by Docker.
> It provides better caching, parallel builds, secret mounting, SSH support, and performance improvements.

Namespace: `docker builder`

---

# 🔹 `docker builder build`

⚠ Equivalent to `docker build` but explicitly uses builder namespace.

## ✅ Use

Build image using BuildKit backend.

## 📌 Syntax

```bash
docker builder build [OPTIONS] PATH
```

## 💻 Basic Example

```bash
docker builder build -t myapp:1.0 .
```

---

## 💻 Build with BuildKit enabled

Linux/macOS:

```bash
export DOCKER_BUILDKIT=1
docker builder build -t myapp:1.0 .
```

Windows PowerShell:

```powershell
$env:DOCKER_BUILDKIT=1
docker builder build -t myapp:1.0 .
```

---

## 💻 Build with no cache

```bash
docker builder build --no-cache -t myapp:latest .
```

---

## 💻 Build with build arguments

```bash
docker builder build \
  --build-arg ENV=production \
  -t myapp:prod .
```

---

## 💻 Secret Mount (BuildKit Feature)

Dockerfile:

```dockerfile
# syntax=docker/dockerfile:1.6
RUN --mount=type=secret,id=mysecret cat /run/secrets/mysecret
```

Build:

```bash
docker builder build \
  --secret id=mysecret,src=secret.txt \
  -t secureapp .
```

🏭 Used for:

* Private tokens
* API keys
* Secure credentials during build

---

## 💻 SSH Mount (Private Git Access)

Dockerfile:

```dockerfile
# syntax=docker/dockerfile:1.6
RUN --mount=type=ssh git clone git@github.com:private/repo.git
```

Build:

```bash
docker builder build --ssh default .
```

---

## 🏭 Production Use Cases

* Secure CI/CD pipelines
* Private dependency downloads
* Optimized multi-stage builds
* Faster caching and parallel layers

---

# 🔹 `docker builder prune`

## ✅ Use

Remove build cache.

## 📌 Syntax

```bash
docker builder prune [OPTIONS]
```

## 💻 Example

```bash
docker builder prune
```

Force:

```bash
docker builder prune -f
```

Remove all unused cache:

```bash
docker builder prune -a
```

Filter by time:

```bash
docker builder prune --filter until=24h
```

🏭 Used when:

* Disk full
* Excessive CI builds
* Cache corruption

---

# 🔹 `docker builder ls`

## ✅ Use

List available builders.

```bash
docker builder ls
```

Shows:

* Builder name
* Driver type
* Status
* Platforms supported

---

# 🔹 `docker builder inspect`

## ✅ Use

Inspect builder details.

```bash
docker builder inspect
```

Inspect specific:

```bash
docker builder inspect default
```

Shows:

* Driver
* Nodes
* BuildKit version
* Supported platforms

---

# 🔥 Real Production Example (Optimized Multi-Stage Build)

```dockerfile
# syntax=docker/dockerfile:1.6

FROM node:18 AS builder
WORKDIR /app
COPY package*.json .
RUN npm install
COPY . .
RUN npm run build

FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
```

Build:

```bash
docker builder build -t frontend:prod .
```

Benefits:

* Smaller image
* Clean separation
* Faster CI builds

---

# 🔥 Parallel Build Example

BuildKit automatically runs independent steps in parallel.

Enable:

```bash
export DOCKER_BUILDKIT=1
```

Then:

```bash
docker builder build .
```

Improves build performance significantly in large projects.

---

# 🏭 Enterprise Best Practices

* Always enable BuildKit
* Use multi-stage builds
* Use secret & SSH mounts
* Regularly prune build cache
* Avoid copying unnecessary files
* Use `.dockerignore`

---

# ✅ Docker Builder (BuildKit) Section Completed

Covered:

* Build
* Cache management
* Secrets
* SSH
* Multi-stage builds
* Production optimization

---

# 🐳 8️⃣ Docker Buildx 

> `buildx` is an extended build tool built on top of BuildKit.
> Used for multi-architecture builds (amd64, arm64), advanced caching, remote builders, and production CI/CD pipelines.

Namespace: `docker buildx`

---

# 🔹 `docker buildx create`

## ✅ Use

Create a new builder instance.

## 📌 Syntax

```bash id="bx1a92"
docker buildx create [OPTIONS]
```

## 💻 Basic Example

```bash id="bx2b73"
docker buildx create --name mybuilder
```

## 💻 Create & use immediately

```bash id="bx3c54"
docker buildx create --name mybuilder --use
```

## 💻 Create with docker-container driver

```bash id="bx4d65"
docker buildx create --driver docker-container --name containerbuilder
```

🏭 Used when:

* Building multi-platform images
* Using isolated builder environments
* CI/CD pipelines

---

# 🔹 `docker buildx ls`

## ✅ Use

List all builders.

```bash id="bx5e76"
docker buildx ls
```

Shows:

* Builder name
* Driver
* Status
* Supported platforms

---

# 🔹 `docker buildx inspect`

## ✅ Use

Inspect builder configuration.

```bash id="bx6f87"
docker buildx inspect
```

Inspect specific:

```bash id="bx7g98"
docker buildx inspect mybuilder
```

Bootstrap builder:

```bash id="bx8h19"
docker buildx inspect --bootstrap
```

---

# 🔹 `docker buildx use`

## ✅ Use

Switch active builder.

```bash id="bx9i20"
docker buildx use mybuilder
```

---

# 🔹 `docker buildx build`

## ✅ Use

Build multi-platform images.

## 📌 Syntax

```bash id="bx10j21"
docker buildx build [OPTIONS] PATH
```

---

## 💻 Multi-Architecture Build Example

```bash id="bx11k32"
docker buildx build \
  --platform linux/amd64,linux/arm64 \
  -t myrepo/myapp:latest \
  --push .
```

🏭 Used for:

* AWS Graviton (ARM)
* Apple Silicon (M1/M2/M3)
* Hybrid cloud environments

---

## 💻 Build & Load Locally

```bash id="bx12l43"
docker buildx build \
  --platform linux/amd64 \
  -t myapp:test \
  --load .
```

`--load` loads image into local Docker engine.

---

## 💻 Build with Cache Export

```bash id="bx13m54"
docker buildx build \
  --cache-to type=local,dest=./cache \
  --cache-from type=local,src=./cache \
  -t myapp:cached .
```

🏭 Used in CI to speed up builds.

---

## 💻 Push Directly to Registry

```bash id="bx14n65"
docker buildx build \
  --platform linux/amd64,linux/arm64 \
  -t registry.company.com/app:1.0 \
  --push .
```

No need to run separate push command.

---

# 🔹 `docker buildx stop`

## ✅ Use

Stop a running builder.

```bash id="bx15o76"
docker buildx stop mybuilder
```

---

# 🔹 `docker buildx rm`

## ✅ Use

Remove builder instance.

```bash id="bx16p87"
docker buildx rm mybuilder
```

---

# 🔹 `docker buildx prune`

## ✅ Use

Remove build cache for buildx.

```bash id="bx17q98"
docker buildx prune
```

Force:

```bash id="bx18r09"
docker buildx prune -f
```

All cache:

```bash id="bx19s10"
docker buildx prune -a
```

---

# 🔹 `docker buildx imagetools create`

## ✅ Use

Create multi-platform manifest list manually.

```bash id="bx20t11"
docker buildx imagetools create \
  -t myrepo/myapp:multi \
  myrepo/myapp:amd64 \
  myrepo/myapp:arm64
```

---

# 🔹 `docker buildx imagetools inspect`

## ✅ Use

Inspect multi-platform image.

```bash id="bx21u12"
docker buildx imagetools inspect myrepo/myapp:latest
```

Shows:

* Architectures
* Digests
* Manifest list

---

# 🔥 Real Enterprise Example

## CI/CD Multi-Platform Build

```bash id="bx22v13"
docker buildx create --use --name cicdbuilder

docker buildx build \
  --platform linux/amd64,linux/arm64 \
  -t myrepo/app:${VERSION} \
  --push .
```

Used in:

* GitHub Actions
* Jenkins pipelines
* GitLab CI

---

# 🔥 Builder Drivers Overview

Available drivers:

* docker (default)
* docker-container (recommended)
* kubernetes
* remote

Example Kubernetes builder:

```bash id="bx23w14"
docker buildx create --driver kubernetes
```

Used for cluster-based builds.

---

# 🏭 Enterprise Best Practices

* Always use `docker-container` driver
* Use `--push` for multi-platform
* Use registry cache for CI
* Avoid `--load` for multi-platform
* Use separate builders per project
* Regularly prune buildx cache

---

# ✅ Docker Buildx Section Completed

Covered:

* Builder creation
* Multi-arch builds
* Cache management
* Manifest tools
* CI/CD examples
* Enterprise best practices

---

# 🐳 9️⃣ Docker Context 

> `docker context` allows you to manage multiple Docker environments
> (local, remote servers, cloud, SSH hosts, Kubernetes, etc.)

Used in:

* Dev → Staging → Production workflows
* Remote Docker hosts
* CI/CD deployments
* Multi-cluster environments

Namespace: `docker context`

---

# 🔹 `docker context ls`

## ✅ Use

List all available Docker contexts.

```bash
docker context ls
```

Output shows:

* NAME
* DESCRIPTION
* DOCKER ENDPOINT
* CURRENT ACTIVE CONTEXT (*)

🏭 Used to verify which environment you’re connected to before running destructive commands.

---

# 🔹 `docker context create`

## ✅ Use

Create a new Docker context.

## 📌 Syntax

```bash
docker context create CONTEXT_NAME [OPTIONS]
```

---

## 💻 Create SSH-Based Remote Context

```bash
docker context create prod-server \
  --docker "host=ssh://user@192.168.1.100"
```

Now you can control remote Docker host securely.

---

## 💻 Create TCP Context

```bash
docker context create remote-tcp \
  --docker "host=tcp://192.168.1.50:2375"
```

⚠ Only use TCP with TLS enabled in production.

---

## 💻 Create Context with Description

```bash
docker context create staging \
  --description "Staging environment server" \
  --docker "host=ssh://user@staging-server"
```

---

# 🔹 `docker context use`

## ✅ Use

Switch active Docker context.

```bash
docker context use prod-server
```

Verify:

```bash
docker context ls
```

Now all commands run on that remote server.

---

# 🔹 `docker context inspect`

## ✅ Use

Inspect context configuration.

```bash
docker context inspect prod-server
```

Shows:

* Endpoint
* TLS configuration
* Metadata

---

# 🔹 `docker context rm`

## ✅ Use

Remove a context.

```bash
docker context rm staging
```

Cannot remove currently active context.

---

# 🔹 `docker context export`

## ✅ Use

Export context to file (backup/share).

```bash
docker context export prod-server > prod.dockercontext
```

Used for:

* Team sharing
* Backup
* Migration

---

# 🔹 `docker context import`

## ✅ Use

Import previously exported context.

```bash
docker context import prod-server prod.dockercontext
```

---

# 🔹 `docker context update`

## ✅ Use

Update existing context configuration.

```bash
docker context update prod-server \
  --description "Updated production server"
```

---

# 🔥 Real Enterprise Workflow Example

## Step 1 – Create Production Context

```bash
docker context create prod \
  --docker "host=ssh://admin@prod-server"
```

## Step 2 – Switch to Production

```bash
docker context use prod
```

## Step 3 – Deploy Container

```bash
docker run -d -p 80:80 nginx
```

This runs on remote production server.

---

# 🔥 Multi-Environment Setup Example

Contexts:

* default (local dev)
* staging
* production

Switch environments easily:

```bash
docker context use staging
docker compose up -d
```

Then:

```bash
docker context use production
docker compose up -d
```

---

# 🔥 Kubernetes Context (if enabled)

```bash
docker context create k8s-context \
  --kubernetes config-file=~/.kube/config
```

Used for Docker Desktop Kubernetes integration.

---

# 🏭 Enterprise Best Practices

* Always verify active context before running:

```bash
docker context ls
```

* Use SSH instead of plain TCP
* Use separate contexts for:

  * Dev
  * QA
  * Staging
  * Production
* Never run `docker system prune -a` on wrong context
* Use role-based SSH access

---

# 🔎 Debugging Remote Context

Check connectivity:

```bash
docker --context prod info
```

Test specific context without switching:

```bash
docker --context prod ps
```

---

# ✅ Docker Context Section Completed

Covered:

* Create
* Use
* Inspect
* Update
* Export / Import
* Remote SSH deployment
* Multi-environment management
* Enterprise workflow

---

# 🐳 🔟 Docker Compose 

> `docker compose` (v2) is integrated into Docker CLI.
> Used for multi-container applications, microservices, dev environments, staging, and production deployments.

Namespace: `docker compose`

---

# 🔹 `docker compose up`

## ✅ Use

Create and start services defined in `docker-compose.yml`.

## 📌 Syntax

```bash id="cmp01"
docker compose up [OPTIONS]
```

## 💻 Basic Example

```bash id="cmp02"
docker compose up
```

## 💻 Detached Mode

```bash id="cmp03"
docker compose up -d
```

## 💻 Force Rebuild

```bash id="cmp04"
docker compose up --build
```

## 💻 Scale Services

```bash id="cmp05"
docker compose up --scale web=3 -d
```

🏭 Used for:

* Starting full app stack
* Local development
* Production-like staging

---

# 🔹 `docker compose down`

## ✅ Use

Stop and remove containers, networks.

```bash id="cmp06"
docker compose down
```

Remove volumes:

```bash id="cmp07"
docker compose down -v
```

Remove images:

```bash id="cmp08"
docker compose down --rmi all
```

---

# 🔹 `docker compose build`

## ✅ Use

Build or rebuild services.

```bash id="cmp09"
docker compose build
```

No cache:

```bash id="cmp10"
docker compose build --no-cache
```

---

# 🔹 `docker compose pull`

## ✅ Use

Pull service images.

```bash id="cmp11"
docker compose pull
```

Specific service:

```bash id="cmp12"
docker compose pull web
```

---

# 🔹 `docker compose push`

## ✅ Use

Push service images to registry.

```bash id="cmp13"
docker compose push
```

---

# 🔹 `docker compose ps`

## ✅ Use

List running services.

```bash id="cmp14"
docker compose ps
```

---

# 🔹 `docker compose logs`

## ✅ Use

View logs from services.

```bash id="cmp15"
docker compose logs
```

Follow:

```bash id="cmp16"
docker compose logs -f
```

Specific service:

```bash id="cmp17"
docker compose logs web
```

---

# 🔹 `docker compose exec`

## ✅ Use

Run command inside service container.

```bash id="cmp18"
docker compose exec web bash
```

Run one command:

```bash id="cmp19"
docker compose exec db mysql -u root -p
```

---

# 🔹 `docker compose run`

## ✅ Use

Run one-off command.

```bash id="cmp20"
docker compose run web npm install
```

No dependencies:

```bash id="cmp21"
docker compose run --no-deps web bash
```

---

# 🔹 `docker compose restart`

```bash id="cmp22"
docker compose restart
```

Specific service:

```bash id="cmp23"
docker compose restart web
```

---

# 🔹 `docker compose stop`

```bash id="cmp24"
docker compose stop
```

---

# 🔹 `docker compose start`

```bash id="cmp25"
docker compose start
```

---

# 🔹 `docker compose pause`

```bash id="cmp26"
docker compose pause
```

---

# 🔹 `docker compose unpause`

```bash id="cmp27"
docker compose unpause
```

---

# 🔹 `docker compose config`

## ✅ Use

Validate and view merged configuration.

```bash id="cmp28"
docker compose config
```

Useful for debugging env variables and overrides.

---

# 🔹 `docker compose events`

## ✅ Use

Stream service events.

```bash id="cmp29"
docker compose events
```

---

# 🔹 `docker compose images`

## ✅ Use

List images used by services.

```bash id="cmp30"
docker compose images
```

---

# 🔹 `docker compose kill`

```bash id="cmp31"
docker compose kill
```

---

# 🔹 `docker compose rm`

Remove stopped containers.

```bash id="cmp32"
docker compose rm
```

Force:

```bash id="cmp33"
docker compose rm -f
```

---

# 🔹 `docker compose create`

Create containers without starting.

```bash id="cmp34"
docker compose create
```

---

# 🔹 `docker compose cp`

Copy files between service container and host.

```bash id="cmp35"
docker compose cp web:/app/file.txt .
```

---

# 🔹 `docker compose top`

Show running processes.

```bash id="cmp36"
docker compose top
```

---

# 🔹 `docker compose version`

```bash id="cmp37"
docker compose version
```

---

# 🔥 Real Production Example (Full Stack)

### docker-compose.yml

```yaml id="cmp38"
version: "3.9"

services:
  web:
    image: nginx
    ports:
      - "80:80"
    networks:
      - appnet

  db:
    image: mysql:8
    environment:
      MYSQL_ROOT_PASSWORD: secret
    volumes:
      - dbdata:/var/lib/mysql
    networks:
      - appnet

networks:
  appnet:

volumes:
  dbdata:
```

Start:

```bash id="cmp39"
docker compose up -d
```

---

# 🏭 Enterprise Best Practices

* Always use `.env` file
* Separate dev & prod configs
* Use `docker compose config` before deploy
* Use restart policies in production
* Avoid exposing DB ports publicly
* Combine with `docker context` for remote deployment
* Use `docker compose pull && docker compose up -d` for rolling updates

---

# 🔥 CI/CD Deployment Example

```bash id="cmp40"
docker compose pull
docker compose up -d --remove-orphans
```

---

# ✅ Docker Compose Section Completed

Covered:

* Full CLI commands
* Production workflow
* CI/CD usage
* Debugging
* Multi-service deployment
* Enterprise best practices

---

# 🐳 1️⃣1️⃣ Docker Swarm 

> Docker Swarm is Docker’s native clustering and orchestration tool.
> Used for managing multi-node production clusters.

Namespaces covered:

* `docker swarm`
* `docker node`
* `docker service`
* `docker stack`

---

# 🔹 `docker swarm` (Cluster Management)

---

## 🔸 `docker swarm init`

### ✅ Use

Initialize a new swarm cluster (create manager node).

```bash id="sw01"
docker swarm init
```

Specify advertise address:

```bash id="sw02"
docker swarm init --advertise-addr 192.168.1.10
```

Custom subnet:

```bash id="sw03"
docker swarm init --default-addr-pool 10.10.0.0/16
```

---

## 🔸 `docker swarm join`

### ✅ Use

Join a node to existing swarm.

Worker:

```bash id="sw04"
docker swarm join --token <worker-token> MANAGER_IP:2377
```

Manager:

```bash id="sw05"
docker swarm join --token <manager-token> MANAGER_IP:2377
```

Get token:

```bash id="sw06"
docker swarm join-token worker
docker swarm join-token manager
```

---

## 🔸 `docker swarm leave`

```bash id="sw07"
docker swarm leave
```

Force (manager):

```bash id="sw08"
docker swarm leave --force
```

---

## 🔸 `docker swarm update`

Update swarm configuration.

```bash id="sw09"
docker swarm update --dispatcher-heartbeat 10s
```

---

## 🔸 `docker swarm unlock`

Unlock encrypted swarm after restart.

```bash id="sw10"
docker swarm unlock
```

---

## 🔸 `docker swarm unlock-key`

Show unlock key.

```bash id="sw11"
docker swarm unlock-key
```

Rotate key:

```bash id="sw12"
docker swarm unlock-key --rotate
```

---

## 🔸 `docker swarm ca`

Manage swarm certificate authority.

```bash id="sw13"
docker swarm ca
```

Rotate CA:

```bash id="sw14"
docker swarm ca --rotate
```

---

# 🔹 `docker node` (Cluster Nodes)

---

## 🔸 `docker node ls`

```bash id="sw15"
docker node ls
```

---

## 🔸 `docker node inspect`

```bash id="sw16"
docker node inspect node_id
```

Pretty format:

```bash id="sw17"
docker node inspect --pretty node_id
```

---

## 🔸 `docker node update`

Drain node:

```bash id="sw18"
docker node update --availability drain node_id
```

Set active:

```bash id="sw19"
docker node update --availability active node_id
```

---

## 🔸 `docker node rm`

```bash id="sw20"
docker node rm node_id
```

---

## 🔸 `docker node promote`

```bash id="sw21"
docker node promote node_id
```

---

## 🔸 `docker node demote`

```bash id="sw22"
docker node demote node_id
```

---

# 🔹 `docker service` (Deploy Services)

---

## 🔸 `docker service create`

### ✅ Use

Create service in swarm.

```bash id="sw23"
docker service create --name web nginx
```

With replicas:

```bash id="sw24"
docker service create --name web --replicas 3 nginx
```

Port publish:

```bash id="sw25"
docker service create \
  --name web \
  --replicas 3 \
  -p 80:80 nginx
```

Attach to network:

```bash id="sw26"
docker service create \
  --network myoverlay \
  nginx
```

Limit resources:

```bash id="sw27"
docker service create \
  --limit-memory 512m \
  --limit-cpu 1 \
  nginx
```

---

## 🔸 `docker service ls`

```bash id="sw28"
docker service ls
```

---

## 🔸 `docker service inspect`

```bash id="sw29"
docker service inspect web
```

Pretty:

```bash id="sw30"
docker service inspect --pretty web
```

---

## 🔸 `docker service ps`

Show tasks (containers under service).

```bash id="sw31"
docker service ps web
```

---

## 🔸 `docker service logs`

```bash id="sw32"
docker service logs web
```

Follow:

```bash id="sw33"
docker service logs -f web
```

---

## 🔸 `docker service update`

Update service:

```bash id="sw34"
docker service update --image nginx:latest web
```

Scale:

```bash id="sw35"
docker service update --replicas 5 web
```

Add env:

```bash id="sw36"
docker service update --env-add ENV=prod web
```

---

## 🔸 `docker service scale`

```bash id="sw37"
docker service scale web=10
```

---

## 🔸 `docker service rollback`

Rollback to previous version:

```bash id="sw38"
docker service rollback web
```

---

## 🔸 `docker service rm`

```bash id="sw39"
docker service rm web
```

---

# 🔹 `docker stack` (Deploy Compose in Swarm)

---

## 🔸 `docker stack deploy`

Deploy stack using compose file:

```bash id="sw40"
docker stack deploy -c docker-compose.yml mystack
```

---

## 🔸 `docker stack ls`

```bash id="sw41"
docker stack ls
```

---

## 🔸 `docker stack services`

```bash id="sw42"
docker stack services mystack
```

---

## 🔸 `docker stack ps`

```bash id="sw43"
docker stack ps mystack
```

---

## 🔸 `docker stack rm`

```bash id="sw44"
docker stack rm mystack
```

---

# 🔥 Real Enterprise Deployment Example

### Step 1 – Initialize Cluster

```bash id="sw45"
docker swarm init --advertise-addr 10.0.0.10
```

### Step 2 – Create Overlay Network

```bash id="sw46"
docker network create --driver overlay appnet
```

### Step 3 – Deploy Service

```bash id="sw47"
docker service create \
  --name web \
  --replicas 3 \
  --network appnet \
  -p 80:80 nginx
```

### Step 4 – Scale

```bash id="sw48"
docker service scale web=5
```

---

# 🏭 Enterprise Best Practices

* Always use overlay networks
* Use replicas >1 for high availability
* Use resource limits
* Use rolling updates
* Backup unlock key
* Use drain mode before maintenance
* Use `docker stack deploy` for multi-service apps
* Never run workloads on manager nodes (best practice)

---

# 🔎 Debug Swarm Issues

Check service tasks:

```bash id="sw49"
docker service ps web
```

Check node status:

```bash id="sw50"
docker node ls
```

Inspect failed container:

```bash id="sw51"
docker service logs web
```

---

# ✅ Docker Swarm Section Completed

Covered:

* Swarm init/join
* Node management
* Service lifecycle
* Scaling & rollback
* Stack deployment
* Overlay networking
* Enterprise production practices

---

# 🐳 1️⃣2️⃣ Docker Plugin 

> Docker plugins extend Docker functionality.
> Used for:

* External storage drivers (NFS, EBS, Ceph)
* Network drivers
* Logging drivers
* Volume drivers in production clusters

Namespace: `docker plugin`

---

# 🔹 `docker plugin ls`

## ✅ Use

List installed plugins.

```bash id="pl01"
docker plugin ls
```

Output shows:

* Plugin ID
* Name
* Description
* Enabled status

---

# 🔹 `docker plugin inspect`

## ✅ Use

Show detailed plugin information.

```bash id="pl02"
docker plugin inspect PLUGIN_NAME
```

Example:

```bash id="pl03"
docker plugin inspect vieux/sshfs
```

Shows:

* Capabilities
* Mount configuration
* Required permissions

---

# 🔹 `docker plugin install`

## ✅ Use

Install plugin from Docker Hub or registry.

```bash id="pl04"
docker plugin install PLUGIN_NAME
```

Example:

```bash id="pl05"
docker plugin install vieux/sshfs
```

Grant permissions automatically:

```bash id="pl06"
docker plugin install vieux/sshfs --grant-all-permissions
```

Disable at install:

```bash id="pl07"
docker plugin install vieux/sshfs --disable
```

---

# 🔹 `docker plugin enable`

## ✅ Use

Enable installed plugin.

```bash id="pl08"
docker plugin enable vieux/sshfs
```

---

# 🔹 `docker plugin disable`

## ✅ Use

Disable plugin.

```bash id="pl09"
docker plugin disable vieux/sshfs
```

Force disable:

```bash id="pl10"
docker plugin disable -f vieux/sshfs
```

⚠ Cannot disable if in use.

---

# 🔹 `docker plugin rm`

## ✅ Use

Remove plugin.

```bash id="pl11"
docker plugin rm vieux/sshfs
```

Force remove:

```bash id="pl12"
docker plugin rm -f vieux/sshfs
```

---

# 🔹 `docker plugin upgrade`

## ✅ Use

Upgrade installed plugin.

```bash id="pl13"
docker plugin upgrade vieux/sshfs
```

With permissions:

```bash id="pl14"
docker plugin upgrade vieux/sshfs --grant-all-permissions
```

---

# 🔹 `docker plugin create`

## ✅ Use

Create plugin from rootfs and config.

```bash id="pl15"
docker plugin create myplugin ./plugin-rootfs
```

Used by plugin developers.

---

# 🔹 `docker plugin push`

## ✅ Use

Push plugin to registry.

```bash id="pl16"
docker plugin push myplugin
```

---

# 🔹 `docker plugin set`

## ✅ Use

Set plugin configuration values.

```bash id="pl17"
docker plugin set vieux/sshfs DEBUG=1
```

Requires plugin disable → set → enable cycle.

---

# 🔥 Real Production Example (NFS Volume Plugin)

## Install NFS Plugin

```bash id="pl18"
docker plugin install vieux/sshfs --grant-all-permissions
```

## Create Volume Using Plugin

```bash id="pl19"
docker volume create \
  -d vieux/sshfs \
  -o sshcmd=user@192.168.1.100:/data \
  -o password=secret \
  sshvolume
```

## Run Container with Plugin Volume

```bash id="pl20"
docker run -d -v sshvolume:/app/data nginx
```

---

# 🔥 Network Plugin Example

Install custom network plugin:

```bash id="pl21"
docker plugin install weaveworks/net-plugin --grant-all-permissions
```

Create network using plugin:

```bash id="pl22"
docker network create -d weave mynet
```

---

# 🏭 Enterprise Best Practices

* Only install trusted plugins
* Always inspect permissions before enabling
* Avoid unnecessary plugin permissions
* Backup configuration before upgrade
* Monitor plugin compatibility after Docker upgrades
* Use plugins mainly in Swarm or production clusters

---

# 🔎 Debug Plugin Issues

List plugins:

```bash id="pl23"
docker plugin ls
```

Inspect:

```bash id="pl24"
docker plugin inspect PLUGIN_NAME
```

Check daemon logs if plugin fails.

---

# ✅ Docker Plugin Section Completed

Covered:

* Install
* Enable / Disable
* Remove
* Upgrade
* Create / Push
* Configure
* Production volume example
* Network plugin example
* Enterprise best practices

---

# 🐳 1️⃣3️⃣ Docker Trust 

> Docker Trust uses **Notary** for image signing and verification.
> Ensures images are signed and verified before pull.
> Used in enterprise production environments for supply chain security.

Namespace: `docker trust`

---

# 🔐 Enable Docker Content Trust

Before using trust:

```bash id="tr01"
export DOCKER_CONTENT_TRUST=1
```

Windows PowerShell:

```powershell id="tr02"
$env:DOCKER_CONTENT_TRUST=1
```

Now Docker will only pull signed images.

---

# 🔹 `docker trust key generate`

## ✅ Use

Generate new signing key.

```bash id="tr03"
docker trust key generate mysigner
```

Creates:

* Private key
* Public key

Used to sign images.

---

# 🔹 `docker trust key load`

## ✅ Use

Load existing private key.

```bash id="tr04"
docker trust key load mykey.pem --name mysigner
```

Used when migrating to new system.

---

# 🔹 `docker trust sign`

## ✅ Use

Sign image with your private key.

## 📌 Syntax

```bash id="tr05"
docker trust sign IMAGE:TAG
```

## 💻 Example

```bash id="tr06"
docker trust sign myrepo/myapp:1.0
```

After signing:

* Signature stored in Notary server
* Registry now has trusted metadata

---

# 🔹 `docker trust inspect`

## ✅ Use

Inspect image signature information.

```bash id="tr07"
docker trust inspect myrepo/myapp:1.0
```

Pretty output:

```bash id="tr08"
docker trust inspect --pretty myrepo/myapp:1.0
```

Shows:

* Signed by
* Signer keys
* Timestamp
* Digest

---

# 🔹 `docker trust revoke`

## ✅ Use

Revoke image signature.

```bash id="tr09"
docker trust revoke myrepo/myapp:1.0
```

Used if:

* Key compromised
* Image should no longer be trusted

---

# 🔹 `docker trust signer add`

## ✅ Use

Add additional signer to repository.

```bash id="tr10"
docker trust signer add --key signer.pub newSigner myrepo/myapp
```

Used for:

* Team-based signing
* Multiple authorized maintainers

---

# 🔹 `docker trust signer remove`

## ✅ Use

Remove signer from repository.

```bash id="tr11"
docker trust signer remove oldSigner myrepo/myapp
```

---

# 🔥 Full Enterprise Workflow Example

## Step 1 – Generate Key

```bash id="tr12"
docker trust key generate prodSigner
```

## Step 2 – Build & Push Image

```bash id="tr13"
docker build -t myrepo/app:1.0 .
docker push myrepo/app:1.0
```

## Step 3 – Sign Image

```bash id="tr14"
docker trust sign myrepo/app:1.0
```

## Step 4 – Verify

```bash id="tr15"
docker trust inspect --pretty myrepo/app:1.0
```

---

# 🔥 Enforced Pull (Secure Environment)

Enable trust:

```bash id="tr16"
export DOCKER_CONTENT_TRUST=1
```

Now:

```bash id="tr17"
docker pull myrepo/app:1.0
```

If image is not signed → pull fails.

---

# 🔐 Security Benefits

* Protect against tampered images
* Verify publisher identity
* Secure CI/CD pipeline
* Prevent unauthorized image deployment
* Ensure immutability

---

# 🏭 Enterprise Best Practices

* Always enable content trust in production
* Store private keys securely
* Rotate keys periodically
* Backup signing keys
* Use multiple signers for large teams
* Combine with:

  * Private registry
  * Role-based access
  * Image scanning (Docker Scout)

---

# ⚠ Important Notes

* Docker Trust uses Notary v1
* Some environments moving to:

  * Sigstore
  * Cosign
  * Notary v2

But `docker trust` still widely used in enterprise setups.

---

# 🔎 Debug Trust Issues

Check signatures:

```bash id="tr18"
docker trust inspect IMAGE:TAG
```

Disable trust temporarily:

```bash id="tr19"
export DOCKER_CONTENT_TRUST=0
```

---

# ✅ Docker Trust Section Completed

Covered:

* Key generation
* Signing images
* Inspecting signatures
* Revoking signatures
* Adding/removing signers
* Enforcing signed image pull
* Enterprise workflow
* Security best practices

---

# 🐳 1️⃣4️⃣ Docker Checkpoint 

> Docker Checkpoint allows you to **freeze a running container and save its state**.
> It uses **CRIU (Checkpoint/Restore In Userspace)**.

Used for:

* Live migration
* Debugging
* Fast recovery
* High availability experiments
* Stateful container pause/resume

Namespace: `docker checkpoint`

⚠ Linux only feature.
⚠ Requires CRIU installed and compatible kernel.

---

# 🔹 `docker checkpoint create`

## ✅ Use

Create a checkpoint of a running container.

## 📌 Syntax

```bash id="cp01"
docker checkpoint create [OPTIONS] CONTAINER CHECKPOINT_NAME
```

## 💻 Basic Example

```bash id="cp02"
docker checkpoint create mycontainer checkpoint1
```

This:

* Freezes container
* Saves memory state
* Saves process state
* Stores under `/var/lib/docker/containers/...`

---

## 💻 Leave Container Running After Checkpoint

```bash id="cp03"
docker checkpoint create --leave-running mycontainer checkpoint2
```

Useful for:

* Backup state without stopping service

---

# 🔹 `docker checkpoint ls`

## ✅ Use

List checkpoints of a container.

```bash id="cp04"
docker checkpoint ls mycontainer
```

Output:

* Checkpoint name
* Creation time

---

# 🔹 `docker checkpoint rm`

## ✅ Use

Remove a specific checkpoint.

```bash id="cp05"
docker checkpoint rm mycontainer checkpoint1
```

Remove multiple:

```bash id="cp06"
docker checkpoint rm mycontainer checkpoint1 checkpoint2
```

---

# 🔥 Restore Container From Checkpoint

Stop container first:

```bash id="cp07"
docker stop mycontainer
```

Start from checkpoint:

```bash id="cp08"
docker start --checkpoint checkpoint1 mycontainer
```

Container resumes from saved state.

---

# 🔥 Real Example – Long Running Process

Run container:

```bash id="cp09"
docker run -d --name test ubuntu sleep 1000
```

Create checkpoint:

```bash id="cp10"
docker checkpoint create test snap1
```

Stop container:

```bash id="cp11"
docker stop test
```

Restore:

```bash id="cp12"
docker start --checkpoint snap1 test
```

Container resumes as if never stopped.

---

# 🔥 Live Migration Concept (Advanced Use)

On Host A:

```bash id="cp13"
docker checkpoint create app check1
```

Copy checkpoint data to Host B
Restore container with same image and configuration.

⚠ Requires identical environment and storage.

---

# 🏭 Enterprise Use Cases

* Research environments
* Stateful simulation systems
* Long-running batch jobs
* HPC workloads
* Testing failover mechanisms
* Debugging production issues

---

# ⚠ Requirements

* Linux host
* CRIU installed
* Matching Docker versions
* Compatible kernel features enabled

Check CRIU:

```bash id="cp14"
criu check
```

---

# ⚠ Limitations

* Not supported on Windows
* Not fully supported on Docker Desktop
* Not ideal for production HA systems
* Does not replace proper orchestration
* Limited support with some storage drivers

---

# 🔎 Debug Checkpoint Issues

Check daemon logs:

```bash id="cp15"
journalctl -u docker
```

Verify CRIU:

```bash id="cp16"
criu --version
```

---

# 🏭 Enterprise Best Practices

* Use for testing only (rare in production)
* Prefer Swarm/Kubernetes for HA
* Ensure same image digest before restore
* Clean unused checkpoints regularly

---

# ✅ Docker Checkpoint Section Completed

Covered:

* Create checkpoint
* List checkpoints
* Remove checkpoint
* Restore from checkpoint
* Live migration concept
* CRIU requirements
* Limitations
* Enterprise usage scenarios

---

# 🐳 1️⃣5️⃣ Docker Config 

> `docker config` is used in **Docker Swarm** to manage configuration files securely.
> Configs are mounted into services as files.
> Used for:

* Application config files
* Nginx config
* App settings
* Non-sensitive configuration

⚠ Only works in Swarm mode.

Namespace: `docker config`

---

# 🔹 `docker config create`

## ✅ Use

Create a new config from file or STDIN.

## 📌 Syntax

```bash id="cfg01"
docker config create CONFIG_NAME FILE
```

---

## 💻 Example – Create Config from File

```bash id="cfg02"
docker config create nginx_conf nginx.conf
```

---

## 💻 Create from STDIN

```bash id="cfg03"
cat nginx.conf | docker config create nginx_conf -
```

---

## 💻 Add Labels

```bash id="cfg04"
docker config create \
  --label env=prod \
  app_config app.conf
```

---

# 🔹 `docker config ls`

## ✅ Use

List all configs.

```bash id="cfg05"
docker config ls
```

Filter:

```bash id="cfg06"
docker config ls --filter name=nginx
```

---

# 🔹 `docker config inspect`

## ✅ Use

Inspect config metadata.

```bash id="cfg07"
docker config inspect nginx_conf
```

Pretty output:

```bash id="cfg08"
docker config inspect --pretty nginx_conf
```

Shows:

* ID
* Created time
* Labels

---

# 🔹 `docker config rm`

## ✅ Use

Remove a config.

```bash id="cfg09"
docker config rm nginx_conf
```

⚠ Cannot remove config if attached to running service.

---

# 🔥 Use Config in Service

## Step 1 – Create Config

```bash id="cfg10"
docker config create nginx_conf nginx.conf
```

## Step 2 – Deploy Service with Config

```bash id="cfg11"
docker service create \
  --name web \
  --config source=nginx_conf,target=/etc/nginx/nginx.conf \
  nginx
```

Config will be mounted as:

```
/etc/nginx/nginx.conf
```

---

# 🔥 Use Config with Stack (Compose in Swarm)

### docker-compose.yml

```yaml id="cfg12"
version: "3.9"

services:
  web:
    image: nginx
    configs:
      - source: nginx_conf
        target: /etc/nginx/nginx.conf

configs:
  nginx_conf:
    file: ./nginx.conf
```

Deploy:

```bash id="cfg13"
docker stack deploy -c docker-compose.yml mystack
```

---

# 🔥 Update Config Workflow

⚠ Configs are immutable.
To update:

1️⃣ Create new config

```bash id="cfg14"
docker config create nginx_conf_v2 nginx.conf
```

2️⃣ Update service

```bash id="cfg15"
docker service update \
  --config-rm nginx_conf \
  --config-add source=nginx_conf_v2,target=/etc/nginx/nginx.conf \
  web
```

3️⃣ Remove old config

```bash id="cfg16"
docker config rm nginx_conf
```

---

# 🏭 Enterprise Use Cases

* Nginx config
* App properties file
* Feature flags
* Service configuration
* Non-sensitive environment settings
* Multi-node distributed configuration

---

# 🔐 Config vs Secret

| Feature           | Config     | Secret             |
| ----------------- | ---------- | ------------------ |
| Sensitive data    | ❌ No       | ✅ Yes              |
| Encrypted at rest | ❌          | ✅                  |
| Use case          | App config | Passwords/API keys |
| Swarm only        | ✅          | ✅                  |

---

# 🏭 Enterprise Best Practices

* Use config for non-sensitive data only
* Use secret for credentials
* Version configs (config_v1, config_v2)
* Avoid storing secrets in configs
* Use labels to identify environment
* Use stack deploy for multi-service setups

---

# 🔎 Debug Config Issues

Check service:

```bash id="cfg17"
docker service inspect web
```

Check mounted file inside container:

```bash id="cfg18"
docker exec -it container_id cat /etc/nginx/nginx.conf
```

---

# ✅ Docker Config Section Completed

Covered:

* Create
* List
* Inspect
* Remove
* Attach to service
* Stack usage
* Update workflow
* Enterprise best practices

---

# 🐳 1️⃣6️⃣ Docker Secret 

> `docker secret` is used in **Docker Swarm** to securely manage sensitive data.
> Secrets are encrypted at rest and in transit.
> Used for:

* Database passwords
* API keys
* TLS certificates
* Private keys
* Tokens

⚠ Works only in Swarm mode.
⚠ Secrets are mounted inside containers as in-memory files.

Namespace: `docker secret`

---

# 🔹 `docker secret create`

## ✅ Use

Create a new secret from file or STDIN.

## 📌 Syntax

```bash id="sec01"
docker secret create SECRET_NAME FILE
```

---

## 💻 Example – Create Secret from File

```bash id="sec02"
docker secret create db_password db_pass.txt
```

---

## 💻 Create from STDIN

```bash id="sec03"
echo "myStrongPassword" | docker secret create db_password -
```

---

## 💻 Add Labels

```bash id="sec04"
docker secret create \
  --label env=prod \
  api_token token.txt
```

---

# 🔹 `docker secret ls`

## ✅ Use

List all secrets.

```bash id="sec05"
docker secret ls
```

Filter:

```bash id="sec06"
docker secret ls --filter name=db
```

---

# 🔹 `docker secret inspect`

## ✅ Use

Inspect secret metadata.

```bash id="sec07"
docker secret inspect db_password
```

Pretty:

```bash id="sec08"
docker secret inspect --pretty db_password
```

⚠ Does NOT show secret content (for security).

---

# 🔹 `docker secret rm`

## ✅ Use

Remove secret.

```bash id="sec09"
docker secret rm db_password
```

⚠ Cannot remove if used by running service.

---

# 🔥 Use Secret in Service

## Step 1 – Create Secret

```bash id="sec10"
docker secret create db_password db_pass.txt
```

## Step 2 – Deploy Service Using Secret

```bash id="sec11"
docker service create \
  --name mysql \
  --secret db_password \
  -e MYSQL_ROOT_PASSWORD_FILE=/run/secrets/db_password \
  mysql:8
```

Secret is mounted at:

```id="a12sdd"
/run/secrets/db_password
```

Container reads password from file.

---

# 🔥 Use Secret in Stack (Compose in Swarm)

### docker-compose.yml

```yaml id="sec12"
version: "3.9"

services:
  db:
    image: mysql:8
    secrets:
      - db_password
    environment:
      MYSQL_ROOT_PASSWORD_FILE: /run/secrets/db_password

secrets:
  db_password:
    file: ./db_pass.txt
```

Deploy:

```bash id="sec13"
docker stack deploy -c docker-compose.yml mystack
```

---

# 🔥 Update Secret Workflow

⚠ Secrets are immutable.

To update:

1️⃣ Create new secret

```bash id="sec14"
docker secret create db_password_v2 new_pass.txt
```

2️⃣ Update service

```bash id="sec15"
docker service update \
  --secret-rm db_password \
  --secret-add db_password_v2 \
  mysql
```

3️⃣ Remove old secret

```bash id="sec16"
docker secret rm db_password
```

---

# 🔐 Secret Security Features

* Encrypted at rest in Raft logs
* Encrypted in transit between nodes
* Only accessible to assigned services
* Stored in memory (tmpfs)
* Not visible in `docker inspect`

---

# 🔐 Secret vs Config Comparison

| Feature        | Config | Secret |
| -------------- | ------ | ------ |
| Encrypted      | ❌      | ✅      |
| Sensitive data | ❌      | ✅      |
| Mounted path   | File   | File   |
| Swarm only     | ✅      | ✅      |

---

# 🏭 Enterprise Use Cases

* Database credentials
* TLS certificates
* OAuth tokens
* SSH private keys
* Internal API keys
* License keys

---

# 🏭 Enterprise Best Practices

* Never store passwords in environment variables
* Use `_FILE` pattern for apps
* Rotate secrets regularly
* Use different secrets per environment
* Limit secret access to specific services
* Never commit secret files to Git

---

# 🔎 Debug Secret Issues

Check service:

```bash id="sec17"
docker service inspect mysql
```

Check mounted file:

```bash id="sec18"
docker exec -it container_id ls /run/secrets
```

Verify secret exists:

```bash id="sec19"
docker secret ls
```

---

# ⚠ Important Notes

* Only available in Swarm
* Cannot access secrets in standalone containers
* Maximum size ~500KB
* Immutable once created

---

# ✅ Docker Secret Section Completed

Covered:

* Create
* List
* Inspect
* Remove
* Attach to service
* Stack usage
* Secret update workflow
* Security model
* Enterprise best practices

---

# 🐳 1️⃣7️⃣ Docker Manifest 

> `docker manifest` is used to create and manage **multi-platform image manifests**.
> It allows one image tag to support multiple architectures (amd64, arm64, etc.).

Used for:

* Apple Silicon (M1/M2/M3)
* AWS Graviton (ARM)
* Mixed architecture clusters
* Enterprise production registries

Namespace: `docker manifest`

---

# 🔹 `docker manifest create`

## ✅ Use

Create a new manifest list (multi-arch image).

## 📌 Syntax

```bash id="mf01"
docker manifest create MANIFEST_LIST IMAGE1 IMAGE2 ...
```

---

## 💻 Example – Create Multi-Arch Manifest

```bash id="mf02"
docker manifest create myrepo/app:latest \
  myrepo/app:amd64 \
  myrepo/app:arm64
```

This combines two architecture images under one tag.

---

# 🔹 `docker manifest inspect`

## ✅ Use

Inspect manifest list.

```bash id="mf03"
docker manifest inspect myrepo/app:latest
```

Verbose:

```bash id="mf04"
docker manifest inspect --verbose myrepo/app:latest
```

Shows:

* Platform architecture
* Digest
* OS
* Variant

---

# 🔹 `docker manifest annotate`

## ✅ Use

Add architecture metadata to image inside manifest.

```bash id="mf05"
docker manifest annotate \
  myrepo/app:latest \
  myrepo/app:arm64 \
  --os linux \
  --arch arm64
```

With variant:

```bash id="mf06"
docker manifest annotate \
  myrepo/app:latest \
  myrepo/app:arm64 \
  --variant v8
```

Used to define platform details manually.

---

# 🔹 `docker manifest push`

## ✅ Use

Push manifest list to registry.

```bash id="mf07"
docker manifest push myrepo/app:latest
```

With purge (remove local manifest after push):

```bash id="mf08"
docker manifest push --purge myrepo/app:latest
```

---

# 🔹 `docker manifest rm`

## ✅ Use

Remove local manifest list.

```bash id="mf09"
docker manifest rm myrepo/app:latest
```

---

# 🔥 Full Enterprise Workflow Example

## Step 1 – Build Architecture Images

```bash id="mf10"
docker build -t myrepo/app:amd64 --platform linux/amd64 .
docker build -t myrepo/app:arm64 --platform linux/arm64 .
```

Push both:

```bash id="mf11"
docker push myrepo/app:amd64
docker push myrepo/app:arm64
```

---

## Step 2 – Create Manifest

```bash id="mf12"
docker manifest create myrepo/app:latest \
  myrepo/app:amd64 \
  myrepo/app:arm64
```

---

## Step 3 – Annotate (Optional)

```bash id="mf13"
docker manifest annotate myrepo/app:latest \
  myrepo/app:arm64 --arch arm64
```

---

## Step 4 – Push Manifest

```bash id="mf14"
docker manifest push myrepo/app:latest
```

Now:

```bash id="mf15"
docker pull myrepo/app:latest
```

Docker automatically pulls correct architecture.

---

# 🔥 Manifest vs Buildx

| Feature                   | Manifest | Buildx |
| ------------------------- | -------- | ------ |
| Manual multi-arch         | ✅        | ❌      |
| Auto multi-arch build     | ❌        | ✅      |
| Recommended modern method | ❌        | ✅      |
| CI/CD friendly            | ⚠        | ✅      |

👉 Modern approach:

```bash id="mf16"
docker buildx build \
  --platform linux/amd64,linux/arm64 \
  -t myrepo/app:latest \
  --push .
```

---

# 🏭 Enterprise Use Cases

* Supporting multiple CPU architectures
* Public Docker Hub images
* Hybrid cloud environments
* Kubernetes clusters with mixed nodes
* Edge computing deployments

---

# 🔎 Debug Multi-Arch Issues

Inspect image:

```bash id="mf17"
docker manifest inspect myrepo/app:latest
```

Check platform:

```bash id="mf18"
docker inspect myrepo/app:latest
```

Force architecture pull:

```bash id="mf19"
docker pull --platform linux/amd64 myrepo/app:latest
```

---

# 🏭 Enterprise Best Practices

* Prefer `docker buildx` for multi-arch
* Use manifest only when manual control required
* Always push architecture-specific tags
* Verify digest before creating manifest
* Test each architecture separately
* Use CI pipeline for automation

---

# ⚠ Important Notes

* Manifest is client-side operation
* Requires registry support
* Not required if using Buildx with `--push`
* Multi-arch images are critical for ARM cloud providers

---

# ✅ Docker Manifest Section Completed

Covered:

* Create
* Inspect
* Annotate
* Push
* Remove
* Manual multi-arch workflow
* Comparison with Buildx
* Enterprise usage

---

# 🐳 1️⃣8️⃣ Docker Extension 

> `docker extension` is used to manage Docker Desktop extensions.
> Extensions add GUI + CLI integrations inside Docker Desktop.

Used for:

* Kubernetes dashboards
* Security scanners
* Database UIs
* Dev tools integrations
* Cloud tools

⚠ Available mainly in **Docker Desktop** (Windows / macOS / Linux Desktop).

Namespace: `docker extension`

---

# 🔹 `docker extension ls`

## ✅ Use

List installed extensions.

```bash id="ext01"
docker extension ls
```

Shows:

* Extension ID
* Version
* Enabled status

---

# 🔹 `docker extension install`

## ✅ Use

Install extension from Docker Hub or local source.

## 📌 Syntax

```bash id="ext02"
docker extension install EXTENSION_NAME
```

---

## 💻 Example – Install Extension

```bash id="ext03"
docker extension install docker/logs-explorer-extension
```

Install from specific version:

```bash id="ext04"
docker extension install docker/logs-explorer-extension:latest
```

Install from local image:

```bash id="ext05"
docker extension install my-extension:dev
```

---

# 🔹 `docker extension uninstall`

## ✅ Use

Remove installed extension.

```bash id="ext06"
docker extension uninstall docker/logs-explorer-extension
```

---

# 🔹 `docker extension update`

## ✅ Use

Update extension to latest version.

```bash id="ext07"
docker extension update docker/logs-explorer-extension
```

---

# 🔹 `docker extension inspect`

## ✅ Use

Inspect extension metadata.

```bash id="ext08"
docker extension inspect docker/logs-explorer-extension
```

Shows:

* Extension version
* Description
* Capabilities
* Installation source

---

# 🔥 Example Workflow

## Step 1 – Install Extension

```bash id="ext09"
docker extension install docker/scout-extension
```

## Step 2 – Verify Installation

```bash id="ext10"
docker extension ls
```

## Step 3 – Update Extension

```bash id="ext11"
docker extension update docker/scout-extension
```

## Step 4 – Remove Extension

```bash id="ext12"
docker extension uninstall docker/scout-extension
```

---

# 🔥 Common Enterprise Extensions

Examples:

* Docker Scout
* Kubernetes dashboard
* Portainer
* Logs Explorer
* Cloud integrations

---

# 🏭 Enterprise Use Cases

* Security monitoring
* Centralized logging
* Kubernetes management
* Database management tools
* CI/CD dashboard integration
* Developer productivity tools

---

# 🏭 Enterprise Best Practices

* Install only trusted extensions
* Regularly update extensions
* Avoid unnecessary extensions in production systems
* Restrict extension installation via admin controls
* Use extension mainly in development environments

---

# ⚠ Important Notes

* Extensions run inside Docker Desktop
* Not available on headless Linux servers
* GUI-based integration with CLI backend
* Some extensions require additional permissions

---

# 🔎 Debug Extension Issues

List extensions:

```bash id="ext13"
docker extension ls
```

Inspect:

```bash id="ext14"
docker extension inspect EXTENSION_NAME
```

Restart Docker Desktop if UI fails.

---

# ✅ Docker Extension Section Completed

Covered:

* Install
* List
* Inspect
* Update
* Uninstall
* Enterprise use cases
* Best practices

---

# 🐳 1️⃣9️⃣ Docker Scout 

> `docker scout` is Docker’s built-in security and image analysis tool.
> Used for:

* CVE vulnerability scanning
* Base image recommendations
* Image comparison
* SBOM generation
* Supply chain security

Works with:

* Local images
* Remote registry images
* Docker Hub
* CI/CD pipelines

Namespace: `docker scout`

---

# 🔹 `docker scout quickview`

## ✅ Use

Get a quick vulnerability summary of an image.

## 📌 Syntax

```bash id="sc01"
docker scout quickview IMAGE
```

## 💻 Example

```bash id="sc02"
docker scout quickview nginx:latest
```

Shows:

* Critical CVEs
* High vulnerabilities
* Base image status
* Fix availability

---

# 🔹 `docker scout cves`

## ✅ Use

Show detailed CVE vulnerabilities.

```bash id="sc03"
docker scout cves IMAGE
```

Example:

```bash id="sc04"
docker scout cves myapp:1.0
```

Filter by severity:

```bash id="sc05"
docker scout cves --only-severity critical myapp:1.0
```

Output includes:

* CVE ID
* Severity
* Affected package
* Fix status

---

# 🔹 `docker scout recommendations`

## ✅ Use

Show base image upgrade recommendations.

```bash id="sc06"
docker scout recommendations myapp:1.0
```

Helps identify:

* Safer base image
* Updated version
* Smaller attack surface

---

# 🔹 `docker scout compare`

## ✅ Use

Compare two images (vulnerability difference).

```bash id="sc07"
docker scout compare myapp:1.0 myapp:1.1
```

Used in:

* CI/CD pipelines
* Release validation
* Security regression testing

---

# 🔹 `docker scout sbom`

## ✅ Use

Generate SBOM (Software Bill of Materials).

```bash id="sc08"
docker scout sbom myapp:1.0
```

Output includes:

* Packages
* Versions
* Dependencies

Export SBOM:

```bash id="sc09"
docker scout sbom myapp:1.0 --format spdx > sbom.json
```

---

# 🔥 Real Enterprise Workflow

## Step 1 – Scan Image After Build

```bash id="sc10"
docker build -t myapp:1.0 .
docker scout quickview myapp:1.0
```

---

## Step 2 – Check Critical CVEs

```bash id="sc11"
docker scout cves --only-severity critical myapp:1.0
```

---

## Step 3 – Compare With Previous Version

```bash id="sc12"
docker scout compare myapp:1.0 myapp:1.1
```

---

## Step 4 – Get Recommendations

```bash id="sc13"
docker scout recommendations myapp:1.0
```

---

# 🔥 CI/CD Security Pipeline Example

```bash id="sc14"
docker build -t myapp:${VERSION} .

docker scout quickview myapp:${VERSION}

docker scout cves --only-severity critical myapp:${VERSION}
```

Fail pipeline if critical vulnerabilities found.

---

# 🔐 Enterprise Security Benefits

* Detect vulnerabilities early
* Prevent insecure deployments
* Improve base image hygiene
* Track CVE history
* Support compliance audits
* Generate SBOM for regulations

---

# 🏭 Enterprise Best Practices

* Scan every build in CI
* Block deployment on critical CVEs
* Use minimal base images (alpine, distroless)
* Keep base images updated
* Combine with Docker Trust signing
* Monitor image lifecycle regularly

---

# 🔎 Debug Scout Issues

Check login:

```bash id="sc15"
docker login
```

Verify image:

```bash id="sc16"
docker scout quickview IMAGE
```

Check Docker Desktop integration if using GUI.

---

# ⚠ Important Notes

* Requires internet for CVE database
* Works best with Docker Hub integration
* Alternative tools:

  * Trivy
  * Grype
  * Snyk
* Scout integrates directly into Docker ecosystem

---

# ✅ Docker Scout Section Completed

Covered:

* Quick vulnerability scan
* Detailed CVE analysis
* Image comparison
* Recommendations
* SBOM generation
* CI/CD integration
* Enterprise security practices

---

# 🐳 2️⃣0️⃣ Docker Init 

> `docker init` automatically generates Docker configuration files for your application.

It helps create:

* Dockerfile
* .dockerignore
* docker-compose.yml
* Optional configuration files

Used for:

* Quickly containerizing new projects
* Standardizing team setups
* Bootstrapping development environments

Namespace: `docker init`

---

# 🔹 `docker init`

## ✅ Use

Initialize Docker setup inside an application directory.

## 📌 Syntax

```bash
docker init
```

---

# 🔥 Basic Example

Navigate to project folder:

```bash
cd my-node-app
```

Run:

```bash
docker init
```

Docker will:

1️⃣ Detect project type (Node, Python, Go, etc.)
2️⃣ Ask configuration questions
3️⃣ Generate:

* Dockerfile
* .dockerignore
* docker-compose.yml

---

# 🔥 Example – Node.js Project

After running:

```bash
docker init
```

Generated files:

### Dockerfile

```dockerfile
FROM node:18
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
CMD ["npm", "start"]
```

### .dockerignore

```
node_modules
.git
Dockerfile
```

### docker-compose.yml

```yaml
services:
  app:
    build: .
    ports:
      - "3000:3000"
```

---

# 🔥 Example – Python Project

Run:

```bash
docker init
```

Generated Dockerfile:

```dockerfile
FROM python:3.11
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
CMD ["python", "app.py"]
```

---

# 🔥 After Initialization

Build:

```bash
docker build -t myapp .
```

Or use Compose:

```bash
docker compose up --build
```

---

# 🏭 Enterprise Use Cases

* Standardizing Dockerfile templates
* Onboarding new developers quickly
* Rapid microservice prototyping
* Reducing manual Dockerfile errors
* Enforcing best practices automatically

---

# 🏭 Enterprise Best Practices

* Review generated Dockerfile before production use
* Add multi-stage builds for production
* Add healthcheck instructions
* Optimize layers
* Add security hardening
* Integrate with Docker Scout scanning

---

# 🔥 Typical Workflow

```bash
git clone repo
cd project
docker init
docker compose up -d
```

---

# 🔎 Debugging Init Issues

Ensure:

* Docker Desktop is running
* Project directory contains recognizable framework files
* You have write permission in folder

---

# ⚠ Important Notes

* Not a production replacement for manual optimization
* Best used for development stage
* May not detect complex custom frameworks
* Always review generated configuration

---

# ✅ Docker Init Section Completed

Covered:

* Initialize project
* Generated files
* Node example
* Python example
* Enterprise usage
* Best practices

---

# 🐳 2️⃣1️⃣ Docker Completion 

> `docker completion` generates shell auto-completion scripts.
> It enables tab-completion for:

* Commands
* Subcommands
* Container names
* Image names
* Options & flags

Supported shells:

* bash
* zsh
* fish
* powershell

Namespace: `docker completion`

---

# 🔹 `docker completion bash`

## ✅ Use

Generate Bash completion script.

## 📌 Syntax

```bash
docker completion bash
```

---

## 💻 Temporary Enable (Current Session)

```bash
source <(docker completion bash)
```

---

## 💻 Permanent Enable (Linux/macOS)

```bash
docker completion bash > /etc/bash_completion.d/docker
```

Or user-level:

```bash
mkdir -p ~/.bash_completion.d
docker completion bash > ~/.bash_completion.d/docker
```

Add to `.bashrc`:

```bash
echo 'source ~/.bash_completion.d/docker' >> ~/.bashrc
```

---

# 🔹 `docker completion zsh`

## ✅ Use

Generate Zsh completion script.

```bash
docker completion zsh > "${fpath[1]}/_docker"
```

Reload:

```bash
exec zsh
```

---

# 🔹 `docker completion fish`

## ✅ Use

Generate Fish shell completion.

```bash
docker completion fish > ~/.config/fish/completions/docker.fish
```

Reload Fish shell.

---

# 🔹 `docker completion powershell`

## ✅ Use

Generate PowerShell completion script.

```powershell
docker completion powershell > docker.ps1
```

Import module:

```powershell
Import-Module ./docker.ps1
```

Permanent enable (Profile):

```powershell
docker completion powershell >> $PROFILE
```

---

# 🔥 How Auto-Completion Helps

Instead of typing:

```bash
docker container inspect my-long-container-name
```

You can type:

```bash
docker con<TAB>
docker container in<TAB>
docker container inspect my<TAB>
```

It auto-completes:

* Commands
* Subcommands
* Resource names

---

# 🏭 Enterprise Use Cases

* Faster CLI productivity
* Reduced typing errors
* Helpful in large clusters
* Useful for DevOps engineers
* Saves time during incident response

---

# 🏭 Enterprise Best Practices

* Enable completion on all DevOps machines
* Combine with:

  * `kubectl` completion
  * `git` completion
* Use in CI debug sessions
* Add to shell profile for persistence

---

# 🔎 Verify Completion Working

Type:

```bash
docker <TAB>
```

If list appears → completion is active.

---

# ⚠ Important Notes

* Requires bash-completion package (Linux)
* Docker must be installed correctly
* Restart shell after enabling

---

# ✅ Docker Completion Section Completed

Covered:

* Bash
* Zsh
* Fish
* PowerShell
* Permanent setup
* Enterprise usage

---

# 🐳 2️⃣2️⃣ Docker Registry Authentication Helpers 

> Docker uses credential helpers to securely store registry credentials.
> Instead of storing passwords in plain text inside `~/.docker/config.json`.

Used for:

* Secure login storage
* Enterprise security compliance
* OS keychain integration
* Cloud registry authentication

---

# 🔐 Credential Storage Overview

After running:

```bash
docker login
```

Credentials are stored in:

```bash
~/.docker/config.json
```

If no helper is configured → password may be stored (base64 encoded).

With credential helper → password stored securely in OS keychain.

---

# 🔹 `docker login` (Recap – Uses Credential Helper)

```bash
docker login
```

Login to private registry:

```bash
docker login registry.company.com
```

---

# 🔹 `docker logout`

```bash
docker logout
```

Removes stored credentials from helper.

---

# 🔹 `docker-credential-<helper>` (Helper Binary)

Docker uses external binaries like:

* `docker-credential-osxkeychain`
* `docker-credential-wincred`
* `docker-credential-pass`
* `docker-credential-secretservice`

These are NOT typed as normal docker commands, but used internally.

---

# 🔹 Configure Credential Store

Edit:

```bash
~/.docker/config.json
```

Example:

```json
{
  "credsStore": "osxkeychain"
}
```

Linux example:

```json
{
  "credsStore": "pass"
}
```

Windows example:

```json
{
  "credsStore": "wincred"
}
```

---

# 🔹 Per-Registry Credential Helper

```json
{
  "credHelpers": {
    "registry.company.com": "pass"
  }
}
```

Used when:

* Multiple registries
* Different auth backends

---

# 🔥 Verify Credential Helper Working

Check config:

```bash
cat ~/.docker/config.json
```

Test login:

```bash
docker login
```

Ensure password not stored directly in JSON.

---

# 🔐 Enterprise Use Cases

* Secure Docker Hub login
* AWS ECR authentication
* GCP Artifact Registry
* Azure Container Registry
* Private enterprise registry

---

# 🔥 AWS ECR Example

Instead of storing password:

```bash
aws ecr get-login-password | docker login \
  --username AWS \
  --password-stdin ACCOUNT_ID.dkr.ecr.region.amazonaws.com
```

Credential stored securely.

---

# 🔥 GCP Artifact Registry Example

```bash
gcloud auth configure-docker
```

---

# 🏭 Enterprise Best Practices

* Never store passwords in plain text
* Always configure credential helper
* Use short-lived tokens where possible
* Use cloud IAM roles instead of static credentials
* Rotate credentials periodically
* Use CI secrets vault (GitHub, GitLab, Jenkins)

---

# 🔎 Debug Credential Issues

Check config:

```bash
cat ~/.docker/config.json
```

Remove stored login:

```bash
docker logout
```

Re-login:

```bash
docker login
```

---

# ⚠ Important Notes

* Credential helpers are OS-dependent
* Docker Desktop configures automatically
* Required for enterprise compliance
* Not needed for public image pulls

---

# ✅ Docker Credential Management Section Completed

Covered:

* Credential helpers
* credsStore
* credHelpers
* Secure login
* Cloud registry authentication
* Enterprise best practices

---
