# Docker Compose

## What is Docker Compose?

**Docker Compose** is a tool used to define and run applications that contain multiple Docker containers.

For example, an application may have:

```
Frontend
   ↓
Backend
   ↓
Database
```

Instead of creating and managing each container separately, Docker Compose allows us to define all these services in one YAML file.

---

# Why Do We Need Docker Compose?

Suppose an application has:

- Frontend container
- Backend container
- Database container
- Redis container

Without Compose, we may need to run many Docker commands manually.

With Compose, we can define everything in a single file and start the application with one command.

```
docker-compose.yml
        ↓
   Docker Compose
        ↓
┌───────────────┐
│ Frontend      │
│ Backend       │
│ Database      │
│ Redis         │
└───────────────┘
```

---

# Compose File

Docker Compose uses a YAML file to define the application.

Common filenames are:

```
docker-compose.yml
docker-compose.yaml
compose.yml
compose.yaml
```

Example:

```yaml
services:
  frontend:
    image: nginx

  backend:
    image: httpd
```

Here we have two services:

- `frontend`
- `backend`

Each service represents a containerized application/service.

---

# Important Compose Components

A Compose file commonly defines:

### Services

Containers that make up the application.

```yaml
services:
  frontend:
    image: nginx
```

### Networks

Used for communication between services.

```yaml
networks:
  app-network:
```

### Volumes

Used for persistent data.

```yaml
volumes:
  app-data:
```

### Build

Used when we want to build an image from a Dockerfile.

```yaml
services:
  backend:
    build: ./backend
```

---

# Simple Docker Compose Example

```yaml
services:
  frontend:
    image: nginx
    ports:
      - "1111:80"

  backend:
    image: httpd
    ports:
      - "1112:80"
```

This defines two services:

```
frontend → NGINX → port 1111
backend  → HTTPD → port 1112
```

---

# Start the Application

Using modern Docker Compose:

```bash
docker compose up -d
```

This creates and starts the required containers.

- `d` means running in detached/background mode.

---

# Check Running Services

```bash
docker compose ps
```

This shows the containers managed by the Compose project.

---

# Stop the Application

```bash
docker compose stop
```

This stops the containers without removing them.

---

# Start Again

```bash
docker compose start
```

This starts the stopped containers again.

---

# View Logs

```bash
docker compose logs
```

To follow logs continuously:

```bash
docker compose logs -f
```

---

# Build Services

If a service uses a Dockerfile:

```bash
docker compose build
```

This builds the required images.

---

# Stop and Remove the Application

```bash
docker compose down
```

This stops and removes the containers and networks created by Compose.

> Volumes are not normally removed by `docker compose down` unless you explicitly request volume removal.
> 

---

# Useful Docker Compose Commands

| Command | Purpose |
| --- | --- |
| `docker compose up -d` | Start services |
| `docker compose stop` | Stop services |
| `docker compose start` | Start stopped services |
| `docker compose ps` | Show services |
| `docker compose logs` | Show logs |
| `docker compose build` | Build images |
| `docker compose down` | Stop and remove services |
| `docker compose config` | Validate/view Compose configuration |

# Simple Example

Without Compose:

```
docker run ...
docker run ...
docker run ...
docker network create ...
docker volume create ...
```

With Compose:

```
compose.yml
     ↓
docker compose up -d
     ↓
All required services start
```

### Main Idea

> **Docker Compose lets us manage a multi-container application from a single YAML configuration file.**
> 

# Database Service + Networks + Volumes

In a multi-container application, the **database** is usually kept as a separate service.

We can connect the database to a Docker network and use a Docker volume to persist its data.

---

# Database Service

Example:

```yaml
services:

  database:
    image: mysql
    networks:
      - network1
    volumes:
      - volume1:/var/lib/mysql
```

Here:

- `image: mysql` → Uses the MySQL Docker image.
- `networks` → Connects the database to a Docker network.
- `volumes` → Stores database data outside the container's writable layer.

---

# Why Use a Volume for a Database?

Database data should not be lost when the container is removed or recreated.

Without a volume:

```
Database Container
       ↓
Container deleted
       ↓
Data may be lost
```

With a volume:

```
Database Container
       ↓
Docker Volume
       ↓
Data remains
```

Example:

```yaml
volumes:
  volume1:

services:
  database:
    image: mysql
    volumes:
      - volume1:/var/lib/mysql
```

The volume is managed by Docker and can continue to exist even if the database container is removed.

---

# Database Network

The database can be placed on a dedicated Docker network.

```yaml
networks:
  network1:

services:

  database:
    image: mysql
    networks:
      - network1
```

Other services that need to communicate with the database can also join the same network.

Example:

```yaml
services:

  backend:
    image: my-backend
    networks:
      - network1

  database:
    image: mysql
    networks:
      - network1

networks:
  network1:
```

Now:

```
Backend
   │
   │ network1
   ↓
Database
```

The backend can communicate with the database through the Docker network.

---

# Complete Example

A simple application can have:

```
Frontend
   │
   ↓
Backend
   │
   ↓
Database
   │
   ↓
Volume
```

Example Compose file:

```yaml
services:

  frontend:
    image: nginx
    networks:
      - frontend_network

  backend:
    image: my-backend
    networks:
      - frontend_network
      - backend_network
    depends_on:
      - database

  database:
    image: mysql
    networks:
      - backend_network
    volumes:
      - database_data:/var/lib/mysql

networks:
  frontend_network:
  backend_network:

volumes:
  database_data:
```

### What this does

- **Frontend** → connected to `frontend_network`
- **Backend** → connected to both networks
- **Database** → connected only to `backend_network`
- **Database data** → stored in `database_data`
- **Backend** → starts after the database container is started because of `depends_on`

This creates a simple separation between application services and database access.

---
