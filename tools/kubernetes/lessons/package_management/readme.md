## **Package Management in Kubernetes**

---

### **Purpose**

Package management in Kubernetes simplifies:

* Installing applications
* Managing dependencies
* Version control
* Reusability and upgrades of configuration manifests

---

### **What Is a Kubernetes Package?**

A **collection of YAML manifests** for deploying one or more Kubernetes resources (e.g., Deployments, Services, ConfigMaps, CRDs), bundled together for reuse and distribution.

---

### **Popular Kubernetes Package Manager: Helm**

#### **Helm Overview**

* De facto standard package manager for Kubernetes
* Helm packages are called **charts**
* Charts contain:

  * Kubernetes manifests
  * Templates
  * Default values
  * Metadata

#### **Helm Chart Structure**

```
mychart/
├── Chart.yaml        # Metadata
├── values.yaml       # Default configuration
├── templates/        # Template files
└── charts/           # Subcharts (dependencies)
```

#### **Chart.yaml**

```yaml
apiVersion: v2
name: mychart
version: 1.0.0
description: A sample Helm chart
```

#### **values.yaml**

```yaml
replicaCount: 3
image:
  repository: nginx
  tag: latest
```

#### **Basic Helm Commands**

| Command            | Purpose                             |
| ------------------ | ----------------------------------- |
| `helm install`     | Install a chart                     |
| `helm upgrade`     | Update an existing release          |
| `helm uninstall`   | Remove a release                    |
| `helm repo add`    | Add a chart repository              |
| `helm search repo` | Search in a chart repository        |
| `helm template`    | Render templates without installing |
| `helm lint`        | Validate chart syntax               |

---

### **Templates and Values**

* Helm templates use **Go templating**
* Values from `values.yaml` are injected into templates

```yaml
# deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: {{ .Release.Name }}-nginx
spec:
  replicas: {{ .Values.replicaCount }}
```

---

### **Subcharts & Dependencies**

* Defined in `Chart.yaml`
* Automatically managed via:

  ```bash
  helm dependency update
  ```

---

### **Helm Repositories**

* Remote servers storing charts (e.g., ArtifactHub, Bitnami)
* You can add repos like:

  ```bash
  helm repo add bitnami https://charts.bitnami.com/bitnami
  ```

---

### **Release Management**

* Helm tracks installations as **releases**
* Stored in Kubernetes as secrets or configmaps in the `kube-system` namespace

---

### **Security & Best Practices**

* Review and pin chart versions before install
* Avoid hardcoded secrets in `values.yaml`
* Use **Helm Secrets** or external secret management tools
* Validate with `helm lint` and test with `helm template`

---

### **Alternatives to Helm**

| Tool             | Description                            |
| ---------------- | -------------------------------------- |
| **Kustomize**    | Template-free YAML patching & layering |
| **Kubecfg**      | JSONNET-based config management        |
| **Jsonnet**      | Functional configuration language      |
| **Carvel**       | Suite including kapp, ytt, kbld, etc.  |
| **Operator SDK** | For managing complex apps via CRDs     |

---
