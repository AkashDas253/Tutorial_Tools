## **Extending Kubernetes**

---

### **Purpose**

Kubernetes is highly extensible, allowing you to **customize, enhance, or integrate** additional functionality **without modifying its core code**. This is essential for adapting Kubernetes to specific infrastructure, operational policies, or application requirements.

---

### **Key Extension Mechanisms**

---

### **Custom Resource Definitions (CRDs)**

* Add new **API resource types** to Kubernetes.
* Work like native resources (e.g., Pods, Deployments).
* Used to manage domain-specific objects (e.g., `Database`, `BackupJob`).

**Extension Example:**
Define `CronTab` as a new resource type using CRDs.

---

### **Controllers and Operators**

* **Controllers**: Watch and reconcile state of CRs or built-in resources.
* **Operators**: Combine CRDs with custom controllers to automate complex application logic.

**Use Cases:**

* Database lifecycle management
* Custom provisioning logic
* Stateful systems like Kafka, PostgreSQL

---

### **Admission Controllers**

* Webhooks that intercept API requests **before persistence**.
* Types:

  * **Validating Admission Webhooks**: Block/allow requests based on custom rules.
  * **Mutating Admission Webhooks**: Modify requests (e.g., inject sidecars).

**Common Use:** Enforcing policies (e.g., `resource limits`, `naming conventions`).

---

### **API Aggregation Layer**

* Add **entire new API groups** alongside the core Kubernetes API.
* Register external servers as extensions via **Aggregation Layer**.
* Used when you need full control over API behavior (e.g., advanced auth, logic).

---

### **Dynamic Admission Webhooks**

* Define **validation or mutation** logic dynamically via CRDs.
* Loaded and invoked on demand by the API server.

---

### **Scheduler Extender**

* Customize pod scheduling without replacing the default scheduler.
* External HTTP service receives scheduling decisions.

**Use Cases:**

* Custom prioritization
* Multi-tenancy
* Resource-aware placement

---

### **Custom CLI Plugins**

* Extend `kubectl` using custom binaries prefixed with `kubectl-`.

```bash
kubectl myplugin
```

* Appears like native command if placed in `$PATH`.

---

### **Device Plugins**

* Register and advertise **hardware devices** (e.g., GPUs, FPGAs) to the Kubelet.
* Enable dynamic device discovery and lifecycle management.

---

### **Container Runtime Interface (CRI)**

* Pluggable container runtimes via **CRI** (e.g., containerd, CRI-O).

---

### **Network Plugin Interface (CNI)**

* Support custom **networking models** via **CNI plugins** (Calico, Flannel, Cilium).
* Handles pod IP address allocation, routing, and network policy.

---

### **Storage Interface (CSI)**

* Support third-party **storage drivers** using **CSI**.
* Enables block and file storage provisioning in a standardized way.

---

### **Metrics Server & Custom Metrics**

* Add **custom application metrics** to support autoscaling and observability.
* Custom metrics used in **Horizontal Pod Autoscaler (HPA)** or **Prometheus Adapter**.

---

### **Service Catalog & Service Brokers**

* Extend Kubernetes to **provision managed services** (e.g., databases, queues) via API.
* Uses **Open Service Broker API** to integrate external service providers.

---

### **Open Policy Agent (OPA) / Gatekeeper**

* Use **OPA** to define custom policies (RBAC, labels, quotas).
* Enforced at runtime via Gatekeeper (validating admission webhook controller).

---

### **Kubernetes API Extensions Table**

| Extension Mechanism   | Purpose                           | Key Component                  |
| --------------------- | --------------------------------- | ------------------------------ |
| CRDs                  | Define new resource types         | `CustomResourceDefinition`     |
| Operators             | App-specific lifecycle automation | CRDs + Custom Controller       |
| Admission Webhooks    | Mutate/validate API requests      | Webhook server                 |
| API Aggregation Layer | Add new APIs                      | `APIService`, extension server |
| Scheduler Extender    | Custom pod scheduling logic       | HTTP extension API             |
| Device Plugin         | Advertise hardware resources      | gRPC Plugin                    |
| CNI                   | Pod networking                    | CNI plugin                     |
| CSI                   | Storage management                | CSI driver                     |
| OPA/Gatekeeper        | Custom policy enforcement         | Rego policies + Webhooks       |
| Kubectl Plugins       | Extend CLI functionality          | Shell binaries                 |

---
