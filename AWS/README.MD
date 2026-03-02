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

> Github actions ,Jenkins
---

## **2. Infrastructure as Code (IaC)**

| Service                         | Purpose                             |
| ------------------------------- | ----------------------------------- |
| **CloudFormation**              | IaC for full AWS stack              |
| **EC2 Image Builder**           | Golden AMI creation                 |

> Terraform also commonly used (not AWS service but major DevOps tool)

---

## **3. Compute (for workloads)**

| Service               | Purpose                        |
| --------------------- | ------------------------------ |
| **EC2**               | VMs for workloads              |
| **Lambda**            | Serverless compute             |
| **Elastic Beanstalk** | Managed app platform           |

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

> Grafana, Prometheus, Datadog also commonly used externally

---

## **7. Storage & Artifacts**

| Service                               | Purpose                                                    | DevOps Use Case                                                     |
| ------------------------------------- | ---------------------------------------------------------- | ------------------------------------------------------------------- |
| **Amazon S3**                         | Object storage                                             | Artifacts storage, backups, Terraform state, static website hosting |
| **Amazon EBS**                        | Block storage for EC2                                      | Persistent storage for EC2, databases, CI build servers             |
| **Amazon EFS**                        | Managed NFS file system                                    | Shared storage across multiple EC2 instances                        |
| **Amazon FSx**                        | Fully managed file systems (Windows/Lustre/NetApp/OpenZFS) | Enterprise apps, HPC workloads                                      |
                           
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

---


## **9. Databases used in DevOps pipelines**

| Service                           | Purpose              |
| --------------------------------- | -------------------- |
| **RDS**                           | Managed SQL DB       |
| **DynamoDB**                      | NoSQL                |
| **ElastiCache (Redis/Memcached)** | Cache                |
| **Aurora**                        | High-performance RDS |
| **QLDB**                          | Ledger DB            |

---

