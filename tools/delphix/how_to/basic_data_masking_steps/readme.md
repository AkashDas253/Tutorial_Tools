## How to Perform a Basic Data Masking Operation in Delphix

**(With All Steps, Options, and Meanings)**

---

### **Step 1: Access the Delphix Masking Engine**

* **Navigate to the Web Interface** of the **Delphix Masking Engine** via browser.
* **Login** using administrator or masking user credentials.

---

### **Step 2: Add or Configure the Environment**

#### Purpose:

Define the **target** (database or file system) containing sensitive data to be masked.

#### Options:

| Option                     | Description                                         |
| -------------------------- | --------------------------------------------------- |
| **Environment Name**       | Logical name to identify the environment            |
| **Environment Type**       | Choose: Oracle, SQL Server, MySQL, PostgreSQL, etc. |
| **OS Credentials**         | Username/password or key used to connect to host    |
| **Database Listener Info** | Hostname, Port, Service/DB name                     |

> Optional: You can add multiple environments for distributed masking.

---

### **Step 3: Add an Inventory (Connector)**

#### Purpose:

Define a **connection** to the schema or data repository.

#### Options:

| Option                 | Description                                           |
| ---------------------- | ----------------------------------------------------- |
| **Connector Name**     | Logical label for this connection                     |
| **Database Type**      | Must match the environment (e.g., Oracle, SQL Server) |
| **Schema/Database**    | Name of the schema or DB containing sensitive data    |
| **Connection Details** | JDBC URL or connection string                         |
| **Authentication**     | User credentials with SELECT/UPDATE permissions       |

---

### **Step 4: Create or Import a Masking Job**

#### Purpose:

Define a **job** that links the **inventory** with **masking rulesets** and **algorithms**.

#### Options:

| Option             | Description                                            |
| ------------------ | ------------------------------------------------------ |
| **Job Name**       | Identifier for the masking job                         |
| **Connector**      | Choose from added inventories                          |
| **Execution Mode** | Options: **On-the-fly**, **In-place**, **Backup Copy** |
| **Fail Behavior**  | Stop or continue on row-level errors                   |

> Optional: You can clone existing jobs and edit them.

---

### **Step 5: Create a Ruleset**

#### Purpose:

Select **specific tables and columns** for masking.

#### Options:

| Option               | Description                                   |
| -------------------- | --------------------------------------------- |
| **Ruleset Name**     | Logical group for the columns/tables          |
| **Tables Included**  | Choose one or more tables to mask             |
| **Columns Included** | Choose specific columns to mask in each table |

> Optional: Exclude audit or metadata columns from masking.

---

### **Step 6: Define Masking Algorithms**

#### Purpose:

Assign **masking functions** to each sensitive column.

#### Options:

| Option                   | Description                                               |
| ------------------------ | --------------------------------------------------------- |
| **Algorithm Type**       | Built-in (e.g., Randomize, Shuffle, Redact) or Custom SQL |
| **Format-Preserving**    | Ensures output format matches the original (e.g., SSN)    |
| **Consistent Masking**   | Ensures same input yields same output across datasets     |
| **Lookup-based Masking** | Uses reference data to replace original values            |
| **Custom Algorithm**     | Write a user-defined masking function                     |

---

### **Step 7: Configure Job Execution Options**

#### Purpose:

Set **runtime parameters** for execution.

#### Options:

| Option              | Description                                         |
| ------------------- | --------------------------------------------------- |
| **Multi-threading** | Improves performance using parallel threads         |
| **Row Limits**      | Mask a subset of data for testing                   |
| **Restart Mode**    | Resume from last successful row or restart entirely |
| **Audit Mode**      | Log actions without applying actual masking         |

> Optional: Dry run mode to validate configurations.

---

### **Step 8: Run the Masking Job**

* Navigate to **Jobs > Execute Job**.
* Select the created job.
* Click **Run** and monitor logs.

---

### **Step 9: Review Logs and Audit Reports**

* View job status, error logs, and masking statistics.
* Download logs for auditing or error resolution.

---

### **Optional: Schedule the Masking Job**

* Use the built-in scheduler to run jobs at regular intervals.
* Define time, frequency, and notification settings.

---

### **Result:**

Target data is now **masked in-place** or via **backup copy**, ensuring **data privacy** and **regulatory compliance** while preserving data format and integrity.

---
