## **Key Subconcepts**

### **Networking**
Docker provides several networking options to allow containers to communicate with each other, the host system, and external networks.

1. **Bridge Network**:
   - Default network for containers on a single host.
   - Containers on the same bridge can communicate using container names.
   - Example:
     ```bash
     docker network create my_bridge
     docker run --network=my_bridge --name=app1 my_image
     ```
   - Use Cases:
     - Isolated container communication within the same host.

2. **Host Network**:
   - Binds the container directly to the host's network.
   - No network isolation between the host and the container.
   - Example:
     ```bash
     docker run --network=host my_image
     ```
   - Use Cases:
     - Performance-sensitive applications requiring minimal network latency.

3. **Overlay Network**:
   - Enables communication between containers across multiple hosts.
   - Typically used in Docker Swarm or Kubernetes.
   - Example:
     ```bash
     docker network create -d overlay my_overlay
     ```
   - Use Cases:
     - Multi-host container communication.

4. **None Network**:
   - Completely disables networking for a container.
   - Example:
     ```bash
     docker run --network=none my_image
     ```
   - Use Cases:
     - Containers requiring complete isolation.

5. **Docker DNS**:
   - Automatic DNS resolution for container names on the same custom network.
   - Simplifies service discovery in containerized applications.

---

### **Storage**
Docker provides flexible storage options for persisting data beyond the lifecycle of a container.

1. **Volumes**:
   - Managed by Docker and stored outside the container’s writable layer.
   - Provides high performance and is the recommended way to persist data.
   - Example:
     ```bash
     docker volume create my_volume
     docker run -v my_volume:/data my_image
     ```
   - Use Cases:
     - Sharing data between containers.

2. **Bind Mounts**:
   - Directly maps a file or directory from the host to the container.
   - Path must exist on the host.
   - Example:
     ```bash
     docker run -v /host_path:/container_path my_image
     ```
   - Use Cases:
     - Accessing host files (e.g., configuration files).

3. **tmpfs**:
   - Mounts temporary storage directly in the container’s memory.
   - Data is not written to disk and is lost when the container stops.
   - Example:
     ```bash
     docker run --tmpfs /tmp my_image
     ```
   - Use Cases:
     - High-speed access to temporary data.

---

### **Orchestration**
Docker enables managing and scaling containerized applications efficiently.

1. **Docker Swarm**:
   - Native clustering and orchestration tool in Docker.
   - Features:
     - Service discovery
     - Load balancing
     - Scaling services
   - Example:
     ```bash
     docker swarm init
     docker service create --replicas=3 my_service
     ```

2. **Services and Tasks**:
   - **Service**: A definition of how containers behave (e.g., replicas, image).
   - **Task**: A single running container managed by a service.

3. **Scaling Containers**:
   - Adjust the number of replicas for a service dynamically.
   - Example:
     ```bash
     docker service scale my_service=5
     ```

---

### **Security**
Docker incorporates several features to enhance container security.

1. **Namespaces**:
   - Isolate container processes, network, and filesystem.
   - Each container has its own namespace (e.g., PID, net, mnt).

2. **Control Groups (cgroups)**:
   - Limit and allocate resources (CPU, memory) to containers.
   - Example:
     ```bash
     docker run --memory=512m --cpus=1 my_image
     ```

3. **Docker Content Trust (DCT)**:
   - Ensures image integrity by verifying signed images.
   - Example:
     ```bash
     export DOCKER_CONTENT_TRUST=1
     ```

4. **Secrets Management**:
   - Securely store and manage sensitive information like passwords.
   - Example:
     ```bash
     docker secret create my_secret /path/to/secret
     ```

---
