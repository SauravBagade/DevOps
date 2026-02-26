---

# 🚀 GitHub Actions –Index

---

## 1️⃣ Introduction to GitHub Actions

* 1.1 What is GitHub Actions
* 1.2 Why GitHub Actions is Used
* 1.3 CI vs CD vs CI/CD
* 1.4 Architecture Overview
* 1.5 GitHub Actions vs Jenkins
* 1.6 GitHub Actions vs GitLab CI
* 1.7 Real DevOps Use Cases

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

* 3.1 `.github/workflows/` Directory
* 3.2 YAML Syntax
* 3.3 Basic Workflow Structure
* 3.4 `name:`
* 3.5 `on:`
* 3.6 `jobs:`
* 3.7 `runs-on:`
* 3.8 `steps:`
* 3.9 `uses:`
* 3.10 `run:`
* 3.11 `with:`
* 3.12 `env:`
* 3.13 `needs:`
* 3.14 `if:`
* 3.15 `strategy:`
* 3.16 `permissions:`
* 3.17 `concurrency:`

---

## 4️⃣ Events (Triggers)

* 4.1 push
* 4.2 pull_request
* 4.3 pull_request_target
* 4.4 workflow_dispatch
* 4.5 schedule (CRON)
* 4.6 release
* 4.7 workflow_call
* 4.8 repository_dispatch
* 4.9 issues
* 4.10 issue_comment
* 4.11 create
* 4.12 delete
* 4.13 fork
* 4.14 check_run
* 4.15 Multiple Events

---

## 5️⃣ Runners

* 5.1 GitHub Hosted Runners
* 5.2 Self-hosted Runners
* 5.3 Runner Labels
* 5.4 OS Versions
* 5.5 Hardware Specs
* 5.6 Scaling
* 5.7 Security Considerations
* 5.8 Runner Groups

---

## 6️⃣ Jobs & Dependencies

* 6.1 Single Job
* 6.2 Parallel Jobs
* 6.3 Sequential Jobs (`needs`)
* 6.4 Multiple Dependencies
* 6.5 Passing Outputs
* 6.6 Conditional Jobs
* 6.7 continue-on-error
* 6.8 timeout-minutes
* 6.9 Job-level permissions

---

## 7️⃣ Secrets & Security

* 7.1 Repository Secrets
* 7.2 Organization Secrets
* 7.3 Environment Secrets
* 7.4 Variables vs Secrets
* 7.5 OIDC Authentication
* 7.6 Environment Protection Rules
* 7.7 Masking Secrets
* 7.8 Branch Protection
* 7.9 Least Privilege Permissions
* 7.10 Security Best Practices

---

## 8️⃣ Matrix Strategy

* 8.1 Basic Matrix
* 8.2 Multi-OS Matrix
* 8.3 Multi-Dimensional Matrix
* 8.4 include / exclude
* 8.5 fail-fast
* 8.6 max-parallel
* 8.7 Dynamic Matrix
* 8.8 Production Use Cases

---

## 9️⃣ Artifacts & Caching

* 9.1 Upload Artifact
* 9.2 Download Artifact
* 9.3 Retention Policies
* 9.4 Cache Basics
* 9.5 Cache Keys
* 9.6 restore-keys
* 9.7 Docker Layer Caching
* 9.8 Terraform Plan Artifact
* 9.9 Performance Best Practices

---

## 🔟 Deployment Patterns

* 10.1 Docker Build & Push
* 10.2 EC2 Deployment
* 10.3 EKS / Kubernetes Deployment
* 10.4 Terraform Deployment
* 10.5 Blue-Green Deployment
* 10.6 Canary Deployment
* 10.7 GitHub Pages Deployment
* 10.8 Multi-Environment Pipeline
* 10.9 CI/CD Separation
* 10.10 Production Blueprint

---

## 1️⃣1️⃣ Reusable Workflows

* 11.1 workflow_call
* 11.2 Inputs & Outputs
* 11.3 Passing Secrets
* 11.4 Version Pinning
* 11.5 Cross-Repository Reuse
* 11.6 Reusable Workflow vs Composite
* 11.7 Enterprise Architecture Pattern

---

## 1️⃣2️⃣ Advanced Topics

* 12.1 Concurrency
* 12.2 Workflow-level concurrency
* 12.3 Cost Optimization
* 12.4 Performance Optimization
* 12.5 Permission Hardening
* 12.6 Required Status Checks
* 12.7 Environment Approvals
* 12.8 Debugging
* 12.9 Enterprise CI/CD Architecture

---

## 1️⃣3️⃣ Monitoring & Logs

* 13.1 Workflow Run View
* 13.2 Job Logs
* 13.3 Step Logs
* 13.4 Re-run Jobs
* 13.5 Debug Mode
* 13.6 Download Logs
* 13.7 Workflow Graph
* 13.8 Audit Logs
* 13.9 Health Checks

---

## 1️⃣4️⃣ GitHub CLI & API

* 14.1 GitHub CLI Setup
* 14.2 gh workflow Commands
* 14.3 gh run Commands
* 14.4 REST API Usage
* 14.5 GraphQL API
* 14.6 Automation Scripts
* 14.7 Secure API Usage
* 14.8 Enterprise Integration

---

## 1️⃣5️⃣ Actions

* 15.1 Pre-built Actions
* 15.2 Creating Custom Action
* 15.3 JavaScript Action
* 15.4 Docker Action
* 15.5 Composite Action
* 15.6 Using Marketplace Actions

---
