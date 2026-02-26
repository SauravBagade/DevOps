---

# 🚀 GitHub Actions Documentation – Index

---

## 1️⃣ Introduction to GitHub Actions

* 1.1 What is GitHub Actions
* 1.2 Why GitHub Actions is Used
* 1.3 CI vs CD vs CI/CD
* 1.4 GitHub Actions Architecture
* 1.5 GitHub Actions vs Jenkins
* 1.6 GitHub Actions vs GitLab CI
* 1.7 Use Cases (DevOps, Automation, Deployment)

---

## 2️⃣ Core Concepts

* 2.1 Workflow
* 2.2 Event
* 2.3 Job
* 2.4 Step
* 2.5 Runner
* 2.6 Action
* 2.7 Marketplace
* 2.8 Artifacts
* 2.9 Secrets
* 2.10 Environment Variables
* 2.11 Matrix Strategy

---

## 3️⃣ Workflow File Structure

* 3.1 `.github/workflows/` directory
* 3.2 YAML Syntax
* 3.3 Basic Workflow Structure
* 3.4 `name:`
* 3.5 `on:` triggers
* 3.6 `jobs:`
* 3.7 `runs-on:`
* 3.8 `steps:`
* 3.9 `uses:`
* 3.10 `run:`

---

## 4️⃣ Events (Triggers)

* 4.1 `push`
* 4.2 `pull_request`
* 4.3 `workflow_dispatch`
* 4.4 `schedule` (CRON)
* 4.5 `release`
* 4.6 `workflow_call`
* 4.7 `repository_dispatch`
* 4.8 `issues`
* 4.9 `pull_request_target`
* 4.10 Multiple Triggers

---

## 5️⃣ Runners

* 5.1 GitHub Hosted Runners
* 5.2 Self-hosted Runners
* 5.3 Supported OS (Ubuntu, Windows, macOS)
* 5.4 Runner Labels
* 5.5 Custom Runners

---

## 6️⃣ Jobs & Steps

* 6.1 Single Job Workflow
* 6.2 Multiple Jobs
* 6.3 Job Dependencies (`needs`)
* 6.4 Conditional Jobs (`if`)
* 6.5 Step Conditions
* 6.6 Continue on Error

---

## 7️⃣ Actions

* 7.1 Pre-built Actions
* 7.2 Creating Custom Action
* 7.3 JavaScript Action
* 7.4 Docker Action
* 7.5 Composite Action
* 7.6 Using Marketplace Actions

---

## 8️⃣ Environment & Secrets

* 8.1 Repository Secrets
* 8.2 Organization Secrets
* 8.3 Environment Secrets
* 8.4 Encrypted Secrets
* 8.5 Accessing Secrets in Workflow
* 8.6 Variables vs Secrets

---

## 9️⃣ Matrix Builds

* 9.1 What is Matrix Strategy
* 9.2 Multi-Version Testing (Node, Python, Java)
* 9.3 OS Matrix
* 9.4 Include & Exclude
* 9.5 Fail Fast Option

---

## 🔟 Artifacts & Caching

* 10.1 Upload Artifact
* 10.2 Download Artifact
* 10.3 Cache Dependencies
* 10.4 Cache Key Strategy
* 10.5 Restore Keys

---

## 1️⃣1️⃣ Deployment

* 11.1 Deploy to AWS
* 11.2 Deploy to Azure
* 11.3 Deploy to GCP
* 11.4 Deploy to Docker Hub
* 11.5 Deploy to Kubernetes
* 11.6 GitHub Pages Deployment

---

## 1️⃣2️⃣ Reusable Workflows

* 12.1 `workflow_call`
* 12.2 Input Parameters
* 12.3 Outputs
* 12.4 Sharing Across Repositories

---

## 1️⃣3️⃣ Advanced Topics

* 13.1 Concurrency Control
* 13.2 Required Status Checks
* 13.3 Environments & Protection Rules
* 13.4 OIDC Authentication
* 13.5 Security Best Practices
* 13.6 Action Version Pinning
* 13.7 Workflow Permissions
* 13.8 Debugging Workflows
* 13.9 Performance Optimization
* 13.10 Cost Optimization

---

## 1️⃣4️⃣ Monitoring & Logs

* 14.1 Workflow Logs
* 14.2 Enable Debug Logs
* 14.3 Re-run Failed Jobs
* 14.4 Download Logs
* 14.5 Audit Logs

---

## 1️⃣5️⃣ GitHub Actions CLI & API

* 15.1 `gh workflow list`
* 15.2 `gh workflow run`
* 15.3 `gh run list`
* 15.4 GitHub REST API
* 15.5 GitHub GraphQL API

---
