# ✅ **AWS Services Used in DevOps — Practical Categories**

---

## **1. CI/CD (Build + Test + Deploy)**

| Service          | Purpose                                              |
| ---------------- | ---------------------------------------------------- |
| **CodeCommit**   | Git repo (like GitHub/GitLab)                        |
| **CodeBuild**    | Builds & tests code                                  |
| **CodeDeploy**   | Deploys to EC2, ECS, Lambda, On-prem                 |
| **CodePipeline** | Full CI/CD pipeline orchestration                    |
| **CodeArtifact** | Artifact/package repository (like Nexus/Artifactory) |
| **CodeGuru**     | Automated code review & performance analysis         |
| **Device Farm**  | Mobile device testing                                |

---

## **2. Infrastructure as Code (IaC)**

| Service                         | Purpose                             |
| ------------------------------- | ----------------------------------- |
| **CloudFormation**              | IaC for full AWS stack              |
| **CDK (Cloud Development Kit)** | IaC using Typescript/Python/Go/Java |
| **OpsWorks (Chef/Puppet)**      | Config management                   |
| **EC2 Image Builder**           | Golden AMI creation                 |

> Terraform also commonly used (not AWS service but major DevOps tool)

---

## **3. Compute (for workloads)**

| Service               | Purpose                        |
| --------------------- | ------------------------------ |
| **EC2**               | VMs for workloads              |
| **Lambda**            | Serverless compute             |
| **Elastic Beanstalk** | Managed app platform           |
| **Lightsail**         | VPS for small/simple workloads |

---

## **4. Containers & Kubernetes**

| Service                              | Purpose                        |
| ------------------------------------ | ------------------------------ |
| **ECS (Elastic Container Service)**  | AWS container orchestration    |
| **ECR (Elastic Container Registry)** | Docker image registry          |
| **Fargate**                          | Serverless compute for ECS/EKS |
| **EKS (Elastic Kubernetes Service)** | Managed Kubernetes             |

---

## **5. Networking & Routing**

| Service                         | Purpose           |
| ------------------------------- | ----------------- |
| **VPC**                         | Networking        |
| **Route53**                     | DNS               |
| **Load Balancer (ALB/NLB/CLB)** | Traffic routing   |
| **API Gateway**                 | APIs management   |
| **CloudFront**                  | CDN               |
| **Transit Gateway**             | Multi-VPC routing |
| **Direct Connect**              | On-prem ↔ AWS     |

---

## **6. Monitoring, Logging & Observability**

| Service        | Purpose                         |
| -------------- | ------------------------------- |
| **CloudWatch** | Metrics + logs + alarms         |
| **X-Ray**      | Distributed tracing             |
| **CloudTrail** | API audit logs                  |
| **Config**     | Resource compliance tracking    |
| **OpenSearch** | Log analytics (ELK alternative) |

> Grafana, Prometheus, Datadog also commonly used externally

---

## **7. Storage & Artifacts**

| Service     | Purpose                             |
| ----------- | ----------------------------------- |
| **S3**      | Backup + Artifacts + Static hosting |
| **EFS**     | Shared POSIX file storage           |
| **FSx**     | Windows/Lustre file systems         |
| **Glacier** | Long-term archival                  |

---

## **8. Security, Compliance, IAM**

| Service                             | Purpose                                       |
| ----------------------------------- | --------------------------------------------- |
| **IAM**                             | Identity & Access                             |
| **KMS**                             | Key Management                                |
| **Secrets Manager**                 | App secrets (opt better than Parameter Store) |
| **Systems Manager Parameter Store** | Config + secrets                              |
| **GuardDuty**                       | Threat detection                              |
| **Security Hub**                    | Security posture                              |
| **Macie**                           | S3 data security                              |
| **Inspector**                       | Vulnerability scanning                        |

---

## **9. Automation + Ops Tools**

| Service                   | Purpose                               |
| ------------------------- | ------------------------------------- |
| **Systems Manager (SSM)** | Patching, automation, remote commands |
| **EventBridge**           | Event system for automation           |
| **Step Functions**        | Workflow orchestration                |
| **AppConfig**             | Feature flags + config rollouts       |
| **Service Catalog**       | Standardized infra provisioning       |

---

## **10. Databases used in DevOps pipelines**

| Service                           | Purpose              |
| --------------------------------- | -------------------- |
| **RDS**                           | Managed SQL DB       |
| **DynamoDB**                      | NoSQL                |
| **ElastiCache (Redis/Memcached)** | Cache                |
| **Aurora**                        | High-performance RDS |
| **QLDB**                          | Ledger DB            |

---

