# 1️⃣ Introduction to GitHub Actions

## 🔷 What is GitHub Actions?

![Image](https://user-images.githubusercontent.com/55514721/101413954-1007d580-389a-11eb-8b15-4f2a45ad9ddb.png)

![Image](https://images.openai.com/static-rsc-3/1JssT43dRnj6AmZc9EbXImzBQaSLk1WhEXVOojNss6t_YgTlxYCTq3I6Db7m8irYraKbjg60ChYTiVETgOUyVSEeJcorUjJVvTpLWL4BD6Q?purpose=fullsize\&v=1)

![Image](https://images.ctfassets.net/8aevphvgewt8/5kVxaacutdvGyusbgk64iw/23fa8c76260945d6a8f28327e9910397/actions-river-breakout.webp)

![Image](https://docs.github.com/assets/cb-95207/images/help/repository/actions-quickstart-logs.png)

**GitHub Actions** is a built-in CI/CD and automation platform inside **GitHub** that allows you to:

* ✅ Build code automatically
* ✅ Run tests on every push
* ✅ Deploy applications
* ✅ Automate workflows
* ✅ Integrate with cloud providers

It helps you automate the **software development lifecycle (SDLC)** directly inside your repository.

---

## 🔷 Simple Definition

> GitHub Actions = **Event-based automation system for CI/CD inside GitHub**

When something happens in your repo (push, PR, release), GitHub Actions runs automated tasks.

---

# 1.1 Why GitHub Actions is Used

### 🔹 1. Continuous Integration (CI)

* Automatically build & test code on every commit.
* Prevent broken code from reaching production.

### 🔹 2. Continuous Deployment (CD)

* Automatically deploy to:

  * AWS
  * Azure
  * GCP
  * Kubernetes
  * Docker Hub

### 🔹 3. Automation

* Auto label issues
* Auto close stale PRs
* Schedule tasks using CRON
* Send notifications

---

# 1.2 CI vs CD vs CI/CD

| Term  | Meaning                | Purpose                    |
| ----- | ---------------------- | -------------------------- |
| CI    | Continuous Integration | Automatically build & test |
| CD    | Continuous Deployment  | Automatically deploy       |
| CI/CD | Combined process       | Fully automated pipeline   |

---

# 1.3 How GitHub Actions Works (Architecture)

## 🧠 Core Components

1. **Workflow** – YAML file inside `.github/workflows/`
2. **Event** – Trigger (push, pull_request, schedule)
3. **Job** – Set of tasks
4. **Step** – Individual command
5. **Runner** – Machine that executes the job
6. **Action** – Reusable automation unit

---

## 🔁 Flow Diagram (Conceptual)

```
Developer Push Code
        ↓
GitHub Event Triggered
        ↓
Workflow Starts
        ↓
Runner Assigned
        ↓
Jobs Execute
        ↓
Steps Run (Build → Test → Deploy)
        ↓
Success / Failure Report
```

---

# 1.4 GitHub Actions vs Jenkins

| Feature      | GitHub Actions | Jenkins      |
| ------------ | -------------- | ------------ |
| Setup        | Built-in       | Manual setup |
| Maintenance  | Low            | High         |
| Plugins      | Marketplace    | Thousands    |
| Scaling      | Automatic      | Manual       |
| Cloud Native | Yes            | Needs config |

> Jenkins is powerful but requires maintenance. GitHub Actions is simpler for modern DevOps.

---

# 1.5 GitHub Actions vs GitLab CI

| Feature           | GitHub Actions       | GitLab CI        |
| ----------------- | -------------------- | ---------------- |
| Platform          | GitHub               | GitLab           |
| YAML Location     | `.github/workflows/` | `.gitlab-ci.yml` |
| Marketplace       | Large                | Moderate         |
| Cloud Integration | Strong               | Strong           |

---

# 1.6 Real DevOps Use Cases

Since you're learning DevOps (Docker, Terraform, EKS), here’s how it fits your stack:

### 🔹 Docker CI

* Build Docker image
* Push to Docker Hub

### 🔹 Terraform Automation

* `terraform init`
* `terraform plan`
* `terraform apply`

### 🔹 Kubernetes Deployment

* Build image
* Push to registry
* Update deployment

### 🔹 EKS Deployment (Your Case)

* Authenticate via OIDC
* Apply Kubernetes manifests

---

# 1.7 Key Advantages

* 🚀 No separate CI server needed
* 🔐 Secure secrets management
* ⚡ Fast setup
* 🔄 Tight GitHub integration
* 🌍 Cloud-ready

---
# 2️⃣ Core Concepts of GitHub Actions (Detailed Guide)

## 🧩 Overview Diagram

![Image](https://docs.github.com/assets/cb-25535/images/help/actions/overview-actions-simple.png)

![Image](https://docs.github.com/assets/cb-497738/images/help/actions/arc-diagram.png)

![Image](https://i.imgur.com/CSW6eQq.png)

![Image](https://www.infracloud.io/assets/img/uploads/2020/09/githubconcept.png)

**GitHub Actions** works using a few core building blocks.
If you understand these properly, you can build any CI/CD pipeline (Docker, Terraform, EKS, etc.).

---

# 🔹 2.1 Workflow

A **workflow** is an automated process defined in a YAML file.

📁 Location:

```
.github/workflows/your-file.yml
```

Example:

```yaml
name: My CI Pipeline

on: push

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Hello DevOps"
```

👉 One repository can have multiple workflows.

---

# 🔹 2.2 Event

An **event** is what triggers the workflow.

Common Events:

| Event             | When It Runs           |
| ----------------- | ---------------------- |
| push              | Code pushed            |
| pull_request      | PR created/updated     |
| workflow_dispatch | Manual trigger         |
| schedule          | Cron-based             |
| release           | When release published |

Example:

```yaml
on:
  push:
    branches:
      - main
```

---

# 🔹 2.3 Job

A **job** is a group of steps that run on the same runner.

Example:

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
```

👉 Multiple jobs run in parallel by default.
👉 Use `needs:` to create dependency.

Example:

```yaml
jobs:
  build:
    runs-on: ubuntu-latest

  deploy:
    needs: build
    runs-on: ubuntu-latest
```

---

# 🔹 2.4 Step

A **step** is a single task inside a job.

Example:

```yaml
steps:
  - run: echo "Build Started"
  - run: npm install
```

Each step:

* Runs sequentially
* Shares the same workspace

---

# 🔹 2.5 Runner

A **runner** is a machine that executes your workflow.

Types:

| Type          | Description       |
| ------------- | ----------------- |
| GitHub Hosted | Managed by GitHub |
| Self-hosted   | Your own server   |

Example:

```yaml
runs-on: ubuntu-latest
```

Supported OS:

* Ubuntu
* Windows
* macOS

---

# 🔹 2.6 Action

An **action** is a reusable automation unit.

Example:

```yaml
- uses: actions/checkout@v4
```

Here:

* `actions/checkout` = action name
* `@v4` = version

Marketplace: Thousands of prebuilt actions available.

---

# 🔹 2.7 Marketplace

You can search reusable actions in the GitHub Marketplace inside **GitHub**.

Examples:

* Checkout code
* Setup Node.js
* Setup Python
* Docker login
* AWS authentication

---

# 🔹 2.8 Artifacts

Artifacts store build output between jobs.

Example:

```yaml
- uses: actions/upload-artifact@v4
  with:
    name: build-files
    path: dist/
```

Use case:

* Store test reports
* Store build packages
* Share data between jobs

---

# 🔹 2.9 Secrets

Secrets store sensitive data securely.

Examples:

* AWS keys
* Docker Hub password
* API tokens

Access in workflow:

```yaml
env:
  AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
```

Never hardcode credentials.

---

# 🔹 2.10 Environment Variables

Define variables globally or per job.

Example:

```yaml
env:
  APP_ENV: production
```

Or per step:

```yaml
- run: echo "Deploying to $APP_ENV"
```

---

# 🔹 2.11 Matrix Strategy

Matrix allows testing multiple combinations.

Example:

```yaml
strategy:
  matrix:
    node-version: [16, 18, 20]
```

This will run job 3 times (parallel).

Use case:

* Multi-version testing
* Multi-OS testing

---

# 🔥 How All Concepts Work Together

Example Flow:

1. Developer pushes code
2. Event triggers workflow
3. Workflow starts
4. Runner assigned
5. Job executes
6. Steps run
7. Action used
8. Artifacts stored
9. Deployment completed

---

# 🏁 Real DevOps Example (Your Case – Docker + Terraform + EKS)

Since you're learning:

* Docker image build → Action
* Push to Docker Hub → Secret
* Terraform apply → Job
* Deploy to EKS → Separate Job
* Matrix for multi-env (dev/stage/prod)

---
# 3️⃣ Workflow File Structure (Deep YAML Explanation)

## 📁 Where Workflow Files Live

![Image](https://user-images.githubusercontent.com/8356977/154872065-f381868c-d489-4548-93f3-b9bfc1cc0127.jpg)

![Image](https://i.sstatic.net/fkLD3.png)

![Image](https://dz2cdn1.dzone.com/storage/temp/13365213-workflow.png)

![Image](https://user-images.githubusercontent.com/1248896/189254453-439dd558-fc6c-4377-b01c-d5e54cc49403.png)

In **GitHub**, all workflow files must be placed inside:

```
.github/workflows/
```

Example:

```
my-project/
 ├── src/
 ├── package.json
 └── .github/
      └── workflows/
           └── ci.yml
```

If the file is not inside this folder → **GitHub Actions will not detect it**.

---

# 🔹 3.1 Basic Workflow Structure

Every workflow file is written in **YAML** format.

Minimum structure:

```yaml
name: CI Pipeline

on: push

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Hello World"
```

---

# 🔹 3.2 Full Workflow Syntax (Production Style)

```yaml
name: Node CI Pipeline

on:
  push:
    branches:
      - main
  pull_request:

env:
  APP_ENV: production

jobs:
  build:
    runs-on: ubuntu-latest
    
    strategy:
      matrix:
        node-version: [18, 20]

    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node-version }}

      - name: Install Dependencies
        run: npm install

      - name: Run Tests
        run: npm test
```

Now let’s break down each keyword.

---

# 🔹 3.3 `name:`

Defines workflow name shown in Actions tab.

```yaml
name: Docker Build Pipeline
```

This appears inside the **Actions tab** of your repository.

---

# 🔹 3.4 `on:` (Trigger Section)

Defines when workflow runs.

### Single Event

```yaml
on: push
```

### Multiple Events

```yaml
on:
  push:
    branches:
      - main
  pull_request:
  workflow_dispatch:
```

### Schedule (CRON)

```yaml
on:
  schedule:
    - cron: "0 0 * * *"
```

---

# 🔹 3.5 `jobs:`

Contains all jobs.

```yaml
jobs:
  build:
  test:
  deploy:
```

Each job:

* Runs on separate runner
* Runs in parallel (unless dependency set)

---

# 🔹 3.6 `runs-on:`

Defines runner OS.

```yaml
runs-on: ubuntu-latest
```

Options:

* ubuntu-latest
* windows-latest
* macos-latest
* self-hosted

---

# 🔹 3.7 `steps:`

Steps run sequentially inside job.

```yaml
steps:
  - name: Step 1
    run: echo "Hello"
```

---

# 🔹 3.8 `uses:` (Using an Action)

Used to call reusable action.

```yaml
- uses: actions/checkout@v4
```

This action:

* Clones repository into runner

Common Actions:

* checkout
* setup-node
* setup-python
* upload-artifact

---

# 🔹 3.9 `run:` (Execute Command)

Executes shell command.

```yaml
- run: npm install
```

Multiple commands:

```yaml
- run: |
    npm install
    npm run build
```

---

# 🔹 3.10 `with:` (Passing Inputs)

Pass parameters to actions.

```yaml
- uses: actions/setup-node@v4
  with:
    node-version: 20
```

---

# 🔹 3.11 `env:` (Environment Variables)

Global:

```yaml
env:
  APP_ENV: production
```

Job-level:

```yaml
jobs:
  build:
    env:
      NODE_ENV: production
```

Step-level:

```yaml
- run: echo $APP_ENV
```

---

# 🔹 3.12 `needs:` (Job Dependency)

```yaml
jobs:
  build:
    runs-on: ubuntu-latest

  deploy:
    needs: build
    runs-on: ubuntu-latest
```

Deploy will run **after build completes successfully**.

---

# 🔹 3.13 `if:` (Conditional Execution)

Job condition:

```yaml
if: github.ref == 'refs/heads/main'
```

Step condition:

```yaml
- run: echo "Only on main"
  if: github.ref == 'refs/heads/main'
```

---

# 🔹 3.14 `strategy:` (Matrix Builds)

```yaml
strategy:
  matrix:
    node-version: [16, 18, 20]
```

Runs job multiple times.

---

# 🔹 3.15 `concurrency:`

Prevents multiple runs simultaneously.

```yaml
concurrency:
  group: deploy-production
  cancel-in-progress: true
```

---

# 🔹 3.16 `permissions:`

Control workflow permissions.

```yaml
permissions:
  contents: read
  id-token: write
```

Used in OIDC authentication (important for AWS/EKS).

---

# 🔥 Complete DevOps Example (Docker + Terraform)

```yaml
name: EKS Deployment

on:
  push:
    branches: [ main ]

jobs:
  docker:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: docker build -t myapp .
      - run: docker push myapp

  terraform:
    needs: docker
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: terraform init
      - run: terraform apply -auto-approve
```

---

# 🧠 YAML Best Practices

✅ Use proper indentation (2 spaces)
✅ Always pin action versions (`@v4`)
✅ Use secrets for credentials
✅ Separate jobs for build & deploy
✅ Use matrix for testing

---

# 🎯 Summary

Workflow Structure =

* `name`
* `on`
* `jobs`
* `runs-on`
* `steps`
* `uses`
* `run`
* `with`
* `env`
* `needs`
* `if`
* `strategy`
* `permissions`

Master this → You can write production CI/CD pipelines.

---
# 4️⃣ GitHub Actions Events (Complete Trigger Guide)

## 🔔 What Are Events?

![Image](https://docs.github.com/assets/cb-25535/images/help/actions/overview-actions-simple.png)

![Image](https://andrewlock.net/content/images/2021/webhooks_banner.png)

![Image](https://docs.github.com/assets/cb-78157/images/help/actions/workflow-dispatch-inputs.png)

![Image](https://media2.dev.to/dynamic/image/width%3D1600%2Cheight%3D900%2Cfit%3Dcover%2Cgravity%3Dauto%2Cformat%3Dauto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F9krj1bvb2gblpr1163ic.png)

In **GitHub Actions**, an **event** is something that happens in your repository that triggers a workflow.

Example:

* Developer pushes code → workflow runs
* PR created → tests run
* Schedule time reached → nightly job runs

Events are defined under the `on:` section in your workflow YAML file.

---

# 🔹 4.1 `push` Event

Triggers when code is pushed.

```yaml
on:
  push:
    branches:
      - main
```

### Filter by branch

```yaml
on:
  push:
    branches:
      - main
      - dev
```

### Ignore branch

```yaml
on:
  push:
    branches-ignore:
      - test
```

---

# 🔹 4.2 `pull_request` Event

Triggers when PR is opened, updated, or reopened.

```yaml
on:
  pull_request:
    branches:
      - main
```

### Filter by PR activity type

```yaml
on:
  pull_request:
    types: [opened, synchronize, reopened]
```

---

# 🔹 4.3 `pull_request_target`

Runs in context of base branch (important for security cases).

```yaml
on:
  pull_request_target:
```

⚠️ Use carefully (security sensitive).

---

# 🔹 4.4 `workflow_dispatch` (Manual Trigger)

Allows manual execution from Actions tab.

```yaml
on:
  workflow_dispatch:
```

### With input parameters

```yaml
on:
  workflow_dispatch:
    inputs:
      environment:
        description: "Choose environment"
        required: true
        default: "dev"
```

Useful for:

* Manual production deployment
* Emergency rollback

---

# 🔹 4.5 `schedule` (CRON Jobs)

Runs workflow at specific time.

```yaml
on:
  schedule:
    - cron: "0 0 * * *"
```

Example:

* Nightly build
* Weekly cleanup
* Daily backup

CRON format:

```
* * * * *
| | | | |
| | | | └ Day of week
| | | └── Month
| | └──── Day of month
| └────── Hour
└──────── Minute
```

---

# 🔹 4.6 `release`

Triggers when release is created or published.

```yaml
on:
  release:
    types: [published]
```

Use case:

* Build release artifacts
* Publish to Docker Hub

---

# 🔹 4.7 `workflow_call` (Reusable Workflow)

Used when one workflow calls another.

```yaml
on:
  workflow_call:
```

Great for:

* Shared CI pipeline across repos
* Organization-wide standards

---

# 🔹 4.8 `repository_dispatch`

External trigger via API.

```yaml
on:
  repository_dispatch:
```

Use case:

* Trigger workflow from external system
* Microservice communication

---

# 🔹 4.9 `issues`

Triggers on issue activity.

```yaml
on:
  issues:
    types: [opened, closed]
```

Use case:

* Auto labeling
* Welcome message bot

---

# 🔹 4.10 `issue_comment`

Runs when comment added to issue or PR.

```yaml
on:
  issue_comment:
```

---

# 🔹 4.11 `fork`

Triggered when repository is forked.

```yaml
on: fork
```

---

# 🔹 4.12 `create`

Triggered when branch or tag created.

```yaml
on: create
```

---

# 🔹 4.13 `delete`

Triggered when branch or tag deleted.

```yaml
on: delete
```

---

# 🔹 4.14 `check_run` & `check_suite`

Advanced integrations with checks API.

```yaml
on: check_run
```

Used in advanced CI tools.

---

# 🔹 4.15 Multiple Events Together

```yaml
on:
  push:
    branches: [main]
  pull_request:
  workflow_dispatch:
  schedule:
    - cron: "0 3 * * 1"
```

Workflow runs on:

* Push
* PR
* Manual trigger
* Every Monday at 3 AM

---

# 🔥 Real DevOps Use Case (Your Learning Path)

Since you're working with:

* Docker
* Terraform
* EKS

Recommended event strategy:

| Event             | Purpose               |
| ----------------- | --------------------- |
| push (dev branch) | Run tests             |
| pull_request      | Validate changes      |
| push (main)       | Deploy to staging     |
| workflow_dispatch | Deploy to production  |
| schedule          | Nightly security scan |

---

# ⚠️ Important Best Practices

✅ Use branch filters
✅ Use path filters if needed
✅ Avoid running on every push unnecessarily
✅ Separate CI & CD triggers
✅ Use manual trigger for production

---

# 🎯 Summary

Events control **WHEN** your pipeline runs.

Most common:

* push
* pull_request
* workflow_dispatch
* schedule
* release

Master events → You control automation timing.

---
# 5️⃣ Runners Deep Dive (GitHub Actions)

## 🖥️ What is a Runner?

![Image](https://docs.github.com/assets/cb-497738/images/help/actions/arc-diagram.png)

![Image](https://neon.com/guides/images/gihub-actions-self-hosted-runners/gihub-actions-self-hosted-runners-droplet-config-1.jpg)

![Image](https://user-images.githubusercontent.com/60080580/148239847-db32352e-50f2-40f6-9f9e-a82238c30374.png)

![Image](https://media2.dev.to/cdn-cgi/image/width%3D800%2Cheight%3D%2Cfit%3Dscale-down%2Cgravity%3Dauto%2Cformat%3Dauto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Ftvbfuh55ec5vz04ckstp.png)

In **GitHub Actions**, a **runner** is the machine that executes your workflow jobs.

When a workflow is triggered:

1. GitHub assigns a runner
2. The runner downloads your code
3. It executes all job steps
4. Reports success or failure

---

# 🔹 5.1 Types of Runners

## 🟢 1. GitHub-Hosted Runners

Managed by **GitHub**.

You don’t manage infrastructure.

Example:

```yaml
runs-on: ubuntu-latest
```

Available environments:

| OS      | Label          |
| ------- | -------------- |
| Ubuntu  | ubuntu-latest  |
| Windows | windows-latest |
| macOS   | macos-latest   |

### ✅ Advantages

* Zero maintenance
* Auto scaling
* Secure & isolated
* Fast setup

### ❌ Limitations

* Limited customization
* Time limits
* Shared resources

---

## 🔵 2. Self-Hosted Runners

You manage the server (EC2, VM, on-prem, Kubernetes node).

Example:

```yaml
runs-on: self-hosted
```

### Setup Flow

1. Go to Repo → Settings → Actions → Runners
2. Add new runner
3. Install runner on your server
4. Start runner service

### ✅ Advantages

* Full control
* Custom software
* No time limits
* Better performance for heavy builds

### ❌ Disadvantages

* Maintenance required
* Security responsibility
* Scaling must be managed

---

# 🔹 5.2 Runner Architecture

Flow:

```
Workflow Triggered
       ↓
GitHub Queue
       ↓
Runner Assigned
       ↓
Runner Downloads Code
       ↓
Executes Jobs & Steps
       ↓
Uploads Logs & Artifacts
```

Each job:

* Runs on a fresh environment (GitHub-hosted)
* Is isolated from other jobs

---

# 🔹 5.3 Runner Labels

Labels define runner selection.

Example:

```yaml
runs-on: [self-hosted, linux, x64]
```

GitHub selects runner that matches **all labels**.

Common labels:

* linux
* windows
* macOS
* x64
* arm64

---

# 🔹 5.4 Using Specific OS Versions

Instead of `ubuntu-latest`, you can use:

```yaml
runs-on: ubuntu-22.04
```

Other examples:

```yaml
runs-on: windows-2022
runs-on: macos-13
```

Best practice:

* Pin OS version in production pipelines

---

# 🔹 5.5 Hardware Specifications (GitHub Hosted)

Typical Ubuntu runner:

* 2-core CPU
* 7 GB RAM
* 14 GB SSD

⚠️ Large builds may require self-hosted runners.

---

# 🔹 5.6 Runner Environment

Each GitHub-hosted runner:

* Is clean environment
* Installs dependencies per job
* Deletes environment after job

Nothing persists between runs (unless using cache/artifacts).

---

# 🔹 5.7 Scaling Behavior

GitHub-hosted:

* Automatically scales
* Parallel jobs supported

Self-hosted:

* Limited to number of machines
* Must scale manually

---

# 🔹 5.8 Security Considerations

### For GitHub Hosted

* Fully isolated VMs
* Destroyed after use
* Secure by default

### For Self-hosted

⚠️ Important:

* Protect from public PRs
* Restrict secrets
* Use firewalls
* Monitor access

Never expose production server directly as public runner.

---

# 🔹 5.9 Runner Groups (Organization Level)

At organization level, you can:

* Create runner groups
* Restrict which repos use runners
* Separate prod/staging runners

Useful for:

* Enterprise environments
* Multi-team setups

---

# 🔹 5.10 When to Use Which?

| Scenario                  | Recommended Runner        |
| ------------------------- | ------------------------- |
| Small project             | GitHub Hosted             |
| Docker build              | GitHub Hosted             |
| Heavy ML build            | Self-hosted               |
| Internal enterprise infra | Self-hosted               |
| EKS + Terraform           | GitHub Hosted (with OIDC) |

---

# 🔥 Your DevOps Case (Docker + Terraform + EKS)

Recommended setup:

* CI (build/test) → GitHub Hosted
* Terraform Apply → GitHub Hosted (OIDC)
* Heavy image build → Self-hosted (optional)

Example:

```yaml
jobs:
  build:
    runs-on: ubuntu-latest

  deploy:
    needs: build
    runs-on: ubuntu-latest
```

---

# 🔹 5.11 Advanced: Ephemeral Self-Hosted Runners

Advanced production pattern:

* Use Kubernetes
* Dynamically create runner pods
* Destroy after job

Secure & scalable approach for enterprises.

---

# 🎯 Summary

Runner = Execution Machine

Types:

* GitHub Hosted (easy)
* Self-hosted (control)

Key Concepts:

* runs-on
* Labels
* Isolation
* Scaling
* Security

Master runners → You control where and how your CI/CD runs.

---

# 6️⃣ Jobs & Dependencies (Advanced Guide)

## 🧩 How Jobs Work in GitHub Actions

![Image](https://i.sstatic.net/7NnYS.png)

![Image](https://calmcode.io/static/images/content/course/github-actions/dependencies.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A2000/1%2A8mUtip6z_oydfLi4P86KUw.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2AuE_5IpYRDnE4RgrI8cy7yA.png)

In **GitHub Actions**, a **job** is a group of steps that run on the same runner.

Important:

* Each job runs on a separate runner
* Jobs run in parallel by default
* Use `needs:` to create dependencies

---

# 🔹 6.1 Single Job Example

```yaml
name: Simple CI

on: push

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Building..."
```

Only one job → simple pipeline.

---

# 🔹 6.2 Multiple Jobs (Parallel Execution)

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Build"

  test:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Test"
```

Both `build` and `test` run **at the same time**.

---

# 🔹 6.3 Sequential Jobs (Using `needs`)

To make jobs run in order:

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Build completed"

  test:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - run: echo "Testing..."

  deploy:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - run: echo "Deploying..."
```

Flow:

```
build → test → deploy
```

If `build` fails → `test` and `deploy` will not run.

---

# 🔹 6.4 Multiple Dependencies

```yaml
jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Linting"

  test:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Testing"

  deploy:
    needs: [lint, test]
    runs-on: ubuntu-latest
    steps:
      - run: echo "Deploying..."
```

Deploy runs only if both succeed.

---

# 🔹 6.5 Passing Data Between Jobs (Outputs)

Since jobs run on different runners, they don’t share memory.

Use **outputs**.

### Step Output

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    outputs:
      image_tag: ${{ steps.build_step.outputs.tag }}
    steps:
      - id: build_step
        run: echo "tag=v1.0.0" >> $GITHUB_OUTPUT
```

### Use Output in Another Job

```yaml
  deploy:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - run: echo "Deploying ${{ needs.build.outputs.image_tag }}"
```

---

# 🔹 6.6 Conditional Jobs (`if:`)

Run job only on specific branch:

```yaml
deploy:
  if: github.ref == 'refs/heads/main'
  runs-on: ubuntu-latest
```

Run only when previous job fails:

```yaml
notify:
  needs: build
  if: failure()
  runs-on: ubuntu-latest
```

Common conditions:

* `success()`
* `failure()`
* `always()`
* `cancelled()`

---

# 🔹 6.7 Continue on Error

Sometimes you don’t want pipeline to stop.

```yaml
- run: npm test
  continue-on-error: true
```

Useful for:

* Non-critical checks
* Optional security scan

---

# 🔹 6.8 Job Timeout

```yaml
build:
  runs-on: ubuntu-latest
  timeout-minutes: 10
```

Prevents infinite runs.

---

# 🔹 6.9 Job-Level Permissions

```yaml
deploy:
  runs-on: ubuntu-latest
  permissions:
    contents: read
    id-token: write
```

Important for:

* OIDC authentication
* AWS/EKS deployments

---

# 🔥 Real DevOps Production Pipeline (Your Stack)

Docker + Terraform + EKS

```yaml
name: Production Pipeline

on:
  push:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: docker build -t myapp .
      - run: echo "image_tag=v1.0.${{ github.run_number }}" >> $GITHUB_OUTPUT
        id: build_step

  terraform:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: terraform init
      - run: terraform apply -auto-approve

  deploy:
    needs: terraform
    runs-on: ubuntu-latest
    steps:
      - run: kubectl apply -f k8s/
```

Flow:

```
Build Docker → Apply Terraform → Deploy to EKS
```

---

# 🔹 6.10 Workflow Visualization

In **GitHub** Actions tab:

* You can see job graph
* Parallel jobs
* Dependencies visually

---

# ⚡ Best Practices

✅ Separate CI & CD jobs
✅ Use `needs` properly
✅ Keep jobs small & focused
✅ Pass outputs instead of rebuilding
✅ Use conditions for production deploy
✅ Add timeout for safety

---

# 🎯 Summary

Jobs control:

* Execution order
* Parallel vs sequential
* Data sharing
* Conditions
* Permissions

Master this → You can design complex CI/CD pipelines.

---
# 7️⃣ Secrets & Security (Very Important – Production Level)

## 🔐 Why Security Matters in CI/CD

![Image](https://www.edwardthomson.com/blog/images/githubactions/11-addingsecret.png)

![Image](https://docs.github.com/assets/cb-63262/images/help/actions/oidc-architecture.png)

![Image](https://itknowledgeexchange.techtarget.com/coffee-talk/files/2020/11/github-actions-secrets-tokens.png)

![Image](https://user-images.githubusercontent.com/395096/105118813-da1b5b00-5aad-11eb-85fa-7ee6323f159c.png)

In **GitHub Actions**, your workflows may need:

* AWS credentials
* Docker Hub password
* Database passwords
* API tokens

These must **never** be hardcoded in YAML.

That’s where **Secrets & Security controls** come in.

---

# 🔹 7.1 Types of Secrets

## 🟢 1. Repository Secrets

Stored at repo level.

Path:

```
Repo → Settings → Secrets and variables → Actions
```

Example:

```
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
DOCKERHUB_TOKEN
```

Accessible inside workflow:

```yaml
env:
  AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
```

---

## 🔵 2. Organization Secrets

Shared across multiple repositories.

Useful for:

* Company-wide AWS account
* Shared Docker registry

Can restrict which repositories can use them.

---

## 🟣 3. Environment Secrets

Linked to specific environments (dev/stage/prod).

Example:

* Prod AWS credentials
* Staging database password

Configured under:

```
Repo → Settings → Environments
```

---

# 🔹 7.2 Using Secrets in Workflow

### Correct Way

```yaml
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Deploying"
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
```

### ❌ Never Do This

```yaml
AWS_SECRET_ACCESS_KEY: mypassword123
```

Hardcoding = security risk.

---

# 🔹 7.3 GitHub Variables vs Secrets

| Feature         | Variables | Secrets |
| --------------- | --------- | ------- |
| Encrypted       | ❌ No      | ✅ Yes   |
| Visible in logs | Yes       | Masked  |
| For credentials | ❌ No      | ✅ Yes   |

Use:

* Variables → Config values
* Secrets → Sensitive data

---

# 🔹 7.4 OIDC (Best Practice – No Long-Term Keys)

Instead of storing AWS keys, use **OIDC authentication**.

This allows **GitHub → AWS trust relationship** without storing credentials.

Requires:

* `permissions: id-token: write`
* IAM role with trust policy

Example:

```yaml
permissions:
  id-token: write
  contents: read
```

Benefits:

* No static AWS keys
* Short-lived credentials
* Production-level security

For your **EKS + Terraform setup**, OIDC is strongly recommended.

---

# 🔹 7.5 Environment Protection Rules

Using Environments in **GitHub**:

You can configure:

* Required reviewers before deployment
* Wait timers
* Branch restrictions

Example:

```yaml
deploy:
  environment: production
```

If production environment requires approval → workflow pauses.

Great for:

* Preventing accidental production deploys
* Enterprise compliance

---

# 🔹 7.6 Masking Secrets in Logs

GitHub automatically masks secrets in logs.

Example:
If secret value = `mypassword`

Log shows:

```
***
```

But avoid:

```yaml
- run: echo ${{ secrets.MY_SECRET }}
```

Even though masked, don’t print secrets unnecessarily.

---

# 🔹 7.7 Restricting Workflow Permissions

Default token = `GITHUB_TOKEN`

Control its permissions:

```yaml
permissions:
  contents: read
  pull-requests: write
```

Principle:
👉 Give minimum required permissions.

---

# 🔹 7.8 Handling Public Repositories

⚠️ Important:

If repo is public:

* PR from fork does NOT get secrets
* Protect self-hosted runners
* Avoid exposing sensitive infra

Never allow untrusted PRs to run privileged workflows.

---

# 🔹 7.9 Secure Deployment Pattern (Recommended for You)

For Docker + Terraform + EKS:

### CI Job

* No secrets needed
* Build + Test only

### CD Job

* Requires OIDC
* Environment protection
* Restricted branch (main only)

Example:

```yaml
on:
  push:
    branches: [main]

jobs:
  deploy:
    if: github.ref == 'refs/heads/main'
    environment: production
    permissions:
      id-token: write
      contents: read
    runs-on: ubuntu-latest
```

---

# 🔹 7.10 Secret Rotation

Best practices:

* Rotate AWS keys every 90 days (if not using OIDC)
* Use IAM roles instead of root account
* Use least privilege IAM policy
* Monitor audit logs

---

# 🔥 Real Enterprise Security Checklist

✅ Use OIDC (no long-term keys)
✅ Restrict production to main branch
✅ Use environment approvals
✅ Set job-level permissions
✅ Do not print secrets
✅ Separate CI & CD workflows
✅ Use self-hosted runners carefully

---

# 🎯 Summary

Security in GitHub Actions includes:

* Repository secrets
* Organization secrets
* Environment secrets
* OIDC authentication
* Permissions control
* Environment protection rules

For your DevOps journey → mastering security is mandatory.

---
# 8️⃣ Matrix Strategy (Advanced Guide)

## 🔁 What is Matrix Strategy?

![Image](https://i.sstatic.net/7NnYS.png)

![Image](https://thekevinwang.com/_next/image?q=75\&url=%2Fimage%2F2021%2F09%2F19%2Fmatrix_diagram-light.webp\&w=3840)

![Image](https://matheusthurler.com.br/images/covers/github-actions-matrix.png)

![Image](https://miro.medium.com/1%2A6veB5Sy6tbv5YftAATqQyg.gif)

In **GitHub Actions**, a **matrix strategy** allows you to run the same job multiple times with different combinations of values.

👉 Instead of writing multiple jobs manually, matrix creates them automatically.

---

# 🔹 8.1 Basic Matrix Example (Multiple Versions)

Test Node.js project on multiple versions:

```yaml
name: Node Matrix CI

on: push

jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [16, 18, 20]

    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: ${{ matrix.node-version }}
      - run: npm install
      - run: npm test
```

💡 This creates **3 parallel jobs**:

* Node 16
* Node 18
* Node 20

---

# 🔹 8.2 Multi-OS Matrix

Test on different operating systems:

```yaml
strategy:
  matrix:
    os: [ubuntu-latest, windows-latest, macos-latest]

runs-on: ${{ matrix.os }}
```

Now job runs on:

* Linux
* Windows
* macOS

---

# 🔹 8.3 Multi-Dimensional Matrix

Combine OS + Version:

```yaml
strategy:
  matrix:
    os: [ubuntu-latest, windows-latest]
    node: [18, 20]

runs-on: ${{ matrix.os }}
```

This creates:

| OS      | Node |
| ------- | ---- |
| Ubuntu  | 18   |
| Ubuntu  | 20   |
| Windows | 18   |
| Windows | 20   |

👉 Total = 4 jobs automatically

---

# 🔹 8.4 Include & Exclude

Sometimes you want custom combinations.

### Exclude Example

```yaml
strategy:
  matrix:
    os: [ubuntu-latest, windows-latest]
    node: [16, 18]
    exclude:
      - os: windows-latest
        node: 16
```

Removes:

* Windows + Node 16

---

### Include Example

```yaml
strategy:
  matrix:
    os: [ubuntu-latest]
    node: [18]
    include:
      - os: ubuntu-latest
        node: 20
```

Adds extra custom combination.

---

# 🔹 8.5 Fail Fast

By default, if one matrix job fails → others continue.

You can control:

```yaml
strategy:
  fail-fast: false
```

If `true` → remaining jobs cancel when one fails.

---

# 🔹 8.6 Max Parallel Jobs

Limit concurrency:

```yaml
strategy:
  max-parallel: 2
  matrix:
    node: [16, 18, 20]
```

Even if 3 jobs created → only 2 run at same time.

Useful for:

* Limited self-hosted runners
* Resource-heavy builds

---

# 🔹 8.7 Dynamic Matrix (Advanced)

Generate matrix dynamically from previous job.

Example:

```yaml
jobs:
  generate:
    runs-on: ubuntu-latest
    outputs:
      matrix: ${{ steps.set.outputs.matrix }}
    steps:
      - id: set
        run: echo 'matrix=["service1","service2"]' >> $GITHUB_OUTPUT

  build:
    needs: generate
    strategy:
      matrix:
        service: ${{ fromJson(needs.generate.outputs.matrix) }}
```

Useful for:

* Monorepo microservices
* Dynamic environments

---

# 🔥 Real DevOps Use Case (Your Path – Docker + EKS)

## 🟢 Example 1: Multi-Environment Deploy

```yaml
strategy:
  matrix:
    environment: [dev, staging, prod]
```

Deploy same app to:

* Dev
* Staging
* Prod

---

## 🟢 Example 2: Multi-Architecture Docker Build

```yaml
strategy:
  matrix:
    arch: [amd64, arm64]
```

Build images for:

* Intel
* ARM (Apple Silicon / Graviton)

---

## 🟢 Example 3: Terraform Multi-Region

```yaml
strategy:
  matrix:
    region: [us-east-1, ap-south-1]
```

Deploy infrastructure in:

* US
* India

---

# 🔹 8.8 Matrix + Needs (Production Pattern)

Combine CI + Matrix:

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Build Done"

  test:
    needs: build
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node: [18, 20]
    steps:
      - run: echo "Testing Node ${{ matrix.node }}"
```

Flow:

```text
Build → Parallel Test (Node 18 & 20)
```

---

# 🔹 8.9 When NOT to Use Matrix

Avoid matrix when:

* Production deployment (usually single target)
* Complex job dependencies
* Very resource-heavy tasks

---

# ⚡ Best Practices

✅ Use matrix for testing only
✅ Limit parallel jobs for heavy builds
✅ Use exclude/include carefully
✅ Separate CI matrix & CD jobs
✅ Avoid deploying production via matrix

---

# 🎯 Summary

Matrix Strategy allows:

* Multi-version testing
* Multi-OS testing
* Multi-region deploy
* Multi-architecture builds
* Parallel job execution

It makes pipelines scalable and clean.

---

# 9️⃣ Artifacts & Caching (Performance Optimization)

## 📦 Why Artifacts & Cache Matter?

![Image](https://user-images.githubusercontent.com/16109154/103645952-223c6880-4f59-11eb-8268-8dca6937b5f9.png)

![Image](https://depot.dev/images/docker-layer-caching-in-github-actions-image5.webp)

![Image](https://docs.github.com/assets/cb-13990/images/help/repository/artifact-drop-down-updated.png)

![Image](https://docs.github.com/assets/cb-40551/images/help/actions/superlinter-workflow-sidebar.png)

In **GitHub Actions**, every job runs on a **fresh runner**.

That means:

* No previous files
* No installed dependencies
* No build outputs

To optimize performance and share data, we use:

* 📦 **Artifacts** → Store files between jobs
* ⚡ **Cache** → Speed up dependency installation

---

# 🔹 9.1 What Are Artifacts?

Artifacts store build outputs so they can be:

* Downloaded later
* Used in another job
* Stored as release assets

Example use cases:

* Test reports
* Build packages (.jar, .zip)
* Docker metadata
* Terraform plan files

---

# 🔹 9.2 Uploading Artifacts

```yaml id="0y41p3"
- name: Upload Build Files
  uses: actions/upload-artifact@v4
  with:
    name: build-output
    path: dist/
```

This stores:

* All files inside `dist/`

---

# 🔹 9.3 Downloading Artifacts (Another Job)

```yaml id="r7m1nk"
- name: Download Build Files
  uses: actions/download-artifact@v4
  with:
    name: build-output
```

Now second job can use files from first job.

---

# 🔹 9.4 Complete Artifact Example

```yaml id="q6omz8"
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: mkdir dist && echo "Hello" > dist/app.txt
      - uses: actions/upload-artifact@v4
        with:
          name: app-build
          path: dist/

  deploy:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - uses: actions/download-artifact@v4
        with:
          name: app-build
      - run: cat dist/app.txt
```

Flow:

```
Build → Upload Artifact → Download → Deploy
```

---

# 🔹 9.5 Artifact Retention

By default:

* Stored for 90 days

You can change:

```yaml id="d2unvw"
with:
  retention-days: 7
```

Good practice:

* Short retention for CI builds
* Longer retention for releases

---

# 🔹 9.6 What Is Cache?

Cache is used to:

* Speed up dependency installation
* Reduce pipeline time
* Avoid reinstalling packages

Common cache targets:

| Language | Cache Folder |
| -------- | ------------ |
| Node.js  | ~/.npm       |
| Python   | ~/.cache/pip |
| Maven    | ~/.m2        |
| Gradle   | ~/.gradle    |
| Docker   | layer cache  |

---

# 🔹 9.7 Basic Cache Example (Node.js)

```yaml id="1l3xmi"
- name: Cache Node Modules
  uses: actions/cache@v4
  with:
    path: ~/.npm
    key: ${{ runner.os }}-node-${{ hashFiles('package-lock.json') }}
    restore-keys: |
      ${{ runner.os }}-node-
```

How it works:

* `key` = unique identifier
* `hashFiles` = detects dependency changes
* `restore-keys` = fallback option

---

# 🔹 9.8 Full CI with Cache Example

```yaml id="mtt6r4"
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - uses: actions/cache@v4
        with:
          path: ~/.npm
          key: node-${{ hashFiles('package-lock.json') }}

      - run: npm install
      - run: npm test
```

First run → installs normally
Next runs → much faster

---

# 🔹 9.9 Cache vs Artifact (Difference)

| Feature           | Artifact                 | Cache            |
| ----------------- | ------------------------ | ---------------- |
| Purpose           | Share files between jobs | Speed up builds  |
| Used Between Jobs | Yes                      | No               |
| Downloadable      | Yes                      | No               |
| Persistent        | Temporary                | Based on key     |
| Example           | Build output             | npm dependencies |

---

# 🔹 9.10 Docker Layer Caching (Advanced)

For Docker builds:

```yaml id="u4jkh2"
- name: Build Docker Image
  run: docker build -t myapp .
```

To optimize:

* Use proper layer ordering
* Use build cache
* Use GitHub cache for Docker layers (advanced setup)

Best practice:

* Copy `package.json` first
* Install dependencies
* Then copy full source

---

# 🔹 9.11 Terraform Plan Artifact (Your Use Case)

Recommended pattern:

```yaml id="dzm2r7"
jobs:
  plan:
    runs-on: ubuntu-latest
    steps:
      - run: terraform plan -out=tfplan
      - uses: actions/upload-artifact@v4
        with:
          name: tfplan
          path: tfplan

  apply:
    needs: plan
    runs-on: ubuntu-latest
    steps:
      - uses: actions/download-artifact@v4
        with:
          name: tfplan
      - run: terraform apply tfplan
```

Safer production pattern:

* Plan in one job
* Apply only after approval

---

# 🔹 9.12 Performance Best Practices

✅ Use cache for dependencies
✅ Use artifacts for build outputs
✅ Short retention for CI
✅ Avoid caching large unnecessary folders
✅ Use hash-based keys
✅ Separate CI & CD stages

---

# 🔥 Real Production Optimization Flow

```
Push Code
   ↓
Checkout
   ↓
Restore Cache
   ↓
Install Dependencies
   ↓
Run Tests
   ↓
Build App
   ↓
Upload Artifact
   ↓
Deploy Job Downloads Artifact
```

Optimized + Secure + Fast

---

# 🎯 Summary

Artifacts:

* Store files between jobs
* Used for build outputs

Cache:

* Speeds up pipeline
* Based on keys
* Not for sharing job outputs

Master this → Your CI/CD becomes fast & production-ready.

---
# 🔟 Deployment Patterns (AWS • Docker • Kubernetes • Production CI/CD)

## 🚀 Overview

![Image](https://d2908q01vomqb2.cloudfront.net/7719a1c782a1ba91c031a682a0a2f8658209adbf/2022/03/27/1-ArchitectureDiagram.png)

![Image](https://miro.medium.com/1%2A5JIcTnXIZpZ6uIsCcuP1nw.jpeg)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1200/1%2AUx9raDEMqqyWrgz3lMppQA.jpeg)

![Image](https://miro.medium.com/1%2AGgIeRA40tqhLPUSpJ1kMzw.png)

In **GitHub Actions**, deployment patterns define **how your application moves from build → production**.

For your DevOps path (Docker + Terraform + EKS), this section is very important.

---

# 🔹 10.1 Pattern 1 – Docker Build & Push (Container Registry)

### 📦 Use Case

* Build Docker image
* Push to Docker Hub / ECR
* Later deploy to Kubernetes

---

## Example: Docker Hub Deployment

```yaml
name: Docker Build & Push

on:
  push:
    branches: [main]

jobs:
  docker:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Login to Docker Hub
        run: echo "${{ secrets.DOCKERHUB_TOKEN }}" | docker login -u USERNAME --password-stdin

      - name: Build Image
        run: docker build -t USERNAME/myapp:${{ github.sha }} .

      - name: Push Image
        run: docker push USERNAME/myapp:${{ github.sha }}
```

### ✅ Best Practice

* Tag images using commit SHA
* Never use `latest` in production

---

# 🔹 10.2 Pattern 2 – Deploy to AWS EC2

### 📦 Use Case

* SSH into EC2
* Pull latest image
* Restart container

```yaml
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: SSH Deploy
        run: |
          ssh user@ec2-ip "
          docker pull myapp:${{ github.sha }}
          docker stop myapp || true
          docker run -d myapp:${{ github.sha }}
          "
```

⚠️ Not ideal for large production setups.

---

# 🔹 10.3 Pattern 3 – Deploy to Amazon EKS (Recommended for You)

For Kubernetes-based deployments.

### Secure Method → OIDC Authentication

```yaml
permissions:
  id-token: write
  contents: read
```

### Deployment Example

```yaml
jobs:
  deploy:
    runs-on: ubuntu-latest
    environment: production
    permissions:
      id-token: write
      contents: read

    steps:
      - uses: actions/checkout@v4

      - name: Configure kubectl
        run: aws eks update-kubeconfig --name my-cluster

      - name: Deploy to Kubernetes
        run: kubectl apply -f k8s/
```

Flow:

```text
Build Image → Push to Registry → Update Kubernetes Deployment
```

Best for:

* Microservices
* Scalable infra
* Enterprise production

---

# 🔹 10.4 Pattern 4 – Terraform Infrastructure Deployment

Infrastructure as Code automation.

```yaml
jobs:
  terraform:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - run: terraform init
      - run: terraform plan -out=tfplan
      - run: terraform apply -auto-approve
```

### Production Pattern (Safer)

* Job 1: `terraform plan`
* Upload artifact
* Manual approval
* Job 2: `terraform apply`

---

# 🔹 10.5 Pattern 5 – Blue-Green Deployment

Two environments:

* Blue (live)
* Green (new version)

Steps:

1. Deploy to green
2. Test green
3. Switch traffic
4. Keep blue as backup

Used in:

* Kubernetes
* Load balancer setups

---

# 🔹 10.6 Pattern 6 – Canary Deployment

Release to small percentage of users.

Flow:

1. Deploy v2 to 10%
2. Monitor
3. Increase gradually

Supported via:

* Kubernetes
* Service mesh (Istio)

---

# 🔹 10.7 Pattern 7 – GitHub Pages Deployment

For static sites:

```yaml
- uses: actions/deploy-pages@v4
```

Auto deploy from `main` branch.

---

# 🔹 10.8 Multi-Environment Deployment Pattern

Dev → Staging → Production

```yaml
jobs:
  deploy-dev:
    runs-on: ubuntu-latest

  deploy-staging:
    needs: deploy-dev
    runs-on: ubuntu-latest

  deploy-prod:
    needs: deploy-staging
    environment: production
    runs-on: ubuntu-latest
```

Add:

* Environment protection rules
* Required reviewers

---

# 🔹 10.9 CI + CD Separation (Best Practice)

### Workflow 1 – CI

* Build
* Test
* Lint
* Security scan

### Workflow 2 – CD

* Deploy only on main
* Requires approval
* Uses OIDC

Keeps production safe.

---

# 🔥 Complete Production Flow (Your DevOps Stack)

```text
Push Code
   ↓
CI Pipeline
   • Install dependencies
   • Run tests
   • Build Docker image
   • Push image
   ↓
CD Pipeline
   • Terraform apply
   • Deploy to EKS
   • Health check
```

Secure + Automated + Scalable

---

# ⚡ Deployment Best Practices

✅ Separate CI & CD workflows
✅ Use OIDC (no AWS static keys)
✅ Protect production with environment rules
✅ Use commit SHA image tagging
✅ Avoid direct SSH deployment
✅ Use infrastructure as code
✅ Add health checks after deployment

---

# 🎯 Summary

Deployment patterns include:

* Docker image push
* EC2 deployment
* EKS Kubernetes deployment
* Terraform automation
* Blue-Green strategy
* Canary releases
* Multi-environment pipelines

Master these → You can design enterprise-grade CI/CD.

---
# 1️⃣1️⃣ Reusable Workflows (Enterprise-Level CI/CD Design)

## 🔁 What Are Reusable Workflows?

![Image](https://alaintd.github.io/assets/img/posts/2022-05-04-How-to-pull-deploy-image-from-ACR-to-App-Service/GitHub-Actions-Pull-Deploy.png)

![Image](https://user-images.githubusercontent.com/3616259/181074881-87e580ca-6a9f-45ec-94c2-f3f1772281de.png)

![Image](https://multiprojectdevops.github.io/tutorials/assets/multi_ci_repo.png)

![Image](https://media2.dev.to/dynamic/image/width%3D800%2Cheight%3D%2Cfit%3Dscale-down%2Cgravity%3Dauto%2Cformat%3Dauto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F56ej3bn1uz9ub5j0799r.png)

In **GitHub Actions**, a **reusable workflow** allows one workflow to call another workflow.

👉 Instead of copying the same CI/CD YAML into multiple repositories, you define it once and reuse it everywhere.

This is **mandatory in enterprise DevOps environments**.

---

# 🔹 11.1 Why Use Reusable Workflows?

Without reusable workflows:

* ❌ Duplicate CI files in every repo
* ❌ Hard to maintain
* ❌ Inconsistent pipelines

With reusable workflows:

* ✅ Centralized CI logic
* ✅ Easier updates
* ✅ Standardized pipelines
* ✅ Enterprise-ready architecture

---

# 🔹 11.2 How It Works

Two parts:

### 1️⃣ Called Workflow (Reusable One)

Must include:

```yaml
on:
  workflow_call:
```

### 2️⃣ Caller Workflow

Calls it using:

```yaml
uses: owner/repo/.github/workflows/file.yml@branch
```

---

# 🔹 11.3 Create a Reusable Workflow

📁 `.github/workflows/node-ci.yml`

```yaml id="b6rkf0"
name: Reusable Node CI

on:
  workflow_call:
    inputs:
      node-version:
        required: true
        type: string

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - uses: actions/setup-node@v4
        with:
          node-version: ${{ inputs.node-version }}

      - run: npm install
      - run: npm test
```

---

# 🔹 11.4 Call the Reusable Workflow

In another workflow:

```yaml id="a3wzkf"
name: Main Pipeline

on:
  push:
    branches: [main]

jobs:
  call-ci:
    uses: my-org/my-repo/.github/workflows/node-ci.yml@main
    with:
      node-version: 20
```

Now:

* No duplication
* Centralized CI logic

---

# 🔹 11.5 Passing Secrets to Reusable Workflow

```yaml id="osq44g"
jobs:
  call-ci:
    uses: my-org/my-repo/.github/workflows/deploy.yml@main
    secrets:
      AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
```

Important:
Secrets must be explicitly passed.

---

# 🔹 11.6 Outputs from Reusable Workflow

Reusable workflow:

```yaml id="gh3r2n"
jobs:
  build:
    runs-on: ubuntu-latest
    outputs:
      image_tag: ${{ steps.build.outputs.tag }}
    steps:
      - id: build
        run: echo "tag=v1.0.0" >> $GITHUB_OUTPUT
```

Caller workflow:

```yaml id="u3v7ra"
jobs:
  call:
    uses: org/repo/.github/workflows/build.yml@main

  deploy:
    needs: call
    runs-on: ubuntu-latest
    steps:
      - run: echo "${{ needs.call.outputs.image_tag }}"
```

---

# 🔹 11.7 Reusable Workflow vs Composite Action

| Feature          | Reusable Workflow | Composite Action |
| ---------------- | ----------------- | ---------------- |
| Contains jobs    | ✅ Yes             | ❌ No             |
| Multiple runners | ✅ Yes             | ❌ No             |
| Best for         | Full pipelines    | Step grouping    |
| Enterprise use   | ✅ Highly used     | Moderate         |

Use:

* Reusable Workflow → Full CI/CD template
* Composite Action → Reusable step logic

---

# 🔥 Real DevOps Pattern (Your Case – Docker + EKS)

### Organization Structure

```
devops-templates/
   ├── node-ci.yml
   ├── docker-build.yml
   ├── terraform-deploy.yml
```

Each microservice repo:

```yaml id="t3p8xn"
jobs:
  ci:
    uses: company/devops-templates/.github/workflows/node-ci.yml@main

  docker:
    uses: company/devops-templates/.github/workflows/docker-build.yml@main

  deploy:
    uses: company/devops-templates/.github/workflows/terraform-deploy.yml@main
```

Enterprise benefit:

* Update once → applies to all repos

---

# 🔹 11.8 Cross-Repository Reusable Workflow

If calling from another private repo:

You must allow access under:

```
Repo Settings → Actions → General → Workflow permissions
```

---

# 🔹 11.9 Version Pinning (Best Practice)

Instead of:

```yaml
@main
```

Use:

```yaml
@v1
```

Or:

```yaml
@commit-sha
```

Prevents unexpected breaking changes.

---

# 🔹 11.10 Enterprise Architecture Example

```text
Microservice A
Microservice B
Microservice C
        ↓
Reusable CI Template Repo
        ↓
Centralized DevOps Control
```

Standardization + Governance + Security

---

# ⚡ Best Practices

✅ Keep reusable workflows generic
✅ Pass inputs instead of hardcoding
✅ Explicitly pass secrets
✅ Version your reusable workflows
✅ Separate CI & CD templates
✅ Use environment protection rules

---

# 🎯 Summary

Reusable workflows allow:

* Centralized CI/CD logic
* Multi-repo automation
* Enterprise-level DevOps architecture
* Scalable pipeline management

For your future DevOps career → this is a must-know advanced topic.

---
# 1️⃣2️⃣ Advanced Topics (Concurrency • Cost Optimization • Performance • Enterprise Controls)

## 🚀 Production-Level GitHub Actions Mastery

![Image](https://i.sstatic.net/yHdBB.png)

![Image](https://docs.github.com/assets/cb-25535/images/help/actions/overview-actions-simple.png)

![Image](https://www.warpbuild.com/_next/image?dpl=dpl_FvxjhXR7niCThDhxxsz41Wv9n17r\&q=75\&url=%2Fimages%2Fblog%2Fgithub-actions-cost-reduction%2Fcover.png\&w=3840)

![Image](https://devopscube.com/content/images/2025/03/actions-ec2-cost-1.gif)

These are **enterprise-grade concepts** in **GitHub Actions** that separate beginner pipelines from production-ready systems.

---

# 🔹 12.1 Concurrency Control

## ❓ Problem

Multiple deployments triggered at same time → production conflict.

## ✅ Solution: `concurrency`

```yaml
concurrency:
  group: production-deploy
  cancel-in-progress: true
```

### How It Works

* `group` → Unique deployment group
* `cancel-in-progress: true` → Cancels older running workflow

### Real Example

```yaml
jobs:
  deploy:
    runs-on: ubuntu-latest
    concurrency:
      group: prod
      cancel-in-progress: true
```

Use case:

* Prevent double production deploy
* Avoid Terraform state conflict

---

# 🔹 12.2 Workflow-Level Concurrency

Apply globally:

```yaml
concurrency:
  group: ${{ github.ref }}
  cancel-in-progress: true
```

Meaning:

* Only one run per branch at a time

Perfect for:

* Rapid push commits
* CI pipelines

---

# 🔹 12.3 Cost Optimization

GitHub-hosted runners consume minutes.

### 💰 Reduce Cost

### 1️⃣ Cancel Old Runs

```yaml
concurrency:
  cancel-in-progress: true
```

---

### 2️⃣ Run Only on Important Branches

```yaml
on:
  push:
    branches:
      - main
```

---

### 3️⃣ Path Filters

Run only if specific files change:

```yaml
on:
  push:
    paths:
      - "src/**"
```

---

### 4️⃣ Use Cache Properly

* Cache dependencies
* Avoid reinstalling every run

---

### 5️⃣ Avoid Matrix Overuse

Matrix multiplies jobs → increases cost.

Use only when required (testing).

---

# 🔹 12.4 Performance Optimization

## ✅ Use Cache

```yaml
uses: actions/cache@v4
```

---

## ✅ Optimize Docker Builds

Correct Dockerfile order:

```dockerfile
COPY package.json .
RUN npm install
COPY . .
```

Reduces rebuild time.

---

## ✅ Split Jobs

Instead of:

```text
Build + Test + Deploy in one job
```

Use:

```text
CI job → CD job
```

Parallel execution saves time.

---

## ✅ Use `max-parallel` for Control

```yaml
strategy:
  max-parallel: 2
```

Useful for:

* Limited self-hosted runners
* Resource-heavy tasks

---

# 🔹 12.5 Workflow Permissions Hardening

Default `GITHUB_TOKEN` has broad access.

Restrict permissions:

```yaml
permissions:
  contents: read
  id-token: write
```

Principle:
👉 Least privilege access

For EKS deployment:

* `id-token: write`
* `contents: read`

---

# 🔹 12.6 Required Status Checks

In **GitHub**:

Settings → Branch Protection Rules

Require:

* CI job success
* Code review
* Signed commits

Prevents merging broken code.

---

# 🔹 12.7 Environments + Approvals (Enterprise)

```yaml
environment: production
```

You can configure:

* Required reviewers
* Wait timer
* Deployment branch restrictions

Enterprise pattern:

```text
CI → Staging → Manual Approval → Production
```

---

# 🔹 12.8 Debugging Workflows

Enable debug logs:

```yaml
ACTIONS_STEP_DEBUG: true
```

Or re-run with debug from UI.

Also:

* Download logs
* Check job graph
* Review step timing

---

# 🔹 12.9 Workflow Visualization Graph

Inside Actions tab:

* See parallel jobs
* Dependency graph
* Failure points

Helps debugging complex pipelines.

---

# 🔹 12.10 Large-Scale Enterprise Pattern

```text
Developer Push
   ↓
CI Pipeline
   - Lint
   - Unit Test
   - Security Scan
   - Build Image
   ↓
Artifact Upload
   ↓
CD Pipeline
   - Terraform Plan
   - Approval
   - Terraform Apply
   - Deploy to EKS
   - Health Check
   ↓
Monitoring & Alert
```

With:

* Concurrency control
* OIDC authentication
* Environment protection
* Reusable workflows
* Cost optimization

---

# 🔹 12.11 Self-Hosted Runner Scaling (Advanced)

Enterprise solution:

* Kubernetes-based ephemeral runners
* Auto-scaling
* Destroy after job

Benefits:

* High security
* High scalability
* Cost-efficient at scale

---

# 🔹 12.12 Security Hardening Checklist

✅ Use OIDC (no AWS keys)
✅ Restrict permissions
✅ Protect production branch
✅ Use environment approvals
✅ Separate CI & CD
✅ Avoid running untrusted PRs on self-hosted runners
✅ Pin action versions (`@v4`)
✅ Monitor audit logs

---

# 🔥 Production-Ready GitHub Actions Blueprint

If you combine everything:

* Reusable workflows
* Matrix testing
* Artifact sharing
* Cache optimization
* Concurrency control
* OIDC secure deployment
* Environment protection
* Cost optimization

You now have **enterprise-level CI/CD architecture**.

---

# 🎯 Final Summary

Advanced Topics include:

* Concurrency
* Cost control
* Performance tuning
* Permission hardening
* Environment approvals
* Debugging
* Enterprise workflow architecture

Master these → You are no longer beginner DevOps.

---
# 1️⃣3️⃣ Monitoring & Logs (Observability in GitHub Actions)

## 🔍 Why Monitoring Matters?

![Image](https://docs.github.com/assets/cb-40738/images/help/actions/download-logs-drop-down.png)

![Image](https://raw.githubusercontent.com/laurent22/joplin/dev/Assets/WebsiteAssets/images/news/20230116-ga-raw-log-colored.png)

![Image](https://docs.github.com/assets/cb-63715/images/help/actions/workflow-graph.png)

![Image](https://user-images.githubusercontent.com/55514721/101413954-1007d580-389a-11eb-8b15-4f2a45ad9ddb.png)

In **GitHub Actions**, monitoring helps you:

* Detect failures quickly
* Debug pipeline issues
* Measure job performance
* Audit deployments

Without proper log understanding → CI/CD troubleshooting becomes difficult.

---

# 🔹 13.1 Workflow Run View

Inside **GitHub**:

```
Repository → Actions → Select Workflow Run
```

You can see:

* Workflow name
* Trigger event
* Branch
* Commit SHA
* Job graph
* Duration
* Status

---

# 🔹 13.2 Job Logs

Click on any job → View detailed logs.

Each step shows:

* Command executed
* Output
* Errors
* Execution time

Example log output:

```text
Run npm install
added 240 packages in 5s
```

If error:

```text
Error: Process completed with exit code 1
```

Exit code determines success/failure.

---

# 🔹 13.3 Step-Level Logs

Each step:

* Collapsible
* Timestamped
* Color-coded
* Shows environment info

Important for debugging:

```text
##[error]
##[warning]
```

---

# 🔹 13.4 Re-run Jobs

Options available:

* 🔁 Re-run all jobs
* 🔁 Re-run failed jobs only

Useful when:

* Temporary network issue
* Dependency registry issue
* External API timeout

---

# 🔹 13.5 Enable Debug Logging

To enable step debug logs:

Go to repository secrets → Add:

```text
ACTIONS_STEP_DEBUG = true
```

Or enable from UI re-run options.

Now logs show:

* Internal execution details
* Action metadata
* Additional debug output

---

# 🔹 13.6 Download Logs

From workflow page:

* Click “Download logs”

You get a `.zip` file containing:

* Job logs
* Step logs
* Metadata

Useful for:

* Sharing with team
* Audit purposes
* Compliance documentation

---

# 🔹 13.7 Workflow Graph Visualization

GitHub provides visual dependency graph:

```text
Build → Test → Deploy
```

Shows:

* Parallel jobs
* Dependencies (`needs`)
* Failed node

Helps understand complex pipelines.

---

# 🔹 13.8 Common Debugging Scenarios

## 🟢 Docker Build Fails

Check:

* Dockerfile path
* Build context
* Login step

---

## 🟢 Terraform Fails

Check:

* AWS authentication
* Backend state lock
* Plan output

---

## 🟢 Kubernetes Deployment Fails

Check:

* Kubeconfig setup
* Image tag mismatch
* Pod logs using:

  ```
  kubectl logs
  ```

---

# 🔹 13.9 Monitoring Deployment Health

After deployment:

Add health check step:

```yaml
- name: Health Check
  run: curl -f https://myapp.com || exit 1
```

Ensures:

* Deployment successful
* Service reachable

---

# 🔹 13.10 Audit Logs (Enterprise)

For organizations:

```
Org Settings → Audit Log
```

Tracks:

* Workflow changes
* Secret modifications
* Permission updates
* Deployment approvals

Important for:

* Compliance
* Enterprise governance

---

# 🔹 13.11 Monitoring Best Practices

✅ Keep logs clean
✅ Avoid printing secrets
✅ Add meaningful step names
✅ Use health checks
✅ Separate CI & CD logs
✅ Keep pipeline stages clear
✅ Use environment approvals

---

# 🔥 Real Production Monitoring Pattern

```text
Push Code
   ↓
CI Run
   ↓
Logs Verified
   ↓
Artifact Stored
   ↓
CD Run
   ↓
Deployment Logs
   ↓
Health Check
   ↓
Success Notification
```

---

# 🎯 Summary

Monitoring in GitHub Actions includes:

* Workflow logs
* Step logs
* Re-run capability
* Debug mode
* Graph visualization
* Audit logs
* Health checks

If you master monitoring → You can troubleshoot any CI/CD issue.

---
# 1️⃣4️⃣ GitHub CLI & API (Automation Beyond YAML)

## 🛠️ Why Use CLI & API?

![Image](https://media2.dev.to/dynamic/image/width%3D800%2Cheight%3D%2Cfit%3Dscale-down%2Cgravity%3Dauto%2Cformat%3Dauto/https%3A%2F%2Fgithub.com%2FLadyKerr%2Fgh-cli-example-repo%2Fassets%2F47188731%2F9124f58c-7556-4494-9616-4a9c608aa7f9)

![Image](https://user-images.githubusercontent.com/98482/84171218-327e7a80-aa40-11ea-8cd1-5177fc2d0e72.png)

![Image](https://s3.us-west-1.wasabisys.com/idbwmedia.com/images/api/postman_curl_request5.png)

![Image](https://www.codejava.net/images/articles/rest-api/curl-crud/cur_test_create_rest_api.png)

While **GitHub Actions** runs pipelines, sometimes you need to:

* Trigger workflows manually via script
* Fetch workflow run status
* Cancel runs automatically
* Integrate with external systems
* Automate DevOps dashboards

That’s where CLI & API come in.

---

# 🔹 14.1 GitHub CLI (`gh`)

Official CLI tool from **GitHub**.

Install:

```bash
brew install gh        # macOS
sudo apt install gh    # Linux
```

Login:

```bash
gh auth login
```

---

# 🔹 14.2 Workflow Commands

## 📌 List Workflows

```bash
gh workflow list
```

Example Output:

```text
CI Pipeline
Deploy Production
Terraform Apply
```

---

## ▶️ Run a Workflow Manually

```bash
gh workflow run ci.yml
```

With inputs:

```bash
gh workflow run deploy.yml -f environment=prod
```

---

## 📊 List Workflow Runs

```bash
gh run list
```

Shows:

* Run ID
* Status
* Branch
* Duration

---

## 🔍 View Run Details

```bash
gh run view 123456
```

View logs:

```bash
gh run view 123456 --log
```

---

## ❌ Cancel a Run

```bash
gh run cancel 123456
```

Useful in:

* Emergency rollback
* Duplicate deploy prevention

---

# 🔹 14.3 Automation Example (Shell Script)

```bash
#!/bin/bash

gh workflow run deploy.yml -f environment=staging
sleep 10
gh run list
```

Used in:

* Release automation
* Scheduled operations

---

# 🔹 14.4 GitHub REST API (Advanced Integration)

API Base:

```text
https://api.github.com
```

Example: List workflow runs

```bash
curl -H "Authorization: Bearer TOKEN" \
https://api.github.com/repos/OWNER/REPO/actions/runs
```

Trigger workflow dispatch:

```bash
curl -X POST \
-H "Authorization: Bearer TOKEN" \
-H "Accept: application/vnd.github+json" \
https://api.github.com/repos/OWNER/REPO/actions/workflows/deploy.yml/dispatches \
-d '{"ref":"main"}'
```

Use case:

* Trigger from external CI system
* Integrate with Jenkins
* Connect with internal tools

---

# 🔹 14.5 GitHub GraphQL API

More flexible than REST.

Single endpoint:

```text
https://api.github.com/graphql
```

Example query:

```graphql
{
  repository(owner: "org", name: "repo") {
    workflows(first: 10) {
      nodes {
        name
      }
    }
  }
}
```

Best for:

* Custom dashboards
* Enterprise reporting
* Advanced analytics

---

# 🔹 14.6 CI/CD Dashboard Automation

You can:

* Fetch deployment status
* Track failed runs
* Build Slack notifications
* Auto-generate reports

Example Flow:

```text
CI Run Completed
   ↓
API Fetch Status
   ↓
Send Slack Alert
   ↓
Store Metrics
```

---

# 🔹 14.7 Secure API Usage

⚠️ Important:

* Use Personal Access Tokens (PAT) securely
* Use fine-grained tokens
* Never expose tokens in logs
* Rotate tokens regularly

Best practice:

* Use GitHub App authentication for enterprise systems

---

# 🔹 14.8 Real DevOps Use Case (Your Path)

For Docker + Terraform + EKS:

You can:

* Trigger production deploy from CLI
* Cancel running Terraform apply
* Fetch deployment logs automatically
* Create custom DevOps monitoring dashboard

Example:

```bash
gh workflow run production.yml
```

---

# 🔹 14.9 When to Use What?

| Tool          | Use Case                 |
| ------------- | ------------------------ |
| YAML Workflow | Standard CI/CD           |
| GitHub CLI    | Manual/Script automation |
| REST API      | System integration       |
| GraphQL API   | Advanced reporting       |

---

# 🔥 Enterprise Pattern

Large companies use:

```text
GitHub Actions
   ↓
REST API
   ↓
Internal Monitoring System
   ↓
Slack / Email Alerts
```

Automated DevOps ecosystem.

---

# 🎯 Summary

GitHub CLI & API allow you to:

* Trigger workflows programmatically
* Monitor runs
* Cancel deployments
* Integrate external tools
* Build DevOps dashboards

Mastering this → You move from pipeline user to DevOps automation engineer.

---
