## **Git concepts and their subconcepts**

---

### **1. Basics of Git**
- **What is Git?**
  - Version control system
  - Local vs. remote repository
- **Installation**
  - Platform-specific installation (Windows, macOS, Linux)
  - Initial setup (`git config`)
- **Git Commands Overview**
  - Common commands: `git init`, `git clone`, `git status`

---

### **2. Repository Management**
- **Creating a Repository**
  - `git init`
  - Cloning (`git clone`)
- **Structure of a Git Repository**
  - Working directory
  - Staging area
  - `.git` folder
- **Ignoring Files**
  - `.gitignore` syntax and rules
  - Patterns and precedence

---

### **3. File Operations**
- **Adding and Removing Files**
  - `git add`
  - `git rm`
- **Renaming Files**
  - `git mv`
- **Checking File Status**
  - `git status`
  - Untracked, modified, staged files

---

### **4. Commit Management**
- **Creating Commits**
  - `git commit`
  - Commit messages and best practices
- **Amending Commits**
  - `git commit --amend`
- **Viewing Commit History**
  - `git log`
  - Flags: `--oneline`, `--graph`, `--stat`

---

### **5. Branching**
- **Creating Branches**
  - `git branch`
- **Switching Branches**
  - `git checkout`
  - `git switch`
- **Branch Management**
  - Deleting: `git branch -d`
  - Renaming: `git branch -m`
- **Branch Comparisons**
  - Merging: `git merge`
  - Rebasing: `git rebase`

---

### **6. Merging and Conflict Resolution**
- **Fast-Forward Merge**
- **Three-Way Merge**
- **Resolving Conflicts**
  - Identifying conflicts
  - Editing files
  - Marking resolved (`git add`)
  - Completing merge (`git commit`)

---

### **7. Remote Repositories**
- **Connecting to Remotes**
  - `git remote add`
  - Viewing remotes (`git remote -v`)
- **Fetching and Pulling**
  - `git fetch`
  - `git pull`
- **Pushing Changes**
  - `git push`
- **Tracking Remote Branches**
  - Upstream branches (`git branch --set-upstream-to`)

---

### **8. Tags**
- **Creating Tags**
  - Lightweight: `git tag`
  - Annotated: `git tag -a`
- **Managing Tags**
  - Deleting: `git tag -d`
  - Pushing: `git push origin --tags`

---

### **9. Stashing**
- **Saving Work**
  - `git stash save`
- **Applying Stashes**
  - `git stash apply`
- **Managing Stashes**
  - `git stash list`
  - `git stash drop`

---

### **10. Undoing Changes**
- **Unstaging Files**
  - `git restore --staged`
- **Reverting Changes**
  - `git checkout --`
  - `git restore`
- **Reverting Commits**
  - `git revert`
- **Resetting Commits**
  - `git reset` (soft, mixed, hard)

---

### **11. Logs and Diffs**
- **Viewing Logs**
  - `git log`
  - `git reflog`
- **Comparing Changes**
  - `git diff`
  - Flags: `--cached`, `--name-only`, `--name-status`

---

### **12. Advanced Features**
- **Cherry-Picking**
  - `git cherry-pick`
- **Bisecting**
  - `git bisect`
- **Submodules**
  - Adding: `git submodule add`
  - Updating: `git submodule update`
- **Hooks**
  - Pre-commit, post-merge, etc.
  - Configuring custom hooks

---

### **13. Collaboration**
- **Pull Requests (PRs)**
  - Concept overview (GitHub, GitLab, etc.)
- **Code Reviews**
  - Using Git tools for reviews
- **Resolving Collaboration Conflicts**
  - Conflict resolution in shared branches

---

### **14. Security and Authentication**
- **SSH Authentication**
  - Generating keys
  - Adding SSH keys to platforms
- **Credential Management**
  - Storing credentials securely
  - Token-based authentication

---

### **15. Optimization and Maintenance**
- **Cleaning Repositories**
  - `git gc`
  - `git clean`
- **Managing Large Repositories**
  - `.gitattributes` for large files
  - Git Large File Storage (LFS)

---

### **16. Customization**
- **Aliases**
  - Creating: `git config alias.<name> <command>`
- **Configuration**
  - Global vs. local settings (`git config`)

---

### **17. Integrations**
- **CI/CD Pipelines**
  - Git workflows in CI/CD tools
- **Git and IDEs**
  - Git integrations in VS Code, IntelliJ, etc.
- **Third-Party Tools**
  - GitKraken, SourceTree

---

## **GitHub concepts and their subconcepts**

---

### **1. Basics of GitHub**
- **What is GitHub?**
  - Platform for hosting and collaborating on Git repositories
  - Public vs. private repositories
- **Getting Started**
  - Creating an account
  - User profile and GitHub handle
- **GitHub vs. Git**
  - Git (version control) vs. GitHub (hosting and collaboration)

---

### **2. Repository Management**
- **Creating a Repository**
  - Local and remote repositories
  - GitHub repository settings (public/private, description, README)
- **Cloning Repositories**
  - HTTPS, SSH, and GitHub CLI methods
- **Forking**
  - What is a fork?
  - Forking a repository for independent contributions
- **Template Repositories**
  - Using repository templates for project scaffolding

---

### **3. Collaboration**
- **Pull Requests (PRs)**
  - Creating PRs
  - Reviewing PRs
  - Merging PRs
  - Draft PRs
- **Code Reviews**
  - Adding comments to specific lines
  - Requesting reviewers
  - Approving or requesting changes
- **Branching Strategies**
  - Feature branches
  - Release branches
  - GitFlow, GitHub Flow

---

### **4. Issues and Project Management**
- **Issues**
  - Creating and managing issues
  - Assigning labels, milestones, and assignees
  - Linking issues to pull requests
- **Project Boards**
  - Kanban-style project management
  - Automating workflows with project boards
- **Discussions**
  - Collaborating with discussions for broader topics
- **Milestones**
  - Grouping issues and pull requests into milestones
  - Tracking progress

---

### **5. Actions (CI/CD)**
- **What is GitHub Actions?**
  - Automating workflows (e.g., testing, deployment)
- **Creating Workflows**
  - Writing YAML configuration files
  - Using prebuilt GitHub Actions
- **Triggers**
  - Events that trigger workflows (push, pull_request, etc.)
- **Secrets**
  - Managing sensitive data for workflows (e.g., API keys)

---

### **6. Security**
- **Branch Protection Rules**
  - Requiring reviews before merging
  - Enforcing status checks
- **Dependabot**
  - Automatic dependency updates
  - Security alerts for vulnerable dependencies
- **Secrets and Encryption**
  - GitHub Secrets for workflows
  - Secret scanning in repositories

---

### **7. GitHub Pages**
- **Hosting Websites**
  - Static site hosting directly from a GitHub repository
- **Custom Domains**
  - Adding custom domains to GitHub Pages
- **Themes and Jekyll**
  - Using Jekyll to generate GitHub Pages
  - Configuring themes with `_config.yml`

---

### **8. Insights and Analytics**
- **Repository Insights**
  - Contribution graphs
  - Traffic statistics (views, clones)
  - Dependency graphs
- **Community Profile**
  - Adding a code of conduct
  - Setting up contributing guidelines
- **Metrics**
  - Commits, contributors, and issue resolution times

---

### **9. GitHub CLI**
- **What is GitHub CLI?**
  - Command-line interface for GitHub
- **Commands**
  - `gh repo clone`, `gh issue create`, `gh pr view`
- **Authentication**
  - Logging in via CLI
  - Configuring SSH or HTTPS for secure connections

---

### **10. GitHub Packages**
- **Package Hosting**
  - Supported formats (Docker, Maven, npm, etc.)
- **Publishing Packages**
  - Automating package publishing with Actions
- **Using Packages**
  - Authenticating and installing packages in projects

---

### **11. Integrations**
- **Third-Party Apps**
  - Integrating CI tools (Jenkins, Travis CI)
  - Linking productivity tools (Slack, Trello)
- **Webhooks**
  - Triggering events based on repository activity
- **GitHub Marketplace**
  - Finding and using prebuilt Actions and apps

---

### **12. Open Source Contributions**
- **Finding Projects**
  - Exploring repositories tagged with `good-first-issue`
- **Submitting Contributions**
  - Forking, cloning, and creating pull requests
- **Licensing**
  - Choosing and understanding licenses for repositories

---

### **13. Personalization**
- **Profile Customization**
  - Adding a README to the profile
  - Showing pinned repositories
- **GitHub Sponsors**
  - Supporting open-source developers
  - Becoming a sponsor or sponsor-ee

---

### **14. Advanced Features**
- **Codespaces**
  - Cloud-based development environments
  - Configuring `.devcontainer.json`
- **Copilot**
  - AI-powered code suggestions
  - Using Copilot in IDEs
- **GraphQL API**
  - Fetching and managing data programmatically
- **GitHub Enterprise**
  - Enterprise-level features for organizations

---

### **15. Troubleshooting and Help**
- **Common Issues**
  - Merge conflicts in pull requests
  - Permission errors in repositories
- **Help Resources**
  - GitHub Docs
  - GitHub Community Discussions

---
