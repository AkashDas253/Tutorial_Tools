## **Storage in Kubernetes**

---

### **Volume**

* A directory accessible to containers in a pod.
* Lifecycle tied to the pod unless using persistent storage.
* Types:

  * `emptyDir`: Temporary storage, deleted when pod is removed
  * `hostPath`: Mounts a file or directory from the host node
  * `configMap` / `secret`: Mounts config or secret data
  * `persistentVolumeClaim`: Connects to persistent storage
  * `nfs`, `csi`, `gitRepo`, etc.

---

### **PersistentVolume (PV)**

* A **cluster resource** representing physical storage.
* Created by the admin or dynamically provisioned.
* Independent of pods or namespaces.
* Specifies:

  * Storage capacity
  * Access modes
  * Reclaim policy
  * Storage class

---

### **PersistentVolumeClaim (PVC)**

* A **user request** for persistent storage.
* Binds to an available PV with matching criteria.
* PVC defines:

  * Requested size
  * Access mode (ReadWriteOnce, etc.)
  * Storage class

---

### **StorageClass**

* Defines **dynamic provisioning strategy** for PVs.
* Specifies:

  * Provisioner plugin (e.g., AWS EBS, GCE PD)
  * Parameters (e.g., type, zones)
  * Reclaim policy
  * Volume binding mode (Immediate / WaitForFirstConsumer)

---

### **Dynamic Provisioning**

* Automatically creates PVs when PVCs are submitted.
* Relies on StorageClass to define how the PV should be created.

---

### **Access Modes**

* Define how volumes can be mounted:

  * **ReadWriteOnce (RWO)**: One node can read/write
  * **ReadOnlyMany (ROX)**: Multiple nodes can read
  * **ReadWriteMany (RWX)**: Multiple nodes can read/write

---

### **Reclaim Policies**

* Determine what happens to PV when bound PVC is deleted:

  * **Retain**: Manual reclaim needed
  * **Recycle**: Deprecated, basic scrub and reuse
  * **Delete**: Volume is deleted automatically

---

### **Volume Plugins**

* Interface to various storage backends:

  * **In-tree plugins**: Built into Kubernetes (e.g., NFS, HostPath)
  * **CSI (Container Storage Interface)**: External plugins with better flexibility and portability

---

### **CSI (Container Storage Interface)**

* Standard interface to provision storage across different vendors.
* Supports dynamic provisioning, resizing, snapshotting, and more.

---

### **Ephemeral Volumes**

* Short-lived volumes tied to pod lifecycle.
* Examples:

  * `emptyDir`
  * `ephemeral` volumes via inline PVC

---

### **Volume Mount**

* Defines where in the container file system the volume is accessible.
* Configured within the pod spec.

---
