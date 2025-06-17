## **Scaling in Kubernetes**

---

### **Why Scaling Matters**

Scaling ensures that applications can handle variable workloads efficiently by increasing or decreasing compute resources.

---

### **Types of Scaling**

#### **Horizontal Scaling (Scaling Out/In)**

* Adds or removes **pod replicas**.
* Handled by:

  * **Horizontal Pod Autoscaler (HPA)** for pods
  * **Cluster Autoscaler** for nodes

#### **Vertical Scaling (Scaling Up/Down)**

* Increases or decreases **CPU/memory resources** of a pod.
* Handled by:

  * **Vertical Pod Autoscaler (VPA)**

---

### **Horizontal Pod Autoscaler (HPA)**

* Automatically adjusts the number of pods in a deployment, stateful set, etc.
* Based on metrics like:

  * CPU utilization (default)
  * Memory usage
  * Custom/external metrics

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: myapp-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: myapp
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

* Requires **metrics-server** deployed in the cluster.

---

### **Vertical Pod Autoscaler (VPA)**

* Automatically adjusts **CPU and memory requests/limits** of pods.
* Components:

  * **Recommender**: Suggests optimal resources
  * **Updater**: Deletes pods for resizing (may cause restart)
  * **Admission Controller**: Sets resources for new pods
* Use cases:

  * Applications with predictable but large resource changes

---

### **Cluster Autoscaler**

* Automatically adds/removes **nodes** in the cluster.
* Based on:

  * Pods pending due to resource shortage
  * Underutilized nodes
* Works with:

  * AWS, GCP, Azure
  * On-prem clusters with compatible node groups

---

### **Manual Scaling**

You can manually scale deployments or replicasets:

```bash
kubectl scale deployment myapp --replicas=5
```

---

### **Scaling StatefulSets**

* Supports scaling like deployments.
* Maintains **stable network IDs** and persistent storage.
* Pods are created/deleted in **order**.

---

### **Best Practices**

* Set resource **requests/limits** properly for autoscaling to work.
* Avoid over-provisioning—use autoscaling with monitoring.
* Use **readiness probes** to avoid routing traffic to unready pods.

---
