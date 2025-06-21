## **All Types of Data Masking in Delphix**

---

### **1. Types of Masking Execution Modes**

| Type                    | Description                                                                |
| ----------------------- | -------------------------------------------------------------------------- |
| **In-Place Masking**    | Applies masking directly on the source database or file system.            |
| **On-the-Fly Masking**  | Applies masking during data movement from source to target.                |
| **Backup Copy Masking** | Creates a masked copy of the source for separate use, preserving original. |

---

### **2. Masking Algorithm Types**

| Algorithm Type                      | Description                                                                |
| ----------------------------------- | -------------------------------------------------------------------------- |
| **Randomization**                   | Replaces original data with random but valid values (e.g., numbers, text). |
| **Shuffling**                       | Randomly rearranges existing values within a column.                       |
| **Redaction**                       | Replaces content with a fixed pattern (e.g., “XXXXXX”).                    |
| **Nullification**                   | Replaces values with NULLs (requires custom masking rule or SQL override). |
| **Lookup-Based Masking**            | Uses external data sets (lookup tables) to substitute values.              |
| **Deterministic Masking**           | Same input always produces same masked output.                             |
| **Non-Deterministic**               | Generates different masked values on each run.                             |
| **Format-Preserving Masking (FPM)** | Maintains data type, length, and pattern of the original data.             |
| **Custom SQL Masking**              | User-defined logic using SQL or stored procedures.                         |
| **Custom Java Algorithm**           | Allows Java-based extensibility for advanced transformations.              |

---

### **3. Supported Data Types and Handling**

| Data Type            | Masking Support                                                         |
| -------------------- | ----------------------------------------------------------------------- |
| **Strings/Text**     | Fully supported: names, addresses, emails, etc.                         |
| **Numbers**          | Random or ranged numeric generation.                                    |
| **Dates/Timestamps** | Shifted or randomized while maintaining valid formats.                  |
| **Booleans**         | Optional replacement (e.g., flip TRUE/FALSE).                           |
| **LOBs (BLOB/CLOB)** | Partially supported with limitations; masking requires custom handlers. |
| **Binary**           | Requires custom logic or exclusion.                                     |
| **Semi-structured**  | Supported via file connectors (JSON, XML, CSV) with parsing.            |

---

### **4. Consistency Options**

| Consistency Type            | Description                                                                    |
| --------------------------- | ------------------------------------------------------------------------------ |
| **Cross-Column**            | Maintains referential integrity within the same row (e.g., first + last name). |
| **Cross-Table**             | Ensures consistent masking of same values across different tables.             |
| **Cross-Environment**       | Same masking logic/output across multiple environments or projects.            |
| **Multi-Column Dependency** | Advanced logic when multiple fields must be masked together.                   |

---

### **5. Execution Controls and Job Options**

| Option                    | Description                                                            |
| ------------------------- | ---------------------------------------------------------------------- |
| **Multi-threading**       | Enables parallel processing to speed up masking.                       |
| **Row Limits**            | Restrict masking to a defined number of rows (useful for testing).     |
| **Restartable Execution** | Resume job from the last completed point if failed.                    |
| **Audit Mode (Dry Run)**  | Logs intended changes without applying them.                           |
| **Error Handling**        | Configure job to stop or continue on row-level or column-level errors. |
| **Preview Mode**          | View masking results without writing to the target.                    |

---

### **6. Masking Rule Definition Steps**

| Step                    | Purpose                                                  |
| ----------------------- | -------------------------------------------------------- |
| **Add Environment**     | Register source/target DB or file system.                |
| **Add Connector**       | Create DB-specific connection info (e.g., JDBC, schema). |
| **Create Ruleset**      | Choose tables and columns for masking.                   |
| **Apply Algorithm**     | Assign masking logic per column.                         |
| **Create Masking Job**  | Bundle ruleset + connector into executable job.          |
| **Configure Execution** | Set performance and error control options.               |
| **Run Job**             | Launch masking and monitor execution.                    |
| **Audit Logs**          | Review job outcomes and generate compliance reports.     |

---

### **7. Advanced Features**

| Feature                          | Description                                                         |
| -------------------------------- | ------------------------------------------------------------------- |
| **Algorithm Chaining**           | Apply multiple transformations in sequence (e.g., mask → redact).   |
| **Conditional Masking**          | Mask values only if conditions are met (requires custom SQL logic). |
| **Dynamic Rule Sets**            | Rules adapt based on metadata or profile scan.                      |
| **Data Profiling**               | Discover sensitive fields automatically (pre-masking scan).         |
| **Masking API Integration**      | Automate masking jobs via REST API and integrate with CI/CD tools.  |
| **Reusable Rules and Templates** | Apply same ruleset across multiple connectors or environments.      |
| **Parallel Job Execution**       | Run multiple masking jobs simultaneously across environments.       |

---

### **8. Job Scheduling and Automation**

| Tool / Feature         | Usage                                                |
| ---------------------- | ---------------------------------------------------- |
| **Internal Scheduler** | Schedule jobs via built-in calendar interface        |
| **External Scheduler** | Trigger jobs using CRON, Jenkins, Azure DevOps, etc. |
| **REST API**           | Automate masking from pipelines or scripts           |
| **CLI**                | Use Delphix command line to manage masking jobs      |

---

### **9. Compliance and Audit Support**

| Feature                             | Description                                                 |
| ----------------------------------- | ----------------------------------------------------------- |
| **Audit Logs**                      | Records all masking job activity (timestamp, user, object). |
| **Report Generation**               | Export masking summaries for regulatory review.             |
| **Data Classification Support**     | Group fields by classification (PII, PHI, PCI) for masking. |
| **GDPR, HIPAA, PCI-DSS Compliance** | Ensured through irreversible and policy-driven masking.     |

---

### **10. Supported Targets and Sources for Masking**

| Source/Target Type                        | Notes                                              |
| ----------------------------------------- | -------------------------------------------------- |
| **Oracle, SQL Server, PostgreSQL, MySQL** | Native support for in-place and on-the-fly masking |
| **Flat Files (CSV, JSON, XML)**           | Via File Connector with parsing/mapping options    |
| **SAP, Salesforce, HANA**                 | Requires schema-level masking through DB layer     |
| **Cloud DBs (RDS, Azure SQL, GCP)**       | Mask via secure connectors and compatible jobs     |

---
