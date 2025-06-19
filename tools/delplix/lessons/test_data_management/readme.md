## **Test Data Management (TDM)** in Delphix

---

### **Definition**

**Test Data Management (TDM)** is the process of creating, managing, and delivering high-quality, secure, and relevant test data to non-production environments such as development, QA, and UAT. Delphix offers an integrated platform for fast, automated, and compliant TDM using data virtualization and masking.

---

### **Core Capabilities of TDM in Delphix**

| Capability                    | Description                                                                        |
| ----------------------------- | ---------------------------------------------------------------------------------- |
| **Data Virtualization**       | Creates virtual copies of production data instantly without duplication.           |
| **Data Masking**              | Irreversibly transforms sensitive data to ensure privacy and compliance.           |
| **Data Subsetting**           | Extracts specific segments of data to reduce size and increase relevance.          |
| **Self-Service Provisioning** | Enables teams to independently manage test data (provision, reset, refresh).       |
| **Bookmarking & Branching**   | Allows saving, restoring, and versioning test data for reuse and parallel testing. |
| **Automated Data Refresh**    | Keeps test environments up to date with production-like data.                      |
| **Policy-Based Access**       | Controls who can provision or view specific test datasets.                         |
| **Integration APIs**          | Enables automation and CI/CD pipeline integration.                                 |

---

### **TDM Workflow in Delphix**

1. **Connect to Source Systems** (production databases, files).
2. **Capture Data** via snapshots or logs using Delphix Engine.
3. **Mask Sensitive Data** using Delphix Masking Engine.
4. **Subset Data (Optional)** to extract relevant slices of data.
5. **Provision Virtual Copies** to target environments as vDBs/vFiles.
6. **Manage Lifecycle** with operations like refresh, rollback, and branching.

---

### **Supported Operations**

| Operation     | Purpose                                                  |
| ------------- | -------------------------------------------------------- |
| **Provision** | Create virtual databases/files in test environments      |
| **Refresh**   | Sync with latest source data without full reprovisioning |
| **Rewind**    | Roll back to earlier snapshot for repeatable testing     |
| **Bookmark**  | Save a specific test data state                          |
| **Branch**    | Create independent environments from a bookmarked state  |
| **Mask**      | Anonymize sensitive data before delivery                 |
| **Subset**    | Deliver only a targeted portion of the dataset           |

---

### **Benefits**

| Area            | Benefit                                                            |
| --------------- | ------------------------------------------------------------------ |
| **Speed**       | Rapid provisioning and refresh of environments                     |
| **Security**    | Built-in masking ensures privacy in non-production                 |
| **Compliance**  | Satisfies data protection regulations (GDPR, HIPAA, PCI-DSS, etc.) |
| **Efficiency**  | Reduces storage and infrastructure cost                            |
| **Flexibility** | Supports multiple environments, use cases, and users               |
| **Automation**  | Seamless integration with DevOps, CI/CD, and orchestration tools   |

---

### **Supported Data Sources**

* **Relational Databases**: Oracle, SQL Server, PostgreSQL, MySQL, SAP ASE, IBM Db2
* **Filesystems**: Linux/Unix, Windows, NFS, SMB
* **Cloud Platforms**: AWS, Azure, GCP, OCI (via virtual or masked provisioning)

---

### **Use Cases**

* Manual and automated testing
* Integration and regression testing
* Secure data sharing with vendors
* Training and demo environments
* Agile development and CI/CD workflows
* Parallel development and test lanes

---

### **Compliance Support**

| Regulation  | How TDM Helps                                            |
| ----------- | -------------------------------------------------------- |
| **GDPR**    | Removes/obfuscates personal data in test environments    |
| **HIPAA**   | Masks health information before provisioning             |
| **PCI-DSS** | Hides payment card details using irreversible masking    |
| **CCPA**    | Prevents personal data exposure for California residents |

---

### **Integration Capabilities**

| Tool Type           | Examples                          |
| ------------------- | --------------------------------- |
| **CI/CD**           | Jenkins, GitLab, Azure DevOps     |
| **IaC**             | Terraform, Ansible                |
| **APIs/CLI**        | REST APIs, CLI for automation     |
| **Self-Service UI** | JetStream for non-technical users |

---

### **Challenges Addressed**

* Long wait times for test data
* Storage sprawl due to full-size copies
* Risk of sensitive data leaks
* Manual and error-prone masking processes
* Inconsistent test environments
* Compliance violations in dev/test setups

---
