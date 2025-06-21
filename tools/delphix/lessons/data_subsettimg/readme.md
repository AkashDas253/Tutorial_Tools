## **Data Subsetting** in Delphix

---

### **Definition**

**Data Subsetting** in Delphix refers to the process of **extracting a smaller, relevant, and referentially intact portion of a larger dataset**, typically from production, for use in **non-production environments** (e.g., development, testing, QA).

---

### **Purpose**

* Reduce data volume for faster provisioning and lower storage costs.
* Deliver only the necessary data required for specific test cases.
* Improve performance and agility in development and testing environments.
* Maintain **referential integrity** and **compliance** while using smaller datasets.

---

### **Core Capabilities**

| Capability                  | Description                                                                  |
| --------------------------- | ---------------------------------------------------------------------------- |
| **Policy-Based Subsetting** | Define inclusion/exclusion rules for tables, rows, or columns.               |
| **Referential Integrity**   | Automatically includes related rows from child tables to preserve integrity. |
| **Static Subsets**          | Extract a fixed, reusable subset.                                            |
| **Dynamic Subsets**         | Generate subsets based on parameters (e.g., date ranges, region, user type). |
| **Masking Integration**     | Apply masking to subsets before delivery to ensure compliance.               |
| **Virtualization Support**  | Supports subsetting for virtual data sets (vDBs/vFiles).                     |
| **Multi-Table Support**     | Subset relational data with complex foreign key relationships.               |

---

### **Subsetting Workflow**

1. **Connect** to source database or vDB.
2. **Define** subset rules and filters:

   * Row filters (e.g., `WHERE country='US'`)
   * Column exclusions
   * Join-based rules
3. **Generate** subset with referential constraints applied.
4. **(Optional)** Apply masking before provisioning.
5. **Provision** to target environments.

---

### **Filtering Options**

| Filter Type       | Example                                              |
| ----------------- | ---------------------------------------------------- |
| **Row Filter**    | Only include users from `Region = 'EU'`              |
| **Date-Based**    | Orders placed within the last 30 days                |
| **Key-Based**     | Specific `customer_id` values and all dependent data |
| **Column Filter** | Exclude large BLOB or sensitive fields               |
| **Random Sample** | Randomly select N% of rows for testing               |

---

### **Benefits**

| Area            | Benefit                                                               |
| --------------- | --------------------------------------------------------------------- |
| **Performance** | Smaller data footprint improves test speed and resource usage.        |
| **Storage**     | Saves infrastructure cost by avoiding full-size dataset provisioning. |
| **Focus**       | Enables focused testing on relevant datasets.                         |
| **Speed**       | Faster extraction, provisioning, and data preparation.                |
| **Compliance**  | Delivers only necessary and masked data, reducing compliance scope.   |

---

### **Use Scenarios**

* Targeted testing for specific customer segments or geographies.
* Developer sandboxes with lightweight datasets.
* Regression testing with filtered business scenarios.
* Performance testing with scaled-down but realistic datasets.
* Training environments with synthetic subsets.

---

### **Integration**

| Tool                | Integration Role                               |
| ------------------- | ---------------------------------------------- |
| **Masking Engine**  | Apply policies to subset data post extraction  |
| **JetStream**       | Provision and manage subset environments       |
| **REST APIs/CLI**   | Automate subsetting and provisioning workflows |
| **CI/CD Pipelines** | Use subsets in automated test pipelines        |

---

### **Limitations**

* Complex subset logic can increase configuration time.
* Referential integrity management requires careful key mapping.
* Very large relational subsets may still require staging resources.

---
