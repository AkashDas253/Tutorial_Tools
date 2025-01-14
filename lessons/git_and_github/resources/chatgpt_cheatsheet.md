# GitHub Cheat Sheet

## Getting Started

- **Git Installation**
  - Install Git: `https://git-scm.com/`
  - Configure username: `git config --global user.name "Your Name"`
  - Configure email: `git config --global user.email "you@example.com"`

- **Create a Repository**
  - Initialize a repository: `git init`
  - Clone a repository: `git clone <url>`

- **Basic Commands**
  - Check the status: `git status`
  - Stage changes: `git add <file>` or `git add .` for all files
  - Commit changes: `git commit -m "commit message"`
  - Push changes: `git push origin <branch-name>`
  - Pull updates: `git pull origin <branch-name>`

---

## Branching and Merging

- **Branching**
  - Create a new branch: `git branch <branch-name>`
  - Switch to a branch: `git checkout <branch-name>`
  - Create and switch to a new branch: `git checkout -b <branch-name>`
  - List branches: `git branch`

- **Merging**
  - Merge a branch into the current branch: `git merge <branch-name>`
  - Resolve merge conflicts: 
    - Edit conflicted files manually.
    - Add files with `git add <file>`
    - Commit with `git commit`

---

## Collaborating

- **Forking**
  - Fork a repository via GitHub UI.
  - Clone the forked repository: `git clone <url-of-fork>`

- **Pull Requests**
  - Create a pull request from a branch via GitHub UI.
  - Review and merge pull requests via GitHub UI.

- **Issues**
  - Create a new issue via GitHub UI.
  - Reference issues in commits: `git commit -m "Fixes #<issue-number>"`

---

## GitHub Flow

- **GitHub Flow Basics**
  - Create a branch: `git checkout -b <branch-name>`
  - Make changes and commit: `git commit -m "message"`
  - Push the branch: `git push origin <branch-name>`
  - Open a pull request via GitHub UI.
  - Get feedback and merge pull request.

---

## Undoing Changes

- **Undo Unstaged Changes**
  - Undo changes in a file: `git checkout -- <file>`

- **Undo Staged Changes**
  - Unstage a file: `git reset <file>`

- **Amending Commits**
  - Amend the last commit: `git commit --amend -m "new message"`

- **Reverting Commits**
  - Revert a commit: `git revert <commit-hash>`

---

## Working with Remotes

- **Remote Commands**
  - Add a remote: `git remote add <name> <url>`
  - Remove a remote: `git remote remove <name>`
  - View remotes: `git remote -v`

- **Syncing**
  - Fetch from the remote: `git fetch`
  - Rebase on top of a branch: `git rebase <branch-name>`

---

## Advanced Git Commands

- **Stashing**
  - Save changes without committing: `git stash`
  - Apply stash: `git stash apply`
  - View stash list: `git stash list`

- **Cherry-picking**
  - Apply a specific commit from another branch: `git cherry-pick <commit-hash>`

- **Squashing Commits**
  - Squash commits interactively: `git rebase -i HEAD~<number-of-commits>`

---

## GitHub Actions

- **Basic Setup**
  - Create a workflow file under `.github/workflows/`
  - Example of workflow file:
    ```yaml
    name: CI Pipeline

    on: [push]

    jobs:
      build:
        runs-on: ubuntu-latest
        steps:
        - name: Checkout
          uses: actions/checkout@v2

        - name: Run Tests
          run: make test
    ```

---

## GitHub Pages

- **Hosting with GitHub Pages**
  - Create a branch named `gh-pages` or use GitHub UI to enable Pages.
  - Push HTML or static files to `gh-pages` branch.

---

## Working with GitHub API (Octokit)

- **Authenticating with Octokit**
  - Install Octokit: `npm install @octokit/rest`
  - Basic example:
    ```javascript
    const { Octokit } = require("@octokit/rest");
    const octokit = new Octokit({ auth: `token YOUR_TOKEN` });

    octokit.repos.listForAuthenticatedUser()
      .then(({ data }) => console.log(data));
    ```

- **Common API Commands**
  - List repository issues:
    ```javascript
    octokit.issues.listForRepo({
      owner: 'owner',
      repo: 'repo-name'
    });
    ```

---

## GitHub CLI

- **Basic Commands**
  - Clone a repository: `gh repo clone <url>`
  - Create a new issue: `gh issue create`
  - View issues: `gh issue list`
  - Create a pull request: `gh pr create`

---

## Tips and Best Practices

- **Commit Messages**
  - Use present tense: "Fix bug" instead of "Fixed bug".
  - Keep messages concise and descriptive.
  - Use issue numbers in commit messages to track progress.

- **Branch Naming**
  - Use clear, descriptive names: `feature/add-login`, `bugfix/fix-ui`

- **Pull Request Etiquette**
  - Write a clear description of changes.
  - Ensure all tests pass before submitting.
  - Request reviews from collaborators.
 