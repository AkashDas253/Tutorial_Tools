## **Kubernetes CLI Tools**

---

### **Purpose**

CLI tools help interact with and manage Kubernetes clusters, resources, and workflows. They enable automation, inspection, deployment, and debugging from the command line.

---

### **Primary CLI Tools**

#### **kubectl**

* Official Kubernetes CLI to control clusters
* Syntax: `kubectl [command] [type] [name] [flags]`

**Common Commands**

```bash
kubectl get pods                     # List all pods
kubectl describe pod mypod          # Show detailed info
kubectl apply -f app.yaml           # Apply config
kubectl delete svc mysvc            # Delete a service
kubectl logs mypod                  # Get logs
kubectl exec -it mypod -- bash      # Access container shell
```

**Useful Flags**

* `-n <namespace>`: Specify namespace
* `--context`: Use specific cluster context
* `--output=yaml|json|wide`: Output format

---

### **Secondary CLI Tools**

#### **kubeadm**

* Bootstraps Kubernetes clusters
* Used for setting up control plane and worker nodes

```bash
kubeadm init      # Initialize master node
kubeadm join ...  # Join worker to cluster
```

---

#### **kustomize**

* Native configuration customization tool
* Works with overlays, patches, and bases

```bash
kustomize build ./overlays/dev | kubectl apply -f -
```

* Supports config reusability without templating

---

#### **helm**

* Kubernetes package manager
* Manages charts and releases

```bash
helm install myapp ./mychart
helm upgrade myapp ./mychart
```

---

#### **kubens**

* Quickly switch between namespaces

```bash
kubens kube-system
```

---

#### **kubectx**

* Switch between multiple clusters/contexts easily

```bash
kubectx dev-cluster
```

---

#### **stern**

* Tail logs from multiple pods and containers with filters

```bash
stern myapp
```

---

#### **k9s**

* Terminal UI to navigate and interact with the cluster visually
* Supports real-time monitoring

---

#### **kubelogin**

* OIDC authentication helper for `kubectl`
* Used in enterprise setups (e.g., Azure AD, Okta)

---

#### **kind (Kubernetes IN Docker)**

* Create local Kubernetes clusters using Docker containers

```bash
kind create cluster
```

---

#### **minikube**

* Run a single-node Kubernetes cluster locally for development

```bash
minikube start
minikube dashboard
```

---

#### **kubetail**

* Aggregates logs from multiple pods into a single stream

```bash
kubetail myapp
```

---

#### **kube-ps1**

* Enhances your shell prompt to display current Kubernetes context and namespace

---

### **Security-Related Tools**

| Tool            | Purpose                              |
| --------------- | ------------------------------------ |
| **kubesec**     | Security risk scanning of YAML files |
| **kube-bench**  | CIS Benchmark auditing               |
| **kube-hunter** | Cluster vulnerability scanning       |

---

### **Best Practices**

* Alias frequently used commands (e.g., `k=kubectl`)
* Use `kubectl explain <resource>` to understand resource structure
* Combine with `jq`, `watch`, and `grep` for scripting
* Use kubeconfig contexts and namespaces to avoid accidental ops

---
