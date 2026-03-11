---
Amazon EFS (Elastic File System)
---
---
# 📁 1. Introduction to Amazon EFS (Elastic File System)
---
## 1.1 What is Amazon EFS

**Amazon Elastic File System (EFS)** is a **fully managed, scalable, and elastic Network File System (NFS)** provided by AWS that allows multiple EC2 instances to share the same file storage simultaneously.

It provides **shared file storage** that can be accessed from multiple servers at the same time.

Amazon EFS automatically **scales storage capacity up and down** as files are added or removed, so there is no need to manually manage storage.

EFS is designed to work with **Linux-based workloads** and uses the **NFS protocol (Network File System)** to allow instances to mount the file system.

It is commonly used for:

* Shared application data
* Content management systems
* Web server storage
* Container persistent storage
* Big data workloads

Unlike **EBS**, which can be attached to **one EC2 instance**, EFS can be attached to **multiple EC2 instances simultaneously**.

---

## 1.2 Why Amazon EFS is Required

Traditional storage systems often require manual configuration and management. Amazon EFS solves several challenges by providing scalable shared storage.

### Common Problems Without EFS

1. Storage needs to be manually increased
2. Sharing files between multiple servers is difficult
3. Storage management requires administrative effort
4. High availability must be configured manually
5. Backup and scaling are complex

### How EFS Solves These Problems

| Problem           | Solution using EFS                                     |
| ----------------- | ------------------------------------------------------ |
| Storage scaling   | Automatically grows and shrinks                        |
| Shared access     | Multiple EC2 instances can access the same file system |
| High availability | Automatically replicated across Availability Zones     |
| Maintenance       | Fully managed by AWS                                   |
| Backup            | Integration with AWS Backup                            |

---

## 1.3 Features of Amazon EFS

Amazon EFS provides several powerful features that make it suitable for cloud workloads.

### 1. Fully Managed Service

AWS manages the infrastructure, patching, and maintenance of the file system.

### 2. Elastic Scalability

EFS automatically scales storage capacity without manual intervention.

### 3. Shared File System

Multiple EC2 instances can mount the same file system simultaneously.

### 4. High Availability

EFS stores data across multiple Availability Zones within a region.

### 5. Secure Storage

Supports:

* Encryption at rest
* Encryption in transit
* IAM access control

### 6. Multiple Performance Modes

EFS supports different performance modes to suit various workloads.

### 7. Lifecycle Management

Automatically moves infrequently accessed data to lower-cost storage.

---

## 1.4 Benefits of Amazon EFS

Using Amazon EFS provides several advantages for cloud-based applications.

### 1. Automatic Scaling

Storage grows and shrinks automatically depending on file usage.

### 2. Highly Durable Storage

Data is stored redundantly across multiple Availability Zones.

### 3. Multi-instance Access

Many EC2 instances can access the same file system simultaneously.

### 4. Cost Optimization

You only pay for the storage that you use.

### 5. Easy Integration

EFS integrates easily with many AWS services.

### 6. Simplified Management

No need to provision storage capacity or manage file servers.

---

## 1.5 Use Cases of Amazon EFS

Amazon EFS is used in many modern cloud architectures.

### 1. Web Server Content Sharing

Multiple web servers can share the same static files.

Example:

```
EC2 Web Server 1
EC2 Web Server 2
EC2 Web Server 3
        ↓
      Amazon EFS
```

---

### 2. Container Storage

EFS provides persistent storage for containers running in:

* Amazon ECS
* Amazon EKS

---

### 3. DevOps Build Environments

Build systems can share artifacts and logs across multiple build servers.

---

### 4. Big Data Analytics

Large datasets can be processed by multiple compute nodes simultaneously.

---

### 5. Content Management Systems

CMS applications like **WordPress** can store shared files on EFS.

---

## EFS vs EBS vs S3 (Important Interview Concept)

| Feature            | EFS                 | EBS                     | S3                      |
| ------------------ | ------------------- | ----------------------- | ----------------------- |
| Storage Type       | File Storage        | Block Storage           | Object Storage          |
| Multiple Instances | Yes                 | No                      | Yes                     |
| Mountable          | Yes                 | Yes                     | No                      |
| Protocol           | NFS                 | Block Device            | HTTP API                |
| Use Case           | Shared file storage | Single instance storage | Backup / object storage |

---

✅ **Simple Example Architecture**

```
            Internet
                │
        Load Balancer
                │
      ┌───────────────┐
      │ EC2 Instance 1 │
      └───────────────┘
                │
      ┌───────────────┐
      │ EC2 Instance 2 │
      └───────────────┘
                │
           Amazon EFS
      (Shared File Storage)
```

Both EC2 instances read and write data to the **same file system**.

---
---
# 📁 2. Amazon EFS Architecture
---
## 2.1 EFS Architecture Overview

Amazon Elastic File System (EFS) is designed to provide **scalable, highly available, and shared file storage** for cloud applications.

The architecture of EFS is built to allow **multiple EC2 instances across multiple Availability Zones (AZs)** to access the same file system simultaneously.

EFS works using the **NFS (Network File System) protocol**, which allows Linux instances to mount remote storage like a local directory.

### Basic Architecture Flow

```
            AWS Region
                │
        ┌─────────────────┐
        │   Amazon EFS    │
        │  File System    │
        └─────────────────┘
           │        │
           │        │
   Mount Target  Mount Target
      (AZ-A)        (AZ-B)
        │              │
   EC2 Instance   EC2 Instance
```

Here:

* One **EFS File System** exists in a region
* Each **Availability Zone has a Mount Target**
* EC2 instances connect to the mount target in their AZ

---

# 2.2 Regional Service Concept

Amazon EFS is a **regional service**, which means:

* The file system exists at the **AWS Region level**
* Data is automatically replicated across multiple **Availability Zones**

Example region:

```
Asia Pacific (Mumbai) – ap-south-1
```

Inside this region there are multiple AZs:

```
ap-south-1a
ap-south-1b
ap-south-1c
```

EFS automatically stores data redundantly across these AZs for **high durability and availability**.

### Benefits

* High availability
* Fault tolerance
* Automatic redundancy
* No manual replication needed

---

# 2.3 Mount Targets

A **Mount Target** is a **network endpoint** used by EC2 instances to connect to an EFS file system.

Each **Availability Zone requires its own mount target**.

### Key Points

* One mount target per AZ
* Uses **Elastic Network Interface (ENI)**
* Assigned a **private IP address**
* Associated with a **security group**

### Example

```
EFS File System
       │
 ┌───────────────┐
 │ Mount Target  │  AZ-a
 └───────────────┘
        │
   EC2 Instance

 ┌───────────────┐
 │ Mount Target  │  AZ-b
 └───────────────┘
        │
   EC2 Instance
```

EC2 instances connect to the **nearest mount target** in their Availability Zone for better performance.

---

# 2.4 EFS and Availability Zones

Amazon EFS is designed for **Multi-AZ architecture**.

This means the file system is accessible from multiple Availability Zones.

### Why Multi-AZ is Important

* Fault tolerance
* High availability
* Disaster resilience

Example architecture:

```
Region: ap-south-1

AZ-a
EC2 Instance
      │
Mount Target
      │
      ├──── Amazon EFS File System ────┤
      │
Mount Target
      │
EC2 Instance
AZ-b
```

If one AZ fails, other AZs can still access the file system.

---

# 2.5 NFS Protocol in EFS

Amazon EFS uses **NFS (Network File System) version 4.1 and 4.2**.

NFS allows remote storage to be mounted as a local directory on Linux systems.

### Example Mount Command

```
sudo mount -t nfs4 fs-12345678:/ /mnt/efs
```

After mounting:

```
/mnt/efs
```

acts like a normal folder.

Example:

```
cd /mnt/efs
touch file1.txt
```

The file is stored directly inside the **EFS file system**.

---

# 2.6 Network Connectivity

Amazon EFS works within a **VPC network environment**.

EC2 instances must have **network connectivity to the EFS mount target**.

### Required Network Components

1️⃣ VPC
2️⃣ Subnets
3️⃣ Security Groups
4️⃣ Mount Targets

### Security Group Rule

EFS uses **NFS port 2049**

Security group rule example:

```
Type: NFS
Protocol: TCP
Port: 2049
Source: EC2 Security Group
```

### Network Flow

```
EC2 Instance
      │
      │  NFS Port 2049
      ▼
Mount Target (ENI)
      │
      ▼
Amazon EFS File System
```

---

# 🔹 Full EFS Architecture Diagram

```
                AWS Region
            (ap-south-1 Mumbai)

                  Amazon EFS
                 File System
                       │
        ┌──────────────┼──────────────┐
        │                              │
   Mount Target                    Mount Target
   (ap-south-1a)                   (ap-south-1b)
        │                              │
   EC2 Instance A                 EC2 Instance B
        │                              │
   Application Server             Application Server
```

Both instances can **read and write files simultaneously**.

---

# Key Architecture Components

| Component          | Description                 |
| ------------------ | --------------------------- |
| EFS File System    | Shared file storage         |
| Mount Target       | Network endpoint for access |
| NFS Protocol       | File access protocol        |
| EC2 Instance       | Compute accessing storage   |
| Security Groups    | Network access control      |
| Availability Zones | High availability           |

---
---
# 📁 3. Amazon EFS Storage Classes
---
Amazon EFS provides **different storage classes** to optimize **cost and performance** depending on how frequently your files are accessed.

Using storage classes helps reduce storage costs by automatically moving infrequently accessed files to cheaper storage tiers.

---

# 3.1 EFS Standard Storage Class

**EFS Standard** is the default storage class in Amazon EFS.

It is designed for **frequently accessed files** and provides **low latency and high throughput**.

### Characteristics

* High performance
* Low latency
* Suitable for active workloads
* Data is stored across multiple Availability Zones

### Use Cases

* Web applications
* Content management systems
* DevOps build environments
* Machine learning workloads

### Example

```
Application Servers
        │
        ▼
   Amazon EFS Standard
   (Frequently accessed files)
```

Example files stored in Standard storage:

```
website_images
application_logs
active_project_files
```

---

# 3.2 EFS Infrequent Access (EFS IA)

**EFS Infrequent Access (IA)** is a lower-cost storage class designed for files that are **not accessed frequently**.

Files are automatically moved to EFS IA based on lifecycle policies.

### Characteristics

* Lower storage cost
* Slightly higher access latency
* Retrieval cost when files are accessed

### Use Cases

* Backup data
* Archive logs
* Old project files
* Rarely accessed data

### Example

```
Amazon EFS
     │
     ├── Standard Storage
     │      (Active files)
     │
     └── Infrequent Access
            (Rarely used files)
```

Example files stored in IA:

```
old_logs
archive_images
old_application_data
```

---

# 3.3 EFS Archive Storage Class

**EFS Archive** is the **lowest-cost storage tier** in Amazon EFS.

It is designed for files that are **very rarely accessed**.

### Characteristics

* Lowest storage cost
* Higher retrieval time
* Suitable for long-term data storage

### Use Cases

* Compliance data
* Long-term backups
* Historical data

Example:

```
Amazon EFS
   │
   ├── Standard
   │
   ├── Infrequent Access
   │
   └── Archive
```

---

# 3.4 Lifecycle Management in EFS

Amazon EFS provides **Lifecycle Management**, which automatically moves files between storage classes depending on access patterns.

This helps reduce storage costs.

### Lifecycle Policy Example

| File Condition           | Storage Class     |
| ------------------------ | ----------------- |
| Recently accessed        | Standard          |
| Not accessed for 30 days | Infrequent Access |
| Not accessed for 90 days | Archive           |

### Example Flow

```
File Created
     │
     ▼
EFS Standard
     │
     │ 30 days no access
     ▼
EFS Infrequent Access
     │
     │ 90 days no access
     ▼
EFS Archive
```

This process happens **automatically** when lifecycle management is enabled.

---

# Example Architecture with Lifecycle Policy

```
EC2 Instances
      │
      ▼
Amazon EFS File System
      │
      ├── Standard Storage
      │
      ├── Infrequent Access
      │
      └── Archive Storage
```

---

# Cost Optimization Example

Without lifecycle:

```
All files stored in Standard
Higher cost
```

With lifecycle:

```
Active files → Standard
Old files → IA
Very old files → Archive
Lower cost
```

---

# Important DevOps Interview Question

### Why use EFS Lifecycle Policies?

Answer:

* Automatically moves unused files to cheaper storage
* Reduces storage cost
* No manual data management required

---

# Quick Comparison

| Storage Class     | Access Frequency | Cost   | Latency |
| ----------------- | ---------------- | ------ | ------- |
| Standard          | Frequent         | High   | Low     |
| Infrequent Access | Occasional       | Medium | Medium  |
| Archive           | Rare             | Lowest | Higher  |

---
---
# 📁 4. Creating Amazon EFS File System
---
In this section, we will learn how to **create an Amazon EFS file system** using the AWS Management Console and configure it so that EC2 instances can access it.

---

# 4.1 Prerequisites

Before creating Amazon EFS, the following resources must already exist in AWS.

### Required Resources

1. **AWS Account**
2. **VPC (Virtual Private Cloud)**
3. **Subnets in multiple Availability Zones**
4. **EC2 Instance (optional for mounting)**
5. **Security Group**

### Network Requirement

EFS uses **NFS protocol on port 2049**, so the security group must allow this port.

Example rule:

| Type | Protocol | Port | Source             |
| ---- | -------- | ---- | ------------------ |
| NFS  | TCP      | 2049 | EC2 Security Group |

---

# 4.2 Steps to Create EFS from AWS Console

Follow these steps to create an EFS file system.

### Step 1 — Open EFS Service

1. Login to **AWS Management Console**
2. Search for **EFS**
3. Open **Amazon Elastic File System**
4. Click **Create file system**

---

### Step 2 — Choose Creation Method

You will see two options:

* **Quick Create**
* **Customize**

For learning and production environments, choose **Customize**.

---

### Step 3 — Configure File System Settings

Enter the following details.

| Setting         | Description           |
| --------------- | --------------------- |
| Name            | File system name      |
| VPC             | Select your VPC       |
| Encryption      | Enable encryption     |
| Throughput Mode | Elastic (recommended) |

Example:

```
Name: devops-efs
VPC: default
Encryption: Enabled
Throughput: Elastic
```

---

### Step 4 — Configure Network (Mount Targets)

Now AWS will automatically create **Mount Targets** for each Availability Zone.

Example:

| Availability Zone | Subnet         | Mount Target |
| ----------------- | -------------- | ------------ |
| ap-south-1a       | Public Subnet  | Created      |
| ap-south-1b       | Private Subnet | Created      |

Mount targets allow EC2 instances to connect to EFS.

---

# 4.3 Configure Security Groups

Attach a **security group** to the mount target.

The security group must allow **NFS access**.

Example rule:

| Type | Protocol | Port | Source             |
| ---- | -------- | ---- | ------------------ |
| NFS  | TCP      | 2049 | EC2 Security Group |

Example architecture:

```
EC2 Instance
     │
Port 2049 (NFS)
     │
Security Group
     │
Mount Target
     │
Amazon EFS
```

---

# 4.4 Configure File System Settings

You can configure additional settings.

### Performance Mode

Options:

* **General Purpose** (recommended)
* **Max I/O**

General Purpose is best for:

* Web servers
* DevOps workloads
* CMS systems

---

### Throughput Mode

Options:

* Bursting
* Provisioned
* Elastic

Recommended:

```
Elastic Throughput
```

because it automatically scales performance.

---

# 4.5 Review and Create EFS

Check all configuration details:

```
File system name
VPC
Mount targets
Security group
Encryption
Performance mode
Throughput mode
```

Click:

```
Create File System
```

AWS will create the EFS file system.

Creation time:

```
~1 minute
```

---

# Example Architecture After Creation

```
            AWS Region
          (ap-south-1)

           Amazon EFS
          File System
                │
        ┌───────────────┐
        │ Mount Target  │  AZ-a
        └───────────────┘
               │
          EC2 Instance

        ┌───────────────┐
        │ Mount Target  │  AZ-b
        └───────────────┘
               │
          EC2 Instance
```

Both EC2 instances can **access the same shared storage**.

---

# 4.6 Verify EFS Creation

After creation, check:

```
EFS → File Systems
```

You should see:

* File System ID
* VPC
* Mount targets
* Security groups

Example:

```
fs-12345678
```

This ID will be used when **mounting EFS to EC2 instances**.

---

# Key Components Created

| Component       | Description          |
| --------------- | -------------------- |
| EFS File System | Shared storage       |
| Mount Targets   | Network access point |
| Security Group  | Controls NFS access  |
| File System ID  | Used for mounting    |

---
---
# 📁 5. Mounting Amazon EFS to EC2 Instance
---
After creating an **Amazon EFS file system**, the next step is to **mount it to an EC2 instance** so the instance can read and write files to the shared storage.

When mounted, the EFS file system behaves like a **local directory** on the EC2 instance.

---

# 5.1 Prerequisites for Mounting EFS

Before mounting EFS to an EC2 instance, ensure the following requirements are met.

### Required Components

| Component       | Requirement          |
| --------------- | -------------------- |
| EC2 Instance    | Linux-based instance |
| VPC             | Same VPC as EFS      |
| Security Group  | Allow NFS port 2049  |
| EFS File System | Already created      |
| Mount Target    | Available in the AZ  |

---

### Security Group Rule

EFS requires **NFS port 2049** to allow communication.

Example rule:

| Type | Protocol | Port | Source             |
| ---- | -------- | ---- | ------------------ |
| NFS  | TCP      | 2049 | EC2 Security Group |

---

# 5.2 Install NFS Client on Linux

To mount EFS, the EC2 instance must have the **NFS client installed**.

### For Amazon Linux / RHEL / CentOS

```bash
sudo yum install -y nfs-utils
```

---

### For Ubuntu

```bash
sudo apt update
sudo apt install -y nfs-common
```

---

# 5.3 Mount the EFS File System

First create a directory where EFS will be mounted.

```bash
sudo mkdir /mnt/efs
```

Now mount the EFS file system.

### Mount Command

```bash
sudo mount -t nfs4 fs-12345678:/ /mnt/efs
```

Replace:

```
fs-12345678
```

with your **EFS File System ID**.

---

### Verify Mount

Check mounted file systems:

```bash
df -h
```

Example output:

```
fs-12345678:/   8.0E   0   8.0E   0%   /mnt/efs
```

This confirms that **EFS is mounted successfully**.

---

# 5.4 Testing the Mount

Create a test file inside the mounted directory.

```bash
cd /mnt/efs
sudo touch testfile.txt
```

List files:

```bash
ls
```

Output:

```
testfile.txt
```

This file is now stored inside **Amazon EFS**.

---

# 5.5 Access Files from Multiple EC2 Instances

One of the main benefits of EFS is that **multiple EC2 instances can access the same file system simultaneously**.

Example architecture:

```
           Amazon EFS
         Shared Storage
               │
     ┌─────────┴─────────┐
     │                   │
EC2 Instance 1     EC2 Instance 2
   /mnt/efs            /mnt/efs
```

Both instances see the same files.

---

### Example Test

Instance 1:

```bash
cd /mnt/efs
echo "Hello from server1" > file1.txt
```

Instance 2:

```bash
cd /mnt/efs
cat file1.txt
```

Output:

```
Hello from server1
```

This proves that **EFS provides shared storage**.

---

# Example Production Architecture

```
                Load Balancer
                       │
        ┌──────────────┼──────────────┐
        │              │              │
     EC2 Server     EC2 Server     EC2 Server
        │              │              │
        └──────────────┼──────────────┘
                       │
                   Amazon EFS
               Shared File System
```

All servers share:

```
uploads
images
logs
application data
```

---

# Real DevOps Use Case

Example:

**WordPress Website Cluster**

```
EC2 Web Server 1
EC2 Web Server 2
EC2 Web Server 3
        │
        ▼
    Amazon EFS
```

All servers store **images and uploads** in the same EFS storage.

---

# Important DevOps Interview Question

### Why do we mount EFS to EC2?

Answer:

* To provide **shared storage**
* Multiple servers can access the same data
* Useful for **web clusters and container storage**

---
---
# 📁 6. Permanent Mount (Auto Mount on Reboot)
---

When you mount Amazon EFS using the normal `mount` command, the mount **disappears after the EC2 instance reboots**.

In production environments, we must configure **automatic mounting**, so the EFS file system mounts automatically whenever the EC2 instance starts.

This is done using the **/etc/fstab file**.

---

# 6.1 Why Permanent Mount is Required

If we mount EFS manually:

```bash
sudo mount -t nfs4 fs-12345678:/ /mnt/efs
```

After reboot:

```bash
reboot
```

The mount **will disappear**.

Example:

```bash
df -h
```

Output:

```
(no EFS mount)
```

So we configure **permanent mount using /etc/fstab**.

---

# 6.2 Install EFS Mount Helper

AWS provides a special tool called **amazon-efs-utils** that simplifies mounting and enables encryption in transit.

Install it on EC2.

### Amazon Linux

```bash
sudo yum install -y amazon-efs-utils
```

---

### Ubuntu

```bash
sudo apt install -y amazon-efs-utils
```

---

# 6.3 Create Mount Directory

Create the directory where EFS will be mounted.

```bash
sudo mkdir /mnt/efs
```

---

# 6.4 Configure /etc/fstab

Edit the `/etc/fstab` file.

```bash
sudo nano /etc/fstab
```

Add the following line at the end of the file.

```bash
fs-12345678:/ /mnt/efs efs defaults,_netdev 0 0
```

Replace:

```
fs-12345678
```

with your **EFS File System ID**.

---

# Explanation of fstab Entry

| Field         | Meaning                          |
| ------------- | -------------------------------- |
| fs-12345678:/ | EFS File System ID               |
| /mnt/efs      | Mount directory                  |
| efs           | File system type                 |
| defaults      | Default mount options            |
| _netdev       | Mount after network is available |

---

# 6.5 Test the Configuration

Now run the following command:

```bash
sudo mount -a
```

Check mounted storage.

```bash
df -h
```

Example output:

```
fs-12345678:/   8.0E   0   8.0E   0%   /mnt/efs
```

This confirms the **EFS mount is working**.

---

# 6.6 Verify After Reboot

Now reboot the EC2 instance.

```bash
sudo reboot
```

After login again:

```bash
df -h
```

Output should still show:

```
/mnt/efs
```

This means **EFS mounted automatically**.

---

# Example Architecture with Auto Mount

```
              Load Balancer
                     │
        ┌────────────┼────────────┐
        │                         │
     EC2 Server 1             EC2 Server 2
        │                         │
        │ /mnt/efs                │ /mnt/efs
        └────────────┼────────────┘
                     │
                Amazon EFS
            Shared File Storage
```

Even if servers restart, **EFS automatically mounts**.

---

# Real DevOps Production Use Case

Example:

**Web Server Cluster**

```
Auto Scaling Group
       │
 ┌─────┼─────┐
 │     │     │
EC2   EC2   EC2
 │     │     │
 └─────┼─────┘
       │
   Amazon EFS
```

Each instance automatically mounts:

```
/mnt/efs
```

This is very common in:

* Web clusters
* Kubernetes persistent storage
* CI/CD build environments

---

# Important DevOps Interview Question

### Why use `_netdev` in `/etc/fstab`?

Answer:

It ensures the file system **mounts only after the network is available**, preventing boot errors.

---
---
# 📁 7. Amazon EFS Performance Modes
---
Amazon EFS provides **performance modes** to optimize how the file system handles **latency, throughput, and scalability** depending on the workload.

Performance mode is selected **when the file system is created** and cannot be changed later.

There are **two performance modes** available.

* General Purpose
* Max I/O

---

# 7.1 General Purpose Performance Mode

**General Purpose mode** is the **default and most commonly used** performance mode.

It provides **low latency** and is ideal for workloads that require **fast file operations**.

### Characteristics

* Low latency
* High performance
* Suitable for most applications
* Supports a large number of operations per second

### Best Use Cases

* Web servers
* Content management systems
* DevOps environments
* WordPress websites
* Application servers

Example architecture:

```
          Load Balancer
               │
     ┌─────────┼─────────┐
     │         │         │
   EC2       EC2       EC2
     │         │         │
     └─────────┼─────────┘
               │
          Amazon EFS
      General Purpose Mode
```

This mode provides **fast response time for file operations**.

---

# 7.2 Max I/O Performance Mode

**Max I/O mode** is designed for workloads that require **very high levels of parallel access**.

It supports **thousands of EC2 instances accessing the file system simultaneously**.

However, it has **higher latency compared to General Purpose mode**.

### Characteristics

* Higher throughput
* Supports massive parallel workloads
* Higher latency

### Best Use Cases

* Big data analytics
* Machine learning workloads
* Media processing
* Large distributed applications

Example architecture:

```
          Data Processing Cluster

EC2  EC2  EC2  EC2  EC2  EC2
 │    │    │    │    │    │
 └────┴────┴────┴────┴────┘
          Amazon EFS
            Max I/O
```

This architecture is commonly used in **data processing clusters**.

---

# Performance Mode Comparison

| Feature     | General Purpose  | Max I/O            |
| ----------- | ---------------- | ------------------ |
| Latency     | Low              | Higher             |
| Scalability | High             | Very High          |
| Best for    | Web applications | Big data workloads |
| Default     | Yes              | No                 |

---

# Important DevOps Interview Concept

### Which performance mode should you choose?

**General Purpose** should be used for:

* Most applications
* Web servers
* CMS systems
* DevOps workloads

**Max I/O** should be used for:

* Large distributed systems
* Big data processing
* Machine learning pipelines

---

# Example DevOps Architecture

```
              Internet
                 │
           Application Load Balancer
                 │
       ┌─────────┼─────────┐
       │         │         │
     EC2       EC2       EC2
       │         │         │
       └─────────┼─────────┘
                 │
            Amazon EFS
         General Purpose Mode
```

All servers share the **same file storage**.

---

# Important Note

Performance mode **cannot be changed after the file system is created**, so it must be chosen carefully during creation.

---
---
# 📁 8. Amazon EFS Throughput Modes
---
Throughput in Amazon EFS determines **how fast data can be read or written** to the file system.

AWS provides different **throughput modes** so that applications can get the required performance depending on workload demand.

There are **three throughput modes** in Amazon EFS:

1. Bursting Throughput
2. Provisioned Throughput
3. Elastic Throughput

---

# 8.1 Bursting Throughput

**Bursting Throughput** is the default throughput mode for Amazon EFS.

In this mode, throughput automatically scales based on the **amount of storage used**.

The more data stored in the file system, the **higher the baseline throughput** available.

### How It Works

EFS uses a **credit system**.

When the file system is not heavily used, it accumulates **burst credits**.
During high workloads, it uses these credits to increase throughput.

### Example

```text
Stored Data Size → Throughput
```

| Data Stored | Baseline Throughput  |
| ----------- | -------------------- |
| 100 GB      | Lower throughput     |
| 1 TB        | Higher throughput    |
| 10 TB       | Very high throughput |

### Use Cases

* Development environments
* Web applications
* Small and medium workloads

Example architecture:

```
EC2 Instances
      │
      ▼
Amazon EFS
(Bursting Throughput)
```

---

# 8.2 Provisioned Throughput

Provisioned Throughput allows you to **manually set the throughput level** for your file system.

This is useful when your application requires **consistent high throughput regardless of storage size**.

### Characteristics

* Throughput is independent of storage size
* Predictable performance
* Ideal for high-performance workloads

### Example

Even if storage is small:

```
Storage = 200 GB
Provisioned Throughput = 200 MB/s
```

The system will still maintain **high throughput**.

### Use Cases

* Big data analytics
* Media processing
* Data-intensive applications

Example architecture:

```
Data Processing Servers
        │
        ▼
    Amazon EFS
(Provisioned Throughput)
```

---

# 8.3 Elastic Throughput

**Elastic Throughput** automatically adjusts throughput based on workload demand.

This is the **recommended mode for most modern applications**.

It eliminates the need to manage throughput manually.

### Characteristics

* Automatically scales throughput
* Handles sudden workload spikes
* Pay only for what you use

### Use Cases

* DevOps pipelines
* Microservices
* Container workloads
* Web applications

Example architecture:

```
Auto Scaling Group
       │
 ┌─────┼─────┐
 │     │     │
EC2   EC2   EC2
 │     │     │
 └─────┼─────┘
       │
   Amazon EFS
Elastic Throughput
```

---

# Throughput Mode Comparison

| Feature            | Bursting         | Provisioned           | Elastic                |
| ------------------ | ---------------- | --------------------- | ---------------------- |
| Throughput Scaling | Based on storage | Manual                | Automatic              |
| Cost               | Lower            | Higher                | Pay as used            |
| Performance        | Variable         | Predictable           | Dynamic                |
| Best For           | Small workloads  | High performance apps | Modern cloud workloads |

---

# Example Throughput Flow

```
Application Servers
        │
        ▼
   Amazon EFS
        │
 ┌─────────────┬─────────────┬─────────────┐
 │             │             │
Bursting   Provisioned   Elastic
Throughput Throughput    Throughput
```

---

# DevOps Interview Question

### What is the difference between Performance Mode and Throughput Mode?

| Feature       | Performance Mode                 | Throughput Mode                  |
| ------------- | -------------------------------- | -------------------------------- |
| Purpose       | Controls latency and scalability | Controls data transfer speed     |
| Options       | General Purpose / Max I/O        | Bursting / Provisioned / Elastic |
| Configuration | Selected during creation         | Can be modified later            |

---

# Example Production Architecture

```
Internet
    │
Load Balancer
    │
 ┌──┴───┬───┴───┬───┴───┐
 │      │       │      │
EC2    EC2     EC2    EC2
 │      │       │      │
 └──────┴───────┴──────┘
         │
      Amazon EFS
   Elastic Throughput
```

All servers share the **same scalable storage**.

---
---
# 📁 9. Amazon EFS Security
---

Security is a critical aspect of Amazon EFS. AWS provides multiple security mechanisms to protect data stored in the file system.

Amazon EFS security works at **multiple layers**, including:

* Network security
* Identity and access management
* Encryption
* Access control

These security mechanisms ensure that **only authorized resources can access the file system**.

---

# 9.1 Security Groups

Security Groups control **network-level access** to the EFS mount targets.

Amazon EFS uses the **NFS protocol on port 2049**, so EC2 instances must be allowed to connect to this port.

### Security Group Rule Example

| Type | Protocol | Port | Source             |
| ---- | -------- | ---- | ------------------ |
| NFS  | TCP      | 2049 | EC2 Security Group |

### Architecture Example

```
EC2 Instance
     │
     │  Port 2049
     ▼
Security Group
     │
Mount Target
     │
Amazon EFS
```

If this rule is not configured correctly, **EC2 instances cannot mount the EFS file system**.

---

# 9.2 IAM Policies for EFS

AWS Identity and Access Management (IAM) controls **who can manage EFS resources**.

IAM policies allow or deny actions such as:

* Creating file systems
* Deleting file systems
* Modifying EFS configuration
* Creating access points

### Example IAM Actions

| Action                                | Description |
| ------------------------------------- | ----------- |
| elasticfilesystem:CreateFileSystem    | Create EFS  |
| elasticfilesystem:DeleteFileSystem    | Delete EFS  |
| elasticfilesystem:DescribeFileSystems | View EFS    |

Example IAM policy snippet:

```json
{
  "Effect": "Allow",
  "Action": "elasticfilesystem:*",
  "Resource": "*"
}
```

---

# 9.3 Encryption at Rest

Encryption at Rest protects data stored in the EFS file system.

When enabled, all files stored in EFS are **encrypted using AWS Key Management Service (KMS)**.

### Key Points

* Data stored in EFS is encrypted
* Encryption uses AWS-managed or customer-managed keys
* Protects against unauthorized disk access

Example architecture:

```
EC2 Instance
      │
      ▼
Encrypted Data
      │
Amazon EFS
(KMS Encryption)
```

Encryption must be enabled **during file system creation**.

---

# 9.4 Encryption in Transit

Encryption in Transit protects data **while it is being transferred between EC2 and EFS**.

This ensures secure communication across the network.

It uses **TLS (Transport Layer Security)**.

### Example Mount Command with Encryption

```bash
sudo mount -t efs -o tls fs-12345678:/ /mnt/efs
```

Here:

```
tls
```

enables encrypted data transfer.

### Data Flow

```
EC2 Instance
     │
Encrypted TLS Connection
     │
Amazon EFS
```

This prevents **network interception or data snooping**.

---

# 9.5 Amazon EFS Access Points

Access Points provide **application-level access control** for EFS.

They allow different applications to access different directories within the same file system.

### Key Benefits

* Simplified access management
* Application-specific access
* Enforced user permissions

Example architecture:

```
Amazon EFS
     │
 ┌───┼───────────┐
 │               │
Access Point 1   Access Point 2
 │               │
App Server A     App Server B
```

Example:

```
Access Point A → /app1
Access Point B → /app2
```

Each application accesses only its own directory.

---

# Security Layers in Amazon EFS

| Layer         | Security Feature      |
| ------------- | --------------------- |
| Network       | Security Groups       |
| Identity      | IAM Policies          |
| Storage       | Encryption at Rest    |
| Data Transfer | Encryption in Transit |
| Application   | Access Points         |

---

# Example Secure Architecture

```
                Internet
                    │
            Application Load Balancer
                    │
        ┌───────────┼───────────┐
        │           │           │
      EC2         EC2         EC2
        │           │           │
        │ TLS Encrypted Traffic │
        └───────────┼───────────┘
                    │
                Mount Target
                    │
                Amazon EFS
            Encrypted Storage
```

This architecture ensures **secure storage and secure data transfer**.

---

# DevOps Interview Question

### How is Amazon EFS secured?

Amazon EFS security uses multiple mechanisms:

1. Security Groups (network access control)
2. IAM policies (user permissions)
3. Encryption at rest (data protection)
4. Encryption in transit (secure communication)
5. Access Points (application-level access)

---
---
# 📁 10. Amazon EFS Access Points
---
Amazon EFS **Access Points** provide a way to manage **application-level access** to a shared EFS file system.

They allow different applications or services to **access specific directories with defined permissions** inside the same EFS file system.

Access Points simplify storage management by providing **controlled access paths** for applications.

---

# 10.1 What are Amazon EFS Access Points

An **Access Point** is a special entry point to an EFS file system that:

* Enforces a specific directory path
* Applies user and group permissions
* Simplifies application access to shared storage

Instead of mounting the **entire file system**, applications mount **specific directories through access points**.

### Example

```
Amazon EFS
      │
 ┌────┼─────┐
 │    │     │
AP1  AP2   AP3
 │    │     │
/app1 /app2 /data
```

Each application gets access only to its **designated directory**.

---

# 10.2 Benefits of Access Points

Using access points provides several advantages.

### 1. Application Isolation

Each application accesses only its own directory.

Example:

```
App1 → /app1
App2 → /app2
```

---

### 2. Simplified Permission Management

Access points automatically enforce **POSIX permissions** for applications.

This removes the need to manually manage file permissions.

---

### 3. Secure Multi-Application Access

Multiple applications can share the same EFS file system without interfering with each other.

Example:

```
Amazon EFS
     │
 ┌───┼─────────────┐
 │   │             │
App1 App2        App3
```

---

### 4. Easy Integration with Containers

Access Points are commonly used with:

* Amazon EKS
* Amazon ECS
* AWS Lambda

They provide **persistent storage for containers**.

---

# 10.3 Creating Amazon EFS Access Points

Follow these steps to create an access point.

### Step 1 — Open EFS Console

1. Login to AWS Console
2. Go to **Amazon EFS**
3. Select your **File System**

---

### Step 2 — Create Access Point

Click:

```
Access Points → Create Access Point
```

---

### Step 3 — Configure Access Point

Provide the following details.

| Setting        | Description            |
| -------------- | ---------------------- |
| Name           | Access point name      |
| File System    | Select EFS file system |
| Root Directory | Directory path         |

Example:

```
Access Point Name: app1-access
Root Directory: /app1
```

---

### Step 4 — Configure POSIX Permissions

Define the **user ID and group ID** for access.

Example:

```
User ID: 1000
Group ID: 1000
Permissions: 755
```

This ensures proper file permissions.

---

### Step 5 — Create Access Point

Click:

```
Create Access Point
```

AWS will generate an **Access Point ID**.

Example:

```
fsap-12345678
```

---

# 10.4 Mounting Using Access Point

To mount the EFS file system using an access point:

```bash
sudo mount -t efs -o tls,accesspoint=fsap-12345678 fs-12345678:/ /mnt/efs
```

Explanation:

| Parameter   | Meaning           |
| ----------- | ----------------- |
| tls         | Enable encryption |
| accesspoint | Access point ID   |
| fs-12345678 | File system ID    |

This mounts the **specific directory configured in the access point**.

---

# Example Architecture

```
                 Application Servers
                         │
        ┌────────────────┼────────────────┐
        │                │                │
     App Server 1     App Server 2     App Server 3
        │                │                │
      Access Point     Access Point     Access Point
        │                │                │
        └────────────────┼────────────────┘
                         │
                     Amazon EFS
```

Each server accesses a **separate directory** within the same file system.

---

# Real DevOps Use Case

Example: **Kubernetes Persistent Storage**

```
Kubernetes Cluster
       │
 ┌─────┼─────┐
 │     │     │
Pod1  Pod2  Pod3
 │     │     │
 └─────┼─────┘
       │
  EFS Access Points
       │
    Amazon EFS
```

Each container uses **its own access point** for storage.

---

# DevOps Interview Question

### Why are EFS Access Points used?

Access Points are used to:

* Provide application-specific access to EFS
* Simplify permission management
* Improve security
* Enable container storage

---

# Access Point vs Mounting Root

| Feature               | Root Mount         | Access Point       |
| --------------------- | ------------------ | ------------------ |
| Access Scope          | Entire file system | Specific directory |
| Security              | Less control       | More secure        |
| Application Isolation | No                 | Yes                |

---
---
# 📁 11. Monitoring Amazon EFS
---

Monitoring Amazon EFS helps administrators and DevOps engineers **track performance, detect issues, and optimize storage usage**.

AWS provides monitoring tools such as **Amazon CloudWatch** to observe the health and activity of the EFS file system.

Monitoring helps answer questions like:

* How much storage is being used?
* What is the current throughput?
* Are there performance bottlenecks?
* Are applications accessing the file system correctly?

---

# 11.1 Amazon CloudWatch Metrics

Amazon EFS automatically sends **performance and usage metrics** to **Amazon CloudWatch**.

CloudWatch allows you to monitor EFS in **real time**.

### Common EFS Metrics

| Metric             | Description                         |
| ------------------ | ----------------------------------- |
| BurstCreditBalance | Available burst credits             |
| DataReadIOBytes    | Amount of data read                 |
| DataWriteIOBytes   | Amount of data written              |
| ClientConnections  | Number of connected clients         |
| PercentIOLimit     | Percentage of throughput limit used |

---

### Example Monitoring Flow

```
EC2 Instances
       │
       ▼
Amazon EFS
       │
       ▼
Amazon CloudWatch
       │
   Monitoring Dashboard
```

Administrators can view metrics directly in the **CloudWatch dashboard**.

---

# 11.2 Monitoring Performance

Performance monitoring helps identify **latency or throughput problems**.

Important metrics to monitor include:

### Throughput

Measures the speed of data transfer between EFS and EC2.

Example:

```
High Throughput → Good performance
Low Throughput → Possible bottleneck
```

---

### I/O Operations

Tracks the number of read and write operations.

Example metrics:

```
DataReadIOBytes
DataWriteIOBytes
```

These metrics show **how actively the file system is being used**.

---

### Client Connections

This metric shows how many EC2 instances are connected to EFS.

Example:

| Metric            | Example Value |
| ----------------- | ------------- |
| ClientConnections | 5             |

Meaning **5 EC2 instances are accessing the file system**.

---

# 11.3 Monitoring Storage Usage

CloudWatch also tracks **how much storage the file system is consuming**.

Example:

```
Total Storage Used
```

Example scenario:

```
Storage used = 200 GB
```

This helps with:

* Capacity planning
* Cost optimization
* Storage lifecycle management

---

# 11.4 Creating CloudWatch Alarms

CloudWatch alarms allow administrators to receive **alerts when metrics exceed defined thresholds**.

### Example Alert Conditions

| Condition               | Alert             |
| ----------------------- | ----------------- |
| High throughput usage   | Performance alert |
| Burst credits low       | Warning           |
| High client connections | Capacity alert    |

---

### Example Alarm Workflow

```
Amazon EFS
      │
      ▼
CloudWatch Metric
      │
      ▼
CloudWatch Alarm
      │
      ▼
SNS Notification
```

When a threshold is reached, AWS sends a notification via:

* Email
* SMS
* Lambda
* Slack integration

---

# Example Monitoring Architecture

```
                EC2 Instances
                     │
                     ▼
                 Amazon EFS
                     │
                     ▼
               Amazon CloudWatch
                     │
                     ▼
               CloudWatch Alarms
                     │
                     ▼
                Email / SMS Alert
```

This architecture ensures **continuous monitoring of storage performance**.

---

# Real DevOps Monitoring Example

Example: **Web application cluster**

```
Load Balancer
      │
 ┌────┼────┐
 │    │    │
EC2  EC2  EC2
 │    │    │
 └────┼────┘
      │
   Amazon EFS
      │
   CloudWatch
      │
Monitoring Dashboard
```

DevOps teams monitor:

* Storage usage
* Throughput
* Application performance

---

# Important DevOps Interview Question

### Why monitor Amazon EFS?

Monitoring helps to:

* Detect performance bottlenecks
* Track storage usage
* Identify abnormal activity
* Optimize cost and performance

---

# Key Monitoring Metrics Summary

| Metric             | Purpose                     |
| ------------------ | --------------------------- |
| BurstCreditBalance | Monitor burst capacity      |
| DataReadIOBytes    | Track read operations       |
| DataWriteIOBytes   | Track write operations      |
| ClientConnections  | Monitor connected instances |
| PercentIOLimit     | Identify performance limits |

---
---
# 📁 12. Backup and Disaster Recovery in Amazon EFS
---
Backup and Disaster Recovery ensure that **data stored in Amazon EFS can be restored in case of data loss, corruption, or system failure**.

AWS provides built-in integration with **AWS Backup**, which allows automatic backups and recovery of EFS file systems.

Backup strategies help organizations maintain **data durability, compliance, and business continuity**.

---

# 12.1 AWS Backup Integration

Amazon EFS integrates directly with **AWS Backup**, a fully managed service that centralizes backup management for AWS resources.

Using AWS Backup you can:

* Automatically back up EFS file systems
* Define backup schedules
* Manage backup retention policies
* Restore data when needed

### Backup Architecture

```id="2pq4x1"
Amazon EFS
     │
     ▼
AWS Backup Service
     │
     ▼
Backup Vault
```

Backups are stored securely in a **Backup Vault**.

---

# 12.2 Creating Backup Policies

Backup policies define **how often backups occur and how long they are stored**.

A backup plan usually includes:

* Backup schedule
* Backup window
* Retention period

### Example Backup Policy

| Parameter        | Example Value |
| ---------------- | ------------- |
| Backup Frequency | Daily         |
| Backup Time      | 2:00 AM       |
| Retention Period | 30 Days       |

Example configuration:

```id="mx74ti"
Backup Plan:
Daily Backup
Retention: 30 Days
```

---

# 12.3 Steps to Enable Backup for EFS

### Step 1 — Open AWS Backup

1. Login to **AWS Console**
2. Search for **AWS Backup**
3. Open the AWS Backup service

---

### Step 2 — Create Backup Plan

Click:

```id="ehl2ze"
Create Backup Plan
```

Options:

* Build a new plan
* Use a predefined template

Example:

```id="8axyr5"
Daily Backup Plan
```

---

### Step 3 — Assign Resources

Select the **EFS File System** you want to back up.

Example:

```id="4ssqsz"
Resource Type: EFS
File System ID: fs-12345678
```

---

### Step 4 — Assign Backup Vault

Choose the **backup vault** where backups will be stored.

Example:

```id="hsdfrh"
Vault Name: efs-backup-vault
```

---

### Step 5 — Enable Backup

Once configured, AWS will **automatically create backups according to the defined schedule**.

---

# 12.4 Restoring Amazon EFS Backup

If data is lost or corrupted, you can restore the EFS file system.

### Steps to Restore

1. Open **AWS Backup Console**
2. Go to **Backup Vault**
3. Select a **recovery point**
4. Click:

```id="jv8z2y"
Restore
```

---

### Restore Options

| Option                | Description              |
| --------------------- | ------------------------ |
| Restore to new EFS    | Create a new file system |
| Restore existing data | Recover previous state   |

Example:

```id="iqltbe"
Backup → Restore → New EFS File System
```

---

# 12.5 Disaster Recovery Strategy

Disaster recovery ensures data availability even during major system failures.

EFS provides high durability by storing data across **multiple Availability Zones**.

However, backups are still important for:

* Accidental file deletion
* Data corruption
* Ransomware attacks

---

### Disaster Recovery Architecture

```id="41bqtk"
EC2 Instances
       │
       ▼
   Amazon EFS
       │
       ▼
   AWS Backup
       │
       ▼
   Backup Vault
       │
       ▼
   Restore Process
```

---

# Example Production Backup Architecture

```id="m2r7u4"
Application Servers
        │
        ▼
     Amazon EFS
        │
        ▼
     AWS Backup
        │
        ▼
     Backup Vault
        │
        ▼
  Disaster Recovery Restore
```

This ensures that **data can be recovered quickly** if a failure occurs.

---

# Key Backup Concepts

| Feature        | Description                  |
| -------------- | ---------------------------- |
| AWS Backup     | Centralized backup service   |
| Backup Plan    | Defines backup schedule      |
| Backup Vault   | Storage location for backups |
| Recovery Point | Snapshot used for restore    |

---

# Important DevOps Interview Question

### Why is backup required even though EFS is highly durable?

Even though EFS stores data across multiple Availability Zones, backups are required to protect against:

* Accidental deletion
* Application errors
* Security incidents
* Data corruption

---
---
# 📁 13. Amazon EFS Pricing Model
---

Amazon EFS pricing is **pay-as-you-go**, meaning you only pay for the resources you use. The cost mainly depends on:

* Storage used
* Storage class
* Throughput configuration
* Data transfer

Pricing varies by AWS Region (for example **Asia Pacific – Mumbai (ap-south-1)**), but the pricing model structure remains the same.

---

# 13.1 Storage Pricing

The primary cost of Amazon EFS is based on the **amount of data stored** in the file system.

AWS charges per **GB per month**.

### Storage Classes Pricing Structure

| Storage Class         | Cost    | Description               |
| --------------------- | ------- | ------------------------- |
| EFS Standard          | Highest | Frequently accessed files |
| EFS Infrequent Access | Lower   | Rarely accessed data      |
| EFS Archive           | Lowest  | Long-term storage         |

Example scenario:

```
Stored Data = 500 GB
Storage Class = Standard
Monthly Cost = 500 × price per GB
```

Example architecture:

```
EC2 Instances
      │
      ▼
Amazon EFS
(Storage charged per GB)
```

You only pay for **actual storage used**, not for allocated capacity.

---

# 13.2 Throughput Pricing

Throughput pricing depends on the **throughput mode selected**.

### Elastic Throughput

* Automatically scales with workload
* Pay for throughput used

Best for:

* Web applications
* DevOps workloads
* Dynamic workloads

---

### Provisioned Throughput

You manually define the throughput level.

Example:

```
Provisioned Throughput = 200 MB/s
```

You pay for the **configured throughput capacity**, even if it is not fully used.

Best for:

* Big data
* Media processing
* Data analytics

---

# 13.3 Data Transfer Pricing

Data transfer charges apply depending on how data moves across the network.

### Data Transfer Rules

| Scenario           | Cost    |
| ------------------ | ------- |
| Same AZ EC2 to EFS | Free    |
| Different AZ       | Charged |
| Internet transfer  | Charged |

Example:

```
EC2 (AZ-a) → EFS Mount Target (AZ-a) = Free
EC2 (AZ-a) → EFS Mount Target (AZ-b) = Cross-AZ cost
```

Architecture example:

```
AZ-a EC2
     │
     ▼
Mount Target (AZ-a)
     │
     ▼
Amazon EFS
```

---

# 13.4 Backup Pricing

When using **AWS Backup**, charges apply for:

* Backup storage
* Restore operations

Example:

```
Backup Storage = charged per GB
Restore = charged per request
```

Backups are stored inside **Backup Vaults**.

---

# 13.5 Lifecycle Cost Optimization

Lifecycle policies help **reduce storage costs automatically**.

Example lifecycle rule:

| Condition                | Storage Class     |
| ------------------------ | ----------------- |
| Active files             | Standard          |
| Not accessed for 30 days | Infrequent Access |
| Not accessed for 90 days | Archive           |

Example flow:

```
New File
   │
   ▼
Standard Storage
   │
30 Days No Access
   ▼
Infrequent Access
   │
90 Days No Access
   ▼
Archive Storage
```

This automatically reduces storage cost.

---

# Example Cost Optimization Architecture

```
Application Servers
        │
        ▼
     Amazon EFS
        │
 ┌─────────────┬─────────────┐
 │             │             │
Standard      IA          Archive
Storage     Storage        Storage
```

Active data stays in **Standard**, older data moves to **cheaper storage classes**.

---

# Cost Optimization Best Practices

To reduce EFS cost:

1. Enable **Lifecycle policies**
2. Use **Elastic throughput**
3. Store infrequently accessed data in **IA or Archive**
4. Monitor storage usage with **CloudWatch**
5. Avoid unnecessary cross-AZ traffic

---

# Example Production Cost Scenario

```
Storage Used = 1 TB
Active Data = 300 GB
Old Data = 500 GB
Archive Data = 200 GB
```

Lifecycle policies move old files to cheaper tiers, reducing total cost.

---

# Key Pricing Components Summary

| Component     | Charged Based On    |
| ------------- | ------------------- |
| Storage       | GB per month        |
| Throughput    | Mode and usage      |
| Data Transfer | Network traffic     |
| Backup        | Backup storage size |

---

# Important DevOps Interview Question

### Why is Amazon EFS considered cost efficient?

Because:

* No storage provisioning required
* Automatic scaling
* Lifecycle policies reduce cost
* Pay only for storage used

---
---
# 📁 14. Amazon EFS Integration with AWS Services
---

Amazon EFS integrates with several AWS services to provide **shared, scalable file storage** for different workloads such as compute, containers, and serverless applications.

The most common integrations include:

* EC2
* ECS
* EKS
* AWS Lambda

These integrations allow applications running on AWS to **share and persist data across multiple compute resources**.

---

# 14.1 Amazon EFS with EC2

Amazon EFS is commonly used with **Amazon EC2 instances** to provide **shared storage across multiple servers**.

Multiple EC2 instances can mount the same EFS file system and access the same data simultaneously.

### Architecture

```
          Application Load Balancer
                   │
        ┌──────────┼──────────┐
        │          │          │
     EC2 Server  EC2 Server  EC2 Server
        │          │          │
        └──────────┼──────────┘
                   │
               Amazon EFS
```

### Use Cases

* Web server clusters
* Shared application data
* DevOps build systems
* Content management systems

Example:

```
/mnt/efs/uploads
/mnt/efs/images
/mnt/efs/logs
```

All EC2 instances can access these directories.

---

# 14.2 Amazon EFS with ECS

Amazon EFS provides **persistent shared storage for containers running in Amazon ECS**.

Containers normally have **ephemeral storage**, meaning data is lost when containers stop. EFS solves this by providing persistent storage.

### Architecture

```
           Amazon ECS Cluster
                 │
        ┌────────┼────────┐
        │        │        │
     Container Container Container
        │        │        │
        └────────┼────────┘
                 │
             Amazon EFS
```

### Benefits

* Persistent container storage
* Shared storage between containers
* Scalable storage for container workloads

Example use case:

```
Container logs
Shared configuration files
Application uploads
```

---

# 14.3 Amazon EFS with EKS

Amazon EFS integrates with **Amazon EKS (Elastic Kubernetes Service)** to provide **persistent volumes for Kubernetes workloads**.

EFS is used through the **EFS CSI Driver**, which allows Kubernetes pods to mount EFS file systems.

### Architecture

```
           Kubernetes Cluster
                 │
         ┌───────┼───────┐
         │       │       │
       Pod1    Pod2    Pod3
         │       │       │
         └───────┼───────┘
                 │
             Amazon EFS
```

### Benefits

* Shared persistent storage for Kubernetes pods
* Dynamic provisioning using access points
* Multi-node data access

Example use case:

```
Shared application data
ML model storage
CI/CD pipelines
```

---

# 14.4 Amazon EFS with AWS Lambda

Amazon EFS can also be used with **AWS Lambda functions** to provide persistent storage.

Normally, Lambda functions have limited temporary storage. EFS allows Lambda to access **large datasets and shared file storage**.

### Architecture

```
            AWS Lambda
                │
                ▼
            Amazon EFS
```

### Benefits

* Access large datasets
* Persistent storage for Lambda functions
* Share data between Lambda executions

### Example Use Cases

* Machine learning inference
* Media processing
* Large file processing

Example:

```
/mnt/efs/models
/mnt/efs/data
```

Lambda functions can access these directories.

---

# Integration Architecture Overview

```
             AWS Cloud
                 │
                 ▼
             Amazon EFS
                 │
 ┌───────────────┼───────────────┐
 │               │               │
EC2             ECS             EKS
 │               │               │
Web Apps     Containers     Kubernetes
                 │
                 ▼
              Lambda
```

Amazon EFS acts as a **central shared file storage system**.

---

# Real DevOps Architecture Example

```
             Internet
                 │
         Application Load Balancer
                 │
        ┌────────┼────────┐
        │        │        │
      EC2      ECS      EKS
        │        │        │
        └────────┼────────┘
                 │
             Amazon EFS
        Shared Persistent Storage
```

All services share the **same scalable storage**.

---

# Benefits of EFS Integration

| AWS Service | Benefit                         |
| ----------- | ------------------------------- |
| EC2         | Shared storage across instances |
| ECS         | Persistent container storage    |
| EKS         | Kubernetes persistent volumes   |
| Lambda      | Serverless persistent storage   |

---

# DevOps Interview Question

### Why is Amazon EFS useful for container workloads?

Because it provides:

* Persistent storage for containers
* Shared storage across multiple containers
* Automatic scaling
* Integration with ECS and EKS

---
