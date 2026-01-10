# 🟢 **1️⃣ Introduction to Jenkins **

## 🔹 What is Jenkins?

**Jenkins** is an **open-source automation server** used to **build, test, and deploy software automatically**.

👉 Jenkins helps you **remove manual work** from:

* Code building
* Testing
* Deployment
* Automation tasks

📌 In simple words:

> **Jenkins = Automation Engine for CI/CD**

---

## 🔹 Why Jenkins is Used?

Before Jenkins:

* Developers manually built code
* Manual testing
* Manual deployment
* Errors were common ❌

With Jenkins:

* Code is **automatically built**
* Tests run automatically
* Deployment happens automatically
* Faster delivery 🚀
* Fewer errors ✅

### Jenkins is used for:

* CI (Continuous Integration)
* CD (Continuous Delivery / Deployment)
* DevOps automation
* Scheduled jobs
* Infrastructure automation

---

## 🔹 Jenkins History

* 2004 → Started as **Hudson**
* 2011 → Renamed to **Jenkins**
* Community-driven & open-source
* Widely used in enterprises

📌 Today Jenkins is one of the **most popular CI/CD tools in the DevOps world**.

---

## 🔹 Jenkins Features

✔ Open-source & free
✔ Plugin-based (1800+ plugins)
✔ Works with any language (Java, Python, Node.js, Go, etc.)
✔ Integrates with Docker, Kubernetes, Git, AWS
✔ Scalable (Master–Agent model)
✔ Supports pipelines as code

---

## 🔹 Jenkins vs Other CI/CD Tools

### Jenkins vs GitHub Actions

| Jenkins             | GitHub Actions |
| ------------------- | -------------- |
| Self-hosted         | GitHub managed |
| More control        | Less control   |
| Complex setup       | Easy setup     |
| Enterprise friendly | GitHub-only    |

---

### Jenkins vs GitLab CI

| Jenkins          | GitLab CI   |
| ---------------- | ----------- |
| Tool independent | GitLab only |
| Plugin-based     | Built-in    |
| More flexible    | Easier      |

---

### Jenkins vs AWS DevOps

| Jenkins        | AWS DevOps       |
| -------------- | ---------------- |
| Cloud agnostic | AWS specific     |
| Open-source    | Managed services |
| Full control   | Less control     |

---

## 🔹 Jenkins Use Cases

* DevOps CI/CD pipelines
* Automation jobs
* Nightly builds
* Infrastructure deployment
* Test automation
* Microservices CI/CD

---

# 🟢 **2️⃣ CI/CD Basics (Very Important)**

## 🔹 What is CI (Continuous Integration)?

CI means:

* Developers **push code frequently**
* Code is **automatically built & tested**

📌 Goal:

> Detect bugs **early**

### CI Steps:

1. Developer pushes code
2. Jenkins pulls code
3. Build starts
4. Tests run
5. Report generated

---

## 🔹 What is CD?

CD has **two meanings**:

### 1️⃣ Continuous Delivery

* Code is ready to deploy
* Deployment is **manual approval**

### 2️⃣ Continuous Deployment

* Code is **automatically deployed**
* No human intervention

---

## 🔹 CI/CD Pipeline Stages

Typical pipeline:

```
Code → Build → Test → Scan → Deploy
```

Stages explained:

* **Build** – Compile code
* **Test** – Unit/Integration tests
* **Scan** – Security / quality checks
* **Deploy** – Release to server

---

## 🔹 DevOps Lifecycle with Jenkins

Jenkins sits at the **center** of DevOps:

```
Plan → Code → Build → Test → Release → Deploy → Monitor
```

Jenkins automates:

* Build
* Test
* Deploy

---

## 🔹 Manual vs Automated Deployment

| Manual          | Automated   |
| --------------- | ----------- |
| Slow            | Fast        |
| Error-prone     | Reliable    |
| Not scalable    | Scalable    |
| Human dependent | Tool driven |

📌 **DevOps = Automation → Jenkins**

---

# 🟢 **3️⃣ Jenkins Architecture **

## 🔹 Jenkins Architecture Overview

Jenkins follows **Controller–Agent architecture**.

### Components:

* Controller (Master)
* Agent (Node)
* Executor
* Workspace

---

## 🔹 Jenkins Controller (Master)

Controller responsibilities:

* Manages jobs
* Schedules builds
* Stores configuration
* UI access
* Plugin management

📌 **Controller does NOT do heavy work**

---

## 🔹 Jenkins Agent (Node)

Agent responsibilities:

* Executes builds
* Runs jobs
* Uses system resources

Types of agents:

* Linux
* Windows
* Docker
* Kubernetes

---

## 🔹 Executor Concept

* Executor = **parallel build slot**
* Each executor can run **one job**
* More executors → more parallel builds

---

## 🔹 Workspace

* Directory where job runs
* Code is checked out here
* Build artifacts stored

Example:

```
/var/lib/jenkins/workspace/my-job
```

---

## 🔹 Jenkins Home Directory

Important directory:

```
/var/lib/jenkins
```

Contains:

* Jobs
* Plugins
* Config files
* Credentials
* Logs

📌 **Backup this directory = backup Jenkins**

---

## 🔹 Jenkins Ports & Processes

* Default port: **8080**
* Java-based application
* Runs as a service

---

## Jenkins Architecture – Diagram

```

                    ┌───────────────────────────┐
                    │        Users / DevOps      │
                    │  (Browser / CLI / API)     │
                    └─────────────┬─────────────┘
                                  │
                                  ▼
                   ┌─────────────────────────────┐
                   │     Jenkins Controller       │
                   │  (Master / Control Plane)   │
                   │─────────────────────────────│
                   │ • Web UI                    │
                   │ • Job Configuration         │
                   │ • Pipeline Scheduling       │
                   │ • Plugin Management         │
                   │ • Credential Store          │
                   │ • Build Queue               │
                   └─────────────┬───────────────┘
                                 │ Assigns Jobs
              ┌──────────────────┼──────────────────┐
              ▼                  ▼                  ▼
┌─────────────────────┐ ┌─────────────────────┐ ┌─────────────────────┐
│   Jenkins Agent 1   │ │   Jenkins Agent 2   │ │   Jenkins Agent N   │
│ (Linux / Windows)  │ │   (Docker / VM)     │ │   (Kubernetes Pod)  │
│─────────────────────│ │─────────────────────│ │─────────────────────│
│ • Executor(s)       │ │ • Executor(s)       │ │ • Executor(s)       │
│ • Workspace         │ │ • Workspace         │ │ • Workspace         │
│ • Build Tools       │ │ • Build Tools       │ │ • Build Tools       │
└──────────┬──────────┘ └──────────┬──────────┘ └──────────┬──────────┘
           │                         │                         │
           ▼                         ▼                         ▼
      Build / Test / Deploy    Build / Test / Deploy    Build / Test / Deploy


```

## Jenkins Architecture in CI/CD Flow

```
Git Push
   ↓
Webhook Trigger
   ↓
Jenkins Controller
   ↓
Select Agent
   ↓
Checkout Code
   ↓
Build & Test
   ↓
Docker Build
   ↓
Deploy

```

# 🟢 **4️⃣ Jenkins UI Basics (Hands-on Understanding)**

## 🔹 Jenkins Dashboard

* Main landing page
* List of jobs
* Build status (✔ ❌)

---

## 🔹 Jobs / Projects

A **job** = task Jenkins performs

Types:

* Freestyle
* Pipeline
* Multibranch

---

## 🔹 Console Output

* Shows real-time logs
* Used for debugging
* Most important screen 🔥

---

## 🔹 Build History

* Shows previous builds
* Success / Failure
* Build numbers

---

## 🔹 Manage Jenkins

Admin control panel:

* Plugins
* Nodes
* Credentials
* System configuration
* Security

---

## 🔹 System Configuration

* Tools (Java, Git, Maven)
* Global environment variables
* Agent configuration

---

# 🟡 **5️⃣ Jenkins Job Types **

In **Jenkins**, a **Job (Project)** is a task Jenkins runs (build, test, deploy, etc.).

---

## 🔹 1. Freestyle Job

📌 **Oldest & simplest job type**

### Characteristics:

* UI-based (click & configure)
* No code required
* Good for beginners
* Less flexible

### Used for:

* Simple builds
* Learning Jenkins basics
* Legacy projects

---

## 🔹 2. Pipeline Job

📌 **Modern & recommended**

### Characteristics:

* Written as code (`Jenkinsfile`)
* Version controlled
* Supports complex workflows
* CI/CD best practice

### Used for:

* Real DevOps pipelines
* Automation
* Production systems

---

## 🔹 3. Multibranch Pipeline

📌 Automatically creates pipelines for each Git branch

### Features:

* Detects branches automatically
* Each branch has its own pipeline
* Uses `Jenkinsfile` from Git

### Used for:

* Feature branch workflows
* GitHub / GitLab projects

---

## 🔹 4. Maven Project

📌 Specialized job for Java + Maven

* Uses `pom.xml`
* Limited flexibility
* Mostly replaced by Pipeline jobs

---

## 🔹 5. External Job

📌 Used when build is done **outside Jenkins**

* Jenkins only tracks status
* Rarely used today

---

## 🔹 6. Folder / Organization Folder

📌 Used to **organize jobs**

* Folder → logical grouping
* Organization Folder → auto discovers Git repos

---

# 🟡 **6️⃣ Freestyle Jobs (Hands-on Concept)**

## 🔹 What is a Freestyle Job?

A **Freestyle Job** is a **GUI-configured job** where you define:

* Source code
* Build steps
* Triggers
* Post actions

---

## 🔹 Step-by-Step Flow

1. New Item → Freestyle Project
2. Configure Source Code
3. Configure Build Triggers
4. Add Build Steps
5. Add Post-Build Actions
6. Save & Build

---

## 🔹 Source Code Management (SCM)

Most commonly Git:

* Git repository URL
* Branch (`main`, `develop`)
* Credentials (if private repo)

Works with:

* Git
* GitHub / GitLab / Bitbucket

---

## 🔹 Build Triggers

Ways to start a build:

* Manual (Build Now)
* SCM Polling
* Webhook
* Cron schedule

---

## 🔹 Build Steps

Examples:

* Execute shell (`sh`)
* Execute Windows batch
* Maven build
* Gradle build

Example:

```bash
mvn clean install
```

---

## 🔹 Post-Build Actions

Runs **after build finishes**:

* Archive artifacts
* Email notification
* Trigger another job
* Publish reports

---

## 🔹 Real Example (Freestyle)

Use case:

> Pull code → Build → Test → Notify

📌 **Limitation:**
❌ Not scalable
❌ No pipeline as code

👉 That’s why **Pipeline Jobs** exist.

---

# 🟡 **7️⃣ Jenkins Pipeline Basics**

## 🔹 What is Jenkins Pipeline?

A **Pipeline** is:

> **CI/CD workflow written as code**

Stored in:

* Jenkins UI (inline)
* Git repository (`Jenkinsfile`) ✅ recommended

---

## 🔹 Why Pipeline?

| Freestyle       | Pipeline      |
| --------------- | ------------- |
| GUI based       | Code based    |
| Hard to version | Git versioned |
| Limited         | Powerful      |
| Not scalable    | Scalable      |

---

## 🔹 Pipeline Structure (Basic)

```groovy
pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Building...'
      }
    }
  }
}
```

---

## 🔹 Jenkinsfile

📌 `Jenkinsfile` = Pipeline definition file

Benefits:

* Stored in Git
* Code review
* Rollback
* DevOps best practice

---

## 🔹 Inline vs Jenkinsfile

| Inline            | Jenkinsfile     |
| ----------------- | --------------- |
| Stored in Jenkins | Stored in Git   |
| Not versioned     | Versioned       |
| Not recommended   | ✅ Best practice |

---

# 🟡 **8️⃣ Declarative Pipeline (Most Important)**

## 🔹 What is Declarative Pipeline?

* Simple
* Structured
* Opinionated
* Easy to read

📌 **Best choice for beginners**

---

## 🔹 Core Blocks Explained

### `pipeline`

Root block of pipeline

### `agent`

Where pipeline runs

```groovy
agent any
```

---

### `stages` & `steps`

```groovy
stages {
  stage('Test') {
    steps {
      echo 'Testing'
    }
  }
}
```

---

### `environment`

Define variables

```groovy
environment {
  APP_ENV = 'prod'
}
```

---

### `parameters`

User inputs

```groovy
parameters {
  string(name: 'ENV', defaultValue: 'dev')
}
```

---

### `tools`

Auto install tools

```groovy
tools {
  maven 'maven3'
}
```

---

### `when`

Conditional execution

```groovy
when {
  branch 'main'
}
```

---

### `post`

Runs after pipeline

```groovy
post {
  success { echo 'Success' }
  failure { echo 'Failed' }
}
```

---

## 🔹 Declarative Pipeline Example

```groovy
pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Building App'
      }
    }
    stage('Deploy') {
      steps {
        echo 'Deploying App'
      }
    }
  }
}
```

---

# 🟡 **9️⃣ Scripted Pipeline (Advanced Logic)**

## 🔹 What is Scripted Pipeline?

* Written fully in **Groovy**
* Very flexible
* Less readable
* More control

📌 Used when **Declarative is not enough**

---

## 🔹 Basic Scripted Structure

```groovy
node {
  stage('Build') {
    echo 'Building'
  }
}
```

---

## 🔹 Groovy Basics

* Variables
* Loops
* Conditions
* Functions

Example:

```groovy
for (i in 1..3) {
  echo "Build ${i}"
}
```

---

## 🔹 Scripted Pipeline Example

```groovy
node {
  stage('Checkout') {
    git 'https://github.com/example/repo.git'
  }
  stage('Build') {
    sh 'mvn clean install'
  }
}
```

---

## 🔹 Declarative vs Scripted

| Declarative | Scripted     |
| ----------- | ------------ |
| Easy        | Complex      |
| Structured  | Flexible     |
| Recommended | Advanced use |

---

# 🔵 **🔟 Jenkinsfile **

## 🔹 What is Jenkinsfile?

A **Jenkinsfile** is a **text file** that defines your **entire CI/CD pipeline as code**.

📌 Stored inside your Git repository.

```text
repo/
 ├── src/
 ├── Dockerfile
 └── Jenkinsfile
```

Uses:

* CI pipelines
* CD pipelines
* Docker builds
* Kubernetes deployments

---

## 🔹 Why Jenkinsfile is Important

✔ Version controlled
✔ Code review possible
✔ Reproducible pipelines
✔ Industry best practice

---

## 🔹 Best Practices

* Always store Jenkinsfile in Git
* One pipeline per repo
* Use declarative syntax
* Avoid hardcoded secrets
* Keep stages small
* Use `post` blocks

---

## 🔹 CI Pipeline Example

```groovy
pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps { git 'https://github.com/org/app.git' }
    }
    stage('Build') {
      steps { sh 'mvn clean package' }
    }
    stage('Test') {
      steps { sh 'mvn test' }
    }
  }
}
```

---

## 🔹 CD Pipeline Example

```groovy
stage('Deploy') {
  steps {
    sh 'scp target/app.jar server:/apps/'
  }
}
```

---

## 🔹 Docker Pipeline Example

```groovy
stage('Docker Build') {
  steps {
    sh 'docker build -t app:1.0 .'
  }
}
```

---

## 🔹 Kubernetes Pipeline Example

```groovy
stage('Deploy to K8s') {
  steps {
    sh 'kubectl apply -f deployment.yaml'
  }
}
```

---

# 🔵 **1️⃣1️⃣ Credentials Management (Security Critical)**

## 🔹 Why Credentials are Needed?

To connect Jenkins with:

* Git
* Docker Registry
* Cloud (AWS)
* Servers (SSH)

---

## 🔹 Credential Types

* **Secret Text** → tokens, API keys
* **SSH Keys** → server access
* **Username/Password** → legacy
* **Tokens** → GitHub, GitLab

---

## 🔹 Credential Scope

| Scope  | Meaning               |
| ------ | --------------------- |
| Global | Available to all jobs |
| System | Jenkins internal use  |

---

## 🔹 Using Credentials in Pipeline

```groovy
withCredentials([string(credentialsId: 'token', variable: 'TOKEN')]) {
  sh 'echo $TOKEN'
}
```

---

## 🔹 Best Practices

❌ Never hardcode secrets
✅ Rotate credentials
✅ Use least privilege
✅ Mask sensitive output

---

# 🔵 **1️⃣2️⃣ Build Triggers (Automation Entry Point)**

## 🔹 SCM Polling

* Jenkins checks Git periodically
* Uses cron syntax

```text
H/5 * * * *
```

---

## 🔹 GitHub Webhooks

* GitHub notifies Jenkins
* Faster & recommended

Uses **GitHub Webhooks**

---

## 🔹 Cron Scheduling

```text
0 2 * * *
```

Runs daily at 2 AM.

---

## 🔹 Parameterized Triggers

Trigger job with input:

```groovy
parameters {
  choice(name: 'ENV', choices: ['dev','prod'])
}
```

---

## 🔹 Trigger Another Job

* Post-build trigger
* Upstream/downstream jobs

---

# 🔵 **1️⃣3️⃣ Environment Variables (Pipeline Control)**

## 🔹 What are Environment Variables?

Key-value pairs used in pipelines.

---

## 🔹 Built-in Variables

* `BUILD_ID`
* `JOB_NAME`
* `WORKSPACE`
* `BRANCH_NAME`

---

## 🔹 Custom Variables

```groovy
environment {
  ENV = 'dev'
}
```

---

## 🔹 Secrets as Env Variables

```groovy
environment {
  DB_PASS = credentials('db-pass')
}
```

---

## 🔹 Debugging Env Variables

```groovy
sh 'env'
```

---

# 🔵 **1️⃣4️⃣ Parameters in Pipeline**

## 🔹 What are Parameters?

User inputs before build starts.

---

## 🔹 Types

* String
* Choice
* Boolean
* File

---

## 🔹 Example

```groovy
parameters {
  string(name: 'VERSION', defaultValue: '1.0')
  booleanParam(name: 'DEPLOY', defaultValue: true)
}
```

---

## 🔹 Use Case

* Select environment
* Control deployments
* Rollbacks

---

# 🔵 **1️⃣5️⃣ Plugins & Extensions**

## 🔹 Why Plugins?

Jenkins core is small → plugins add power.

---

## 🔹 Important Plugins

* Git / GitHub
* Docker
* Pipeline
* Credentials
* Blue Ocean
* SonarQube
* Kubernetes

---

## 🔹 Plugin Best Practices

❌ Don’t install everything
✅ Update regularly
✅ Remove unused plugins

---

# 🔵 **1️⃣6️⃣ Jenkins + Git & GitHub**

## 🔹 Webhook Integration

Flow:

```
Git Push → Webhook → Jenkins Build
```

---

## 🔹 Build on PR / Push

* CI for every commit
* PR validation

---

## 🔹 Multibranch Pipelines

* One pipeline per branch
* Auto discovery
* Uses Jenkinsfile

---

## 🔹 Branch-based Workflow

* main → prod
* develop → staging
* feature/* → testing

---

# 🔵 **1️⃣7️⃣ Jenkins + Docker**

## 🔹 Jenkins inside Docker

Benefits:

* Portable
* Easy setup
* Clean environment

---

## 🔹 Build & Tag Image

```groovy
sh 'docker build -t app:${BUILD_NUMBER} .'
```

---

## 🔹 Push to Registry

* DockerHub
* AWS ECR

```groovy
sh 'docker push app:1.0'
```

---

## 🔹 Docker Pipeline Example

```groovy
pipeline {
  agent any
  stages {
    stage('Docker Build') {
      steps {
        sh 'docker build -t app .'
      }
    }
  }
}
```

---

# 🔵 **1️⃣8️⃣ Jenkins + Kubernetes**

## 🔹 Deploy to Kubernetes

```bash
kubectl apply -f deployment.yaml
```

---

## 🔹 Helm Usage

```bash
helm upgrade --install app chart/
```

---

## 🔹 Dynamic Agents (Game Changer)

* Jenkins spins up pods
* No fixed agents
* Auto scale builds

---

## 🔹 Deployment Strategies

* Rolling updates
* Blue-Green
* Canary

---

# 🔴 **1️⃣9️⃣ Distributed Builds & Scaling**

## 🔹 Why Distributed Builds?

* Faster builds
* Scalability
* Heavy workloads

---

## 🔹 Controller + Agent Setup

* Controller schedules jobs
* Agents execute jobs

---

## 🔹 Agent Types

* SSH agents
* Docker agents
* Kubernetes agents

---

## 🔹 Executor Tuning

* Each executor = 1 parallel job
* Tune based on CPU/RAM

---

## 🔹 Distributed Workspace

* Shared storage
* Artifact management

---

# 🔴 **2️⃣0️⃣ Security & Hardening (Production Critical)**

## 🔹 Why Jenkins Security is Important?

Jenkins controls:

* Source code
* Credentials
* Production deployments
* Cloud infrastructure

❌ One misconfiguration = **full system compromise**

---

## 🔹 Authentication (Who can login?)

Ways to login into **Jenkins**:

### Authentication Methods

* Jenkins local users
* LDAP / Active Directory
* OAuth (GitHub, Google)
* SSO (Enterprise)

📌 **Best practice**:
✔ Integrate Jenkins with **LDAP / SSO**

---

## 🔹 Authorization (What users can do?)

Controls **permissions**.

### Authorization Strategies

* Anyone can do anything ❌
* Matrix-based security
* Role-Based Strategy (RBAC) ✅

---

## 🔹 RBAC (Role-Based Access Control)

Users get **roles**, not full access.

### Example Roles

| Role   | Permissions       |
| ------ | ----------------- |
| Admin  | Full control      |
| Dev    | Build & read jobs |
| Viewer | Read-only         |

📌 Implement using **Role Strategy Plugin**

---

## 🔹 Secrets Management

* Store secrets in Jenkins Credentials
* Inject secrets at runtime
* Mask secrets in logs

Optional integrations:

* HashiCorp Vault
* AWS Secrets Manager

---

## 🔹 Plugin Security

* Plugins = attack surface
* Update plugins regularly
* Remove unused plugins
* Use LTS Jenkins version

---

## 🔹 Credential Rotation

* Rotate keys periodically
* Avoid long-lived secrets
* Use short-lived tokens

---

# 🔴 **2️⃣1️⃣ Notifications & Messaging**

## 🔹 Why Notifications Matter?

* Faster incident response
* Build failures are visible
* Dev teams react quickly

---

## 🔹 Email Notifications

* SMTP configuration
* Send build status emails
* Useful for legacy teams

---

## 🔹 Slack Integration

Integrate Jenkins with **Slack**:

* Build success/failure alerts
* Channel-based notifications
* Real-time feedback

Example:

```groovy
post {
  failure {
    slackSend channel: '#ci-alerts', message: 'Build Failed'
  }
}
```

---

## 🔹 Microsoft Teams

* Webhook-based
* Enterprise friendly
* Similar to Slack

---

## 🔹 Webhooks

* Trigger external systems
* Integrate monitoring tools
* CI/CD event-driven workflows

---

## 🔹 Alerting Strategy

✔ Notify on failure
✔ Notify on recovery
❌ Avoid notification spam

---

# 🔴 **2️⃣2️⃣ Backup & Restore (Disaster Recovery)**

## 🔹 Why Backup Jenkins?

Jenkins stores:

* Jobs
* Pipelines
* Credentials
* Plugins
* Build history

📌 **Without backup → total loss**

---

## 🔹 Jenkins Home Backup

Critical directory:

```text
/var/lib/jenkins
```

Backup includes:

* `jobs/`
* `config.xml`
* `plugins/`
* `credentials.xml`

---

## 🔹 ThinBackup Plugin

Features:

* Scheduled backups
* Config-only backups
* Easy restore

📌 Suitable for **small–medium setups**

---

## 🔹 Enterprise Backup Strategy

* Daily automated backup
* Store backups in:

  * S3
  * NFS
  * Remote storage
* Test restore regularly

---

## 🔹 Disaster Recovery Plan

* Document restore steps
* Keep Jenkins version consistent
* Backup before upgrades

---

# 🔴 **2️⃣3️⃣ Logs & Troubleshooting**

## 🔹 Jenkins Logs Location

Linux default:

```text
/var/log/jenkins/jenkins.log
```

Also check:

* System logs
* Container logs (Docker/K8s)

---

## 🔹 Pipeline Debugging

Most common place:
👉 **Console Output**

Debug tips:

* Use `echo`
* Enable verbose logs
* Break pipeline into stages

---

## 🔹 Webhook Errors

Common issues:

* Wrong webhook URL
* Firewall blocking
* SSL certificate issues

Fix:

* Test webhook manually
* Check GitHub webhook logs

---

## 🔹 Agent Connectivity Issues

Reasons:

* SSH failure
* Network issues
* Resource exhaustion

Solutions:

* Restart agent
* Check executor count
* Validate credentials

---

## 🔹 Common Jenkins Problems

| Issue       | Reason        |
| ----------- | ------------- |
| Build stuck | No executor   |
| Job fails   | Missing tools |
| Slow builds | Low resources |

---

# 🔴 **2️⃣4️⃣ Cloud & DevOps Integrations (Enterprise Level)**

## 🔹 Jenkins + AWS

Integrates with:

* EC2 (agents)
* ECR (Docker images)
* EKS (Kubernetes deploy)
* S3 (artifacts & backups)

Works with **AWS**

---

## 🔹 Jenkins + Terraform

Infrastructure as Code using **Terraform**:

Pipeline flow:

```
Code → terraform plan → terraform apply
```

Used for:

* Infra provisioning
* Environment automation

---

## 🔹 Jenkins + Ansible

Configuration management using **Ansible**

Use cases:

* App deployment
* Server config
* Rolling updates

---

## 🔹 Jenkins + GitOps

Git as source of truth:

* ArgoCD
* Flux

Jenkins handles:

* CI
* Image build

GitOps tool handles:

* CD

---

## 🔹 Jenkins + SonarQube

Code quality & security using **SonarQube**

Checks:

* Bugs
* Vulnerabilities
* Code smells

Pipeline gate:
❌ Fail build if quality gate fails

---
