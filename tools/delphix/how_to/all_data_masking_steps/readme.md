## **Guide to All Operations That Can Be Done in Delphix Masking**

---

### **1. Set Up a Masking Environment**

#### Step: Add a New Environment

**Purpose:** Register the server or cloud instance that hosts the data to be masked.

**Options:**

* **Environment Type:** Oracle, SQL Server, MySQL, PostgreSQL, File, etc.
* **Connection Protocol:** JDBC, TCP/IP, local OS shell
* **Authentication:** Username/password or SSH key
* **Multiple Environments:** Add as many as needed

---

### **2. Add a Connector (Inventory)**

#### Step: Define a Connection to a Schema or File Source

**Purpose:** Let the masking engine access specific DBs or files within the environment.

**Options:**

* **Connector Name:** Logical name for identification
* **Database Type:** Oracle, SQL Server, etc.
* **Schema Name / File Path:** Exact path to data
* **Connection Method:** Direct or via data source reference
* **Username/Password:** With SELECT/UPDATE access

---

### **3. Create or Import a Masking Job**

#### Step: Build a job to execute masking logic

**Purpose:** Link connectors, rulesets, and execution logic.

**Options:**

* **Job Type:** Standard Masking Job
* **Execution Mode:** In-Place, On-the-Fly, Backup Copy
* **Error Handling:** Stop on error or skip row
* **Pre/Post Scripts:** Add scripts to run before/after masking
* **Scheduling:** Set now or define a recurring job later

---

### **4. Define Rulesets**

#### Step: Choose what tables and columns to mask

**Purpose:** Limit masking to sensitive fields only.

**Options:**

* **Tables:** Manually select or bulk import
* **Columns:** Auto-detect using profiling or select manually
* **Column Grouping:** Logical groups for easy handling

---

### **5. Assign Masking Algorithms**

#### Step: Apply logic to transform sensitive values

**Purpose:** Choose how each column should be masked.

**Options (Per Column):**

* **Algorithm Type:** Random, Shuffle, Redact, Lookup, Format-Preserving
* **Consistency:** Deterministic or Non-deterministic
* **Custom Function:** Write SQL or Java logic
* **Masking Options:** Nullify, shift values, replace, substitute from list
* **Chaining:** Combine multiple algorithms sequentially

---

### **6. Use Masking Sets (Reusable Logic)**

#### Step: Create templates for reuse

**Purpose:** Define reusable logic to apply across projects/environments.

**Options:**

* **Global Rulesets:** Apply to all environments of the same type
* **Reusable Algorithms:** Saved logic for future assignments

---

### **7. Add Transformation Scripts (Optional)**

#### Step: Pre-process or post-process masking data

**Purpose:** Modify data before or after masking (e.g., formatting).

**Options:**

* **SQL Scripts:** Run custom queries before/after job
* **Shell Scripts:** Execute system-level tasks
* **Use Case:** Drop/recreate indexes, clear cache, copy audit logs

---

### **8. Enable Consistency Controls**

#### Step: Enforce same output for same input

**Purpose:** Preserve referential integrity across columns/tables.

**Options:**

* **Cross-Column Mapping:** Use consistent substitution within a table
* **Cross-Table Linking:** Share consistent values across jobs
* **Token Reuse Policy:** Control how many times a masked value is reused

---

### **9. Apply Data Filters (Optional)**

#### Step: Limit which rows get masked

**Purpose:** Use WHERE clause to scope masking.

**Options:**

* **Static Filters:** e.g., `WHERE country='US'`
* **Dynamic Filters:** Apply based on profiling or input data
* **Use Cases:** Mask only active records, recent data, etc.

---

### **10. Configure Execution Settings**

#### Step: Define job runtime behavior

**Purpose:** Optimize job speed, reliability, and auditing.

**Options:**

* **Thread Count:** Control parallel masking threads
* **Restart Mode:** Resume from last point or restart fully
* **Row Limit:** Mask only a subset of rows
* **Audit Mode (Dry Run):** Simulate without modifying data
* **Performance Tuning:** Batch size, commit rate, error logging

---

### **11. Execute the Masking Job**

#### Step: Run the job manually or on schedule

**Purpose:** Begin the masking process.

**Options:**

* **Immediate Execution:** Run now
* **Scheduled Execution:** Daily, weekly, or CRON-based
* **Manual Trigger:** API or CLI

---

### **12. Monitor Job Execution**

#### Step: View logs and live progress

**Purpose:** Detect failures or warnings during job run.

**Options:**

* **Live Console:** Progress bar with per-table status
* **Error View:** Row-level error messages
* **Execution Summary:** Count of rows masked, time taken, skipped rows

---

### **13. Audit and Export Reports**

#### Step: Generate compliance and usage reports

**Purpose:** Prove data has been masked and record who did it.

**Options:**

* **Audit Logs:** Full masking history
* **Execution Reports:** Downloadable summary of job run
* **Column-Level Logs:** Show how each sensitive field was handled

---

### **14. Schedule Recurring Masking Jobs**

#### Step: Automate regular masking

**Purpose:** Keep non-prod environments compliant and up to date.

**Options:**

* **Frequency:** Daily, Weekly, Monthly
* **Retry on Failure:** Enable automatic re-run on failure
* **Notification Settings:** Email alerts on success/failure

---

### **15. Automate via API or CLI**

#### Step: Integrate with pipelines or custom workflows

**Purpose:** Mask data automatically during CI/CD or provisioning.

**Options:**

* **Delphix REST API:** Full job control
* **Delphix CLI:** Run commands from script
* **DevOps Integration:** Jenkins, Azure DevOps, GitLab

---

### **16. Use Data Profiling (Optional but Important)**

#### Step: Scan data to identify sensitive fields

**Purpose:** Discover what needs to be masked.

**Options:**

* **Profiling Rules:** Email, SSN, Credit Card, Name, etc.
* **Custom Regex Patterns:** Define new sensitive field rules
* **Auto Ruleset Generation:** Build rulesets based on profiling results

---
