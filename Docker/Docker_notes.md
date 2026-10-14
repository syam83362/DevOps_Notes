# Why Docker?

Let's assume we are developing an application.

A typical application may contain:

- Frontend
- Backend
- Database

To run the application, we need to install the required **dependencies and tools** on our system.

For example:

- Java 11
- ReactJS
- MongoDB

Later, another application may require different versions of the same tools.

For example:

- Java 17 instead of Java 11
- A different React version
- A different MongoDB version

Managing multiple versions of the same software on one system can become difficult.

Docker helps solve this problem by packaging an application together with the dependencies it needs.

---

# Virtualization

**Virtualization** is a technology used to create virtual machines inside a physical machine.

A virtual machine can have its own **Guest Operating System**, on which we can run applications.

### How it works

```
Physical Machine
       |
    Hypervisor
       |
  -----------------
  |       |       |
 VM 1    VM 2    VM 3
  |       |       |
 OS      OS      OS
```

The **Hypervisor** is responsible for creating and managing virtual machines.

### Drawbacks of Virtualization

- Virtual machines require a complete operating system.
- Running multiple virtual machines requires more CPU, RAM, and storage.
- Because of this, system performance can decrease when many VMs are running.

Instead of using a complete virtual machine for every application, we can use **containers**.

---

# Containerization

**Containerization** is a method of packaging an application together with its dependencies so that it can run consistently in different environments.

A container typically contains:

- Application code
- Runtime
- System libraries
- Dependencies

Containers share the host operating system's kernel instead of requiring a complete guest operating system for each container.

---

# Container

A **container** is a lightweight, isolated environment used to run an application and its dependencies.

Docker is one of the tools used to create and manage containers.

### Simple comparison

```
Virtual Machine

Host Machine
    |
Hypervisor
    |
Guest OS
    |
Application

Container

Host Machine
    |
Docker
    |
Container
    |
Application
```

Containers are generally smaller and faster to start than virtual machines because they do not require a separate full operating system for each application.

---

# Docker

**Docker** is an open-source platform used to build, package, deploy, and run applications using containers.

Docker uses **containerization** to isolate applications and their dependencies.

One of the main benefits of Docker is consistency.

For example, an application may work on a developer's machine but fail on another machine because of differences in dependencies or software versions.

Docker helps package the application and its required dependencies together so that it can run more consistently across different environments.

### Important Point

Docker containers share the host operating system's kernel, while virtual machines run with their own guest operating system.

# Docker Basic Commands

## Install Docker on Linux

```bash
yum install docker -y
systemctl start docker
systemctl enable docker
```

## Check Docker Version

```bash
docker --version
```

## Start Docker Service

```bash
service docker start
```

## Check Docker Service Status

```bash
service docker status
```

## Check Docker Information

```bash
docker info
```

## List Docker Images

```bash
docker images
```

## Search for an Image

```bash
docker search <image-name>
```

Example:

```bash
docker search nginx
```

## Download an Image

Use `docker pull` to download an image from a Docker Registry.

```bash
docker pull <image-name>
```

Example:

```bash
docker pull nginx
```

## Build an Image

```bash
docker build -t <image-name>:<tag> .
```

Here, `.` represents the current directory.

Example:

```bash
docker build -t myapp:v1 .
```

## Create and Run a Container

```bash
docker run -itd --name <container-name> -p <host-port>:<container-port> <image-name>:<tag>
```

Example:

```bash
docker run -itd --name mycontainer -p 8080:80 nginx
```

## Inspect an Image

```bash
docker image inspect <image-name>:<tag>
```

## Start a Container

```bash
docker start <container-name>
```

## Enter a Running Container

```bash
docker exec -it <container-name> bash
```

Example:

```bash
docker exec -it mycontainer bash
```

## Check the OS Inside a Container

```bash
cat /etc/os-release
```

## Exit from a Container

```bash
exit
```

## List All Containers

```bash
docker ps -a
```

## List Only Running Containers

```bash
docker ps
```

`ps` stands for **Process Status**.

# Container Management Commands

## 1. Check Exited Containers

To see containers that have already stopped:

```bash
docker ps -q -f "status=exited"
```

To see all containers, including stopped containers:

```bash
docker ps -a
```

---

## 2. Stop a Container

To stop a running container:

```bash
docker stop container_name
```

Example:

```bash
docker stop cont1
```

---

## 3. Remove a Container

To remove a stopped container:

```bash
docker rm container_name
```

Example:

```bash
docker rm cont1
```

> A running container normally needs to be stopped before removing it.
> 

---

## 4. Stop All Containers

To stop all containers:

```bash
docker stop $(docker ps -a -q)
```

⚠️ This stops **all containers** on the Docker host.

---

## 5. Remove All Stopped Containers

```bash
docker rm $(docker ps -a -q)
```

This removes containers that are already stopped.

---

## 6. Remove All Docker Images

```bash
docker rmi -f $(docker images -q)
```

⚠️ **Be careful:** this removes all local Docker images.

Use this only when you intentionally want to clean up all images.

---

# Docker Rename

We can rename an existing container using:

```bash
docker rename old_container new_container
```

Example:

```bash
docker rename cont1 web-container
```

Now the container name changes from `cont1` to `web-container`.

---

# Useful Container Commands

### List running containers

```bash
docker container ls
```

Same as:

```bash
docker ps
```

### List all containers

```bash
docker container ls -a
```

Same as:

```bash
docker ps -a
```

### Show the latest created container

```bash
docker container ls --latest
```

### Show only container IDs

```bash
docker container ls -aq
```

---

# Remove All Containers

To forcefully remove all containers:

```bash
docker container rm -f $(docker container ls -aq)
```

⚠️ This removes **all containers**, including running containers.

---

# Check Container Size

```bash
docker container ls -a -s
```

This shows the size information of containers.

---

# Run a Container

Example using NGINX:

```bash
docker run --name cont1 -d nginx
```

Here:

- `docker run` → creates and starts a container
- `-name cont1` → gives the container a name
- `d` → runs in detached/background mode
- `nginx` → image used to create the container

---

# Inspect a Container

To see detailed information about a container:

```bash
docker inspect cont1
```

This can show information such as:

- Container ID
- IP address
- Network configuration
- Mounts
- Environment variables
- Container settings

---

# Publish a Container Port

Example:

```bash
docker run --name cont2 -d -p 8081:80 nginx
```

Here:

```
8081 → Host port
80   → Container port
```

So you can access NGINX through:

```
http://localhost:8081
```

---

# Docker Exec

`docker exec` is used to run a command **inside an already running container**.

Syntax:

```bash
docker exec -it container_name command
```

Example:

```bash
docker exec -it cont1 ls
```

This runs `ls` inside `cont1`.

To open a shell inside the container:

```bash
docker exec -it cont1 bash
```

You can then run commands inside the container.

Example:

```bash
mkdir devops
```

Exit the container shell using:

```bash
exit
```

> **Important:** `docker exec` does not create a new container. It executes a command inside an existing running container.
> 

# Dockerfile

## What is a Dockerfile?

A **Dockerfile** is a text file that contains instructions for creating a Docker image.

Instead of manually installing everything inside a container, we write the required steps in a Dockerfile and Docker builds the image automatically.

### Basic workflow

```
Dockerfile
    ↓
docker build
    ↓
Docker Image
    ↓
docker run
    ↓
Docker Container
```

---

# Dockerfile Naming

The default Dockerfile name is:

```
Dockerfile
```

The `D` and `F` are normally uppercase.

Example:

```
my-project/
├── Dockerfile
├── app.py
└── requirements.txt
```

Docker instruction keywords are conventionally written in uppercase:

```docker
FROM
RUN
COPY
WORKDIR
CMD
```

---

# Important Dockerfile Instructions

## 1. FROM

Specifies the base image.

```docker
FROM ubuntu
```

Example:

```docker
FROM python:3.12
```

This means the image starts from the Python 3.12 base image.

---

## 2. LABEL

Adds information or metadata to the image.

```docker
LABEL maintainer="devops-team"
```

---

## 3. RUN

Runs a command **while building the image**.

Example:

```docker
RUN apt update
RUN apt install nginx -y
```

Important:

> `RUN` happens during **image build time**.
> 

---

## 4. COPY

Copies files from the build context into the image.

Example:

```docker
COPY index.html /var/www/html/
```

This copies `index.html` into the specified directory inside the image.

---

## 5. ADD

`ADD` can also copy files into the image.

Example:

```docker
ADD index.html /var/www/html/
```

For simple file copying, **`COPY` is generally preferred**.

---

## 6. EXPOSE

Documents the port that the application inside the container listens on.

Example:

```docker
EXPOSE 80
```

> `EXPOSE` does **not** publish the port to the host by itself.
> 

Port publishing is done when running the container:

```bash
docker run -p 8080:80 nginx
```

---

## 7. WORKDIR

Sets the working directory inside the image/container.

Example:

```docker
WORKDIR /app
```

After this, commands such as `RUN`, `CMD`, and `COPY` can work relative to `/app`.

---

## 8. CMD

Specifies the **default command** to run when a container starts.

Example:

```docker
CMD ["python", "app.py"]
```

`CMD` can be overridden when starting the container.

---

## 9. ENTRYPOINT

Defines the main executable for the container.

Example:

```docker
ENTRYPOINT ["python"]
```

We can combine it with `CMD`:

```docker
ENTRYPOINT ["python"]
CMD ["app.py"]
```

The container effectively runs:

```bash
python app.py
```

### Simple difference

```
ENTRYPOINT → main executable
CMD        → default command/arguments
```

---

## 10. ENV

Defines environment variables inside the image.

Example:

```docker
ENV APP_ENV=production
```

The application can access:

```
APP_ENV=production
```

---

# Docker PULL vs Docker RUN

These two commands are different.

### docker pull

Downloads an image from a registry.

```bash
docker pull nginx
```

### docker run

Creates and starts a container using an image.

```bash
docker run nginx
```

Simple flow:

```
docker pull
    ↓
Download Image
    ↓
docker run
    ↓
Create + Start Container
```

---

# RUN vs CMD vs ENTRYPOINT

This is important to remember:

| Instruction | Purpose |
| --- | --- |
| `RUN` | Executes commands while building the image |
| `CMD` | Provides the default command/arguments when container starts |
| `ENTRYPOINT` | Defines the main executable for the container |

---

# Example Dockerfile

```docker
FROM ubuntu

RUN touch aws devops linux

WORKDIR /app

COPY . .

CMD ["bash"]
```

Build the image:

```bash
docker build -t myimage:1.0 .
```

Run the container:

```bash
docker run -it --name mycontainer myimage:1.0
```

Here:

```
Dockerfile
    ↓
docker build
    ↓
myimage:1.0
    ↓
docker run
    ↓
mycontainer
```

# EXPOSE vs Port Publishing

These two are related, but they are **not the same**.

## EXPOSE

`EXPOSE` is written inside the Dockerfile.

It tells Docker and other developers which port the application is expected to use.

Example:

```docker
EXPOSE 80
```

It does **not** make the application accessible from the host by itself.

---

## Port Publishing

To make a container port accessible from the host, use `-p` with `docker run`.

```bash
docker run -d -p 8080:80 nginx
```

Here:

```
8080 → Host port
80   → Container port
```

So the request:

```
http://localhost:8080
```

is forwarded to port `80` inside the container.

### Simple difference

```
EXPOSE
→ Documents the container port

-p
→ Publishes the container port to the host
```

---

# NGINX Dockerfile Example

Let's create a simple NGINX image.

### Step 1: Create Dockerfile

```docker
FROM ubuntu

RUN apt update -y
RUN apt install nginx -y

COPY index.html /var/www/html/

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
```

### Step 2: Create index.html

```html
<h1>Hello from Docker NGINX</h1>
```

### Step 3: Build the Image

```bash
docker build -t nginx-custom:1.0 .
```

Here:

```
nginx-custom → image name
1.0          → image tag
.            → current directory as build context
```

### Step 4: Run the Container

```bash
docker run -d --name nginx-container -p 8080:80 nginx-custom:1.0
```

Now open:

```
http://localhost:8080
```

You should see:

```
Hello from Docker NGINX
```

---

# Why `daemon off;`?

NGINX normally starts as a background process.

Inside a Docker container, the main application should stay in the foreground.

So we use:

```docker
CMD ["nginx", "-g", "daemon off;"]
```

This keeps NGINX running as the container's main process.

---

# Apache HTTPD Dockerfile

A similar Dockerfile can be created for Apache HTTPD:

```docker
FROM ubuntu

RUN apt update -y
RUN apt install apache2 -y

COPY index.html /var/www/html/

EXPOSE 80

CMD ["apachectl", "-D", "FOREGROUND"]
```

Build:

```bash
docker build -t apache-custom:1.0 .
```

Run:

```bash
docker run -d --name apache-container -p 8080:80 apache-custom:1.0
```

# Application Server Dockerfiles

Docker can be used to package application servers such as:

- Python applications
- Node.js applications
- Database services

The main idea is to put the application's dependencies and required files into an image.

---

# Python Application

## Manual Deployment Without Docker

Normally, we may need to install Python and the application dependencies manually.

Example:

```bash
git clone <repository-url>

cd <project-directory>

python --version

pip install -r requirements.txt

python app.py
```

The application then runs on a specific port.

With Docker, we can put these steps into a Dockerfile.

---

# Python Dockerfile

Example:

```docker
FROM python:3.12

WORKDIR /app

COPY requirements.txt .

RUN pip install -r requirements.txt

COPY . .

CMD ["python", "app.py"]
```

## Explanation

```
FROM
→ Provides the Python environment

WORKDIR
→ Sets the application directory

COPY requirements.txt
→ Copies dependency file

RUN pip install
→ Installs Python dependencies

COPY . .
→ Copies application source code

CMD
→ Starts the application
```

Build the image:

```bash
docker build -t python-app:1.0 .
```

Run the container:

```bash
docker run -d --name python-container python-app:1.0
```

If the application listens on port `8000`, publish it using:

```bash
docker run -d --name python-container -p 8000:8000 python-app:1.0
```

---

# Node.js Application

Node.js applications can also be packaged using Docker.

## Node.js Dockerfile

```docker
FROM node:22

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

CMD ["node", "index.js"]
```

## Explanation

```
FROM
→ Provides Node.js environment

WORKDIR
→ Sets the application directory

COPY package*.json
→ Copies package files first

RUN npm install
→ Installs Node.js dependencies

COPY . .
→ Copies application source code

CMD
→ Starts the application
```

Build:

```bash
docker build -t node-app:1.0 .
```

Run:

```bash
docker run -d --name node-container -p 3000:3000 node-app:1.0
```

---

# Database Dockerfile

Docker can also run databases such as MySQL.

Example:

```docker
FROM mysql

EXPOSE 3306

COPY init.sql /docker-entrypoint-initdb.d/

ENV MYSQL_ROOT_PASSWORD=example-password
```

Build the image:

```bash
docker build -t mysql-custom:1.0 .
```

Run the container:

```bash
docker run -d \
  --name mysql-container \
  -p 1111:3306 \
  mysql-custom:1.0
```

Here:

```
1111 → Host port
3306 → MySQL container port
```

### Important

For real projects, **do not hardcode production passwords inside a Dockerfile**.

Use environment variables, secrets, or a proper secret-management solution instead.

---

# Quick Comparison

| Application | Base Image | Common Port |
| --- | --- | --- |
| Python | `python` | 8000 |
| Node.js | `node` | 3000 |
| MySQL | `mysql` | 3306 |
| NGINX | `nginx` | 80 |
| Apache | `httpd` | 80 |

# Production-Grade Dockerfile Rules

A Dockerfile that works is not always a Dockerfile that is ready for production.

For production applications, we should focus on:

- Security
- Image size
- Performance
- Reliability
- Maintainability

---

## 1. Use Supported Base Images

Always use a supported and maintained base image.

Example:

```docker
FROM python:3.12
```

Avoid using old or unsupported images.

---

## 2. Use Smaller Base Images

Prefer smaller images when they are suitable for your application.

Common options include:

```
alpine
slim
distroless
```

Example:

```docker
FROM python:3.12-slim
```

Smaller images can reduce:

- Image size
- Download time
- Storage usage
- Potential attack surface

---

## 3. Use Multi-Stage Builds

For applications that require a build process, use **multi-stage builds**.

This allows us to keep build-time dependencies separate from the final production image.

Example:

```docker
FROM node:22-alpine AS build

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .
RUN npm run build

FROM node:22-alpine

WORKDIR /app

COPY --from=build /app/dist ./dist

CMD ["node", "dist/server.js"]
```

The final image does not need all the files and tools used during the build.

---

## 4. Don't Run as Root

Containers should preferably run the application as a non-root user.

Example:

```docker
USER node
```

This improves container security.

---

## 5. Don't Store Secrets in Dockerfiles

Never put passwords, API keys, or other sensitive information directly inside a Dockerfile.

❌ Avoid:

```docker
ENV DB_PASSWORD=my-secret-password
```

Use environment variables or a proper secrets-management solution instead.

---

## 6. Use `.dockerignore`

Create a `.dockerignore` file to prevent unnecessary files from being copied into the image.

Example:

```
node_modules
.git
.env
Dockerfile
README.md
```

This helps reduce the build context and image size.

---

## 7. Pin Application Dependencies

Avoid installing completely unpinned dependencies when reproducibility matters.

For example, use a dependency lock file such as:

```
package-lock.json
requirements.txt
poetry.lock
```

This helps ensure that builds use predictable dependency versions.

---

## 8. Don't Install Unnecessary Packages

Only install packages that the application actually needs.

Avoid unnecessary tools and dependencies in production images.

This helps keep the image:

- Smaller
- Faster
- More secure

---

## 9. Avoid `latest` in Production

Instead of:

```docker
FROM node:latest
```

prefer a specific version:

```docker
FROM node:22-alpine
```

Using a specific version makes builds more predictable.

---

## 10. Scan Docker Images

Security scanning tools can detect vulnerabilities in Docker images.

One commonly used tool is **Trivy**.

Example:

```bash
trivy image myimage:1.0
```

This scans the image for known vulnerabilities.

---

# Production Dockerfile Checklist

Before using a Docker image in production, check:

```
☑ Supported base image
☑ Small/suitable base image
☑ Multi-stage build when appropriate
☑ Non-root user
☑ No secrets in Dockerfile
☑ .dockerignore present
☑ Dependencies pinned
☑ No unnecessary packages
☑ Avoid latest tag
☑ Image security scan completed
```

# Production Dockerfiles

In production, we should improve our Dockerfiles for:

- Smaller image size
- Better security
- Faster builds
- Fewer unnecessary dependencies

Below are improved examples for common applications.

---

# 1. Production NGINX Dockerfile

Instead of installing NGINX manually on Ubuntu, we can directly use the official lightweight NGINX image.

```docker
FROM nginx:alpine

RUN rm -rf /usr/share/nginx/html/*

COPY index.html /usr/share/nginx/html/

RUN chown -R nginx:nginx /usr/share/nginx/html

USER nginx

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
```

### Why is this better?

- `nginx:alpine` → smaller base image
- Removes the default NGINX page
- Copies only our application files
- Runs NGINX as a non-root user

---

# 2. Production HTTPD Dockerfile

For Apache HTTPD:

```docker
FROM httpd:alpine

RUN rm -rf /usr/local/apache2/htdocs/*

COPY index.html /usr/local/apache2/htdocs/

RUN chown -R daemon:daemon /usr/local/apache2/htdocs

USER daemon

EXPOSE 80

CMD ["httpd-foreground"]
```

### Why is this better?

- Uses lightweight `alpine`
- Removes the default page
- Copies only required files
- Runs Apache as a non-root user

---

# 3. Production Node.js Dockerfile

```docker
FROM node:22-alpine

WORKDIR /app

COPY package*.json ./

RUN npm install --omit=dev

COPY --chown=node:node . .

USER node

EXPOSE 3000

CMD ["node", "index.js"]
```

### Important points

```
node:22-alpine
→ Lightweight Node.js image

npm install --omit=dev
→ Installs production dependencies

USER node
→ Runs the application as a non-root user

EXPOSE 3000
→ Documents the application port
```

---

# 4. Production Python Dockerfile

A simple production Python image can start with:

```docker
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

CMD ["python", "app.py"]
```

### Why `python:slim`?

The `slim` image contains fewer unnecessary packages than the full Python image.

This can help reduce the final image size.

---

# Production Dockerfile Pattern

A simple pattern to remember:

```
Choose a suitable base image
        ↓
Set working directory
        ↓
Copy dependency files
        ↓
Install dependencies
        ↓
Copy application code
        ↓
Run as non-root user
        ↓
Expose application port
        ↓
Start application
```

This pattern is useful for many application Dockerfiles.

# Multi-Stage Docker Builds

## What is a Multi-Stage Build?

A **multi-stage Dockerfile** uses multiple `FROM` statements to separate different stages of the build.

The main goal is to keep the **final production image smaller and cleaner**.

For example:

```
Stage 1 → Install dependencies
Stage 2 → Build application
Stage 3 → Create production image
```

The final image contains only what is required to run the application.

---

# Example — Node.js Multi-Stage Dockerfile

```docker
FROM node:22-alpine AS dependencies

WORKDIR /app

COPY package*.json ./

RUN npm ci

FROM node:22-alpine AS build

WORKDIR /app

COPY --from=dependencies /app/node_modules ./node_modules

COPY . .

RUN npm run build

FROM node:22-alpine AS production

WORKDIR /app

COPY package*.json ./

RUN npm ci --omit=dev

COPY --from=build /app/dist ./dist

EXPOSE 3000

USER node

CMD ["node", "dist/server.js"]
```

---

# Understanding the Stages

## Stage 1 — Dependencies

```docker
FROM node:22-alpine AS dependencies
```

This stage installs the application's dependencies.

```docker
COPY package*.json ./

RUN npm ci
```

---

## Stage 2 — Build

```docker
FROM node:22-alpine AS build
```

The dependencies from the previous stage are copied:

```docker
COPY --from=dependencies /app/node_modules ./node_modules
```

Then the application source code is copied and built:

```docker
COPY . .

RUN npm run build
```

---

## Stage 3 — Production

```docker
FROM node:22-alpine AS production
```

This is the final image.

Only the required production dependencies and built application are copied:

```docker
RUN npm ci --omit=dev

COPY --from=build /app/dist ./dist
```

Then the application starts:

```docker
CMD ["node", "dist/server.js"]
```

---

# Why Use Multi-Stage Builds?

### 1. Smaller Final Image

Build tools and unnecessary files don't need to be included in the final image.

### 2. Better Security

Fewer packages and tools mean a smaller attack surface.

### 3. Cleaner Production Image

The final image contains mainly what the application needs to run.

### 4. Separate Build and Runtime

Build dependencies can stay in the build stages instead of being included in production.

---

# Single-Stage vs Multi-Stage

### Single-Stage

```
Dependencies
     +
Build tools
     +
Source code
     +
Application
     ↓
Large Production Image
```

### Multi-Stage

```
Dependencies
     ↓
Build
     ↓
Production
     ↓
Only required files
     ↓
Smaller Production Image
```

---

# Simple Rule to Remember

> **Build everything you need in earlier stages, then copy only the required output into the final stage.**
> 

# Docker Fundamentals — 4 Pillars

The main Docker concepts covered here are:

1. **Containers**
2. **Images**
3. **Volumes**
4. **Networks**

Docker also provides tools such as:

- **Docker Compose**
- **Docker Swarm**
- **Docker Stack**

---

# Docker Volumes

## Why Do We Need Volumes?

Containers are temporary by nature.

If a container is deleted, the data stored inside its writable container filesystem can also be lost.

For example:

```
Container
   ↓
Application Data
   ↓
Container Deleted
   ↓
Data Lost
```

To keep data even after the container is deleted, we can use **Docker Volumes**.

```
Container
   ↓
Docker Volume
   ↓
Persistent Data
```

---

# What is a Docker Volume?

A **Docker volume** is Docker-managed storage that can be mounted inside a container.

The volume exists separately from the container.

Therefore:

```
Container deleted
       ↓
Volume remains
       ↓
Data remains
```

Volumes are commonly used for:

- Database data
- Application data
- Uploaded files
- Persistent configuration/data

---

# Create a Volume

```bash
docker volume create mydata
```

Check available volumes:

```bash
docker volume ls
```

---

# Use a Volume with a Container

```bash
docker run -itd \
  --name cont1 \
  --mount source=mydata,target=/data \
  ubuntu
```

Here:

```
mydata
   ↓
Docker Volume

/data
   ↓
Directory inside the container
```

---

# Inspect a Volume

```bash
docker volume inspect mydata
```

This shows information about the volume, including where Docker stores it on the host.

---

# Remove a Volume

```bash
docker volume rm mydata
```

⚠️ Removing a volume can permanently remove the data stored in it.

---

# Remove Unused Volumes

Docker can remove volumes that are no longer being used:

```bash
docker volume prune
```

⚠️ Use this carefully because unused volumes may still contain data you want to keep.

---

# Named Volume vs Anonymous Volume

## Named Volume

We explicitly provide a name:

```bash
docker run -itd \
  --name cont1 \
  -v mydata:/data \
  ubuntu
```

Here:

```
mydata → Volume name
/data  → Container path
```

Named volumes are easier to identify and manage.

---

## Anonymous Volume

We provide only the container path:

```bash
docker run -itd \
  --name cont2 \
  -v /data \
  ubuntu
```

Docker automatically creates a volume and assigns it an ID/name.

---

# Read-Only Volume

Sometimes a container should be able to **read** data but should not modify it.

Example:

```bash
docker run -itd \
  --name cont1 \
  --mount source=mydata,target=/data,readonly \
  ubuntu
```

The container can read the files but cannot modify them.

---

# Sharing a Volume Between Containers

The same volume can be mounted into multiple containers.

```
             ┌──────────────┐
             │   cont1      │
             └──────┬───────┘
                    │
                mydata
                    │
             ┌──────┴───────┐
             │   cont2      │
             └──────────────┘
```

Example:

```bash
docker run -itd --name cont1 -v mydata:/data ubuntu
```

```bash
docker run -itd --name cont2 -v mydata:/data ubuntu
```

Both containers can access the same volume.

---

# Volume vs Container

Remember:

```
Container
→ Runs the application

Image
→ Template used to create the container

Volume
→ Stores persistent data

Network
→ Allows containers/services to communicate
```

---

# Important Commands

| Command | Purpose |
| --- | --- |
| `docker volume ls` | List volumes |
| `docker volume create` | Create a volume |
| `docker volume inspect` | View volume details |
| `docker volume rm` | Remove a volume |
| `docker volume prune` | Remove unused volumes |

---

# Simple Example

```bash
docker volume create mydata
```

```bash
docker run -itd \
  --name cont1 \
  -v mydata:/data \
  ubuntu
```

Now `/data` inside `cont1` is backed by the `mydata` volume.

If `cont1` is deleted:

```bash
docker rm cont1
```

The volume still exists:

```bash
docker volume ls
```

So the data can be used by another container.

# Docker Networks

## Why Do We Need Docker Networks?

In a real application, we may have multiple services such as:

```
Frontend
Backend
Database
Payment Service
Cart Service
```

These services need to communicate with each other.

For example:

```
Frontend
   ↓
Backend
   ↓
Database
```

Docker Networks provide a way for containers to communicate with each other.

---

# Default Docker Network

When Docker is installed, it provides some default networks.

Check them using:

```bash
docker network ls
```

Common default networks are:

```
bridge
host
none
```

### Bridge

The default network for containers.

### Host

The container shares the host's network stack.

### None

The container has no network connectivity by default.

---

# Docker Bridge Network

A bridge network allows containers on the same Docker network to communicate with each other.

Example:

```bash
docker network create database
```

Now run a container using that network:

```bash
docker run -d \
  --name cont1 \
  --network database \
  nginx
```

The container is now connected to the `database` network.

---

# List Networks

```bash
docker network ls
```

Example:

```
NETWORK ID     NAME       DRIVER
xxxxxx         bridge     bridge
xxxxxx         host       host
xxxxxx         none       null
xxxxxx         database   bridge
```

---

# Inspect a Network

```bash
docker network inspect database
```

This shows information such as:

- Network configuration
- Connected containers
- IP addresses
- Network driver

---

# Connect a Container to a Network

A running container can be connected to another network.

```bash
docker network connect database cont1
```

Now `cont1` is connected to the `database` network.

---

# Disconnect a Container

To disconnect a container:

```bash
docker network disconnect database cont1
```

---

# Create a Network

```bash
docker network create mynetwork
```

Then run containers using it:

```bash
docker run -d --name cont1 --network mynetwork nginx
```

```bash
docker run -d --name cont2 --network mynetwork nginx
```

Containers connected to the same user-defined network can communicate with each other.

---

# Network Communication

Consider:

```
                 mynetwork
        ┌─────────────────────────┐
        │                         │
        │  Frontend → Backend     │
        │              ↓          │
        │           Database      │
        │                         │
        └─────────────────────────┘
```

For example:

```
Frontend
   ↓
Backend
   ↓
Database
```

---

# Key Points

Remember these three things:

```
Network → Allows containers to communicate

Volume  → Keeps important data persistent

Database → Usually uses both a network and a volume
```

Docker

Docker HUB

Docker Compose
