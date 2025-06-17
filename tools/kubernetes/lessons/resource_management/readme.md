## **Resource Management in Kubernetes**

---

### **Resource Requests and Limits**

* Control the CPU and memory (RAM) usage of containers.
* Defined in pod specs under `resources`.

#### **Request**

* Minimum amount of resource guaranteed.
* Scheduler uses it to place pods on appropriate nodes.

#### **Limit**

* Maximum resource a container can use.
* If exceeded:

  * CPU: throttled
  * Memory: pod is killed (OOM)

```yaml
resources:
  requests:
    memory: "512Mi"
    cpu: "500m"
  limits:
    memory: "1Gi"
    cpu: "1"
```

---

### **QoS (Quality of Service) Classes**

* Kubernetes assigns QoS class to each pod based on its resource requests/limits.

| QoS Class      | Conditions                                           |
| -------------- | ---------------------------------------------------- |
| **Guaranteed** | All containers have equal `requests = limits`        |
| **Burstable**  | Some, but not all containers have requests or limits |
| **BestEffort** | No requests or limits specified                      |

---

### **Resource Quotas**

* Enforce resource usage **limits per namespace**.
* Prevent a single team/app from consuming all cluster resources.
* Types:

  * **Compute resources** (CPU, memory)
  * **Object count** (pods, services)
  * **Storage** (PVCs, ephemeral storage)

```yaml
apiVersion: v1
kind: ResourceQuota
spec:
  hard:
    requests.cpu: "4"
    requests.memory: "8Gi"
    pods: "10"
```

---

### **LimitRange**

* Sets default **resource requests and limits per container** within a namespace.
* Ensures containers don’t start without proper resource specs.

```yaml
apiVersion: v1
kind: LimitRange
spec:
  limits:
  - default:
      cpu: 1
      memory: 1Gi
    defaultRequest:
      cpu: 500m
      memory: 512Mi
    type: Container
```

---

### **Horizontal Pod Autoscaler (HPA)**

* Automatically scales the number of pod replicas based on CPU/memory or custom metrics.
* Requires metrics server installed.

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: my-app
  minReplicas: 2
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 80
```

---

### **Vertical Pod Autoscaler (VPA)**

* Adjusts CPU and memory **requests/limits of individual pods** automatically.
* Not used together with HPA in most cases.

---

### **Cluster Autoscaler**

* Automatically scales the **number of nodes** in the cluster.
* Adds nodes if pods are pending due to resource shortage.
* Removes nodes if underutilized.

---

### **Priority and Preemption**

* Assigns **priority** to pods using `PriorityClass`.
* If resources are scarce, lower-priority pods may be evicted.

```yaml
apiVersion: scheduling.k8s.io/v1
kind: PriorityClass
value: 100000
globalDefault: false
description: "High priority for critical workloads"
metadata:
  name: high-priority
```

---

### **CPU vs Memory Management**

* **CPU**:

  * Can be throttled (millicores)
  * `cpu: 1` = 1 vCPU/core
* **Memory**:

  * Not throttled
  * Exceeding memory = eviction

---
