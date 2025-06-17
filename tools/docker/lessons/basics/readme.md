### Docker Basics

#### 1. **What is Docker?**
Docker is a platform for developing, shipping, and running applications inside containers. Containers are lightweight, portable, and ensure consistent environments across development, testing, and production.

---

#### 2. **Core Docker Components**
- **Images**: Read-only templates used to create containers. Built using Dockerfiles.
- **Containers**: Instances of images, representing the runtime environment for your applications.
- **Dockerfile**: A script containing instructions to build Docker images.
- **Docker Hub**: A registry for storing and sharing Docker images.

---

#### 3. **Common Docker Commands**

**3.1 docker run**
- Starts a new container from an image.
```bash
docker run [OPTIONS] IMAGE [COMMAND]
```
- Example: 
```bash
docker run -d -p 8080:80 nginx
```
  - `-d`: Run container in detached mode.
  - `-p`: Map host port 8080 to container port 80.

---

**3.2 docker ps**
- Lists running containers.
```bash
docker ps
```
- To list all containers (including stopped ones):
```bash
docker ps -a
```

---

**3.3 docker build**
- Builds an image from a Dockerfile.
```bash
docker build -t my-image .
```
- `-t`: Tags the image with a name.

---

**3.4 docker images**
- Lists all images on the system.
```bash
docker images
```

---

**3.5 docker pull**
- Downloads an image from Docker Hub or another registry.
```bash
docker pull nginx
```

---

**3.6 docker push**
- Uploads an image to a registry (requires login).
```bash
docker push my-image:tag
```

---

**3.7 docker stop**
- Stops a running container.
```bash
docker stop container_name_or_id
```

---

**3.8 docker rm**
- Removes a stopped container.
```bash
docker rm container_name_or_id
```

---

**3.9 docker rmi**
- Removes an image.
```bash
docker rmi image_name_or_id
```

---

#### 4. **Dockerfile Basics**
A **Dockerfile** defines how an image is built.

**Sample Dockerfile**:
```dockerfile
# Use a base image
FROM python:3.9-slim

# Set the working directory
WORKDIR /app

# Copy project files into the container
COPY . /app

# Install dependencies
RUN pip install -r requirements.txt

# Expose the application port
EXPOSE 5000

# Define the default command
CMD ["python", "app.py"]
```

---

#### 5. **Key Dockerfile Instructions**
- **FROM**: Specifies the base image.
- **WORKDIR**: Sets the working directory inside the container.
- **COPY**: Copies files from the host to the image.
- **RUN**: Executes commands to build the image (e.g., installing dependencies).
- **CMD**: Specifies the default command for the container.

---

#### 6. **Docker Compose**
For multi-container applications, Docker Compose simplifies setup using a `docker-compose.yml` file.

**Sample `docker-compose.yml`**:
```yaml
version: '3.8'
services:
  app:
    build: .
    ports:
      - "5000:5000"
  db:
    image: postgres:latest
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
```

Run the application:
```bash
docker-compose up
```

---

#### 7. **Volumes**
Persist data between container restarts using volumes.

- Create and mount a volume:
```bash
docker run -d -v my-volume:/data nginx
```

---

#### 8. **Best Practices**
- Use official base images.
- Keep Dockerfiles simple and clean.
- Use `.dockerignore` to exclude unnecessary files.
- Limit container permissions for security.

---