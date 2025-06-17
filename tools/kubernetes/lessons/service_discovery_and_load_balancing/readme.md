## **Service Discovery and Load Balancing in Kubernetes**

---

### **Service Discovery**

Service discovery in Kubernetes enables automatic detection of services and their endpoints, allowing components to communicate without hardcoding IPs.

#### **Mechanisms**

* **DNS-Based Discovery (CoreDNS)**

  * Services get a DNS name like `my-service.my-namespace.svc.cluster.local`
  * CoreDNS resolves it to the virtual IP of the service

* **Environment Variables**

  * Kubernetes injects environment variables into pods at startup
  * Includes service name, port, and protocol
  * Example: `MY_SERVICE_SERVICE_HOST`, `MY_SERVICE_SERVICE_PORT`

#### **Discovery Flow**

1. Client pod looks up DNS for service name
2. DNS resolves to **ClusterIP**
3. Traffic is routed to a backend pod via kube-proxy or service mesh

---

### **Service Object**

The service object abstracts a set of pods and handles routing traffic to them.

| Type                                     | Use Case                                                                  |
| ---------------------------------------- | ------------------------------------------------------------------------- |
| **ClusterIP**                            | Default; for internal communication only                                  |
| **NodePort**                             | Exposes service on a static port across all nodes                         |
| **LoadBalancer**                         | Provisions an external load balancer (cloud-provider based)               |
| **ExternalName**                         | Maps service to an external DNS name outside the cluster                  |
| **Headless Service** (`clusterIP: None`) | Directly returns pod IPs for client-side load balancing or service meshes |

---

### **Load Balancing**

Kubernetes performs basic load balancing at the service level by distributing requests among pod endpoints.

#### **Components Involved**

* **kube-proxy**

  * Implements load balancing using `iptables` or `IPVS`
  * Forwards requests from service IP to a selected pod

* **Service Endpoint List**

  * Maintained dynamically as pods scale or restart
  * Used by kube-proxy to balance traffic

#### **Strategies**

* Round-robin (default for kube-proxy with iptables/IPVS)
* Session Affinity (`ClientIP`): routes traffic from a client to the same pod

---

### **Ingress Load Balancing**

Used for **HTTP/HTTPS** routing at layer 7.

* **Ingress Controller** (e.g., NGINX, Traefik):

  * Routes traffic based on paths, hosts, etc.
  * Handles TLS termination
* **Ingress Resource**:

  * Defines routing rules
  * Targets specific services

---

### **External Load Balancing**

* For cloud environments:

  * **LoadBalancer** type creates a cloud provider-managed LB
* For on-premises:

  * Combine **NodePort** with an external load balancer (e.g., MetalLB)

---

### **Advanced Load Balancing with Service Mesh**

* Tools like **Istio**, **Linkerd** provide:

  * Fine-grained traffic control
  * mTLS
  * A/B testing, canary routing
  * Observability and retries

---
