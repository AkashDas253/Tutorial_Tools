## Delphix Architecture

---

### **Logical Architecture Components**

| Component                  | Function                                                                        |
| -------------------------- | ------------------------------------------------------------------------------- |
| **Delphix Engine**         | Core software appliance for data virtualization and masking                     |
| **Delphix Masking Engine** | Performs sensitive data discovery and masking operations                        |
| **Source Systems**         | Production databases or applications from which data is ingested                |
| **Target Environments**    | Development, test, or analytics environments that consume virtual data          |
| **vFiles / vDBs**          | Virtual representations of files or databases created from snapshots            |
| **TimeFlow**               | Timeline of snapshots enabling point-in-time access, rewind, and branching      |
| **JetStream**              | Self-service interface for managing, bookmarking, refreshing, or branching data |
| **Storage**                | Underlying storage (block or object) used for storing snapshots and deltas      |
| **APIs / CLI**             | Interfaces for automation, scripting, and integration                           |

---

### **Deployment Architecture Diagram**

```mermaid
flowchart TB
  A[Source Databases / Apps] --> B[Delphix Engine]
  B --> C[Data Virtualization Layer]
  B --> D[Data Masking Layer]
  C --> E[vDBs / vFiles]
  D --> E
  E --> F[Target Systems (Dev/Test/Cloud)]
  B --> G[JetStream Self-Service]
  B --> H[REST APIs / CLI]
  B --> I[Storage Layer (Snapshots, Logs)]
```

---

### **Data Flow Summary**

* **Ingestion**: Data is pulled from source systems into the Delphix Engine via snapshots or backups.
* **Virtualization**: Delphix stores only changes (deltas) and creates lightweight virtual copies (vDBs or vFiles).
* **Masking**: Sensitive fields are anonymized using the masking engine before provisioning to targets.
* **Provisioning**: vDBs or vFiles are mounted on target systems (on-prem or cloud) for access.
* **Time Management**: TimeFlow tracks all snapshots and enables bookmarking, branching, and rollback.
* **Self-Service / Automation**: Users or pipelines interact through JetStream or REST APIs to manage data.

---

### **Supported Infrastructure Modes**

* **On-Premise**
* **Hybrid Cloud**
* **Full Cloud-native** (via cloud images for AWS, Azure, GCP)

---

### **Architecture Characteristics**

* Agentless operation on most source systems
* Non-disruptive data capture
* High-performance storage optimization
* Horizontal scalability via multiple engine instances
* Integration-ready via APIs and DevOps tools

---
