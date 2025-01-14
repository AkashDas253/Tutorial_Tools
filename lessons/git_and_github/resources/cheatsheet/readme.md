## Git: A Detailed and Generalized Note

#### **Introduction to Git**
Git is a distributed version control system that helps developers track changes in source code during software development. It allows multiple people to collaborate, ensures version history integrity, and facilitates branching, merging, and reverting changes.

---

### **Git Syntax Overview**
Git commands follow a general structure:
```
git [command] [options] [arguments]
```

- **`[command]`**: Specifies the action (e.g., `clone`, `commit`, `push`).
- **`[options]`**: Modifies the behavior of the command.
- **`[arguments]`**: Specifies targets like files, directories, or branch names.

---

### **Essential Git Commands and Their Parameters**

#### **1. `git init`**
Initializes a new Git repository.

- **Usage**:
  ```
  git init [directory]
  ```
- **Parameters**:
  - **`directory`** *(optional)*: The directory to initialize. Defaults to the current directory.

---

#### **2. `git clone`**
Clones an existing repository.

- **Usage**:
  ```
  git clone [repository-url] [directory]
  ```
- **Parameters**:
  - **`repository-url`** *(required)*: The URL of the repository.
  - **`directory`** *(optional)*: Directory name for the cloned repository. Defaults to the repository name.

---

#### **3. `git add`**
Stages changes for the next commit.

- **Usage**:
  ```
  git add [file-pattern]
  ```
- **Parameters**:
  - **`file-pattern`** *(optional)*: Files to stage. Defaults to `.` (all files).

---

#### **4. `git commit`**
Records staged changes to the repository.

- **Usage**:
  ```
  git commit [options]
  ```
- **Parameters**:
  - **`-m`** *(optional)*: Message for the commit. *(Default: None)*.
  - **`--amend`** *(optional)*: Amends the last commit.

---

#### **5. `git status`**
Shows the current status of the working directory and staging area.

- **Usage**:
  ```
  git status [options]
  ```
- **Parameters**:
  - **`-s` / `--short`** *(optional)*: Outputs a short-format status. *(Default: Full)*.

---

#### **6. `git log`**
Displays commit history.

- **Usage**:
  ```
  git log [options]
  ```
- **Parameters**:
  - **`--oneline`** *(optional)*: Displays logs in one line. *(Default: Full format)*.
  - **`-n <count>`** *(optional)*: Limits output to `<count>` commits.

---

#### **7. `git branch`**
Manages branches.

- **Usage**:
  ```
  git branch [options] [branch-name]
  ```
- **Parameters**:
  - **`branch-name`** *(optional)*: Name of the branch to create or delete.
  - **`-d`** *(optional)*: Deletes a branch. *(Default: List branches)*.

---

#### **8. `git checkout`**
Switches branches or restores files.

- **Usage**:
  ```
  git checkout [branch-name | file-name]
  ```
- **Parameters**:
  - **`branch-name`** *(optional)*: The branch to switch to.
  - **`file-name`** *(optional)*: File to restore.

---

#### **9. `git merge`**
Merges changes from one branch to another.

- **Usage**:
  ```
  git merge [branch-name]
  ```
- **Parameters**:
  - **`branch-name`** *(required)*: The branch to merge into the current branch.

---

#### **10. `git push`**
Pushes local changes to a remote repository.

- **Usage**:
  ```
  git push [remote-name] [branch-name]
  ```
- **Parameters**:
  - **`remote-name`** *(optional)*: Name of the remote repository. *(Default: `origin`)*.
  - **`branch-name`** *(optional)*: Name of the branch to push. *(Default: Current branch)*.

---

#### **11. `git pull`**
Fetches and merges changes from a remote repository.

- **Usage**:
  ```
  git pull [options] [remote-name] [branch-name]
  ```
- **Parameters**:
  - **`remote-name`** *(optional)*: Remote repository name. *(Default: `origin`)*.
  - **`branch-name`** *(optional)*: Branch to pull changes from. *(Default: Current branch)*.

---

#### **12. `git diff`**
Displays differences between commits, branches, or working states.

- **Usage**:
  ```
  git diff [options] [path]
  ```
- **Parameters**:
  - **`path`** *(optional)*: File or directory to compare. *(Default: Entire repository)*.

---

### **Key Ranges and Values**
- Boolean flags like `-m` or `--amend` are either present or absent (no specific range).
- Options like `-n <count>` for `git log` accept positive integers only.
- Path-based arguments (e.g., `directory`, `file-pattern`) depend on the system's file structure.

---

### **Best Practices**
1. Use **meaningful commit messages** with `git commit -m`.
2. Regularly **push changes** to avoid data loss.
3. **Merge carefully** after resolving conflicts.
4. Always check the **status** with `git status` before committing.

This note serves as a generalized guide to Git's commands, their syntax, and parameters for consistent usage.


## Detailed and Generalized Note on Git and GitHub

Below is a comprehensive table of Git and GitHub commands and features categorized based on tasks.

---

#### **Repository Management**

| **Command**                  | **Description**                                      | **Parameters**                                                                                                                                                      |
|------------------------------|------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `git init`                   | Initializes a local Git repository.                 | **None**: Creates a repository in the current directory.                                                                                                           |
| `git clone <url> [dir]`      | Clones a GitHub repository.                         | `<url>`: Repository URL (Required). <br> `[dir]`: Destination directory (Optional, defaults to repo name).                                                         |
| `git remote add <name> <url>`| Adds a remote to track a repository.                | `<name>`: Remote name (e.g., `origin`). <br> `<url>`: Repository URL.                                                                                              |

---

#### **Staging and Committing**

| **Command**                   | **Description**                                      | **Parameters**                                                                                                                                                      |
|-------------------------------|------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `git add <file>`              | Adds files to the staging area.                     | `<file>`: File path or wildcard (e.g., `*.txt`). <br> Defaults to all files with `.`.                                                                               |
| `git commit -m "<message>"`   | Commits staged changes with a message.              | `-m`: Commit message flag. <br> `<message>`: Commit description (Required).                                                                                        |
| `git commit --amend`          | Modifies the last commit.                           | No parameters required.                                                                                                                                           |

---

#### **Branching and Merging**

| **Command**                   | **Description**                                      | **Parameters**                                                                                                                                                      |
|-------------------------------|------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `git branch <name>`           | Creates a new branch.                               | `<name>`: Branch name (Required).                                                                                                                                 |
| `git checkout <name>`         | Switches to the specified branch.                  | `<name>`: Branch name (Required).                                                                                                                                 |
| `git merge <branch>`          | Merges the specified branch into the current branch.| `<branch>`: Branch name (Required).                                                                                                                              |

---

#### **Collaboration**

| **Command**                   | **Description**                                      | **Parameters**                                                                                                                                                      |
|-------------------------------|------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `git push [remote] [branch]`  | Pushes changes to a remote repository.              | `[remote]`: Remote name (Defaults to `origin`). <br> `[branch]`: Branch name (Defaults to the current branch).                                                      |
| `git pull [remote] [branch]`  | Fetches and merges changes from a remote repository.| `[remote]`: Remote name (Defaults to `origin`). <br> `[branch]`: Branch name (Defaults to the current branch).                                                      |
| `git fetch <remote>`          | Fetches updates from the remote repository.         | `<remote>`: Remote name (Defaults to `origin`).                                                                                                                    |

---

#### **Viewing Changes**

| **Command**                   | **Description**                                      | **Parameters**                                                                                                                                                      |
|-------------------------------|------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `git status`                  | Displays the status of the working directory.       | `-s`: Outputs a short format (Optional).                                                                                                                           |
| `git diff`                    | Shows differences between commits or branches.      | `[path]`: File or directory to compare (Optional).                                                                                                                 |
| `git log`                     | Displays the commit history.                        | `--oneline`: One-line format (Optional). <br> `-n <count>`: Limits the output to `<count>` commits (Optional).                                                     |

---

#### **GitHub-Specific Features**

| **Feature**                   | **Description**                                      | **Examples/Syntax**                                                                                                                                                 |
|-------------------------------|------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Issues**                    | Tracks bugs or feature requests.                    | Create via GitHub UI or API. <br> API Endpoint: `POST /repos/{owner}/{repo}/issues`.                                                                               |
| **Pull Requests**             | Proposes changes to a repository.                  | Use GitHub UI to submit PRs. <br> API Endpoint: `POST /repos/{owner}/{repo}/pulls`.                                                                                |
| **Actions**                   | Automates workflows like CI/CD pipelines.          | YAML Syntax: <br> ```yaml<br>on: push<br>jobs:<br> build:<br>  steps:<br>   - uses: actions/checkout@v2<br>```                                                     |
| **GitHub Pages**              | Hosts websites from repositories.                  | Enable via repository settings. <br> Requires an `index.html` or framework like Jekyll.                                                                           |

---

#### **API Operations**

| **Operation**                 | **Description**                                      | **Examples/Syntax**                                                                                                                                                 |
|-------------------------------|------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Create Repository             | Creates a new repository via API.                   | API Endpoint: `POST /user/repos`. <br> Parameters: `{ "name": "new-repo", "private": true }`.                                                                      |
| List Repositories             | Retrieves repositories for a user.                  | API Endpoint: `GET /users/{username}/repos`. <br> Parameters: `type=all` (Default: `all`).                                                                         |
| Manage Webhooks               | Automates repository event triggers.                | API Endpoint: `POST /repos/{owner}/{repo}/hooks`. <br> Payload: `{ "config": { "url": "http://example.com/webhook", "content_type": "json" } }`.                   |

---

#### **GUI Tools**

| **Tool**                      | **Description**                                      | **Key Features**                                                                                                                                                   |
|-------------------------------|------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **GitHub Desktop**            | GUI for managing repositories.                      | Clone, commit, push, and pull without the terminal.                                                                                                               |
| **GitHub Web Interface**      | Manage repositories and view insights visually.     | Includes options for creating issues, pull requests, and editing files online.                                                                                    |

---

This table integrates Git and GitHub operations, providing a unified view categorized by tasks for ease of use and reference. Let me know if you need additional details!


Yes, there are additional Git and GitHub commands and features that cater to more advanced use cases, such as **undoing changes**, **rebasing**, **stashing**, **handling conflicts**, and **using GitHub for collaborative workflows**. Below, I’ll expand the table with additional tasks and commands for these scenarios.

---

#### **Undoing Changes**

| **Command**                   | **Description**                                      | **Parameters**                                                                                                                                                      |
|-------------------------------|------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `git reset [mode] <commit>`   | Moves the current branch to a specific commit.       | `[mode]`: Reset mode (`--soft`, `--mixed`, or `--hard`). <br> `<commit>`: Commit hash or reference (Required).                                                     |
| `git revert <commit>`         | Creates a new commit to undo a specific commit.      | `<commit>`: Commit hash or reference (Required).                                                                                                                   |
| `git restore <file>`          | Discards changes in a working directory.            | `<file>`: File path (Required).                                                                                                                                    |

---

#### **Rebasing and Rewriting History**

| **Command**                   | **Description**                                      | **Parameters**                                                                                                                                                      |
|-------------------------------|------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `git rebase <branch>`         | Reapplies commits on top of another branch.          | `<branch>`: Target branch (Required).                                                                                                                              |
| `git rebase -i <commit>`      | Interactive rebase to edit or squash commits.        | `<commit>`: Base commit hash (Required).                                                                                                                           |
| `git cherry-pick <commit>`    | Applies specific commits from another branch.        | `<commit>`: Commit hash or reference (Required).                                                                                                                   |

---

#### **Stashing Changes**

| **Command**                   | **Description**                                      | **Parameters**                                                                                                                                                      |
|-------------------------------|------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `git stash`                   | Saves uncommitted changes temporarily.               | No parameters required.                                                                                                                                           |
| `git stash pop`               | Applies the latest stash and removes it from the stack. | No parameters required.                                                                                                                                           |
| `git stash list`              | Lists all stashed changes.                          | No parameters required.                                                                                                                                           |

---

#### **Handling Conflicts**

| **Command**                   | **Description**                                      | **Parameters**                                                                                                                                                      |
|-------------------------------|------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `git merge <branch>`          | Merges changes from another branch (may cause conflicts).| `<branch>`: Branch name (Required).                                                                                                                              |
| `git mergetool`               | Launches a merge resolution tool.                   | No parameters required.                                                                                                                                           |
| `git diff`                    | Examines conflicting changes.                       | `[file]`: File path (Optional).                                                                                                                                    |

---

#### **Tagging and Releases**

| **Command**                   | **Description**                                      | **Parameters**                                                                                                                                                      |
|-------------------------------|------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `git tag <name>`              | Creates a lightweight tag.                          | `<name>`: Tag name (Required).                                                                                                                                    |
| `git tag -a <name> -m "<msg>"`| Creates an annotated tag.                           | `<name>`: Tag name (Required). <br> `-m "<msg>"`: Tag message (Required).                                                                                         |
| `git push <remote> <tag>`     | Pushes a tag to the remote repository.              | `<remote>`: Remote name (Defaults to `origin`). <br> `<tag>`: Tag name (Required).                                                                                 |

---

#### **Collaborative Workflows on GitHub**

| **Feature**                   | **Description**                                      | **Examples/Syntax**                                                                                                                                                 |
|-------------------------------|------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Forking**                   | Creates a copy of another user’s repository.        | Done through the GitHub web interface.                                                                                                                             |
| **Pull Requests**             | Proposes changes from a forked or feature branch.   | Compare changes via GitHub’s UI and request reviews.                                                                                                              |
| **Code Reviews**              | Allows team members to review and comment on PRs.   | Use GitHub’s "Review Changes" option for feedback.                                                                                                                |

---

#### **Advanced GitHub Actions**

| **Feature**                   | **Description**                                      | **Examples/Syntax**                                                                                                                                                 |
|-------------------------------|------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Custom Actions**            | Create reusable GitHub Actions workflows.           | YAML Syntax: <br> ```yaml<br>on: push<br>jobs:<br> custom:<br>   steps:<br>     - uses: org/repo@v1.0.0<br>```                                                    |
| **Matrix Builds**             | Test code on multiple platforms or configurations.  | YAML Syntax: <br> ```yaml<br>strategy:<br>  matrix:<br>    os: [ubuntu, windows]<br>```                                                                           |
| **Scheduled Workflows**       | Run workflows on a schedule.                        | YAML Syntax: <br> ```yaml<br>on:<br>  schedule:<br>    - cron: '0 0 * * *'<br>```                                                                                 |

---

#### **Repository Insights on GitHub**

| **Feature**                   | **Description**                                      | **Examples/Syntax**                                                                                                                                                 |
|-------------------------------|------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Insights**                  | Provides statistics on contributors, commits, and code frequency. | View via the GitHub web interface under the "Insights" tab.                                                                                                     |
| **Graphs**                    | Visualizes repository activity and contributions.   | Includes activity graphs, network graphs, and punch card views.                                                                                                  |

---

### **Advanced Git Configuration**

| **Command**                   | **Description**                                      | **Parameters**                                                                                                                                                      |
|-------------------------------|------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `git config --global <key> <value>` | Sets global Git configuration.                 | `<key>`: Configuration key (e.g., `user.name`, `user.email`). <br> `<value>`: Value to set (Required).                                                            |
| `git config --list`           | Displays the current configuration.                 | No parameters required.                                                                                                                                           |
| `git config alias.<alias-name> <command>` | Creates a shortcut for a Git command.    | `<alias-name>`: Alias name (Required). <br> `<command>`: Git command to alias (Required).                                                                          |

---

### **Performance Optimization for Large Repositories**

| **Command**                   | **Description**                                      | **Parameters**                                                                                                                                                      |
|-------------------------------|------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `git gc`                      | Runs garbage collection to optimize repository size. | No parameters required.                                                                                                                                           |
| `git sparse-checkout`         | Limits the working directory to specific files.     | `[patterns]`: Patterns for files or directories to include (Optional).                                                                                            |
| `git shallow clone --depth <n>` | Clones a repository with limited history.         | `--depth <n>`: Number of recent commits to include (Required).                                                                                                    |

---

### **Submodules**

| **Command**                   | **Description**                                      | **Parameters**                                                                                                                                                      |
|-------------------------------|------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `git submodule add <repo-url>`| Adds another repository as a submodule.             | `<repo-url>`: URL of the submodule repository (Required).                                                                                                          |
| `git submodule update --init` | Initializes and updates submodules.                 | No parameters required.                                                                                                                                           |
| `git submodule foreach <cmd>` | Runs a command in all submodules.                   | `<cmd>`: Shell command to execute (Required).                                                                                                                     |

---

### **Advanced Collaboration Features in GitHub**

| **Feature**                   | **Description**                                      | **Examples/Syntax**                                                                                                                                                 |
|-------------------------------|------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Branch Protection Rules**   | Restricts actions like merging without reviews.     | Configurable via GitHub repository settings.                                                                                                                      |
| **Required Reviews**          | Enforces code reviews before merging.               | Set under "Settings > Branches > Branch protection rules."                                                                                                        |
| **Status Checks**             | Ensures tests or CI pipelines pass before merging.  | Example in YAML: <br> ```yaml<br>name: Build Test<br>jobs:<br> test:<br>   runs-on: ubuntu-latest<br>```                                                          |

---

### **GitHub Advanced Features for DevOps**

| **Feature**                   | **Description**                                      | **Examples/Syntax**                                                                                                                                                 |
|-------------------------------|------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **GitHub Codespaces**         | Cloud-based development environments.               | Launchable via the "Code" dropdown in a repository.                                                                                                               |
| **Self-Hosted Runners**       | Use custom servers for GitHub Actions.              | Requires installing a runner binary on your server and configuring it with GitHub.                                                                                |
| **Secret Management**         | Stores API keys and sensitive data for workflows.   | YAML Syntax: <br> ```yaml<br>env:<br>   API_KEY: ${{ secrets.API_KEY }}<br>```                                                                                    |

---

### **Audit Logs and Security Features**

| **Feature**                   | **Description**                                      | **Examples/Syntax**                                                                                                                                                 |
|-------------------------------|------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Audit Logs**                | Tracks all actions in a repository or organization. | Available via GitHub's "Settings > Audit Log" or via the GitHub API.                                                                                              |
| **Token Scanning**            | Identifies leaked tokens in commits.                | GitHub scans for sensitive tokens automatically and notifies maintainers.                                                                                        |
| **Code Scanning Alerts**      | Detects security vulnerabilities.                   | Configurable via "Security > Code Scanning Alerts" and GitHub Actions workflows.                                                                                  |

---

### **Automating Advanced Workflows with GitHub CLI**

| **Command**                   | **Description**                                      | **Parameters**                                                                                                                                                      |
|-------------------------------|------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `gh repo create`              | Creates a new repository via CLI.                   | `<name>`: Repository name (Required). <br> `--private`: Makes the repository private (Optional).                                                                  |
| `gh pr create`                | Opens a pull request from the CLI.                  | `<title>`: PR title (Required). <br> `<base>`: Base branch (Required).                                                                                            |
| `gh issue list`               | Lists all issues in a repository.                   | `--state [open|closed|all]`: Filter issues by state (Optional).                                                                                                   |

---

### **GitHub Packages**

| **Feature**                   | **Description**                                      | **Examples/Syntax**                                                                                                                                                 |
|-------------------------------|------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Publishing Packages**       | Uploads binaries, containers, or other packages.    | Example in YAML: <br> ```yaml<br>steps:<br>  - name: Publish<br>    uses: actions/setup-java@v2<br>```                                                             |
| **Consuming Packages**        | Downloads and uses published packages.              | Configurable via `package.json` (NPM) or similar tools for other package managers.                                                                                |

---

### **Git Worktrees**

| **Command**                   | **Description**                                      | **Parameters**                                                                                                                                                      |
|-------------------------------|------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `git worktree add <path> <branch>` | Creates a linked working directory.            | `<path>`: Directory path (Required). <br> `<branch>`: Branch to associate with the directory (Required).                                                          |
| `git worktree list`           | Lists all linked worktrees.                         | No parameters required.                                                                                                                                           |
| `git worktree remove <path>`  | Removes a linked working directory.                 | `<path>`: Directory path (Required).                                                                                                                              |




### **Stashing Advanced Use Cases**

| **Command**                          | **Description**                                     | **Parameters**                                                                                                                                                      |
|--------------------------------------|-----------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `git stash`                          | Saves uncommitted changes temporarily.             | No parameters required.                                                                                                                                           |
| `git stash save "<message>"`         | Saves stash with a custom message.                 | `<message>`: Description for the stash (Optional).                                                                                                                 |
| `git stash apply [<stash-index>]`    | Applies a specific stash.                          | `<stash-index>`: Stash reference (Optional). <br> **Default**: Most recent stash.                                                                                  |
| `git stash pop`                      | Applies and removes the most recent stash.         | No parameters required.                                                                                                                                           |
| `git stash list`                     | Lists all stashes in the repository.               | No parameters required.                                                                                                                                           |

---

### **Working with Patches**

| **Command**                          | **Description**                                     | **Parameters**                                                                                                                                                      |
|--------------------------------------|-----------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `git format-patch <revision-range>`  | Creates patch files from commits.                  | `<revision-range>`: Range of commits (Required).                                                                                                                   |
| `git apply <patch-file>`             | Applies changes from a patch file.                 | `<patch-file>`: Path to the patch file (Required).                                                                                                                 |
| `git am <patch-file>`                | Applies patches with commit metadata.              | `<patch-file>`: Path to the patch file (Required).                                                                                                                 |

---

### **Rebasing Advanced Features**

| **Command**                          | **Description**                                     | **Parameters**                                                                                                                                                      |
|--------------------------------------|-----------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `git rebase -i <base>`               | Performs an interactive rebase.                    | `<base>`: Commit or branch to rebase onto (Required).                                                                                                              |
| `git rebase --autosquash`            | Automatically squashes commits marked in the rebase. | No parameters required.                                                                                                                                           |
| `git rebase --preserve-merges`       | Preserves merge commits during rebasing.           | No parameters required.                                                                                                                                           |

---

### **Git Hooks**

| **Hook**                             | **Description**                                     | **Examples/Syntax**                                                                                                                                                 |
|--------------------------------------|-----------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `pre-commit`                         | Runs before a commit is made.                      | Example: Enforce coding standards with a script.                                                                                                                   |
| `post-merge`                         | Runs after a `git merge`.                          | Example: Automatically update dependencies after merging a branch.                                                                                                 |
| `pre-push`                           | Runs before pushing changes to a remote.           | Example: Verify tests before pushing.                                                                                                                              |

---

### **GitHub Wiki**

| **Feature**                          | **Description**                                     | **Examples/Syntax**                                                                                                                                                 |
|--------------------------------------|-----------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| GitHub Wiki                          | Built-in documentation feature for repositories.   | Markdown-based syntax for pages and navigation.                                                                                                                    |
| Wiki Cloning                         | Allows editing wikis locally.                      | ```bash<br>git clone https://github.com/<owner>/<repo>.wiki.git<br>```                                                                                              |

---

### **GitHub Discussions**

| **Feature**                          | **Description**                                     | **Examples/Syntax**                                                                                                                                                 |
|--------------------------------------|-----------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Discussions**                      | Platform for community engagement.                 | Available under the "Discussions" tab in repositories.                                                                                                             |
| Categories                           | Organize discussions by type.                      | Categories include Q&A, Ideas, and Announcements.                                                                                                                  |

---

### **Advanced GitHub Actions Features**

| **Feature**                          | **Description**                                     | **Examples/Syntax**                                                                                                                                                 |
|--------------------------------------|-----------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Reusable Workflows**               | Share workflows across repositories.               | ```yaml<br>jobs:<br>   build:<br>     uses: ./.github/workflows/build.yml<br>```                                                                                   |
| **Matrix Builds**                    | Test multiple environments in parallel.            | ```yaml<br>strategy:<br>  matrix:<br>     os: [ubuntu-latest, macos-latest]<br>```                                                                                  |
| **Artifact Management**              | Store and share files between jobs.                | ```yaml<br>steps:<br>  - name: Upload artifact<br>    uses: actions/upload-artifact@v2<br>```                                                                       |

---

### **Git Large File Storage (LFS)**

| **Command**                          | **Description**                                     | **Parameters**                                                                                                                                                      |
|--------------------------------------|-----------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `git lfs install`                    | Installs Git LFS in the repository.                | No parameters required.                                                                                                                                           |
| `git lfs track <file-pattern>`       | Tracks large files using a pattern.                | `<file-pattern>`: Glob pattern for files (Required).                                                                                                               |
| `git lfs push origin <branch>`       | Pushes large files to the remote.                  | `<branch>`: Target branch (Required).                                                                                                                              |

---

### **Git Bisect for Debugging**

| **Command**                          | **Description**                                     | **Parameters**                                                                                                                                                      |
|--------------------------------------|-----------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `git bisect start`                   | Starts a binary search for a faulty commit.        | No parameters required.                                                                                                                                           |
| `git bisect good <commit>`           | Marks a commit as good.                            | `<commit>`: SHA of a commit (Required).                                                                                                                            |
| `git bisect bad <commit>`            | Marks a commit as bad.                             | `<commit>`: SHA of a commit (Required).                                                                                                                            |

---

### **GitHub Enterprise Features**

| **Feature**                          | **Description**                                     | **Examples/Syntax**                                                                                                                                                 |
|--------------------------------------|-----------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Enterprise Insights**              | Provides analytics for repositories.               | Available in the Enterprise dashboard.                                                                                                                             |
| **SAML Single Sign-On**              | Integrates GitHub authentication with SSO.         | Configurable in Enterprise settings.                                                                                                                               |
| **GitHub Connect**                   | Links on-premise and cloud GitHub instances.       | Available in the Enterprise admin panel.                                                                                                                           |

