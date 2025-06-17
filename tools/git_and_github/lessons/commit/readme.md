## **Commit Management in Git/GitHub**

---

Commits are the core of Git version control, representing snapshots of the project's state at specific points in time. Effective commit management ensures a clear and maintainable project history.

---

### **1. What is a Commit?**
- A commit is a saved snapshot of changes in the repository.
- Contains:
  - Metadata: Commit ID (hash), author, date, and message.
  - Changes: Added, modified, or deleted files.
- Commits form a **commit history**, reflecting project evolution.

---

### **2. Creating Commits**
#### **a. Basic Workflow**
1. **Stage Changes**:
   - `git add <filename>`: Stage specific files.
   - `git add .`: Stage all changes in the working directory.
2. **Commit Staged Changes**:
   - `git commit -m "Commit message"`
3. **Best Practices for Commit Messages**:
   - Be concise and descriptive.
   - Use imperative mood (e.g., "Add new feature" instead of "Added new feature").
   - Optionally include a detailed description.

#### **b. Skipping the Staging Area**
- Directly commit changes: `git commit -a -m "Commit message"`
  *(Only works for tracked files)*.

---

### **3. Viewing Commit History**
#### **a. Basic History**
- `git log`: View detailed commit history.
- `git log --oneline`: Show history with commit hashes and messages in a compact format.

#### **b. Advanced Options**
- Limit the number of commits: `git log -n <number>`
- Filter by author: `git log --author="<author_name>"`
- Show changes in each commit: `git log -p`

---

### **4. Amending Commits**
- Modify the most recent commit (message or content):
  - `git commit --amend -m "Updated message"`
- To add new changes:
  1. Make changes to files.
  2. Stage the changes: `git add <filename>`
  3. Amend the commit: `git commit --amend`

---

### **5. Undoing Commits**
#### **a. Undo Changes Without Deleting History**
- Revert a commit:
  - `git revert <commit_hash>`: Creates a new commit that negates the changes of the specified commit.
  
#### **b. Undo Changes and Delete History**
- Reset to a previous state:
  - `git reset --soft <commit_hash>`: Retain changes in the staging area.
  - `git reset --mixed <commit_hash>`: Retain changes in the working directory.
  - `git reset --hard <commit_hash>`: Discard all changes after the specified commit.

---

### **6. Managing Commit Messages**
#### **a. Updating the Last Commit Message**
- `git commit --amend`: Edit the most recent commit message.

#### **b. Rewriting Multiple Messages**
- Use `git rebase -i <base_commit>`:
  1. Replace `pick` with `reword` for commits to edit.
  2. Update messages as prompted.

---

### **7. Splitting Commits**
1. Use `git reset HEAD~1` to unstage the last commit.
2. Stage changes selectively: `git add <filename>` or `git add -p`.
3. Commit changes individually.

---

### **8. Squashing Commits**
- Combine multiple commits into one:
  - `git rebase -i <base_commit>`:
    1. Mark commits as `squash` or `s` to merge them into the previous commit.
    2. Edit the resulting commit message.

---

### **9. Cherry-Picking Commits**
- Apply changes from specific commits to the current branch:
  - `git cherry-pick <commit_hash>`

---

### **10. Comparing Commits**
- Compare two commits:
  - `git diff <commit1> <commit2>`
- Compare with the working directory:
  - `git diff <commit_hash>`

---

### **11. Signing Commits**
- Add a GPG signature to commits:
  1. Configure GPG: `git config --global user.signingkey <key_id>`
  2. Sign a commit: `git commit -S -m "Signed commit"`

---

### **12. Managing Commit History**
#### **a. Rebasing**
- Reorganize or edit commit history:
  - `git rebase -i <base_commit>`
- Rebase onto another branch:
  - `git rebase <branch_name>`

#### **b. Cleaning Up History**
- Remove dangling commits (unreferenced):
  - `git reflog` to view references.
  - `git gc` to clean up dangling commits.

---

### **13. Pushing Commits to Remote**
- Push commits to a remote branch:
  - `git push origin <branch_name>`
- Force-push (use with caution):
  - `git push --force`

---

### **14. Pull Requests and Commits**
- Each pull request displays a series of commits.
- Squash commits when merging to reduce noise in the main branch:
  - Enable **"Squash and merge"** option in GitHub.

---

### **15. Best Practices for Commit Management**
1. **Commit Often**:
   - Save logical units of work in separate commits.
2. **Use Descriptive Messages**:
   - Clearly convey what the commit achieves.
3. **Avoid Committing Sensitive Data**:
   - Add secrets to `.gitignore`.
4. **Keep Commits Small**:
   - Avoid including unrelated changes.
5. **Test Before Committing**:
   - Ensure changes work as intended.

---
