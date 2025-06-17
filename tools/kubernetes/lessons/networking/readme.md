## **Networking in Kubernetes**

---

### **Pod-to-Pod Communication**

* Every pod gets a unique IP address.
* Pods can communicate **without NAT** within the same cluster.
* Network rules enforced via **network plugins** (CNI).

---

### **Service**

* Provides stable access to a dynamic set of pods.
* Acts as a **load balancer** and **discovery mechanism**.
* Types:

  * **ClusterIP**: Default; accessible only within cluster
  * **NodePort**: Exposes service on each node’s IP at a static port
  * **LoadBalancer**: Uses cloud provider’s external LB
  * **ExternalName**: Maps service to external DNS name

---

### **DNS (CoreDNS)**

* Automatically provides DNS names for services and pods.
* Resolves names like `my-service.my-namespace.svc.cluster.local`.

---

### **Ingress**

* Manages external HTTP/HTTPS access to services.
* Provides:

  * URL routing
  * SSL termination
  * Host-based routing
* Requires an **Ingress Controller** (e.g., NGINX, Traefik)

---

### **Network Policies**

* Define **rules for pod communication** (who can talk to whom).
* Based on:

  * Pod selectors
  * Namespace selectors
  * IP blocks
* Default is open; policies restrict it.

---

### **CNI (Container Network Interface)**

* Pluggable architecture for networking backends.
* Popular CNI plugins:

  * Calico
  * Flannel
  * Weave Net
  * Cilium

---

### **kube-proxy**

* Maintains network rules for services.
* Uses:

  * **iptables** or **IPVS** to route traffic
  * Forwards service requests to backend pods

---

### **Service Discovery**

* Done via:

  * Environment variables (injected into pods)
  * DNS entries (CoreDNS)

---

### **Endpoints**

* Objects that map a service to its current backend pods.
* Dynamically updated as pods start/stop.

---

### **Port Types**

| Port Type         | Description                                              |
| ----------------- | -------------------------------------------------------- |
| **containerPort** | Port the application listens to inside the container     |
| **hostPort**      | Maps containerPort to port on the node                   |
| **nodePort**      | Exposes service on a static port on all nodes            |
| **targetPort**    | Port that the service forwards traffic to inside the pod |

---

### **Overlay Networking**

* Abstracts pod communication across multiple hosts.
* CNI plugins use virtual networks over physical interfaces.

---
