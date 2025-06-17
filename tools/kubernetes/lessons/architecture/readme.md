## **Kubernetes Architecture**

---

### **1. High-Level Structure**

Kubernetes follows a **client-server architecture** composed of:

* **Control Plane (Master)**
* **Worker Nodes (Minions)**
* **Cluster Store (etcd)**

```mermaid
graph TD
  subgraph Control Plane
    APIServer[kube-apiserver]
    Scheduler[kube-scheduler]
    Controller[kube-controller-manager]
    CloudController[cloud-controller-manager]
    Etcd[etcd (Cluster Store)]
  end

  subgraph Worker Node 1
    Kubelet1[kubelet]
    KubeProxy1[kube-proxy]
    CR1[Container Runtime]
    Pod1[Pod(s)]
  end

  subgraph Worker Node 2
    Kubelet2[kubelet]
    KubeProxy2[kube-proxy]
    CR2[Container Runtime]
    Pod2[Pod(s)]
  end

  User[User (kubectl / UI)] --> APIServer
  APIServer --> Etcd
  APIServer --> Scheduler
  APIServer --> Controller
  APIServer --> CloudController

  APIServer --> Kubelet1
  APIServer --> Kubelet2

  Kubelet1 --> Pod1
  Kubelet2 --> Pod2
  Kubelet1 --> CR1
  Kubelet2 --> CR2
  KubeProxy1 --> Pod1
  KubeProxy2 --> Pod2
```

---

### **2. Kubernetes Cluster**

| Component   | Description                                                                           |
| ----------- | ------------------------------------------------------------------------------------- |
| **Cluster** | A group of nodes managed by the control plane and running containerized applications. |
| **Node**    | A physical or virtual machine that runs containerized workloads via kubelet.          |

---

### **3. Control Plane Components**

These components manage the cluster’s overall state and configuration:

#### **a. kube-apiserver**

* Central access point to the Kubernetes API
* Handles REST operations and validates/executes requests

#### **b. etcd**

* Distributed, consistent key-value store
* Stores all cluster state and configuration
* Backup and restore critical for disaster recovery

#### **c. kube-scheduler**

* Assigns pods to nodes based on:

  * Resource availability
  * Constraints (taints, labels)
  * Affinity rules
  * Custom policies

#### **d. kube-controller-manager**

Manages various controllers:

* **Node Controller**: Monitors node health
* **Replication Controller**: Ensures desired pod count
* **Endpoints Controller**: Manages service endpoints
* **Service Account & Token Controllers**

#### **e. cloud-controller-manager**

* Abstracts cloud-specific operations

  * Node discovery
  * Load balancers
  * Volume provisioning

---

### **4. Node Components (Worker Nodes)**

These components run on every worker node:

#### **a. kubelet**

* Primary agent that:

  * Communicates with the API server
  * Ensures containers are running as defined in the PodSpecs

#### **b. kube-proxy**

* Manages network routing for services
* Handles:

  * IP address management
  * NAT rules
  * Service discovery

#### **c. Container Runtime**

* Executes containers on the node
* Examples:

  * Docker
  * containerd
  * CRI-O

---

### **5. Cluster Store (etcd)**

| Aspect      | Details                                         |
| ----------- | ----------------------------------------------- |
| Role        | Stores entire cluster state in key-value format |
| Security    | Must be encrypted and backed up                 |
| Consistency | Uses Raft consensus algorithm                   |

---

### **6. Add-on Components (Optional but Common)**

| Component              | Role                                      |
| ---------------------- | ----------------------------------------- |
| **CoreDNS**            | DNS for service discovery                 |
| **Ingress Controller** | HTTP(S) routing for external access       |
| **Dashboard**          | Web UI to manage cluster                  |
| **Metrics Server**     | Collects resource metrics for autoscaling |

---

### **7. Communication Flow**

1. User sends a request to `kube-apiserver`
2. `apiserver` validates and stores the desired state in `etcd`
3. Controllers & scheduler act to match actual state with desired state
4. `kubelet` on the worker node applies configuration
5. `kube-proxy` and DNS components route and expose traffic as required

---

### **8. Security Layers**

* **TLS** for all API communications
* **RBAC** for access control
* **Namespaces** for multi-tenancy
* **Network Policies** for isolation
* **Admission Controllers** for validation/mutation

---

### **9. Architecture Features**

| Feature                       | Benefit                                                 |
| ----------------------------- | ------------------------------------------------------- |
| **Decoupled Components**      | Scalability and flexibility                             |
| **Declarative Configuration** | Predictable and version-controlled                      |
| **Self-healing**              | Restarts failed containers, reschedules on node failure |
| **Autoscaling**               | Adjusts pod/node counts dynamically                     |
| **Rolling Updates**           | Zero-downtime deployments                               |

---

### **10. Deployment Models**

* **Single Master Cluster**
* **HA (High Availability) Cluster**
* **Federated Clusters** (for geo-distribution)

---
