## Supported Sources & Targets in Delphix

---

### **Supported Source Systems**

Delphix connects to source systems to ingest data (via snapshots, backups, or logs) without impacting performance.

#### **Databases**

| RDBMS                | Notes                                   |
| -------------------- | --------------------------------------- |
| Oracle               | Supports RMAN, ASM, DataGuard           |
| Microsoft SQL Server | Full support for clustering and backups |
| PostgreSQL           | Streaming replication supported         |
| MySQL                | Binary log-based capture                |
| SAP ASE (Sybase)     | Limited support for legacy systems      |
| IBM Db2              | Partial support via integration tools   |
| MongoDB              | Requires connector-based ingestion      |
| SAP HANA             | Integration via file-based snapshots    |

#### **Files and File Systems**

| File System   | Notes                     |
| ------------- | ------------------------- |
| Unix/Linux    | File-based ingestion      |
| Windows NTFS  | Supported via file shares |
| NFS, SMB/CIFS | Shared file access        |

#### **Enterprise Applications**

| Application       | Notes                                              |
| ----------------- | -------------------------------------------------- |
| SAP ECC / S/4HANA | Requires database-level and file-level integration |
| Salesforce        | API-based connectors required                      |

---

### **Supported Target Environments**

Delphix provisions virtual datasets (vDBs or vFiles) to the following target environments.

#### **Operating Systems**

| OS Type                      | Notes                                     |
| ---------------------------- | ----------------------------------------- |
| Linux (RHEL, CentOS, Ubuntu) | Common target for databases               |
| Windows Server               | Supports SQL Server and file provisioning |
| Unix (AIX, Solaris, HP-UX)   | Legacy environments supported             |

#### **Databases (as Targets)**

| RDBMS             | Notes                                  |
| ----------------- | -------------------------------------- |
| Oracle            | Provision vDBs with full functionality |
| SQL Server        | Supports VMs or physical hosts         |
| PostgreSQL        | Fast recovery and refresh options      |
| MySQL             | Target-side virtual data provisioning  |
| SAP ASE, SAP HANA | File/database-level provisioning       |

#### **Cloud Platforms**

| Cloud Provider  | Notes                                        |
| --------------- | -------------------------------------------- |
| AWS             | EC2, RDS, S3 – full support                  |
| Microsoft Azure | Azure VMs, Azure SQL, Blob storage           |
| Google Cloud    | GCE, GCS – supported with customization      |
| Oracle Cloud    | OCI Compute and DBaaS environments supported |

---

### **Development, Test, and Analytics Tools**

| Tool Type          | Examples                         |
| ------------------ | -------------------------------- |
| CI/CD              | Jenkins, GitLab, Azure DevOps    |
| Testing Frameworks | Selenium, Postman, JMeter        |
| Data Science       | Jupyter, R, Python (via vDBs)    |
| ETL/ELT            | Informatica, Talend, Apache NiFi |

---

### **Integration Channels**

| Interface          | Purpose                         |
| ------------------ | ------------------------------- |
| REST APIs          | Automation and orchestration    |
| CLI (Command Line) | Scripting and task execution    |
| JetStream UI       | Self-service data provisioning  |
| SDKs               | Optional for custom integration |

---
