---

# 7. AWS Documentation – EC2 Instance Creation

---
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

---
# 8. Access EC2 Instance from Windows
---
After launching an EC2 instance, administrators need to connect to the instance to configure software, deploy applications, and manage the system.

From a **Windows machine**, EC2 instances can be accessed using several methods:

| Method         | Tool                 | Protocol          |
| -------------- | -------------------- | ----------------- |
| Git Bash       | Git Bash terminal    | SSH               |
| Command Prompt | OpenSSH              | SSH               |
| PowerShell     | PowerShell SSH       | SSH               |
| Web Browser    | EC2 Instance Connect | Browser-based SSH |

Most Linux EC2 instances use **SSH (Secure Shell)** for secure remote access.

---

# 8.1 Access EC2 Using Git Bash (Windows)

Git Bash provides a **Linux-like terminal environment for Windows** and supports SSH commands.

### Step 1 – Install Git Bash

Download and install:

[https://git-scm.com](https://git-scm.com)

After installation, open **Git Bash**.

---

### Step 2 – Locate the Key Pair File

During EC2 instance creation, AWS provides a **key pair file (.pem)**.

Example:

```
devops-key.pem
```

Move the file to a known directory.

Example:

```
C:\Users\username\Downloads
```

---

### Step 3 – Set Correct Permissions (Optional)

Run the following command in Git Bash:

```bash
chmod 400 devops-key.pem
```

This ensures only the owner can read the private key.

---

### Step 4 – Connect to the Instance

Use the SSH command:

```bash
ssh -i devops-key.pem ec2-user@public-ip
```

Example:

```bash
ssh -i devops-key.pem ec2-user@54.221.10.20
```

---

### Step 5 – Successful Connection

If the connection is successful, the terminal will show:

```
[ec2-user@ip-172-31-10-24 ~]$
```

You are now connected to the EC2 instance.

---

# 8.2 Access EC2 Using Windows Command Prompt (CMD)

Modern Windows systems include **OpenSSH client support**, allowing connections through Command Prompt.

---

### Step 1 – Open Command Prompt

Press:

```
Windows + R
```

Type:

```
cmd
```

---

### Step 2 – Navigate to Key Pair Location

Example:

```
cd Downloads
```

---

### Step 3 – Connect Using SSH

Run:

```bash
ssh -i devops-key.pem ec2-user@public-ip
```

Example:

```bash
ssh -i devops-key.pem ec2-user@54.221.10.20
```

---

### Step 4 – Accept Security Prompt

First-time connection will show:

```
Are you sure you want to continue connecting?
```

Type:

```
yes
```

The EC2 terminal session will start.

---

# 8.3 Access EC2 Using Windows PowerShell

PowerShell also supports **OpenSSH-based connections**.

---

### Step 1 – Open PowerShell

Press:

```
Windows + X
```

Select:

```
Windows PowerShell
```

---

### Step 2 – Navigate to Key File

Example:

```powershell
cd C:\Users\username\Downloads
```

---

### Step 3 – Run SSH Command

```powershell
ssh -i devops-key.pem ec2-user@public-ip
```

Example:

```powershell
ssh -i devops-key.pem ec2-user@54.221.10.20
```

---

### Step 4 – Connected Session

After successful login, you will see the Linux shell prompt.

Example:

```
[ec2-user@ip-172-31-10-24 ~]$
```

---

# 8.4 Access EC2 Using Web Browser (EC2 Instance Connect)

AWS also provides **browser-based SSH access**.

This method does not require installing any SSH client.

---

### Step 1 – Open AWS Console

Navigate to:

```
AWS Console → EC2 → Instances
```

---

### Step 2 – Select the Instance

Select the EC2 instance you want to connect to.

---

### Step 3 – Click Connect

Click:

```
Connect
```

Choose:

```
EC2 Instance Connect
```

---

### Step 4 – Connect Using Browser

Click:

```
Connect
```

AWS will open a **browser-based terminal session**.

Example terminal:

```
ec2-user@ip-172-31-10-24:~$
```

---

# 8.5 Default SSH Usernames

The username depends on the AMI used.

| AMI          | Default Username |
| ------------ | ---------------- |
| Amazon Linux | ec2-user         |
| Ubuntu       | ubuntu           |
| Red Hat      | ec2-user         |
| Debian       | admin            |
| CentOS       | centos           |

Example connection:

```bash
ssh -i devops-key.pem ubuntu@public-ip
```

---

# 8.6 Security Requirements

To connect successfully, the following conditions must be met:

### Security Group Rules

Inbound rule must allow SSH:

| Type | Port | Source  |
| ---- | ---- | ------- |
| SSH  | 22   | Your IP |

---

### Key Pair

The correct **private key (.pem)** must be used.

---

### Public IP

The instance must have a **public IP address**.

---

# 8.7 Troubleshooting Connection Issues

| Issue                | Cause                           |
| -------------------- | ------------------------------- |
| Connection timed out | Security group blocking port 22 |
| Permission denied    | Incorrect key file              |
| Host unreachable     | Instance not running            |
| Network error        | Public IP not assigned          |

---

# 9. EC2 Instance Types and Pricing Models

---
Amazon EC2 provides different **instance types** and **pricing models** so organizations can choose the most suitable combination for their application workloads.

Instance types define the **hardware configuration**, while pricing models determine **how you pay for using those resources**.

---

# 9.1 EC2 Instance Types

An **EC2 Instance Type** defines the hardware specifications of a virtual machine running in AWS.

It determines:

* Number of **vCPUs**
* Amount of **RAM**
* **Storage performance**
* **Network bandwidth**
* **GPU capability**

AWS provides multiple instance families optimized for different workloads.

---

## General Purpose Instances

General purpose instances provide a balance of **compute, memory, and networking resources**.

Common families:

| Instance Family | Example | Use Case            |
| --------------- | ------- | ------------------- |
| T-Series        | t2, t3  | Small applications  |
| M-Series        | m5, m6  | Web servers         |
| A-Series        | a1      | ARM-based workloads |

Example:

```
t2.micro
1 vCPU
1 GB RAM
```

Common uses:

* Small web servers
* Development environments
* Testing applications

---

## Compute Optimized Instances

Compute optimized instances are designed for **high CPU performance workloads**.

| Instance Family | Example | Use Case                |
| --------------- | ------- | ----------------------- |
| C-Series        | c5, c6  | CPU-intensive workloads |

Typical applications:

* High-performance computing
* Batch processing
* Video encoding
* Scientific modeling

---

## Memory Optimized Instances

Memory optimized instances are designed for workloads requiring **large memory capacity**.

| Instance Family | Example | Use Case                    |
| --------------- | ------- | --------------------------- |
| R-Series        | r5, r6  | In-memory databases         |
| X-Series        | x1      | Large-scale enterprise apps |

Typical applications:

* SAP HANA
* Redis
* Large database servers

---

## Storage Optimized Instances

Storage optimized instances provide **high disk throughput and low latency**.

| Instance Family | Example | Use Case                   |
| --------------- | ------- | -------------------------- |
| I-Series        | i3      | High-performance databases |
| D-Series        | d2      | Big data storage           |

Common workloads:

* Data warehousing
* NoSQL databases
* Big data analytics

---

## Accelerated Computing Instances

These instances use **hardware accelerators such as GPUs or FPGAs**.

| Instance Family | Example | Use Case            |
| --------------- | ------- | ------------------- |
| P-Series        | p3, p4  | Machine learning    |
| G-Series        | g4      | Graphics processing |
| F-Series        | f1      | FPGA workloads      |

Typical applications:

* Machine learning training
* Artificial intelligence
* Video rendering
* Scientific simulations

---

## EC2 Instance Type Categories

---

| Instance Category     | Instance Family              | Example Types | Key Features                     | Common Use Cases                             |
| --------------------- | ---------------------------- | ------------- | -------------------------------- | -------------------------------------------- |
| General Purpose       | T-Series, M-Series           | t2, t3, m5    | Balanced CPU, memory, networking | Web servers, development environments        |
| Compute Optimized     | C-Series                     | c5, c6        | High CPU performance             | High performance computing, batch processing |
| Memory Optimized      | R-Series, X-Series           | r5, r6, x1    | Large RAM capacity               | In-memory databases, caching systems         |
| Storage Optimized     | I-Series, D-Series           | i3, d2        | High disk throughput             | Data warehousing, big data workloads         |
| Accelerated Computing | P-Series, G-Series, F-Series | p3, p4, g4    | GPU / FPGA acceleration          | Machine learning, AI, video rendering        |

---
# 9.2 EC2 Instance Pricing Models

AWS offers multiple **pricing models** to help optimize costs depending on workload requirements.

---

# 9.2.1 On-Demand Pricing

On-Demand instances allow users to **pay for compute capacity by the hour or second without long-term commitment**.

Characteristics:

* No upfront cost
* Pay only for usage
* Flexible scaling

Example:

```
Run EC2 for 3 hours
Pay only for 3 hours
```

Use cases:

* Development environments
* Short-term workloads
* Testing applications

---

# 9.2.2 Reserved Instances (RI)

Reserved Instances provide **significant discounts in exchange for a commitment to use EC2 for 1 or 3 years**.

Benefits:

* Lower hourly cost
* Capacity reservation
* Predictable pricing

Savings:

```
Up to 70% cheaper than On-Demand
```

Use cases:

* Production servers
* Long-running workloads
* Databases

---

# 9.2.3 Spot Instances

Spot Instances allow users to use **unused AWS compute capacity at a much lower price**.

However, AWS may terminate these instances if the capacity is needed elsewhere.

Cost savings:

```
Up to 90% cheaper than On-Demand
```

Use cases:

* Batch processing
* Data analysis
* CI/CD pipelines
* Machine learning training

---

# 9.2.4 Savings Plans

Savings Plans allow users to commit to a **specific amount of compute usage per hour for 1 or 3 years**.

Benefits:

* Flexible instance usage
* Lower cost compared to On-Demand

Savings:

```
Up to 72% cost reduction
```

---

# 9.2.5 Dedicated Hosts

Dedicated Hosts provide **physical servers dedicated to a single customer**.

Benefits:

* Hardware isolation
* Compliance requirements
* License-based applications

Use cases:

* Enterprise software licensing
* Government or regulated workloads

---

## EC2 Pricing Models

---

| Pricing Model      | Description                                    | Commitment           | Cost Savings     | Best Use Case                         |
| ------------------ | ---------------------------------------------- | -------------------- | ---------------- | ------------------------------------- |
| On-Demand          | Pay for compute capacity by the hour or second | None                 | Standard price   | Development, testing, short workloads |
| Reserved Instances | Reserve instances for 1 or 3 years             | Long-term commitment | Up to 70%        | Production servers, databases         |
| Spot Instances     | Use unused AWS capacity                        | No guarantee         | Up to 90%        | Batch processing, CI/CD pipelines     |
| Savings Plans      | Commit to hourly usage for 1 or 3 years        | Flexible commitment  | Up to 72%        | Long-running workloads                |
| Dedicated Hosts    | Physical server dedicated to one customer      | Long-term            | Depends on usage | Compliance and license requirements   |

---

# 9.3 Example EC2 Pricing Scenario

Example application architecture:

```
Web Application
     │
     ▼
Application Load Balancer
     │
 ├── EC2 Instance (Web Server)
 ├── EC2 Instance (Application Server)
     │
     ▼
RDS Database
```

Possible pricing strategy:

| Component           | Pricing Model      |
| ------------------- | ------------------ |
| Web Servers         | On-Demand          |
| Application Servers | Reserved Instances |
| Batch Processing    | Spot Instances     |

This helps optimize infrastructure cost.

---

# 10. Amazon Machine Image (AMI) and Launch Templates

---
Amazon EC2 uses **Amazon Machine Images (AMIs)** and **Launch Templates** to standardize and automate the process of launching instances. These features help organizations maintain consistent infrastructure and enable automated deployments in DevOps environments.

---

# 10.1 Amazon Machine Image (AMI)

## Definition

An **Amazon Machine Image (AMI)** is a preconfigured template used to launch EC2 instances.

An AMI contains the information required to start an instance, including:

* Operating system
* Application server (optional)
* Pre-installed software
* System configuration
* Boot configuration
* Storage configuration

When an EC2 instance is launched, AWS uses the AMI as a **blueprint to create the virtual machine**.

---

## Components of an AMI

An AMI typically contains the following components.

### Root Volume Template

The root volume contains the **operating system and system files** required to start the instance.

Supported storage types:

* EBS-backed storage
* Instance store-backed storage

---

### Launch Permissions

Launch permissions control **which AWS accounts are allowed to use the AMI**.

Possible permissions:

| Type    | Description                         |
| ------- | ----------------------------------- |
| Private | Only owner account can use the AMI  |
| Public  | Any AWS account can launch the AMI  |
| Shared  | Specific AWS accounts can access it |

---

### Block Device Mapping

Block device mapping defines the **storage volumes attached to the instance** when it launches.

Example configuration:

| Volume            | Type | Size  |
| ----------------- | ---- | ----- |
| Root Volume       | gp3  | 8 GB  |
| Additional Volume | gp3  | 20 GB |

---

## Types of AMIs

AWS supports several AMI types.

### AWS Provided AMIs

Provided and maintained by AWS.

Examples:

* Amazon Linux
* Amazon Linux 2023
* Windows Server

---

### AWS Marketplace AMIs

Preconfigured AMIs available from vendors.

Examples:

* WordPress servers
* Security appliances
* Database images

These AMIs may include **additional licensing costs**.

---

### Community AMIs

Created and shared by AWS users.

Used for:

* Open source software
* Custom environments

Users must verify the security of these AMIs before using them.

---

### Custom AMIs

Organizations can create their own AMIs.

Example process:

```
Launch EC2
Install applications
Configure environment
Create AMI
```

The custom AMI can then be used to launch multiple identical servers.

---

## Creating an AMI

Steps to create an AMI:

1. Launch an EC2 instance
2. Install required software
3. Configure system settings
4. Stop the instance
5. Create image (AMI)

Console path:

```
EC2 → Instances → Actions → Image → Create Image
```

AWS will create:

* AMI image
* Associated EBS snapshot

---

## Advantages of AMIs

Benefits of AMIs include:

* Rapid instance deployment
* Standardized server environments
* Easy scaling
* Infrastructure consistency
* Disaster recovery support

---

# 10.2 Launch Templates

## Definition

A **Launch Template** is a configuration template that defines how EC2 instances should be launched.

It stores **all instance configuration settings in a reusable template**.

Launch Templates simplify infrastructure management by allowing users to **launch instances with predefined settings**.

---

## Purpose of Launch Templates

Launch templates are commonly used in:

* Auto Scaling Groups
* DevOps automation
* Infrastructure as Code
* CI/CD pipelines

They help ensure consistent infrastructure deployment.

---

## Components of a Launch Template

A launch template can include the following configuration settings.

### AMI ID

Specifies the operating system image used when launching instances.

Example:

```
ami-0513a13abf4d498f5
```

---

### Instance Type

Defines hardware specifications.

Example:

```
t2.micro
```

---

### Key Pair

Used for SSH or RDP access.

Example:

```
devops-key
```

---

### Security Groups

Defines firewall rules for the instance.

Example:

| Protocol | Port | Purpose       |
| -------- | ---- | ------------- |
| SSH      | 22   | Remote access |
| HTTP     | 80   | Web server    |

---

### Storage Configuration

Defines EBS volume settings.

Example:

| Volume Type | Size |
| ----------- | ---- |
| gp3         | 8 GB |

---

### Network Configuration

Defines networking components such as:

* VPC
* Subnet
* Public IP
* Network interfaces

---

### User Data

User data scripts run automatically when an instance launches.

Example:

```
#!/bin/bash
yum update -y
yum install httpd -y
systemctl start httpd
```

This automatically installs a web server.

---

## Launch Template Versions

Launch templates support **versioning**.

Each time a configuration is modified, AWS creates a **new version**.

Example:

| Version | Description            |
| ------- | ---------------------- |
| v1      | Initial configuration  |
| v2      | Updated instance type  |
| v3      | Added user data script |

This allows controlled infrastructure updates.

---

## Creating a Launch Template

Steps:

1. Open AWS Console
2. Navigate to EC2
3. Select Launch Templates
4. Click Create Launch Template

Console path:

```
EC2 → Launch Templates → Create Launch Template
```

Provide configuration such as:

* Template name
* AMI
* Instance type
* Security group
* Storage
* Key pair

---

## Launch Template vs Launch Configuration

Launch configurations were previously used with Auto Scaling but are now **deprecated in favor of Launch Templates**.

Comparison:

| Feature                 | Launch Template | Launch Configuration |
| ----------------------- | --------------- | -------------------- |
| Versioning              | Supported       | Not supported        |
| Multiple instance types | Supported       | Not supported        |
| Spot instance support   | Yes             | Limited              |
| Future AWS support      | Yes             | Limited              |

Launch templates are the **recommended method for EC2 deployments**.

---

# 10.3 AMI vs Launch Template

| Feature              | AMI (Amazon Machine Image)      | Launch Template                                 |
| -------------------- | ------------------------------- | ----------------------------------------------- |
| Purpose              | Server image                    | Instance launch configuration                   |
| Contains             | OS + Installed software         | Instance settings                               |
| Defines              | Operating system environment    | How instance should launch                      |
| Includes             | OS, packages, configuration     | AMI ID, instance type, key pair, security group |
| Used for             | Creating identical servers      | Automating instance creation                    |
| User Data            | Normally not stored permanently | User data can be defined                        |
| Versioning           | No version control              | Supports versions                               |
| Used in Auto Scaling | Yes                             | Yes (recommended method)                        |

---

# 11. EC2 Instance Metadata and User Data

---
Amazon EC2 provides two important mechanisms that help configure and manage instances automatically:

* **Instance Metadata**
* **User Data**

These features allow applications and scripts running inside an EC2 instance to access information about the instance and automatically configure the system during startup.

---

# 11.1 EC2 Instance Metadata

## Definition

**Instance Metadata** is information about the EC2 instance that can be accessed from within the instance itself.

This data includes details about:

* Instance ID
* Instance type
* Security groups
* Network configuration
* IAM role credentials
* Availability zone
* Public and private IP addresses

The metadata is available through a special **local HTTP endpoint** provided by AWS.

---

## Metadata Service Endpoint

Instance metadata can be accessed through the following address:

```
http://169.254.169.254/latest/meta-data/
```

This IP address is a **link-local address**, meaning it is accessible only from inside the EC2 instance.

Example command:

```bash
curl http://169.254.169.254/latest/meta-data/
```

This command returns a list of metadata categories.

---

## Common Metadata Information

Some commonly accessed metadata items include:

| Metadata                    | Description                       |
| --------------------------- | --------------------------------- |
| instance-id                 | Unique ID of the EC2 instance     |
| instance-type               | Type of instance (e.g., t2.micro) |
| local-ipv4                  | Private IP address                |
| public-ipv4                 | Public IP address                 |
| security-groups             | Attached security groups          |
| ami-id                      | AMI used to launch the instance   |
| placement/availability-zone | Instance AZ location              |

Example:

```bash
curl http://169.254.169.254/latest/meta-data/instance-id
```

Output example:

```
i-0a12bc34d56ef7890
```

---

## Metadata Categories

Instance metadata contains several categories of information.

### Instance Identity

Information about the instance identity.

Examples:

* instance-id
* instance-type
* ami-id

---

### Network Information

Details about the instance networking.

Examples:

* public-ipv4
* local-ipv4
* network interfaces

---

### Security Information

Security-related configuration.

Examples:

* security groups
* IAM role credentials

---

### Placement Information

Information about the instance location.

Examples:

* region
* availability zone

---

# 11.2 Instance Metadata Service Versions

AWS supports two versions of the metadata service.

---

## IMDSv1

The original metadata service.

Characteristics:

* Simple HTTP requests
* No authentication token required

Example:

```bash
curl http://169.254.169.254/latest/meta-data/
```

---

## IMDSv2 (Recommended)

A more secure version of metadata service.

Requires a **session token** before accessing metadata.

Example token request:

```bash
TOKEN=$(curl -X PUT "http://169.254.169.254/latest/api/token" \
-H "X-aws-ec2-metadata-token-ttl-seconds: 21600")
```

Retrieve metadata using token:

```bash
curl -H "X-aws-ec2-metadata-token: $TOKEN" \
http://169.254.169.254/latest/meta-data/
```

Benefits of IMDSv2:

* Protection against SSRF attacks
* Improved security
* Session-based authentication

---

# 11.3 IAM Role Metadata

If an IAM role is attached to an EC2 instance, the metadata service provides **temporary security credentials**.

Example path:

```
http://169.254.169.254/latest/meta-data/iam/security-credentials/
```

Example usage:

Applications can automatically obtain AWS credentials without storing access keys.

Example use case:

```
EC2 instance → Access S3 bucket using IAM role
```

---

# 11.4 EC2 User Data

## Definition

**User Data** is a feature that allows users to provide scripts or commands that run automatically when an EC2 instance launches.

This feature is commonly used to automate instance configuration during startup.

User Data is executed during the **first boot of the instance**.

---

## Common Uses of User Data

User Data is widely used for:

* Installing software
* Updating operating systems
* Configuring services
* Deploying applications
* Running initialization scripts

---

## Example User Data Script

Example script to install Apache web server:

```bash
#!/bin/bash
yum update -y
yum install httpd -y
systemctl start httpd
systemctl enable httpd
```

When the EC2 instance starts, this script will:

1. Update system packages
2. Install Apache
3. Start the web server
4. Enable Apache at boot

---

## How User Data Works

User data scripts are processed by a service called **cloud-init**.

The process:

```
EC2 Instance Launch
        │
        ▼
cloud-init reads User Data
        │
        ▼
Script executed
        │
        ▼
Instance configured automatically
```

---

## Adding User Data

User Data can be added during instance launch.

Steps:

```
EC2 → Launch Instance → Advanced Details → User Data
```

Paste the script into the User Data field.

---

## Viewing User Data

User data can be viewed inside the instance.

Example command:

```bash
curl http://169.254.169.254/latest/user-data
```

---

# 11.5 Differences Between Metadata and User Data

| Feature       | Instance Metadata                       | User Data                               |
| ------------- | --------------------------------------- | --------------------------------------- |
| Purpose       | Provides information about the instance | Executes scripts during instance launch |
| Access Method | Metadata service (HTTP endpoint)        | Passed during instance launch           |
| Availability  | Always available inside instance        | Available only if provided              |
| Use Case      | Retrieve instance information           | Automate system configuration           |

---
