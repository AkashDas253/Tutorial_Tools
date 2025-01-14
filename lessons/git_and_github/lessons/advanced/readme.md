## **Advanced Features in Git**

---

Git provides advanced features to handle specific scenarios efficiently, such as isolating changes, debugging issues, managing external dependencies, and automating tasks. Below are detailed notes on **Cherry-Picking**, **Bisecting**, **Submodules**, and **Hooks**.

---

### **Cherry-Picking**

#### **Overview**
Cherry-picking allows you to apply changes from a specific commit in one branch to another branch.

---

#### **Usage**
- Apply a specific commit to the current branch:
  ```bash
  git cherry-pick <commit_hash>
  ```
- Apply multiple commits:
  ```bash
  git cherry-pick <commit_hash1> <commit_hash2>
  ```
- Resolve conflicts during cherry-picking, then continue:
  ```bash
  git cherry-pick --continue
  ```

---

#### **Best Practices**
- Use cherry-picking sparingly, as it can create duplicate commits across branches.
- Always test the changes applied by cherry-picking to ensure correctness.

---

### **Bisecting**

#### **Overview**
Git bisect is a binary search tool used to identify the commit that introduced a bug.

---

#### **Usage**
1. Start the bisect process:
   ```bash
   git bisect start
   ```
2. Mark the current commit as bad (contains the bug):
   ```bash
   git bisect bad
   ```
3. Mark a known good commit (does not contain the bug):
   ```bash
   git bisect good <commit_hash>
   ```
4. Git checks out commits between good and bad. Test each commit, and mark as either good or bad:
   ```bash
   git bisect good
   git bisect bad
   ```
5. After identifying the problematic commit, stop bisecting:
   ```bash
   git bisect reset
   ```

---

#### **Best Practices**
- Automate testing during bisecting with scripts:
  ```bash
  git bisect run <test_script>
  ```
- Document the results to avoid repeating the bisecting process.

---

### **Submodules**

#### **Overview**
Git submodules allow you to include and manage other Git repositories within a parent repository.

---

#### **Adding a Submodule**
- Add a submodule to the repository:
  ```bash
  git submodule add <repository_url> <submodule_path>
  ```
- Initialize submodules after cloning a repository:
  ```bash
  git submodule update --init
  ```

---

#### **Working with Submodules**
- Update submodules to the latest commit:
  ```bash
  git submodule update --remote
  ```
- Remove a submodule:
  ```bash
  git submodule deinit -f <submodule_path>
  git rm -f <submodule_path>
  rm -rf .git/modules/<submodule_path>
  ```

---

#### **Best Practices**
- Use submodules for projects with clear dependencies and separate lifecycles.
- Document submodule paths and purposes for team members.

---

### **Hooks**

#### **Overview**
Git hooks are scripts that run automatically at specific points in the Git workflow, such as before committing or pushing changes.

---

#### **Types of Hooks**
- **Client-Side Hooks**: Operate on individual repositories (e.g., pre-commit, pre-push).
- **Server-Side Hooks**: Operate on repositories hosted on a server (e.g., post-receive).

---

#### **Using Hooks**
1. Navigate to the `.git/hooks` directory.
2. Add or modify hook scripts (e.g., `pre-commit`).
3. Make the script executable:
   ```bash
   chmod +x .git/hooks/pre-commit
   ```

---

#### **Examples**
- **Pre-Commit Hook**: Prevent committing files with syntax errors.
  ```bash
  #!/bin/bash
  if ! pylint *.py; then
    echo "Python linting failed. Commit aborted."
    exit 1
  fi
  ```
- **Pre-Push Hook**: Ensure tests pass before pushing.
  ```bash
  #!/bin/bash
  if ! npm test; then
    echo "Tests failed. Push aborted."
    exit 1
  fi
  ```

---

#### **Best Practices**
- Store hooks in a version-controlled directory and symlink them to `.git/hooks` for consistency:
  ```bash
  ln -s ../hooks/pre-commit .git/hooks/pre-commit
  ```
- Document the purpose and behavior of each hook for team members.

---
