---

# 7. AWS Documentation – EC2 Instance Creation

## 7.1 Introduction to Amazon EC2

**Amazon EC2 (Elastic Compute Cloud)** is a cloud computing service that allows users to launch and manage **virtual servers in the AWS cloud**.

It provides scalable compute capacity that enables organizations to run applications without investing in physical hardware.

EC2 instances are widely used for:

* Web hosting
* Application servers
* DevOps pipelines
* Development and testing environments
* Container workloads
* Big data processing
* Microservices architectures

Key capabilities of EC2 include:

* Full operating system control
* Flexible compute resources
* Integration with AWS networking
* Scalable infrastructure
* Secure access and monitoring

---

# 7.2 Launch an EC2 Instance

To create an EC2 instance:

```
AWS Console → EC2 → Instances → Launch Instance
```

The instance creation wizard consists of several configuration sections.

---

# 7.3 Name and Tags

The **Name and Tags** section allows users to assign a name and metadata to the instance.

### Name

A human-readable identifier for the instance.

Example:

```
My-Web-Server
DevOps-EC2
Production-App-Server
```

---

### Tags

Tags are **key-value pairs** used to organize AWS resources.

Example:

| Key         | Value      |
| ----------- | ---------- |
| Environment | Production |
| Project     | DevOps     |
| Owner       | Saurav     |

Tags help in:

* Resource organization
* Cost tracking
* Automation
* Access control

---

# 7.4 Application and OS Image (AMI)

An **Amazon Machine Image (AMI)** is a template used to launch EC2 instances.

It contains:

* Operating system
* Pre-installed software
* System configuration
* Boot configuration

---

## Example AMI Options

Common AMIs include:

| OS             | Description                    |
| -------------- | ------------------------------ |
| Amazon Linux   | AWS optimized Linux OS         |
| Ubuntu         | Popular Linux distribution     |
| Windows Server | Microsoft Windows environment  |
| Red Hat        | Enterprise Linux distribution  |
| Debian         | Lightweight Linux distribution |
| SUSE Linux     | Enterprise Linux environment   |

Example selected AMI:

```
Amazon Linux 2023 AMI
Architecture: 64-bit (x86)
Username: ec2-user
```

Amazon Linux is optimized for:

* AWS services
* Security updates
* High performance

---

# 7.5 Instance Type

The **Instance Type** defines the hardware configuration of the EC2 instance.

This includes:

* CPU (vCPU)
* Memory (RAM)
* Network performance
* Storage performance

---

## Example Instance Type

```
t2.micro
```

Specifications:

| Resource | Value           |
| -------- | --------------- |
| vCPU     | 1               |
| RAM      | 1 GB            |
| Network  | Low to Moderate |

This instance type is **Free Tier eligible**.

---

## Instance Family Categories

| Instance Family | Purpose                     |
| --------------- | --------------------------- |
| T-series        | General purpose             |
| M-series        | Balanced compute and memory |
| C-series        | Compute optimized           |
| R-series        | Memory optimized            |
| P-series        | GPU workloads               |

---

# 7.6 Key Pair (Login)

A **Key Pair** is used for secure authentication when connecting to an EC2 instance.

It consists of:

* Public Key (stored by AWS)
* Private Key (downloaded by user)

---

## Linux Access (SSH)

Example:

```
ssh -i devops-key.pem ec2-user@public-ip
```

---

## Windows Access (RDP)

Steps:

1. Download RDP file
2. Decrypt administrator password
3. Connect using Remote Desktop

---

# 7.7 Network Settings

Network settings configure how the EC2 instance connects to the network.

Key components include:

* VPC
* Subnet
* Public IP
* Security groups

---

## VPC (Virtual Private Cloud)

A **VPC** is a logically isolated network in AWS.

It allows users to control:

* IP addressing
* Routing
* Security
* Internet access

---

## Subnet

A **Subnet** is a smaller network inside a VPC.

Example:

```
Subnet in Availability Zone ap-south-1a
```

---

## Public IP Address

A public IP allows the instance to be accessed from the internet.

Example:

```
Auto-assign public IP → Enabled
```

---

# 7.8 Security Groups (Firewall)

A **Security Group** acts as a virtual firewall controlling inbound and outbound traffic.

Example rule:

| Type  | Port | Source   |
| ----- | ---- | -------- |
| SSH   | 22   | Anywhere |
| HTTP  | 80   | Anywhere |
| HTTPS | 443  | Anywhere |

Security groups are **stateful firewalls**.

This means:

* If inbound traffic is allowed, the response is automatically allowed.

---

# 7.9 Configure Storage

EC2 instances use **Amazon Elastic Block Store (EBS)** for storage.

Example configuration:

```
Volume Type: gp3
Size: 8 GB
IOPS: 3000
```

---

## EBS Features

* Persistent storage
* Snapshots for backup
* High availability
* Encryption support

---

## Free Tier Limit

AWS Free Tier allows:

```
30 GB of EBS storage
```

---

# 7.10 Advanced Details

The **Advanced Details** section allows configuration of advanced instance behavior.

---

## Domain Join Directory

Allows the EC2 instance to join an **AWS Directory Service domain**.

Used mainly in enterprise environments.

---

## IAM Instance Profile

An **IAM Role** attached to the EC2 instance.

Allows the instance to securely access AWS services.

Example services:

* S3
* DynamoDB
* CloudWatch

---

## Instance Auto-Recovery

Automatically recovers the instance if AWS detects hardware failure.

---

## Shutdown Behavior

Defines what happens when the OS shuts down.

| Option    | Behavior         |
| --------- | ---------------- |
| Stop      | Instance stops   |
| Terminate | Instance deleted |

---

## Termination Protection

Prevents accidental deletion of the instance.

---

## Stop Protection

Prevents the instance from being stopped accidentally.

---

## CloudWatch Monitoring

Two monitoring modes exist:

| Type     | Interval  |
| -------- | --------- |
| Basic    | 5 minutes |
| Detailed | 1 minute  |

---

## Credit Specification

Used for **burstable instances** like:

```
t2
t3
t4g
```

Modes:

* Standard
* Unlimited

---

## Placement Groups

Control how EC2 instances are placed on physical hardware.

Types:

| Type      | Purpose                    |
| --------- | -------------------------- |
| Cluster   | High performance computing |
| Spread    | Fault isolation            |
| Partition | Distributed systems        |

---

## EBS Optimized Instances

Provides dedicated bandwidth between EC2 and EBS storage.

Improves disk performance.

---

## Capacity Reservation

Guarantees compute capacity in a specific **Availability Zone**.

---

## Tenancy

Defines hardware isolation.

| Type               | Description            |
| ------------------ | ---------------------- |
| Shared             | Default                |
| Dedicated Instance | Dedicated hardware     |
| Dedicated Host     | Entire physical server |

---

## Metadata Service (IMDS)

The **Instance Metadata Service** provides information about the instance.

Examples:

* Instance ID
* Region
* IAM role
* Network information

---

## Metadata Version

| Version | Description |
| ------- | ----------- |
| IMDSv1  | Older       |
| IMDSv2  | Secure      |

Recommended:

```
IMDSv2
```

---

## User Data

User Data allows scripts to run automatically during instance launch.

Example:

```
#!/bin/bash
yum update -y
yum install httpd -y
systemctl start httpd
systemctl enable httpd
```

This automatically installs and starts **Apache web server**.

---

# 7.11 Launch Instance

After configuring all settings:

Click:

```
Launch Instance
```

The EC2 instance will be created within seconds.

---

# 7.12 EC2 Instance Lifecycle

| State      | Description        |
| ---------- | ------------------ |
| Pending    | Instance launching |
| Running    | Instance active    |
| Stopped    | Instance stopped   |
| Terminated | Instance deleted   |

Example lifecycle:

```
Launch → Pending → Running → Stopped → Terminated
```

---

# 7.13 Example DevOps Architecture

Example production architecture using EC2:

```
Users
 │
 ▼
Route53
 │
 ▼
Application Load Balancer
 │
 ├── EC2 (AZ-1)
 ├── EC2 (AZ-2)
 └── EC2 (AZ-3)
 │
 ▼
RDS Database
 │
 ▼
S3 Storage
```

This architecture provides:

* High availability
* Scalability
* Fault tolerance

---
