## **Data Masking for Compliance** in Delphix

---

### **Objective**

Protect sensitive data in non-production environments (dev, test, analytics) by applying **irreversible masking** to meet **data privacy and regulatory compliance** requirements.

---

### **Core Functions**

| Function                              | Description                                                                       |
| ------------------------------------- | --------------------------------------------------------------------------------- |
| **Sensitive Data Discovery**          | Scans schemas to locate Personally Identifiable Information (PII), PHI, PCI, etc. |
| **Masking Rules Engine**              | Applies built-in or custom rules to anonymize sensitive data                      |
| **Format-Preserving Masking**         | Maintains original format (length, type, checksum) of data fields                 |
| **Deterministic Masking**             | Ensures same input always produces same masked output (for joins)                 |
| **Reversible Masking**                | Not supported – ensures data cannot be restored                                   |
| **Multi-Source Masking**              | Supports masking across databases, files, and applications                        |
| **Consistent Masking Across Systems** | Preserves referential integrity and cross-database joins                          |

---

### **Workflow in Delphix**

1. **Connect** to source data repositories.
2. **Discover** sensitive data using pattern matching and classifiers.
3. **Define** masking rules and policies per column or data type.
4. **Apply** masking using the Delphix Masking Engine.
5. **Provision** masked, virtualized data to non-production environments.

---

### **Supported Data Types**

* Names, emails, phone numbers, addresses
* National IDs, credit card numbers, bank details
* Medical records and health information
* Corporate confidential data

---

### **Regulatory Compliance Covered**

| Regulation           | Requirement Addressed by Delphix Masking                   |
| -------------------- | ---------------------------------------------------------- |
| **GDPR**             | Anonymization of personal data in test environments        |
| **HIPAA**            | Protection of health-related information                   |
| **PCI-DSS**          | Masking of credit card and payment data                    |
| **CCPA**             | Secure handling of personal data for California residents  |
| **SOX, GLBA, POPIA** | Support for other region-specific data protection mandates |

---

### **Masking Engine Capabilities**

| Capability                    | Description                                           |
| ----------------------------- | ----------------------------------------------------- |
| **Custom Masking Algorithms** | Allows writing custom scripts and logic               |
| **Predefined Algorithms**     | Out-of-the-box templates for common data types        |
| **High Performance**          | Parallelized masking of large data volumes            |
| **Audit Logging**             | Tracks masking actions for compliance audits          |
| **Integration Ready**         | Masking jobs triggered via REST API or CLI automation |

---

### **Benefits**

| Area              | Benefit                                                               |
| ----------------- | --------------------------------------------------------------------- |
| **Data Security** | Protects sensitive information from exposure                          |
| **Compliance**    | Helps meet legal and regulatory obligations                           |
| **Speed**         | Masking done before or during provisioning to minimize workflow delay |
| **Consistency**   | Uniform masking across systems maintains test validity                |
| **Integration**   | Supports automation in CI/CD and TDM workflows                        |

---

### **Supported Sources for Masking**

* **Databases**: Oracle, SQL Server, PostgreSQL, MySQL, SAP ASE, MongoDB, etc.
* **Files**: CSV, JSON, flat files (limited capabilities)
* **Cloud Platforms**: Masking before provisioning to AWS, Azure, GCP, etc.

---

### **Common Use Cases**

* Masking production data before provisioning to dev/test environments
* Automated masking in CI/CD pipelines
* Secure data for analytics and training
* Standardized data obfuscation across enterprise environments

---
