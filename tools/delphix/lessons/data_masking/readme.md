## **Data Masking** in Delphix

---

### **Definition**

**Data Masking** in Delphix refers to the process of **permanently transforming sensitive data** into **non-sensitive, yet realistic** values that **preserve data format and usability**, while ensuring **compliance and security** in non-production environments.

---

### **Purpose**

* Prevent exposure of **Personally Identifiable Information (PII)**, **Protected Health Information (PHI)**, and **Payment Card Information (PCI)**.
* Ensure data privacy in development, testing, analytics, and training.
* Achieve compliance with data protection regulations (e.g., GDPR, HIPAA, PCI-DSS, CCPA).
* Provide **realistic but non-sensitive** test data that behaves like production data.

---

### **Core Capabilities**

| Capability                          | Description                                                                      |
| ----------------------------------- | -------------------------------------------------------------------------------- |
| **Static Masking**                  | Masks data at rest before delivery to environments.                              |
| **Format-Preserving Masking**       | Keeps original format (length, type, structure) of data fields.                  |
| **Deterministic Masking**           | Ensures repeatable masking (same input → same output) for referential integrity. |
| **Non-Reversible Masking**          | Data cannot be unmasked or re-identified once transformed.                       |
| **Consistent Cross-System Masking** | Maintains referential relationships across databases.                            |
| **High-Performance Engine**         | Parallel execution for fast masking of large datasets.                           |
| **Out-of-the-Box Algorithms**       | Predefined rules for common data types (e.g., names, emails, SSNs).              |
| **Custom Algorithms**               | User-defined masking logic for specific use cases.                               |
| **Data Discovery**                  | Automated scanning of schemas to detect sensitive fields.                        |
| **Audit Logging**                   | Tracks masking operations and changes for compliance.                            |
| **Policy-Based Execution**          | Apply reusable masking templates across multiple environments.                   |
| **Multi-Source Support**            | Masks data across different RDBMSs, files, and cloud sources.                    |

---

### **Delphix Masking Engine**

* **Dedicated module** or integrated into Delphix Engine.
* Used to **define, execute, and manage** masking workflows.
* Supports **batch execution**, **scheduling**, and **API-based triggering**.
* Works **independently** or in **combination with data virtualization**.

---

### **Masking Workflow**

1. **Connect** to source (or virtual) data.
2. **Discover** sensitive columns using metadata, pattern recognition, or user input.
3. **Define** masking rules:

   * Use built-in algorithms.
   * Customize rules as needed.
4. **Test & Validate** masking outputs.
5. **Execute** masking job:

   * Can be run manually, on schedule, or via API.
6. **Provision** masked data to target environments.

---

### **Supported Masking Types**

| Type                    | Description                                                            |
| ----------------------- | ---------------------------------------------------------------------- |
| **Format-Preserving**   | Maintains format (e.g., credit card remains a 16-digit number).        |
| **Deterministic**       | Ensures same input → same output across tables and systems.            |
| **Randomized**          | Introduces randomness while preserving format.                         |
| **Nulling / Redaction** | Replaces sensitive data with null or fixed values.                     |
| **Shuffling**           | Replaces column values with shuffled content from same column.         |
| **Custom Scripting**    | User-defined logic via Java, JavaScript, or SQL for complex scenarios. |

---

### **Masking Algorithms**

| Data Type           | Sample Masking Techniques                              |
| ------------------- | ------------------------------------------------------ |
| **Names**           | Random name generation from dictionary                 |
| **Emails**          | Replace domain, use consistent local parts             |
| **SSNs**            | Format-preserving numeric substitution                 |
| **Dates**           | Random offset, fixed interval shift                    |
| **Addresses**       | Replace with valid region-specific addresses           |
| **Phone Numbers**   | Random number generation with format                   |
| **Account Numbers** | Regenerated with checksum preservation                 |
| **Free Text**       | Pattern-matching redaction or placeholder substitution |

---

### **Masking Execution Modes**

| Mode             | Description                                          |
| ---------------- | ---------------------------------------------------- |
| **Batch Mode**   | Mask entire dataset in one pass                      |
| **Incremental**  | Apply masking to newly ingested data only            |
| **On Provision** | Automatically apply masking before provisioning vDBs |

---

### **Masking Targets**

* **Relational Databases**: Oracle, SQL Server, PostgreSQL, MySQL, SAP ASE, IBM Db2.
* **Cloud DBs**: Amazon RDS, Azure SQL, Oracle Cloud DB, etc.
* **Files**: CSV, flat files, XML, JSON (limited format support).
* **Application-Specific Tables**: SAP, Salesforce (via connectors or DB access).

---

### **Integration**

| Tool/Platform         | Purpose                                          |
| --------------------- | ------------------------------------------------ |
| **CI/CD Tools**       | Automate masking in pipelines (Jenkins, GitLab)  |
| **REST APIs**         | Programmatically trigger masking jobs            |
| **CLI**               | Scripted masking execution and job control       |
| **Scheduling Tools**  | Integration with cron, enterprise job schedulers |
| **Delphix JetStream** | For end-user workflow management                 |

---

### **Audit and Monitoring**

* Masking logs with timestamps, record counts, and rule usage.
* Dashboard showing masking job status and history.
* Exportable reports for audits and compliance verification.

---

### **Regulatory Compliance Support**

| Regulation  | How Masking Helps                                         |
| ----------- | --------------------------------------------------------- |
| **GDPR**    | Ensures anonymization of PII in non-prod systems          |
| **HIPAA**   | De-identifies PHI for healthcare test environments        |
| **PCI-DSS** | Masks credit card data before use in dev/test             |
| **CCPA**    | Prevents exposure of Californian residents’ personal data |
| **SOX**     | Supports secure development and internal controls         |
| **GLBA**    | Masks financial and customer data for compliance          |

---

### **Benefits**

| Area              | Description                                                    |
| ----------------- | -------------------------------------------------------------- |
| **Security**      | Prevents misuse or exposure of sensitive data                  |
| **Compliance**    | Enables adherence to global data privacy regulations           |
| **Data Quality**  | Produces realistic, usable test data                           |
| **Automation**    | Easily integrated with CI/CD pipelines and data workflows      |
| **Speed & Scale** | High-performance masking for large, distributed datasets       |
| **Consistency**   | Ensures integrity across interrelated systems and environments |

---

### **Challenges Addressed**

* Eliminates delays in test data delivery due to manual masking.
* Reduces risk of data breaches in non-production environments.
* Replaces error-prone scripting with scalable, consistent automation.
* Enables enterprise-wide data privacy controls.

---

### **Typical Use Scenarios**

* Test data provisioning in secure SDLC workflows.
* Dev/test analytics with de-identified data.
* Data sharing with external teams/vendors without real PII.
* Migration testing to staging or cloud with masked datasets.
* Enterprise-wide data privacy governance implementation.

---
