## **File Operations in GitHub**

---

File operations in GitHub involve creating, modifying, managing, and organizing files within a repository. Below is a detailed overview of the key file operations and related commands.

---

### **1. Creating Files**
#### **a. From GitHub Web Interface**
1. Go to the repository.
2. Click **"Add file"** → **"Create new file"**.
3. Provide a file name and optionally include folder paths (e.g., `folder_name/file_name.txt`).
4. Add content, commit directly, or propose changes via a pull request.

#### **b. From Local System**
1. Create a file using your preferred method (e.g., text editor, IDE, or `touch` command).
2. Use `git add <filename>` to stage the file.
3. Commit the file: `git commit -m "Add new file"`

---

### **2. Viewing Files**
#### **a. From GitHub Web Interface**
- Navigate to the file in the repository to view its content.
- Use the **"History"** button to see file change history.

#### **b. From Local Repository**
- Open the file in any text editor or IDE.
- View staged changes using `git diff --staged`.

---

### **3. Modifying Files**
#### **a. From GitHub Web Interface**
1. Open the file.
2. Click the pencil (edit) icon.
3. Make changes, commit directly, or propose via a pull request.

#### **b. From Local System**
1. Edit the file in your preferred text editor or IDE.
2. Stage the changes: `git add <filename>`.
3. Commit the changes: `git commit -m "Edit file"`

---

### **4. Deleting Files**
#### **a. From GitHub Web Interface**
1. Navigate to the file.
2. Click the trash can icon.
3. Commit the change directly or propose via a pull request.

#### **b. From Local Repository**
1. Use the `git rm` command:
   - Remove the file from the repository: `git rm <filename>`
   - Keep the file locally: `git rm --cached <filename>`
2. Commit the change: `git commit -m "Remove file"`

---

### **5. Moving and Renaming Files**
#### **a. From GitHub Web Interface**
1. Open the file.
2. Click the pencil (edit) icon.
3. Change the file name or path in the **file name** field.
4. Commit the change directly or via a pull request.

#### **b. From Local Repository**
1. Use the `git mv` command:
   - `git mv <old_filename> <new_filename>` for renaming.
   - `git mv <old_path>/<filename> <new_path>/<filename>` for moving.
2. Commit the changes: `git commit -m "Rename/move file"`

---

### **6. Uploading Files**
#### **a. From GitHub Web Interface**
1. Go to the repository.
2. Click **"Add file"** → **"Upload files"**.
3. Drag and drop files or browse to select them.
4. Commit directly or propose via a pull request.

#### **b. From Local Repository**
1. Place the file in the repository directory.
2. Stage the file: `git add <filename>`.
3. Commit the file: `git commit -m "Upload file"`

---

### **7. Tracking Files**
#### **a. Checking File Status**
- `git status`: View changes in files (modified, untracked, staged).
- `git diff`: View uncommitted changes in tracked files.

#### **b. Ignoring Files**
- Add file patterns to `.gitignore` to exclude them from tracking.
- Example `.gitignore` content:
  ```plaintext
  # Ignore log files
  *.log
  
  # Ignore build directories
  /build/
  ```

---

### **8. Restoring Files**
#### **a. Undoing Changes**
- Discard uncommitted changes:
  - `git restore <filename>`: Undo changes to a specific file.
  - `git restore .`: Undo changes to all files.
- Restore a file to the previous commit:
  - `git checkout <commit_hash> -- <filename>`

#### **b. Recovering Deleted Files**
- If staged but not committed:
  - `git restore --staged <filename>`
- If committed:
  - `git checkout HEAD^ -- <filename>`

---

### **9. Viewing File History**
#### **a. Using GitHub Web Interface**
1. Navigate to the file.
2. Click **"History"** to see all commits affecting the file.

#### **b. Using Git Command**
- `git log -- <filename>`: View commit history for a file.
- `git blame <filename>`: View line-by-line history with authors.

---

### **10. File Permissions**
Git does not track file permissions except for the executable bit:
- Change file to executable: `chmod +x <filename>`
- Stage and commit the change:
  - `git add <filename>`
  - `git commit -m "Make file executable"`

---

### **11. Binary and Large File Handling**
#### **a. Binary Files**
- Git tracks binary files but does not show diffs.
- Use `--binary` with diff commands: `git diff --binary`

#### **b. Large Files**
- Use Git Large File Storage (LFS):
  1. Install LFS: `git lfs install`
  2. Track large files: `git lfs track "*.filetype"`
  3. Stage `.gitattributes`: `git add .gitattributes`

---

### **12. Best Practices for File Operations**
1. Use meaningful commit messages describing file changes.
2. Avoid committing sensitive data (e.g., credentials, API keys).
3. Regularly update `.gitignore` for files that should not be tracked.
4. Organize files into folders for better project structure.

---
