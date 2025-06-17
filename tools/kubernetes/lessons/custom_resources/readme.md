## **Custom Resources in Kubernetes**

---

### **What Are Custom Resources?**

Custom Resources extend Kubernetes' functionality by allowing you to define your own **resource types**—just like built-in ones such as `Pods` or `Services`.

* Enable **domain-specific objects** (e.g., `Database`, `Cache`, `Backup`)
* Work alongside Kubernetes' native API machinery
* Fully support versioning, validation, and lifecycle management

---

### **Core Components**

#### **Custom Resource (CR)**

* An **instance** of your custom data
* Created using your defined schema

```yaml
apiVersion: "example.com/v1"
kind: CronTab
metadata:
  name: my-crontab
spec:
  schedule: "*/5 * * * *"
  image: myjob:1.0
```

#### **Custom Resource Definition (CRD)**

* Registers a new **kind** to Kubernetes
* Lives in the Kubernetes API as a **schema**
* Enables `kubectl get <new-resource>` and CRUD operations

```yaml
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
  name: crontabs.example.com
spec:
  group: example.com
  names:
    kind: CronTab
    plural: crontabs
  scope: Namespaced
  versions:
    - name: v1
      served: true
      storage: true
      schema:
        openAPIV3Schema:
          type: object
          properties:
            spec:
              type: object
              properties:
                schedule:
                  type: string
                image:
                  type: string
```

---

### **Controller**

A program that watches for changes to CRs and **manages their state**.

* Commonly built using:

  * **client-go** library
  * **Kubebuilder** (SDK for writing controllers)
  * **Operator SDK** (for building full operators)

---

### **Operator Pattern**

Combines:

* **CRDs** (to define new objects)
* **Custom Controllers** (to manage their lifecycle)

Operators automate:

* Application lifecycle (install, update, backup, scale, etc.)
* Complex workflows (e.g., failover, recovery)

---

### **Versioning & Validation**

CRDs support:

* **Multiple versions** (`v1`, `v1beta1`, etc.)
* **Schema validation** using OpenAPIv3
* **Defaulting** and **pruning** of unknown fields

---

### **Status Subresource**

CRs can include a `status` field, updated separately from `spec`.

```yaml
status:
  lastRunTime: "2025-06-17T14:30:00Z"
```

* Helps avoid conflicts with users updating `spec`

---

### **Subresources**

* `status` – to update status independently
* `scale` – enables integration with HPA

---

### **Accessing Custom Resources**

```bash
kubectl get crontabs.example.com
kubectl describe crontab my-crontab
```

Use `kubectl explain` for field introspection.

---

### **Use Cases**

* Databases: PostgreSQLCluster, MongoReplicaSet
* Messaging: KafkaCluster, RabbitMQBroker
* Storage: VolumeSnapshot, Backup
* Infrastructure: DNSRecord, Certificate, FirewallRule

---

### **Best Practices**

* Validate CRs via schema
* Use `status` for controller-driven updates
* Leverage labels and annotations for filtering
* Use Operators for complex automation

---
