## **Configuration Management in Kubernetes**

---

### **ConfigMap**

* Stores **non-sensitive configuration data** as key-value pairs.
* Used to decouple environment-specific settings from application images.
* Can be mounted as:

  * Environment variables
  * Command-line arguments
  * Volume files

---

### **Secret**

* Stores **sensitive data** (e.g., passwords, tokens, SSH keys) in base64-encoded form.
* More secure than ConfigMap:

  * Stored separately from pod specs
  * Can be encrypted at rest
* Used like ConfigMap:

  * As env variables or mounted volumes

---

### **Environment Variables**

* Used to inject configuration into containers at runtime.
* Can reference:

  * Static values
  * Values from ConfigMap/Secret
  * Pod fields using **Downward API**

---

### **Downward API**

* Exposes pod and container metadata to applications.
* Provides runtime information such as:

  * Pod name, namespace
  * Resource limits
  * Labels and annotations
* Available via:

  * Environment variables
  * Mounted files

---

### **Init Containers**

* Special containers that run **before app containers** in a pod.
* Used for:

  * Setup or pre-conditions (e.g., downloading files, waiting for services)
* Must complete successfully for main containers to start

---

### **Sidecar Containers**

* Auxiliary containers that run alongside the main container(s) in a pod.
* Used for:

  * Logging agents
  * Data syncing
  * Monitoring or proxies

---

### **Projected Volumes**

* Combine multiple sources (ConfigMap, Secret, Downward API, etc.) into a single volume.
* Useful when configuration is spread across different sources.

---

### **Advantages of Configuration Management**

* Separation of config from code
* Easy updates without rebuilding images
* Dynamic reconfiguration
* Environment-specific customization

---
