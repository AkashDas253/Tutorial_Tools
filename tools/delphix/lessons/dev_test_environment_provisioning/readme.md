## **Dev/Test Environment Provisioning** in Delphix

---

### **Objective**

Provision **production-like, consistent, and secure environments** rapidly for development and testing without full physical data copies.

---

### **Key Features**

| Feature                               | Description                                                             |
| ------------------------------------- | ----------------------------------------------------------------------- |
| **Virtual Data Copies (vDBs/vFiles)** | Lightweight, space-efficient representations of real data.              |
| **Self-Service Provisioning**         | Developers/testers can create, refresh, rewind, or branch environments. |
| **Bookmarking**                       | Save environment states to return to them later.                        |
| **Branching**                         | Create parallel environments for different test cases or teams.         |
| **Point-in-Time Provisioning**        | Provision environments from any past snapshot state.                    |
| **Automated Refresh**                 | Keep environments synced with latest source data automatically.         |

---

### **Provisioning Workflow**

1. **Ingest**: Capture data from source databases/applications into Delphix Engine.
2. **Snapshot**: Create consistent points-in-time using incremental or full snapshots.
3. **Virtualization**: Generate virtual copies (vDBs or vFiles) using shared storage.
4. **Mask (Optional)**: Apply masking policies before provisioning to targets.
5. **Provision**: Deliver the virtual dataset to the target dev/test system.
6. **Manage**: Use JetStream or APIs to bookmark, branch, rewind, or refresh as needed.

---

### **Benefits**

| Aspect              | Benefit                                                          |
| ------------------- | ---------------------------------------------------------------- |
| **Speed**           | Environment setup in minutes instead of hours/days               |
| **Storage Savings** | No full data copies; uses deduplicated and compressed snapshots  |
| **Isolation**       | Multiple environments from same data source without interference |
| **Data Freshness**  | Regular, automated refresh keeps test environments up to date    |
| **Scalability**     | Easily provision for multiple parallel testing streams           |
| **Security**        | Integration with masking ensures compliance before provisioning  |

---

### **Use Scenarios**

* Functional testing
* Regression testing
* Integration testing
* User Acceptance Testing (UAT)
* Bug reproduction and debugging
* Feature branch testing
* CI/CD pipeline integration

---

### **Supported Tools & Interfaces**

* **JetStream**: GUI for self-service environment control.
* **REST APIs/CLI**: For automation in CI/CD and scripting.
* **Infrastructure Tools**: Integration with Ansible, Terraform, Jenkins, GitLab, etc.

---

### **Environment Management Operations**

| Operation     | Description                                            |
| ------------- | ------------------------------------------------------ |
| **Provision** | Create new virtual environment from snapshot.          |
| **Refresh**   | Update environment with latest source data.            |
| **Rewind**    | Roll back to earlier point in TimeFlow.                |
| **Bookmark**  | Save current state for future reference.               |
| **Branch**    | Create a new path/environment from a bookmarked state. |

---
