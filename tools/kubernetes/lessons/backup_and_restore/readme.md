## **Backup and Restore in Kubernetes**

---

### **Purpose**

Backup and restore ensure **disaster recovery**, **data integrity**, and **cluster portability** in Kubernetes environments. It covers **both stateless configuration** (YAML manifests) and **stateful data** (volumes).

---

## **Backup Targets**

### **Kubernetes Resources**

* Deployments, Services, ConfigMaps, Secrets, etc.
* Stored in **etcd** (Kubernetes’ key-value store)

### **Persistent Volumes (PVs)**

* Application data in storage backends (block, file systems, object stores)

---

## **Backup Approaches**

### **etcd Backup (Control Plane Backup)**

* Critical for **cluster recovery**
* Includes all Kubernetes resource definitions
* Use `etcdctl` or managed backups (EKS, AKS, GKE)

```bash
ETCDCTL_API=3 etcdctl snapshot save snapshot.db \
  --endpoints=https://127.0.0.1:2379 \
  --cacert=<ca.pem> --cert=<cert.pem> --key=<key.pem>
```

---

### **YAML-Based Resource Backup**

* Export resources as YAML manifests for redeployment

```bash
kubectl get all --all-namespaces -o yaml > cluster-backup.yaml
```

* Can use `kustomize` or `helm` to version/manage backups

---

### **Volume Snapshots (PVC Backup)**

* Take snapshots using **CSI drivers** (supported by storage providers)
* Kubernetes supports `VolumeSnapshot` and `VolumeSnapshotContent`

```yaml
apiVersion: snapshot.storage.k8s.io/v1
kind: VolumeSnapshot
metadata:
  name: my-snapshot
spec:
  source:
    persistentVolumeClaimName: my-pvc
```

---

### **Backup Tools**

| Tool           | Key Features                                                 |
| -------------- | ------------------------------------------------------------ |
| **Velero**     | Backup/restore resources + persistent volumes (most popular) |
| **Kasten K10** | Enterprise-grade with RBAC, compliance, UI                   |
| **Stash**      | Backup operator for workloads + volumes (by AppsCode)        |
| **Ark**        | Predecessor of Velero (now deprecated)                       |

---

### **Velero Overview**

#### **Capabilities**

* Backup cluster resources and volumes
* Schedule recurring backups
* Store in object storage (e.g., S3, GCS, MinIO)
* Migrate across clusters

#### **Sample Velero CLI Commands**

```bash
velero install --provider aws --bucket my-bucket ...
velero backup create my-backup --include-namespaces my-ns
velero restore create --from-backup my-backup
velero schedule create daily-backup --schedule="0 2 * * *"
```

---

### **Restore Strategies**

| Scenario                    | Restore Approach                        |
| --------------------------- | --------------------------------------- |
| Full Cluster Recovery       | Restore etcd + redeploy components      |
| Specific Namespace/Resource | Use `kubectl apply` or `velero restore` |
| Application + Data Recovery | Restore YAML + PVC snapshot             |

---

## **Best Practices**

* Automate regular backups (use Velero schedules or cronjobs)
* Backup both **resource definitions** and **PVCs**
* Store backups **off-cluster** (e.g., S3 or another region)
* Test restore process periodically
* Encrypt backups at rest
* Monitor backup success/failures
* Use **GitOps** for declarative resource versioning

---
