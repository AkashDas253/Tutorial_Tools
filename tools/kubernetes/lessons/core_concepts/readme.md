## **Core Concepts in Kubernetes**

---

### **Cluster**

* A collection of machines (nodes) that run containerized applications.
* Managed by the control plane to maintain desired state and ensure orchestration.

---

### **Node**

* A physical or virtual machine within a Kubernetes cluster.
* Types:

  * **Master Node**: Runs control plane components.
  * **Worker Node**: Runs containerized applications (pods).
* Key components on worker node:

  * `kubelet`, `kube-proxy`, and container runtime.

---

### **Pod**

* The smallest and most basic deployable unit in Kubernetes.
* Represents one or more containers sharing:

  * Network namespace (IP, ports)
  * Storage volumes
* Types:

  * Single-container pod
  * Multi-container pod (e.g., with sidecar)

---

### **ReplicaSet**

* Ensures a specified number of identical pod replicas are running at all times.
* Automatically replaces failed pods.

---

### **Deployment**

* Provides declarative updates for Pods and ReplicaSets.
* Supports:

  * Rolling updates
  * Rollbacks
  * Version history

---

### **StatefulSet**

* Manages stateful applications.
* Provides:

  * Persistent storage with stable identity
  * Ordered deployment and scaling
  * Ordered rolling updates

---

### **DaemonSet**

* Ensures one pod runs on **every node** (or selected nodes).
* Used for:

  * Node monitoring (e.g., log agents)
  * Networking tools (e.g., CNI)

---

### **Job**

* Creates one or more pods that **run to completion**.
* Used for:

  * Batch processing
  * One-off tasks

---

### **CronJob**

* Runs Jobs **on a schedule**.
* Follows standard UNIX cron syntax.
* Good for recurring batch tasks or maintenance.

---

### **Service**

* Abstracts and exposes a group of pods as a network service.
* Types:

  * **ClusterIP**: Internal access within the cluster
  * **NodePort**: Exposes service on a static port on each node
  * **LoadBalancer**: Uses external load balancer for access
  * **ExternalName**: Maps to an external DNS name

---

### **Volume**

* Provides storage to be shared between containers in a pod.
* Types:

  * `emptyDir`, `hostPath`, `persistentVolumeClaim`, `configMap`, `secret`, etc.

---

### **PersistentVolume (PV)**

* Cluster-level storage resource provisioned by an admin or dynamically.

---

### **PersistentVolumeClaim (PVC)**

* A request for storage by a user or pod.
* Binds to a matching PV based on size and access mode.

---

### **Namespace**

* Virtual cluster within a physical cluster.
* Used for:

  * Multi-tenancy
  * Resource segregation
  * Access control

---

### **Label**

* Key-value pairs attached to Kubernetes objects.
* Used for:

  * Selection
  * Grouping
  * Management

---

### **Selector**

* Queries for labels to operate on selected sets of objects (e.g., in a service or ReplicaSet).

---

### **Annotation**

* Non-identifying metadata attached to objects.
* Used by tools and system components.

---

### **Taints and Tolerations**

* **Taints**: Mark a node as unsuitable for some pods.
* **Tolerations**: Allow pods to be scheduled on tainted nodes.

---

### **Affinity and Anti-Affinity**

* Rules for scheduling pods based on other pods or node labels.

  * **Node Affinity**: Schedule pods on specific nodes.
  * **Pod Affinity**: Co-locate pods together.
  * **Pod Anti-Affinity**: Keep pods away from each other.

---
