# Docker Hub — Push & Pull Images

## What is Docker Hub?

**Docker Hub** is a public Docker registry where we can store and share Docker images.

We can:

- Push our Docker images to Docker Hub
- Pull images from Docker Hub
- Share images with other developers
- Use images on different servers

---

# Basic Flow

```
Build Docker Image
       ↓
Tag Image
       ↓
Login to Docker Hub
       ↓
Push Image
       ↓
Docker Hub
       ↓
Pull Image on another machine
```

---

# Step 1: Create a Docker Hub Repository

First, create an account on Docker Hub.

Then create a repository.

For example:

```
Username: SandhyaM
Repository: Docker
```

The image name will follow this format:

```
username/repository:tag
```

Example:

```
SandhyaM/Docker:new
```

---

# Step 2: Tag Your Docker Image

Suppose we already have an image:

```bash
docker images
```

Example:

```
myimage    latest
```

Tag it using your Docker Hub repository name:

```bash
docker tag myimage:latest SandhyaM/Docker:new
```

Now Docker knows where this image should be pushed.

---

# Step 3: Login to Docker Hub

```bash
docker login
```

Docker will ask for your Docker Hub credentials.

After successful login, you can push images to your repository.

---

# Step 4: Push the Image

```bash
docker push SandhyaM/Docker:new
```

Docker uploads the image to the Docker Hub repository.

After the push completes, the image will be available in your Docker Hub repository.

---

# Step 5: Pull the Image

On another machine, we can download the image using:

```bash
docker pull SandhyaM/Docker:new
```

Then check the downloaded image:

```bash
docker images
```

---

# Step 6: Run the Pulled Image

After pulling the image:

```bash
docker run -d --name mycontainer SandhyaM/Docker:new
```

Now the container is created from the image downloaded from Docker Hub.

---

# Complete Example

### Build

```bash
docker build -t myapp:1.0 .
```

### Tag

```bash
docker tag myapp:1.0 SandhyaM/myapp:1.0
```

### Login

```bash
docker login
```

### Push

```bash
docker push SandhyaM/myapp:1.0
```

### Pull on another server

```bash
docker pull SandhyaM/myapp:1.0
```

### Run

```bash
docker run -d --name myapp-container SandhyaM/myapp:1.0
```

---

# Removing a Local Image

If you want to remove an image from your local machine:

```bash
docker rmi myapp:1.0
```

This removes the **local image**.

It does not remove the image from Docker Hub.

---

# Important Naming Format

Docker Hub images generally follow:

```
username/repository:tag
```

Example:

```
SandhyaM/Docker:new
```

Where:

```
SandhyaM → Docker Hub username
Docker   → Repository name
new      → Image tag
```
