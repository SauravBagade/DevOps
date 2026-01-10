#  Jenkins Learning Index

A complete Jenkins roadmap designed for **learning, teaching, documentation, and interview preparation**. This guide follows a **Beginner → Intermediate → Advanced → Expert** progression with real-world DevOps focus.

---

## 🟢 Beginner Level (Fundamentals)

### 1️⃣ Introduction to Jenkins

* What is Jenkins
* Why Jenkins is used
* Jenkins history
* Jenkins features
* Jenkins vs other CI/CD tools

  * Jenkins vs GitHub Actions
  * Jenkins vs GitLab CI
  * Jenkins vs AWS DevOps tools
* Jenkins use cases (DevOps, Automation)

---

### 2️⃣ CI/CD Basics

* What is CI (Continuous Integration)
* What is CD (Continuous Delivery vs Continuous Deployment)
* CI/CD pipeline stages
* DevOps lifecycle with Jenkins
* Manual vs Automated deployments

---

### 3️⃣ Jenkins Architecture

* Jenkins architecture overview
* Jenkins Controller (Master)
* Jenkins Agent (Node)
* Executor concept
* Workspace
* Jenkins home directory
* Jenkins ports & processes

---

### 4️⃣ Jenkins UI Basics

* Dashboard overview
* Jobs / Projects
* Console Output
* Build History
* Manage Jenkins
* System configuration

---

## 🟡 Intermediate Level (Hands-on Usage)

### 5️⃣ Job Types

* Freestyle Job
* Pipeline Job
* Multibranch Pipeline
* Maven Project
* External Job
* Folder / Organization Folder

---

### 6️⃣ Freestyle Jobs

* Create Freestyle job
* Source Code Management (Git)
* Build Triggers (Manual / Webhook / SCM Polling)
* Build Steps
* Post-build Actions
* Freestyle job real-time example

---

### 7️⃣ Pipeline Basics

* What is Jenkins Pipeline
* Declarative vs Scripted Pipeline
* Pipeline syntax structure
* Jenkinsfile overview
* Inline pipeline vs Jenkinsfile in Git

---

### 8️⃣ Declarative Pipeline

* pipeline block
* agent / node
* stages and steps
* Environment variables
* Parameters
* Tools
* Post conditions
* when conditions
* Options
* Declarative pipeline example

---

### 9️⃣ Scripted Pipeline

* Scripted pipeline basics
* node block
* Groovy basics
* Stages in scripted pipeline
* Scripted pipeline example
* Declarative vs Scripted comparison

---

## 🔵 Advanced Level (DevOps Integration + CI/CD Projects)

### 🔟 Jenkinsfile (Real CI/CD Use)

* What is Jenkinsfile
* Store Jenkinsfile in Git repository
* Jenkinsfile best practices
* CI pipeline example
* CD pipeline example
* Docker pipeline example
* Kubernetes pipeline example

---

### 1️⃣1️⃣ Credentials Management

* Why credentials are required
* Credential types

  * Secret text
  * SSH keys
  * Tokens
  * Username / Password
* Credential scope (Global / System)
* Using credentials in pipelines
* Credentials security best practices

---

### 1️⃣2️⃣ Build Triggers

* SCM Polling
* GitHub Webhooks
* Cron scheduling
* Parameterized build triggers
* Trigger jobs from another job
* Manual triggers
* Multi-job pipelines

---

### 1️⃣3️⃣ Environment Variables

* What are environment variables
* Built-in Jenkins environment variables
* Custom environment variables
* Using env in pipelines
* Secrets as environment variables
* Debugging environment variables

---

### 1️⃣4️⃣ Parameters in Pipeline

* Parameterized builds
* String parameter
* Choice parameter
* Boolean parameter
* File parameter
* Parameterized workflows

---

### 1️⃣5️⃣ Plugins & Extensions

* Git / GitHub plugins
* Docker plugin
* Pipeline plugin
* Credentials plugin
* Blue Ocean
* SonarQube
* Kubernetes plugin

---

### 1️⃣6️⃣ Jenkins + Git & GitHub

* Webhook integration
* Build on Push / Pull Request
* Multibranch pipelines
* Branch-based workflows

---

### 1️⃣7️⃣ Jenkins + Docker

* Jenkins inside Docker
* Build Docker image and tagging
* Push image to DockerHub / ECR
* Docker pipeline example

---

### 1️⃣8️⃣ Jenkins + Kubernetes

* Deploy applications to Kubernetes
* Helm integration
* Dynamic agents using Kubernetes Pods
* Rolling updates
* Blue-Green deployments

---

## 🔴 Expert Level (Production + Cloud + DevSecOps)

### 1️⃣9️⃣ Distributed Builds & Scaling

* Controller + Agent setup
* SSH Agents
* Docker Agents
* Executor tuning
* Distributed workspace

---

### 2️⃣0️⃣ Security & Hardening

* Authentication methods
* Authorization strategies
* RBAC (Role-Based Access Control)
* Secrets management
* Plugin security
* Credential rotation

---

### 2️⃣1️⃣ Notifications & Messaging

* Email notifications
* Slack integration
* Microsoft Teams
* Webhooks
* Success / Failure alerts

---

### 2️⃣2️⃣ Backup & Restore

* Jenkins home backup
* ThinBackup plugin
* Disaster recovery strategies

---

### 2️⃣3️⃣ Logs & Troubleshooting

* Jenkins logs location
* Pipeline debugging techniques
* Webhook errors
* Agent connectivity issues

---

### 2️⃣4️⃣ Cloud & DevOps Integrations

* Jenkins with AWS (EC2, ECR, EKS, S3)
* Jenkins + Terraform (Infrastructure as Code)
* Jenkins + Ansible (Configuration Management)
* Jenkins + GitOps (ArgoCD, Flux)
* Jenkins + SonarQube (Code Quality)

---