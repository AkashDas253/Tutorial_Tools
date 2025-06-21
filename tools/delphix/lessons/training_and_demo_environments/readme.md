## **Training and Demo Environments** in Delphix

---

### **Objective**

Provision **realistic, secure, and lightweight environments** for internal training, partner enablement, and product demonstrations — using masked and virtualized copies of production data without the overhead of full physical environments.

---

### **Key Capabilities**

| Capability                    | Description                                                                          |
| ----------------------------- | ------------------------------------------------------------------------------------ |
| **Virtual Data Provisioning** | Instantly create training/demo databases or file environments.                       |
| **Data Masking**              | Secure sensitive data for public or internal use.                                    |
| **Bookmarking & Branching**   | Save and reuse baseline environments for repeatable sessions.                        |
| **Self-Service Access**       | Instructors and trainees can provision, reset, or rewind environments independently. |
| **Lightweight Footprint**     | Share multiple isolated environments without duplicating full datasets.              |
| **TimeFlow & Rewind**         | Reset environments to known states before or after each session.                     |
| **Automation**                | Automate provisioning, refresh, or reset using APIs or CLI.                          |
| **Multi-User Scalability**    | Support concurrent, identical environments for multiple users simultaneously.        |

---

### **Workflow**

1. **Create a baseline virtual dataset** (vDB or vFile) from production or masked data.
2. **Bookmark** a clean, ready-to-use state for training or demo purposes.
3. **Provision multiple clones** for different users or sessions.
4. **During the session**, allow experimentation or exercises on isolated environments.
5. **Rewind or destroy** environments post-session to reset for next use.
6. **Automate** the entire lifecycle via scripting or CI/CD integration.

---

### **Use Cases**

* Internal employee onboarding and technical training
* Customer or partner training sessions
* Hands-on workshops or labs
* Pre-sales and post-sales product demos
* Simulation of production scenarios for education
* Sandbox environments for certification programs

---

### **Benefits**

| Area                | Benefit                                                                    |
| ------------------- | -------------------------------------------------------------------------- |
| **Speed**           | Environments provisioned in minutes for immediate access                   |
| **Security**        | Masking protects sensitive data during public-facing use                   |
| **Scalability**     | Provision identical instances for dozens or hundreds of users concurrently |
| **Repeatability**   | Restore environments to clean states after each use                        |
| **Cost-Efficiency** | Avoid full physical copies — save storage and infrastructure costs         |
| **Simplicity**      | Enable non-technical users to manage their environments with JetStream     |

---

### **Features Supporting Training/Demo**

| Feature             | Role                                                                 |
| ------------------- | -------------------------------------------------------------------- |
| **JetStream UI**    | Provides visual interface for non-technical users to manage sessions |
| **TimeFlow**        | Visual timeline of data snapshots for rewind/reset                   |
| **Bookmarks**       | Snapshots for consistent environment setup                           |
| **Branching**       | Parallel sessions using the same data baseline                       |
| **REST APIs / CLI** | Automate environment orchestration for large training sessions       |

---

### **Best Practices**

* Always use **masked data** for training/demos to avoid compliance risks.
* Create **template environments** as bookmarks for easy reuse.
* **Automate provisioning and teardown** for repeat events using scripts or CI/CD.
* Assign **self-service access** to users for flexibility during long-running workshops.
* Enable **parallel branch environments** for exercises requiring independent data changes.

---

### **Challenges Solved**

| Challenge                           | How Delphix Solves It                                     |
| ----------------------------------- | --------------------------------------------------------- |
| Slow setup of demo/training systems | Virtual provisioning in minutes with bookmarks            |
| Data privacy concerns               | Integrated masking for secure data use                    |
| High infra/storage costs            | Thin-cloning drastically reduces resource requirements    |
| Inconsistent training experience    | Bookmarks ensure all users start from the same data state |

---
