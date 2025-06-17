## **Kubernetes Security**

---

### **Authentication**

* Verifies the identity of a user or component accessing the API.
* Methods:

  * **Static Tokens**
  * **X.509 Client Certificates**
  * **OpenID Connect (OIDC)**
  * **Service Account Tokens**
  * **Webhook Token Authentication**

---

### **Authorization**

* Determines if an authenticated user is **allowed** to perform an action.
* Modes:

  * **RBAC (Role-Based Access Control)**: Most common
  * **ABAC (Attribute-Based)**
  * **Webhook**
* Resources:

  * **Role**: Permissions within a namespace
  * **ClusterRole**: Cluster-wide permissions
  * **RoleBinding / ClusterRoleBinding**: Binds users to roles

---

### **Admission Controllers**

* Intercept API requests before persistence.
* Validate or mutate requests (e.g., check policies).
* Types:

  * **ValidatingAdmissionWebhook**
  * **MutatingAdmissionWebhook**
* Common Controllers:

  * `NamespaceLifecycle`, `LimitRanger`, `PodSecurity`, `ResourceQuota`

---

### **Service Accounts**

* Provide identity to pods.
* Automatically mounted in pods via secrets.
* Used for pod-to-API communication.

---

### **Secrets Management**

* Use `Secret` objects to store:

  * Passwords, API keys, certificates
* Can be mounted as:

  * Env vars or files in volumes
* **Encryption at rest** should be enabled (via KMS or config)

---

### **Network Policies**

* Restrict pod-to-pod or pod-to-external communication.
* Based on:

  * Pod labels
  * Namespace selectors
  * IP blocks

---

### **Pod Security Standards (PSS)**

* Define privilege levels for pod execution:

  * **Privileged**: Full host access
  * **Baseline**: Limited risky behavior
  * **Restricted**: Strongest constraints
* Enforced via `PodSecurity` admission controller or Gatekeeper (OPA)

---

### **Security Context**

* Defines pod/container-level security settings:

  * `runAsUser`, `fsGroup`
  * `readOnlyRootFilesystem`
  * `capabilities`, `privileged`, `allowPrivilegeEscalation`

---

### **Node Security**

* Node-level protection:

  * Disable root login
  * Use kubelet authentication/authorization
  * TLS between components
* Use:

  * `kubelet` authorization
  * Pod-level isolation
  * Seccomp, AppArmor

---

### **TLS Everywhere**

* All communication in the cluster (API server, etcd, kubelet) should use TLS.
* Enable certificate rotation for service accounts and components.

---

### **etcd Security**

* Store etcd data encrypted and behind firewall.
* Use TLS for client/server connections.
* Enable encryption for secret data.

---

### **Audit Logging**

* Records all requests to the API server.
* Helps detect unauthorized access and misconfigurations.

---

### **Runtime Security**

* Monitor container behavior (e.g., with Falco).
* Detect:

  * Unexpected syscalls
  * Privilege escalations
  * Unauthorized file access

---

### **Best Practices**

* **Least privilege** for users and pods
* **Read-only root filesystem** when possible
* Rotate credentials regularly
* Use **network segmentation** and firewalls
* **Avoid running containers as root**

---
