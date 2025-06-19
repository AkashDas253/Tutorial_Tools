## Key Components in Delphix

---

### **Delphix Engine**

* Central software appliance for data virtualization and management.
* Performs ingestion, snapshotting, provisioning, and timeflow management.
* Connects to source systems and target environments.
* Deployed as a virtual machine or cloud instance (e.g., AWS, Azure).

---

### **Delphix Masking Engine**

* Separate engine or module for sensitive data discovery and masking.
* Applies deterministic, format-preserving, and irreversible masking rules.
* Supports multiple databases, files, and structured data formats.
* Used to ensure compliance with data privacy regulations (e.g., GDPR, HIPAA).

---

### **TimeFlow**

* Timeline of data snapshots and changes for each virtual dataset.
* Enables operations such as:

  * **Bookmark**: Save a known state.
  * **Branch**: Create independent test environments.
  * **Rewind**: Roll back to a prior state.
  * **Fast Refresh**: Pull latest changes from source.

---

### **Virtual Databases (vDBs) / vFiles**

* Thin-clone, space-efficient representations of real databases/files.
* Created from TimeFlow snapshots without full duplication.
* Mountable on target environments within minutes.
* Reflect production-like behavior for dev, test, and analytics.

---

### **JetStream**

* Self-service interface for developers, testers, and data consumers.
* Supports:

  * On-demand provisioning
  * Bookmarking
  * Branching
  * Resetting data to a prior point-in-time
* Designed for workflow independence and user empowerment.

---

### **Source Environment**

* The original data source (e.g., production databases or applications).
* Delphix captures data via:

  * RMAN/Backup (for Oracle)
  * Log shipping
  * API-based replication
* Non-intrusive capture ensures zero or minimal downtime.

---

### **Target Environment**

* Systems where virtual copies are provisioned for consumption.
* Typically includes:

  * Development
  * QA
  * UAT
  * Staging
  * Data science
* Supports both on-premises and cloud targets.

---

### **Storage Layer**

* Holds snapshot data, logs, metadata, and deltas.
* Optimized with compression and deduplication.
* Supports:

  * Block storage (SAN, NAS)
  * Cloud object storage (e.g., AWS S3, Azure Blob)

---

### **APIs and CLI**

* RESTful APIs for automation and external integration.
* CLI for command-line control and scripting.
* Use cases:

  * CI/CD integration
  * Automated provisioning and masking
  * Workflow orchestration

---

### **Data Templates**

* Predefined masking and provisioning configurations.
* Reusable across environments and workflows.
* Speeds up setup and ensures consistency.

---

### **Monitoring and Analytics Dashboard**

* Visual console for tracking:

  * Engine performance
  * Storage consumption
  * Provisioning status
  * Alerts and logs

---
