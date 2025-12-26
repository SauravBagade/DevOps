# Git & GitHub Complete Documentation

# 📘 Source Code Management (SCM)

## 🔹 What is Source Code Management?

**Source Code Management (SCM)** is used to manage, track, and control changes in source code during software development.

---

## 🔹 Types of Source Code Management

There are **two main types**:

### 1️⃣ CVCS — Centralized Version Control System

### 2️⃣ DVCS — Distributed Version Control System

---

## 🟦 CVCS — Centralized Version Control System

### 🔹 How it works

* There is **one central repository (server)**
* All developers connect to this server
* Code checkout, commit, and update happen from the central server

### 🔹 Architecture

* **Repository (Server)**
* Multiple **Working Copies** on developer machines

### 🔹 Flow

* Checkout → Modify → Commit → Update

### 🔹 Disadvantage

* **Single point of failure**
* If server is down → no commits possible

### 🔹 Examples

* SVN
* CVS
* Perforce

---

## 🟩 DVCS — Distributed Version Control System

### 🔹 How it works

* Every developer has a **full repository copy**
* Repository exists on **local machine + remote server**
* Developers can work **offline**

### 🔹 Architecture

* Central repository (optional)
* Multiple local repositories
* Push & pull between repositories

### 🔹 Flow

* Commit locally → Push to remote
* Pull updates from remote

### 🔹 Advantages

* No single point of failure
* Faster operations
* Offline commits supported

### 🔹 Examples

* Git
* Mercurial

---

## 🔄 CVCS vs DVCS (Comparison)

| Feature       | CVCS         | DVCS           |
| ------------- | ------------ | -------------- |
| Repository    | Central only | Local + Remote |
| Offline work  | ❌ No         | ✅ Yes          |
| Speed         | Medium       | Fast           |
| Failure risk  | High         | Low            |
| Popular today | Low          | Very High      |

---
## 🚀 What is Git?
Git is a distributed version control system that helps developers track changes in source code during software development.

Imagine you're writing code or working on a project. Over time, you make changes — some good, some maybe not. Git allows you to:
- ✅ Track every change made to your files
- ⏪ Go back to previous versions if something breaks
- 🤝 Work with teammates without overwriting each other’s work

## ⚡ Key Features of Git

| Feature                | Description                                                               |
| ---------------------- | ------------------------------------------------------------------------- |
| ✅ Version Tracking    | Keeps history of file changes and who made them                         |
| 🤝 Collaboration       | Lets multiple people work on the same project at the same time          |
| 🔁 Branching & Merging | Work on features separately without affecting main code               |
| 💻 Distributed         | Every developer has a full copy of the project                         |
| ⏪ Undo/Restore        | Roll back to previous states of the project easily                     |

## 🌐 Real-World Use Case
Suppose you're developing a website.  
- You make a mistake while changing a file → Git lets you undo it.  
- Your friend wants to add a new feature → She can work in a separate branch.  
- Later, both of you can merge changes safely.

## 📊 Git Workflow Diagram

```

+----------------+
\|  Working Dir   | git init
+----------------+
|
v
git add \<file(s)>
|
v
+----------------+
\|  Staging Area  |
+----------------+
|
v
git commit -m "message"
|
v
+----------------+
\|   Local Repo   |
+----------------+
|
v
git push origin main
|
v
+----------------+
\|  Remote Repo   |
+----------------+

````

### Git Three-Stage Architecture Diagram

````
+-------------------+        git add        +-------------------+       git commit
|                   |  ----------------->  |                   |  ----------------->
|  Working Directory|                      |   Staging Area     |                  |
|  (Edit files)     |  <-----------------  |   (Index)          |  <----------------
|                   |     git restore      |                   |     git checkout
+-------------------+                      +-------------------+                  |
                                                                                  |
                                                                                  v
                                                                          +-------------------+
                                                                          |                   |
                                                                          |   Git Repository  |
                                                                          |   (.git folder)   |
                                                                          |                   |
                                                                          +-------------------+


````

## 📚 Git Command Flow

| Stage             | Action                         | Git Command                           |
| ----------------- | ------------------------------ | ------------------------------------- |
| Edit files        | Make changes                   | Manual                              |
| Stage files       | Add to staging area            | `git add .` or `git add filename`   |
| Commit changes    | Save snapshot locally          | `git commit -m "message"`            |
| Push changes      | Upload to GitHub               | `git push origin main`               |

## 🌐 What is GitHub?
GitHub is a web-based platform hosting Git repositories online.  
It makes collaboration easier by:
- Hosting repositories in the cloud
- Visual interface & cloud storage
- Issue tracking, code review with PRs

## ⚔️ Git vs GitHub

| Git                      | GitHub                                |
| ------------------------ | ------------------------------------- |
| Local tool (installed)   | Online platform (github.com)         |
| Tracks local file changes| Hosts Git repositories in the cloud |
| CLI or GUI usage         | Browser + Git commands               |
| No account needed        | Requires GitHub account              |

---
## 📊 Git & GitHub Commands – Table Format

### 🔹 Basic Git Commands

| Command                       | Description                         |
| ----------------------------- | ----------------------------------- |
| `git init`                    | Initialize a new Git repository     |
| `git clone <repo-url>`        | Clone a repository from GitHub      |
| `git remote`                  | Show remote repositories            |
| `git remote add origin <url>` | Connect local repo to GitHub        |
| `git status`                  | Check current repository status     |
| `git show <commit-id>`        | Show details of a specific commit   |
| `git add .`                   | Add all files to staging area       |
| `git commit -m "message"`     | Commit staged changes               |
| `git push`                    | Push commits to remote repository   |
| `git pull`                    | Fetch and merge changes from remote |
| `git fetch origin`            | Fetch changes without merging       |

---

### logs

| Command                   | Use                    |
| ------------------------- | ---------------------- |
| `git log --oneline`       | Short commit log       |
| `git log --graph`         | Visual branch graph    |
| `git log --author="name"` | Filter by author       |
| `git blame <file>`        | Who changed which line |


---

### 🔹 Branching & Merging

| Command                      | Description                            |
| ---------------------------- | -------------------------------------- |
| `git branch`                 | List all branches                      |
| `git branch <name>`          | Create a new branch                    |
| `git branch -m <new-name>`   | Rename a branch                        |
| `git checkout <branch>`      | Switch to another branch               |
| `git merge <branch>`         | Merge branch into current branch       |
| `git merge --no-ff <branch>` | No fast-forward merge (creates commit) |

---

### 🔹 Undo & Recovery

| Command                        | Description                               |
| ------------------------------ | ----------------------------------------- |
| `git restore <file>`           | Restore file to last committed state      |
| `git reset --hard <commit-id>` | Reset code and history (dangerous)        |
| `git revert <commit-id>`       | Safely undo a commit                      |
| `git reflog`                   | Recover lost commits                      |
| `git cherry-pick <commit-id>`  | Apply specific commit from another branch |

---

### 🔹 Git Diff

| Command             | Description           |
| ------------------- | --------------------- |
| `git diff`          | Show unstaged changes |
| `git diff --cached` | Show staged changes   |

---

### 🔹 Git Stash

| Command           | Description              |
| ----------------- | ------------------------ |
| `git stash`       | Save uncommitted changes |
| `git stash list`  | List all stashes         |
| `git stash apply` | Apply last stash         |
| `git stash pop`   | Apply and delete stash   |
| `git stash drop`  | Delete a stash           |

---

### 🔹 Advanced Git

| Command                    | Description                       |
| -------------------------- | --------------------------------- |
| `git rebase <branch>`      | Reapply commits on another branch |
| `git bisect`               | Find bug-causing commit           |
| `git tag -a v1.0 -m "msg"` | Create annotated tag              |
| `git hooks`                | Automated scripts on Git events   |
| `git clean -n`             | Preview untracked file removal    |
| `git clean -f`             | Remove untracked files            |

---

### 🔹 Git Configuration

| Command                                  | Description            |
| ---------------------------------------- | ---------------------- |
| `git config --global user.name "Name"`   | Set username           |
| `git config --global user.email "email"` | Set email              |
| `git config --list`                      | View Git configuration |

---

## 👥 GitHub Workflow Diagram (Team Collaboration)

```
+---------------------+
| GitHub Repository   |
+----------+----------+
           ^
           |
    git push / pull
           |
+----------+----------+
|                     |
| Developer A         | Developer B
+----------+----------+----------------+
      |                     |
      v                     v
Create Feature Branch   Create Feature Branch
      |                     |
      v                     v
Commit & Push          Commit & Push
      |                     |
      v                     v
    Pull Request → Review PR
      |                     |
      v                     v
 Merge to `main` ← Approve & Merge
```

## 🧱 GitHub Team Flow (Steps Summary)

| Step                     | Description                           |
| ------------------------ | ------------------------------------- |
| Fork or Clone            | Developers copy the repo              |
| Create a Branch          | Work on feature/login branch          |
| Commit and Push          | Push changes                          |
| Create Pull Request (PR) | Propose changes for review            |
| Review & Merge           | Merge into main branch after approval |

---

## 🏗 Example Repository Structure

```
project-name/
│
├── README.md               # Project overview
├── .gitignore              # Files to ignore
├── requirements.txt        # Dependencies
├── LICENSE                 # License file
│
├── src/                    # Source code
│   ├── main.py
│   └── helpers.py
│
├── tests/                  # Unit tests
│   └── test_main.py
│
├── docs/                   # Documentation
│   └── setup-guide.md
│
└── .github/                # GitHub config
    └── workflows/
        └── ci.yml          # CI/CD configuration
```

---

## 🧠 Fork & PR Flow Summary

| Step                 | Command/Action                                                 |
| -------------------- | -------------------------------------------------------------- |
| Fork repo            | GitHub → Fork button                                           |
| Clone fork           | `git clone https://github.com/your-username/repo.git`          |
| Add upstream         | `git remote add upstream https://github.com/original/repo.git` |
| Create branch        | `git checkout -b feature-branch`                               |
| Make & commit        | `git add .` → `git commit -m "Message"`                        |
| Push branch          | `git push origin feature-branch`                               |
| Create PR            | GitHub → Open PR                                               |
| Sync fork (optional) | `git pull upstream main` → `git push origin main`              |
