# Docker Cheat Sheet

## Basic Concepts

- **Image**: A lightweight, standalone, and executable package that includes everything needed to run a piece of software (code, libraries, environment variables).
- **Container**: A running instance of an image, which includes the application and its dependencies.
- **Dockerfile**: A text file containing commands to build a Docker image.

---

## Installing Docker

- **On Linux**
  - Install Docker: `sudo apt-get install docker.io`
  - Start Docker service: `sudo systemctl start docker`
  - Enable Docker at startup: `sudo systemctl enable docker`

- **On Windows and Mac**
  - Download and install from `https://www.docker.com/get-started`

---

## Common Commands

- **Check Docker Version**: `docker --version`
- **Display Docker Info**: `docker info`
- **List Running Containers**: `docker ps`
- **List All Containers**: `docker ps -a`
- **List All Images**: `docker images`
- **Start a Container**: `docker start <container-id>`
- **Stop a Container**: `docker stop <container-id>`
- **Remove a Container**: `docker rm <container-id>`
- **Remove an Image**: `docker rmi <image-id>`
- **Kill a Running Container**: `docker kill <container-id>`

---

## Working with Images

- **Pull an Image**: `docker pull <image-name>`
- **Build an Image from Dockerfile**: `docker build -t <image-name> .`
- **Tag an Image**: `docker tag <image-id> <repository>:<tag>`
- **Push an Image to Docker Hub**: `docker push <repository>:<tag>`
- **Search for Images**: `docker search <image-name>`
- **Save an Image to File**: `docker save -o <file-name>.tar <image-name>`
- **Load an Image from File**: `docker load -i <file-name>.tar`

---

## Running Containers

- **Run a Container**:
  - `docker run <image-name>`
  - Example: `docker run ubuntu`
  
- **Run a Container with Interactive Terminal**: `docker run -it <image-name> /bin/bash`
  
- **Run a Container in Detached Mode**: `docker run -d <image-name>`

- **Name a Container**: `docker run --name <container-name> <image-name>`

- **Run with Port Mapping**: `docker run -p <host-port>:<container-port> <image-name>`
  - Example: `docker run -p 8080:80 nginx`

- **Run with Volume Mounting**: `docker run -v <host-path>:<container-path> <image-name>`
  - Example: `docker run -v /host/data:/container/data ubuntu`

---

## Managing Containers

- **Start a Stopped Container**: `docker start <container-id>`
- **Stop a Running Container**: `docker stop <container-id>`
- **Restart a Container**: `docker restart <container-id>`
- **Attach to a Running Container**: `docker attach <container-id>`
- **Rename a Container**: `docker rename <old-name> <new-name>`

---

## Container Logs

- **View Container Logs**: `docker logs <container-id>`
- **Tail Logs (Real-Time)**: `docker logs -f <container-id>`

---

## Networking

- **List Networks**: `docker network ls`
- **Create a Network**: `docker network create <network-name>`
- **Connect a Container to a Network**: `docker network connect <network-name> <container-id>`
- **Disconnect a Container from a Network**: `docker network disconnect <network-name> <container-id>`
- **Inspect a Network**: `docker network inspect <network-name>`

---

## Docker Volumes

- **List Volumes**: `docker volume ls`
- **Create a Volume**: `docker volume create <volume-name>`
- **Inspect a Volume**: `docker volume inspect <volume-name>`
- **Remove a Volume**: `docker volume rm <volume-name>`
- **Mount a Volume to a Container**: 
  - `docker run -v <volume-name>:<container-path> <image-name>`
  - Example: `docker run -v my_data:/var/www/html ubuntu`

---

## Docker Compose

- **What is Docker Compose**: A tool for defining and running multi-container Docker applications using a YAML file (`docker-compose.yml`).

- **Common Commands**:
  - Start services: `docker-compose up`
  - Start services in detached mode: `docker-compose up -d`
  - Stop services: `docker-compose down`
  - Build services: `docker-compose build`
  - View service logs: `docker-compose logs`
  - View real-time logs: `docker-compose logs -f`
  - Scale services: `docker-compose up --scale <service-name>=<num-instances>`

- **Basic `docker-compose.yml` Example**:
  ```yaml
  version: '3'
  services:
    web:
      image: nginx
      ports:
        - "8080:80"
    db:
      image: mysql
      environment:
        MYSQL_ROOT_PASSWORD: example

## Dockerfile Basics

- **Dockerfile Commands**:
  - `FROM`: Sets the base image.
  - `RUN`: Executes commands in a new layer on top of the current image.
  - `COPY` or `ADD`: Copies files/directories into the container.
  - `CMD`: Specifies the default command to run within the container.
  - `ENTRYPOINT`: Sets a command that will always run when the container starts.
  - `EXPOSE`: Informs Docker that the container listens on the specified network ports.
  - `ENV`: Sets environment variables.

- **Sample Dockerfile**:
  ```Dockerfile
  # Use an official Python runtime as a parent image
  FROM python:3.8-slim

  # Set the working directory in the container
  WORKDIR /app

  # Copy the current directory contents into the container at /app
  COPY . /app

  # Install any needed packages
  RUN pip install --no-cache-dir -r requirements.txt

  # Make port 80 available to the world outside this container
  EXPOSE 80

  # Run the application
  CMD ["python", "app.py"]

## Docker Swarm

- **Initialize a Swarm**: `docker swarm init`
- **Join a Swarm**: `docker swarm join --token <token> <manager-ip>`
- **List Nodes in the Swarm**: `docker node ls`
- **Deploy a Stack**: `docker stack deploy -c <compose-file> <stack-name>`
- **List Stacks**: `docker stack ls`
- **List Services in a Stack**: `docker stack services <stack-name>`
- **Remove a Stack**: `docker stack rm <stack-name>`

---

## Useful Docker Tips

- **Clean Up Unused Resources**:
  - Remove unused containers: `docker container prune`
  - Remove unused images: `docker image prune`
  - Remove all unused resources: `docker system prune -a`
  
- **Check Disk Usage**: `docker system df`
  
- **Export a Running Container to Image**: `docker commit <container-id> <new-image-name>`
