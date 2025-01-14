## **Branching in Git/GitHub**

---

Branching in Git enables parallel development by allowing multiple versions of a project to coexist. This approach supports feature development, bug fixing, and code experimentation without disrupting the main codebase.

---

### **Overview of Branching**
Branches are pointers to specific commits in a repository. The default branch in most repositories is called `main` or `master`. Branching allows developers to work on isolated changes while maintaining a stable main branch.

---

### **Creating Branches**
Branches can be created locally or via the GitHub interface.

#### **Using Git (Local)**
- Create a new branch: `git branch branch_name`.
- Switch to the new branch: `git checkout branch_name` or `git switch branch_name`.
- Combine creation and switching: `git checkout -b branch_name` or `git switch -c branch_name`.

#### **Using GitHub**
- Navigate to the repository.
- Open the branches menu.
- Create a new branch by entering a name and clicking **Create branch**.

---

### **Viewing Branches**
#### **Local Branches**
- List all local branches: `git branch`.
- Display the current branch: Look for the branch name with an asterisk (*) in the output of `git branch`.

#### **Remote Branches**
- List remote branches: `git branch -r`.
- Show all branches (local and remote): `git branch -a`.

---

### **Switching Between Branches**
- Move to another branch: `git checkout branch_name` or `git switch branch_name`.
- Automatically switch and create the branch if it doesn’t exist: `git checkout -b branch_name`.

---

### **Merging Branches**
Merging combines the changes from one branch into another.

#### **Fast-Forward Merge**
- Occurs when the branch being merged has no divergent history.
- Example: `git merge branch_name`.

#### **Three-Way Merge**
- Happens when branches have diverged.
- Resolve conflicts if required, then complete the merge: `git merge branch_name`.

---

### **Rebasing Branches**
Rebasing moves the base of the branch to a new commit.

- Rebase a branch onto another: `git rebase target_branch`.
- Interactive rebasing: `git rebase -i base_commit` to rewrite history.

---

### **Deleting Branches**
#### **Local Branch**
- Delete a branch: `git branch -d branch_name`.
- Force-delete an unmerged branch: `git branch -D branch_name`.

#### **Remote Branch**
- Delete a branch from the remote: `git push origin --delete branch_name`.

---

### **Tracking Branches**
Remote branches can be tracked locally to stay in sync with the remote repository.

- Set up a local branch to track a remote one: `git checkout --track origin/branch_name`.
- View tracking information: `git branch -vv`.

---

### **Pulling Changes**
To update your branch with the latest changes from the remote, use `git pull`. This fetches updates and merges them into your current branch.

---

### **Pushing Branches**
#### **Pushing a New Branch**
- Push to a remote repository: `git push origin branch_name`.

#### **Pushing Updates**
- Push changes to an existing branch: `git push`.

---

### **Branching Strategies**
Branches are central to collaborative workflows. Common strategies include:

- **Feature Branching**: Each feature is developed on its branch.
- **Git Flow**: A structured workflow with branches like `develop`, `feature`, `release`, and `hotfix`.
- **Trunk-Based Development**: Developers frequently commit to the main branch with small, incremental changes.

---

### **Handling Conflicts**
Branch merging or rebasing can lead to conflicts. Resolve conflicts as follows:

- Identify conflicting files: Git highlights these during a merge.
- Edit files to resolve conflicts manually.
- Stage resolved files: `git add <filename>`.
- Complete the merge or rebase.

---

### **Best Practices for Branching**
- Use descriptive names for branches, such as `feature/add-login` or `bugfix/fix-crash`.
- Avoid committing directly to the main branch.
- Regularly sync branches with the main branch to avoid large merge conflicts.
- Delete stale branches after merging to keep the repository clean.

---
