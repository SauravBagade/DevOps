# Git & GitHub Full Documentation

## 🚀 Git Basics - List of All Commands
Below is a **complete Git command list** you asked for — **table format + clear use-cases**, beginner → advanced level.
Direct, practical, **no sugarcoating** (as you prefer).

---

## ✅ Complete List of Git Commands (with Use Cases)

| Command             | Syntax                                                 | Use Case / Purpose                             |
| ------------------- | ------------------------------------------------------ | ---------------------------------------------- |
| **git init**        | `git init`                                             | Initialize a new Git repository in a directory |
| **git clone**       | `git clone <repo-url>`                                 | Copy a remote repository to local machine      |
| **git status**      | `git status`                                           | Show working directory & staging status        |
| **git add**         | `git add <file>`<br>`git add .`                        | Add files to staging area                      |
| **git commit**      | `git commit -m "msg"`                                  | Save staged changes to local repo              |
| **git log**         | `git log`                                              | View commit history                            |
| **git show**        | `git show <commit-id>`                                 | Show details of a specific commit              |
| **git push**        | `git push origin main`                                 | Upload local commits to remote                 |
| **git pull**        | `git pull origin main`                                 | Fetch + merge remote changes                   |
| **git fetch**       | `git fetch origin`                                     | Download remote changes (no merge)             |
| **git branch**      | `git branch`<br>`git branch dev`                       | List or create branches                        |
| **git checkout**    | `git checkout dev`                                     | Switch branches                                |
| **git checkout -b** | `git checkout -b dev`                                  | Create & switch to new branch                  |
| **git merge**       | `git merge dev`                                        | Merge another branch into current              |
| **git rebase**      | `git rebase main`                                      | Reapply commits on another base                |
| **git reset**       | `git reset --soft HEAD~1`<br>`git reset --hard HEAD~1` | Undo commits (soft/mixed/hard)                 |
| **git revert**      | `git revert <commit-id>`                               | Undo commit safely (new commit)                |
| **git restore**     | `git restore <file>`                                   | Discard file changes                           |
| **git rm**          | `git rm <file>`                                        | Delete file from repo + working tree           |
| **git diff**        | `git diff`                                             | Show code changes                              |
| **git stash**       | `git stash`<br>`git stash pop`<br>`git stash list`<br>`git stash apply`<br>`git stash drop`                         | Temporarily save work                          |
| **git clean**       | `git clean -f`                                         | Remove untracked files                         |
| **git tag**         | `git tag v1.0`                                         | Create version tags                            |
| **git remote**      | `git remote -v`                                        | View remote repositories                       |
| **git remote add**  | `git remote add origin <url>`                          | Add remote repo                                |
| **git cherry-pick** | `git cherry-pick <commit-id>`                          | Apply specific commit to branch                |
| **git bisect**      | `git bisect start`                                     | Find bug using binary search                   |
| **git reflog**      | `git reflog`                                           | Recover lost commits                           |
| **git hooks**       | `.git/hooks/`                                          | Run scripts before/after Git actions           |
| **git config**      | `git config --global user.name`                        | Set Git configuration                          |
| **.gitignore**      | `.gitignore` file                                      | Ignore files from tracking                     |

---

## 🔥 Important Reset Types (Very Important)

| Reset Type | Command                    | Effect                             |
| ---------- | -------------------------- | ---------------------------------- |
| Soft       | `git reset --soft HEAD~1`  | Undo commit, keep changes staged   |
| Mixed      | `git reset --mixed HEAD~1` | Undo commit, keep changes unstaged |
| Hard       | `git reset --hard HEAD~1`  | **Delete commit + code (danger)**  |

---

## 🔁 Reset vs Revert (Interview Favorite)

| Feature | reset           | revert           |
| ------- | --------------- | ---------------- |
| History | Changes history | Keeps history    |
| Safety  | ❌ Dangerous     | ✅ Safe           |
| Use     | Local mistakes  | Production fixes |

---

## 🧠 Advanced Commands (DevOps Reality)

| Command           | Why Used                |
| ----------------- | ----------------------- |
| `git cherry-pick` | Move specific fixes     |
| `git rebase`      | Clean commit history    |
| `git bisect`      | Find breaking commit    |
| `git reflog`      | Recover deleted commits |
| `git hooks`       | CI/CD automation        |

---

## 📌 Real-World Workflow (Daily Use)

```bash
git status
git add .
git commit -m "feature added"
git pull origin main
git push origin main
```
------------------------------------------------------------------------

## 🧱 Git Basics: Step-by-Step Guide

### 1. Initialize a Repository

``` bash
git init
```

### 2. Clone a Repository from GitHub

``` bash
git clone https://github.com/username/repo.git
```

### 3. Connect Local Repo to GitHub

``` bash
git remote add origin https://github.com/username/repo.git
git remote -v
```

### 4. Check Status

``` bash
git status
```

### 5. Stage Files

``` bash
git add .
```

### 6. Commit Changes

``` bash
git commit -m "Your commit message"
```

### 7. View Commit History

``` bash
git log
```

### 8. Show Commit Details

``` bash
git show <commit-id>
```

### 9. Push Code

``` bash
git push origin main
```

### 10. Pull Changes

``` bash
git pull origin main
```

### 11. Fetch Only

``` bash
git fetch origin
```

### Branching & Merging

``` bash
git branch                    # List all branches
git branch dev                # Create new branch 'dev'
git branch -m main new-main   # Rename main to new-mai
git checkout dev
git merge dev
```

### Managing Files

``` bash
git rm filename
git restore filename
git diff               # View unstaged changes
git diff --cached      # View staged changes
```

### Stashing

```bash
git stash            # Save current changes
git stash list       # Show all stashed entries
git stash apply      # Reapply the last stash
git stash pop        # Reapply and delete the stash
git stash drop       # Delete a specific stash
```

### Rebase

``` bash
git rebase main
```

### Tagging

``` bash
git tag              # List tags
git tag -a v1.0 -m "First release"
git push origin v1.0
```

### Clean

``` bash
git clean -n     # Preview what will be deleted
git clean -f     # Force delete untracked files
```

### .gitignore Example

    node_modules/
    .env
    *.log

## ✅ Recommended Workflow

``` bash
git init                          # Step 1
git remote add origin <url>       # Connect to GitHub
git add .                         # Stage changes
git commit -m "Initial commit"    # Commit changes
git push -u origin main           # Push to GitHub

# Daily work cycle

git pull origin main              # Sync with remote
git add .                         # Stage work
git commit -m "Work updates"
git push origin main              # Push updates
```

------------------------------------------------------------------------

## 💻 Install Git on Ubuntu

``` bash
sudo apt update
sudo apt install git
git --version
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --list
```

--------------------------------------------------------------------------
# Git + GitHub Full Workflow (Ubuntu to GitHub)

## Step 1: Install Git on Ubuntu

```bash
sudo apt update
sudo apt install git
````

## Step 2: Verify Git Installation

```bash
git --version
```

## Step 3: Configure Git (One-Time Setup)

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Check your configuration:

```bash
git config --list
```

## Step 4: Create a GitHub Account (Skip if already done)

* Go to [https://github.com](https://github.com)
* Click **Sign Up**
* Create your account

## Step 5: Create a New Repository on GitHub

1. Click the **+** icon in the top-right → "New repository"
2. Enter:

   * Repository name
   * Description (optional)
   * Choose **Public** or **Private**
3. Click **Create repository**

## Step 6: Create Project Locally

```bash
mkdir my-project
cd my-project
```

Add a file (example):

```bash
echo "# My Project" > README.md
```

## Step 7: Initialize Git Repository

```bash
git init
```

## Step 8: Add Files to Staging Area

```bash
git add .
```

Check status:

```bash
git status
```

## Step 9: Commit Changes

```bash
git commit -m "Initial commit"
```

## Step 10: Connect to GitHub (Remote Repo)

### Option A: HTTPS

Copy HTTPS link from GitHub (example):

```
https://github.com/username/my-project.git
```

```bash
git remote add origin https://github.com/username/my-project.git
```

### Option B: SSH

Copy SSH link (example):

```
git@github.com:username/my-project.git
```

```bash
git remote add origin git@github.com:username/my-project.git
```

Use SSH if you’ve already added your SSH key to GitHub.

## Step 11: Push to GitHub

For first push:

```bash
git push -u origin main
```

Use `main`, or `master` if your default branch is named that.

## Step 12: Confirm on GitHub

* Go to your repo page on GitHub
* You’ll see your files and commit!

## Summary of Commands

```bash
sudo apt update
sudo apt install git
git --version
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git init
git add .
git commit -m "Initial commit"
git remote add origin <URL>
git push -u origin main
```

-------------------------------------------------------------------
# 🔄 Forking & Pull Request — Step-by-Step Guide

---

## Part 1: Fork a Repository on GitHub

1. **Go to the original repository** (e.g., [https://github.com/original-author/project](https://github.com/original-author/project))
2. Click the **Fork** button (top-right corner)
3. GitHub will copy that repo to **your GitHub account**  
   → Now you own:  
   `https://github.com/your-username/project`

---

## Part 2: Clone Your Fork Locally

Open your terminal and run:

```bash
git clone https://github.com/your-username/project.git
cd project
````

OR (if using SSH):

```bash
git clone git@github.com:your-username/project.git
```

---

## Part 3: Add Original Repo as Upstream (to keep your fork updated)

```bash
git remote add upstream https://github.com/original-author/project.git
```

Check remotes:

```bash
git remote -v
```

You’ll see:

```
origin    https://github.com/your-username/project.git
upstream  https://github.com/original-author/project.git
```

---

## Part 4: Create a New Branch for Your Work

Always create a separate branch for your fixes or features:

```bash
git checkout -b my-feature-branch
```

---

## Part 5: Make Changes and Commit

Make code changes → Save → Then:

```bash
git add .
git commit -m "Add feature or fix issue"
```

---

## Part 6: Push Branch to Your Fork

```bash
git push origin my-feature-branch
```

---

## Part 7: Create a Pull Request (PR)

1. Go to your repo on GitHub:
   `https://github.com/your-username/project`
2. You’ll see a message: **“Compare & pull request”**
3. Click it
4. Fill out:

   * **PR title** (e.g., "Fix issue #12")
   * **Description of changes**
5. Click **Create pull request**

---

## Part 8: PR Review & Merge (by repo owner)

* The original repo’s maintainers will:

  * Review your code
  * Suggest changes (if needed)
  * Approve and **merge** it

🔁 You may need to **update your PR** if changes are requested.

---

## 🔄 Optional: Keep Your Fork Updated with Upstream

If the original repo has new changes:

```bash
git checkout main
git pull upstream main
git push origin main
```
