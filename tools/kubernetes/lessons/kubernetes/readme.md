## **Overview of Kubernetes**

---

### **Definition**

Kubernetes (K8s) is an **open-source container orchestration platform** that automates the **deployment, scaling, management, and operation** of application containers (e.g., Docker). It abstracts infrastructure and provides a consistent environment for development and operations.

---

### **Core Concepts**

| Component          | Description                                                                                      |
| ------------------ | ------------------------------------------------------------------------------------------------ |
| **Cluster**        | A set of nodes (VMs or physical machines) running containerized applications.                    |
| **Node**           | A worker machine in Kubernetes, either a VM or a physical machine.                               |
| **Pod**            | The smallest deployable unit; a group of one or more containers with shared storage and network. |
| **Service**        | Defines a policy to access pods, enabling communication between components.                      |
| **Volume**         | Persistent or ephemeral storage attached to pods.                                                |
| **Namespace**      | Logical partitioning of cluster resources for multi-tenancy.                                     |
| **Label/Selector** | Key-value pairs for organizing, selecting, and operating on Kubernetes resources.                |

---

### **Architecture**

#### **Master Components (Control Plane)**

| Component                    | Role                                                                  |
| ---------------------------- | --------------------------------------------------------------------- |
| **kube-apiserver**           | Central API interface for all operations.                             |
| **etcd**                     | Consistent and highly available key-value store for all cluster data. |
| **kube-scheduler**           | Assigns pods to nodes based on constraints and availability.          |
| **kube-controller-manager**  | Runs various controllers to regulate system state.                    |
| **cloud-controller-manager** | Manages cloud-specific control logic.                                 |

#### **Node Components**

| Component             | Role                                               |
| --------------------- | -------------------------------------------------- |
| **kubelet**           | Agent on each node to manage pod lifecycle.        |
| **kube-proxy**        | Manages network routing for services.              |
| **Container Runtime** | Runs containers (e.g., Docker, containerd, CRI-O). |

---

### **Workloads and Controllers**

| Controller      | Purpose                                                   |
| --------------- | --------------------------------------------------------- |
| **Deployment**  | Manages stateless applications; provides rolling updates. |
| **StatefulSet** | Manages stateful applications with stable identities.     |
| **DaemonSet**   | Ensures a pod runs on all (or some) nodes.                |
| **Job**         | Creates pods that run to completion.                      |
| **CronJob**     | Creates jobs on a scheduled time.                         |
| **ReplicaSet**  | Ensures a specified number of pod replicas are running.   |

---

### **Networking**

| Feature                | Description                                               |
| ---------------------- | --------------------------------------------------------- |
| **Flat Network**       | All pods can communicate without NAT.                     |
| **Service Discovery**  | Services get DNS names for pod communication.             |
| **Ingress Controller** | Manages external access to services (HTTP/HTTPS routing). |
| **Network Policies**   | Restrict traffic between pods using firewall rules.       |

---

### **Storage in Kubernetes**

| Type                            | Description                                                      |
| ------------------------------- | ---------------------------------------------------------------- |
| **PersistentVolume (PV)**       | Cluster-wide storage resource.                                   |
| **PersistentVolumeClaim (PVC)** | Request for PV by a pod.                                         |
| **StorageClass**                | Defines types of storage (e.g., SSD, HDD, dynamic provisioners). |

---

### **Configuration Management**

| Object                    | Use                                                          |
| ------------------------- | ------------------------------------------------------------ |
| **ConfigMap**             | Inject configuration data as environment variables or files. |
| **Secret**                | Store and manage sensitive data like passwords, tokens, etc. |
| **Environment Variables** | Direct injection into pods.                                  |
| **Annotations**           | Non-identifying metadata for tools.                          |

---

### **Security**

| Feature                              | Purpose                             |
| ------------------------------------ | ----------------------------------- |
| **RBAC (Role-Based Access Control)** | Regulate access to resources.       |
| **Service Accounts**                 | Identity for processes inside pods. |
| **PodSecurityPolicies (deprecated)** | Define pod-level security rules.    |
| **Network Policies**                 | Limit pod-to-pod communication.     |
| **Secrets Encryption**               | Encrypt secrets at rest in `etcd`.  |

---

### **Kubernetes Objects (Manifests)**

Defined in YAML or JSON

| Field        | Description               |
| ------------ | ------------------------- |
| `apiVersion` | API version               |
| `kind`       | Resource type             |
| `metadata`   | Name, labels, annotations |
| `spec`       | Desired state             |

---

### **Kubernetes Tools**

| Tool          | Function                                   |
| ------------- | ------------------------------------------ |
| **kubectl**   | Command-line tool to interact with K8s API |
| **Helm**      | Kubernetes package manager (charts)        |
| **kustomize** | Template-free configuration customization  |
| **Minikube**  | Run local K8s cluster for development      |
| **kubeadm**   | Tool to bootstrap a Kubernetes cluster     |
| **Dashboard** | Web-based GUI for managing clusters        |

---

### **Common Operations**

| Operation           | Description                                        |
| ------------------- | -------------------------------------------------- |
| **Rolling Update**  | Gradually update pods with zero downtime           |
| **Scaling**         | Increase/decrease number of pod replicas           |
| **Self-healing**    | Restart failed containers automatically            |
| **Resource Quotas** | Control resource usage per namespace               |
| **Health Checks**   | Liveness and readiness probes for container health |

---

### **Advanced Features**

* **Autoscaling**:

  * Horizontal Pod Autoscaler (HPA)
  * Vertical Pod Autoscaler (VPA)
  * Cluster Autoscaler

* **Federation**:

  * Manage multiple clusters across regions

* **Custom Resources**:

  * Extend Kubernetes with CRDs and controllers

* **Service Mesh** (via Istio/Linkerd):

  * Observability, security, traffic control between services

---

### **Use Cases**

* Microservices deployment
* CI/CD pipelines
* Hybrid and multi-cloud infrastructure
* Big Data and AI/ML workflows
* Edge computing

---

### **Benefits**

* Automated scaling and failover
* Platform-agnostic deployment
* Declarative configuration and infrastructure as code
* Improved resource utilization
* Ecosystem and extensibility

---
