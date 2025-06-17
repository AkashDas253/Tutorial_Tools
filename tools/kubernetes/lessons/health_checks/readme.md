## **Health Checks in Kubernetes**

---

### **Purpose**

Health checks allow Kubernetes to monitor and maintain the health of containers, ensuring high availability, fault detection, and automatic recovery.

---

### **Types of Probes**

| Probe Type    | Purpose                                       | Effect                                              |
| ------------- | --------------------------------------------- | --------------------------------------------------- |
| **Liveness**  | Checks if the container is **alive**          | If fails, container is **restarted**                |
| **Readiness** | Checks if the container is **ready** to serve | If fails, pod is **removed from Service endpoints** |
| **Startup**   | Checks if the container **has started**       | Blocks liveness & readiness until successful        |

---

### **Probe Handler Types**

| Handler        | Description                                         |
| -------------- | --------------------------------------------------- |
| **HTTP GET**   | Performs an HTTP GET on a container endpoint        |
| **TCP Socket** | Opens a TCP connection to the specified port        |
| **Exec**       | Runs a command inside the container                 |
| **gRPC**       | (v1.24+) Calls a gRPC service with health check API |

---

### **Configuration Fields**

| Field                 | Description                                      |
| --------------------- | ------------------------------------------------ |
| `initialDelaySeconds` | Time before first probe (gives app time to boot) |
| `periodSeconds`       | Time between subsequent checks                   |
| `timeoutSeconds`      | Timeout for a single probe attempt               |
| `successThreshold`    | Min consecutive successes to mark healthy        |
| `failureThreshold`    | Max consecutive failures to mark unhealthy       |

---

### **Example: Liveness and Readiness Probes**

```yaml
livenessProbe:
  httpGet:
    path: /healthz
    port: 8080
  initialDelaySeconds: 10
  periodSeconds: 5

readinessProbe:
  tcpSocket:
    port: 8080
  initialDelaySeconds: 5
  periodSeconds: 10
```

---

### **Example: Startup Probe**

```yaml
startupProbe:
  exec:
    command:
    - cat
    - /tmp/healthy
  initialDelaySeconds: 5
  periodSeconds: 10
  failureThreshold: 30
```

---

### **Best Practices**

* Use **startup probes** for slow-starting apps to avoid premature restarts.
* Always define **readiness probes** for services exposed to users.
* Combine probes logically to ensure lifecycle correctness.

---
