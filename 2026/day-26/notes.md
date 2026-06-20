# Day 26 – GitHub CLI (gh)

## Objective

Learn how to manage GitHub repositories, issues, pull requests, and workflows directly from the terminal using GitHub CLI (`gh`).

---

# Task 1: Install and Authenticate

## Install GitHub CLI

Ubuntu:

```bash
sudo apt update
sudo apt install gh -y
```

Verify installation:

```bash
gh --version
```

Login to GitHub:

```bash
gh auth login
```

Verify active account:

```bash
gh auth status
```

### Authentication Methods Supported

* GitHub Web Browser Authentication
* Personal Access Token (PAT)
* SSH Authentication
* HTTPS Authentication

### Observation

GitHub CLI allows authentication without manually configuring Git credentials every time.

---

# Task 2: Working with Repositories

## Create Repository

```bash
gh repo create gh-demo-repo --public --clone --add-readme
```

### Observation

A new GitHub repository can be created directly from the terminal.

---

## Clone Repository

```bash
gh repo clone owner/repository-name
```

### Observation

Repository cloned without using `git clone`.

---

## View Repository Details

```bash
gh repo view
```

### Observation

Displays repository information including description, visibility, and URL.

---

## List All Repositories

```bash
gh repo list
```

### Observation

Displays repositories associated with the authenticated account.

---

## Open Repository in Browser

```bash
gh repo view --web
```

### Observation

Opens repository directly in the default browser.

---

## Delete Repository

```bash
gh repo delete gh-demo-repo
```

### Observation

Repository can be permanently removed from the terminal.

---

# Task 3: Issues

## Create Issue

```bash
gh issue create \
--title "Demo Issue" \
--body "Testing GitHub CLI issue creation" \
--label bug
```

### Observation

Issue created without visiting GitHub UI.

---

## List Issues

```bash
gh issue list
```

### Observation

Displays all open issues.

---

## View Issue

```bash
gh issue view 1
```

### Observation

Shows issue details, comments, and status.

---

## Close Issue

```bash
gh issue close 1
```

### Observation

Issue status changes to closed directly from terminal.

---

## How gh issue Can Be Used in Automation

* Auto-create issues when monitoring detects failures.
* Create incident tickets automatically.
* Generate bug reports from scripts.
* Integrate alerts with GitHub Issues.

---

# Task 4: Pull Requests

## Create Branch

```bash
git checkout -b feature-update
```

---

## Commit Changes

```bash
git add .
git commit -m "Added new update"
```

---

## Push Branch

```bash
git push origin feature-update
```

---

## Create Pull Request

```bash
gh pr create \
--title "Feature Update" \
--body "Adding latest changes"
```

### Observation

PR created completely from terminal.

---

## List Pull Requests

```bash
gh pr list
```

### Observation

Displays open pull requests.

---

## View Pull Request

```bash
gh pr view
```

### Observation

Shows reviewers, checks, commits, and PR status.

---

## Merge Pull Request

```bash
gh pr merge
```

### Observation

PR merged without opening GitHub UI.

---

## Supported Merge Methods

```bash
gh pr merge --merge
gh pr merge --squash
gh pr merge --rebase
```

### Merge Types

* Merge Commit
* Squash Merge
* Rebase Merge

---

## Reviewing Someone Else's PR

```bash
gh pr checkout <pr-number>
```

Review changes:

```bash
gh pr diff <pr-number>
```

Approve:

```bash
gh pr review <pr-number> --approve
```

Request changes:

```bash
gh pr review <pr-number> --request-changes
```

---

# Task 5: GitHub Actions & Workflows

## List Workflow Runs

```bash
gh run list
```

### Observation

Displays workflow execution history.

---

## View Workflow Run Details

```bash
gh run view <run-id>
```

### Observation

Shows workflow status and execution logs.

---

## How gh run and gh workflow Help CI/CD

* Trigger workflows remotely.
* Monitor build pipelines.
* Check deployment status.
* Download workflow logs.
* Automate release processes.

---

# Task 6: Useful GitHub CLI Commands

## GitHub API

```bash
gh api user
```

Purpose:

Access GitHub API directly from terminal.

---

## Gist Management

```bash
gh gist create notes.txt
```

Purpose:

Create and manage GitHub Gists.

---

## Release Management

```bash
gh release create v1.0
```

Purpose:

Create software releases.

---

## Aliases

```bash
gh alias set prs "pr list"
```

Purpose:

Create shortcuts for frequently used commands.

---

## Search Repositories

```bash
gh search repos devops
```

Purpose:

Search GitHub repositories from terminal.

---

# Useful Commands for git-commands.md

```bash
gh auth login
gh auth status

gh repo create
gh repo clone
gh repo list
gh repo view
gh repo delete

gh issue create
gh issue list
gh issue view
gh issue close

gh pr create
gh pr list
gh pr view
gh pr merge
gh pr checkout
gh pr review

gh run list
gh run view

gh api
gh gist
gh release
gh alias
gh search repos
```

---

# What I Learned

1. GitHub repositories can be managed entirely from the terminal.
2. Pull Requests and Issues can be created and reviewed without opening a browser.
3. GitHub CLI is useful for automation, scripting, and CI/CD workflows.
4. Workflow runs and repository operations can be monitored directly from the command line.
5. GitHub CLI saves time and improves productivity for DevOps engineers.

