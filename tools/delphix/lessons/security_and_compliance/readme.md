## Security and Compliance in Delphix

---

### **Data Masking for Compliance**

* **Irreversible Masking**: Sensitive data is anonymized permanently.
* **Format-Preserving**: Maintains data structure and referential integrity.
* **Consistent Masking**: Ensures identical masking across related datasets.
* **Rule-Based Automation**: Applies masking based on defined policies.

---

### **Access Control**

| Feature                              | Description                                       |
| ------------------------------------ | ------------------------------------------------- |
| **Role-Based Access Control (RBAC)** | Granular control over user roles and privileges   |
| **User Management**                  | Native, LDAP, Active Directory, SAML integrations |
| **Environment Isolation**            | Controls access to specific datasets and engines  |

---

### **Authentication and Authorization**

* **LDAP/AD Integration**: Centralized user authentication.
* **SAML Support**: Federated identity with SSO.
* **Token-Based Authentication**: For secure API access.

---

### **Auditing and Logging**

* **Comprehensive Audit Logs**: Tracks user activity and system events.
* **Data Access Monitoring**: Records who accessed, masked, or provisioned data.
* **Log Export**: Compatible with external SIEM tools like Splunk, ELK.

---

### **Data Encryption**

| Area                            | Encryption Type                             |
| ------------------------------- | ------------------------------------------- |
| **At Rest**                     | AES-256 encryption for stored data          |
| **In Transit**                  | TLS/SSL encryption for all communications   |
| **Backup and Snapshot Storage** | Encrypted within the Delphix engine storage |

---

### **Compliance Standards Support**

| Regulation  | Compliance Support Areas                        |
| ----------- | ----------------------------------------------- |
| **GDPR**    | Data masking, access control, audit trails      |
| **HIPAA**   | PHI protection, encrypted data, masking         |
| **PCI-DSS** | Secure data masking, restricted access, logging |
| **CCPA**    | Data anonymization, user access control         |
| **SOX**     | Audit trails and access restrictions            |

---

### **Network and Host Security**

* **Port Hardening**: Only required ports open.
* **API Security**: Controlled via authentication tokens.
* **Firewall Rules**: Support for secure deployment in DMZs or internal networks.

---

### **Security Policies and Best Practices**

* Mask before provisioning non-production environments.
* Use RBAC to limit environment and dataset access.
* Audit user actions regularly.
* Enforce encryption by default for all data paths.

---

### **Certifications (Depending on Deployment)**

* Security posture depends on cloud provider and enterprise configuration.
* Delphix supports compliance-ready deployments but does not itself certify environments.

---
