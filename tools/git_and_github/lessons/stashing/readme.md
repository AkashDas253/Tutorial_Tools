## **Stashing in Git**

---

Stashing in Git is a way to save changes in your working directory temporarily without committing them. This allows you to switch branches or perform other tasks without losing your uncommitted work.

---

### **Purpose of Stashing**
- Temporarily save work that is incomplete or not ready for a commit.
- Clear the working directory to work on other tasks without losing changes.
- Apply saved changes later when they are ready to be completed or committed.

---

### **Creating a Stash**
- Save all changes in the working directory (staged and unstaged):
  ```bash
  git stash
  ```
- Save changes with a custom message:
  ```bash
  git stash save "Descriptive message"
  ```
- Stash only staged changes:
  ```bash
  git stash --keep-index
  ```
- Stash untracked files along with changes:
  ```bash
  git stash -u
  ```

---

### **Viewing Stashes**
- List all saved stashes:
  ```bash
  git stash list
  ```
- Each stash is identified by an index and description, e.g., `stash@{0}: WIP on main`.

---

### **Applying Stashes**
#### **Apply Without Removing**
- Apply the latest stash to the working directory:
  ```bash
  git stash apply
  ```
- Apply a specific stash:
  ```bash
  git stash apply stash@{index}
  ```

#### **Apply and Remove**
- Apply the stash and remove it from the stash list:
  ```bash
  git stash pop
  ```
- Apply a specific stash and remove it:
  ```bash
  git stash pop stash@{index}
  ```

---

### **Dropping Stashes**
- Delete the latest stash:
  ```bash
  git stash drop
  ```
- Delete a specific stash:
  ```bash
  git stash drop stash@{index}
  ```

---

### **Clearing All Stashes**
- Remove all stashes:
  ```bash
  git stash clear
  ```

---

### **Branch-Specific Stashing**
- Stash changes specific to a branch and apply them on another branch:
  ```bash
  git stash
  git checkout branch_name
  git stash apply
  ```

---

### **Stashing Use Cases**
- Quickly switch branches:
  - Stash changes: `git stash`.
  - Switch branch: `git checkout branch_name`.
  - Apply stash: `git stash apply`.
- Save uncommitted changes to focus on urgent tasks without committing incomplete work.
- Experiment with different changes and revert using stashing.

---

### **Best Practices for Stashing**
- Always use descriptive messages to track stashes easily.
- Regularly clear unused stashes to avoid clutter.
- Use `git stash pop` carefully, as it removes the stash immediately after application.
- Avoid relying on stashing as a long-term solution; commit changes if they are ready.

---
