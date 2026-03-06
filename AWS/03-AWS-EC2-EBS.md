# 12. AWS EC2 – Elastic Block Store (EBS)

## 12.1 Introduction to Amazon EBS

**Amazon Elastic Block Store (EBS)** is a high-performance **block storage service** used with Amazon EC2 instances.

It provides **persistent storage volumes** that can be attached to EC2 instances. These volumes behave like **virtual hard drives** and can store operating systems, applications, and data.

EBS is designed for applications that require **low latency, high durability, and consistent performance**.

---

## 12.2 What is Block Storage

Block storage divides storage into **fixed-size blocks**, each with its own address.

Applications can read and write data directly to these blocks.

Example comparison:

| Storage Type   | Example    |
| -------------- | ---------- |
| Block Storage  | Amazon EBS |
| Object Storage | Amazon S3  |
| File Storage   | Amazon EFS |

In EC2 environments, EBS acts like a **hard disk attached to a virtual server**.

---

## 12.3 EBS Architecture

An EBS volume is created in a specific **Availability Zone** and attached to an EC2 instance within that same zone.

Example architecture:

```
EC2 Instance
     │
     ▼
EBS Volume
     │
     ▼
Stored in AWS Availability Zone
```

Each EBS volume automatically replicates data within its **Availability Zone** to ensure high availability.

---

## 12.4 Key Features of Amazon EBS

### Persistent Storage

EBS volumes retain data even if the EC2 instance is stopped or restarted.

Example:

```
Stop EC2 Instance
Start Instance
Data still available
```

---

### High Availability

EBS volumes replicate data automatically inside the Availability Zone.

This protects data against hardware failures.

---

### Elastic Storage

EBS volumes can be resized without stopping the EC2 instance.

Example:

```
Increase storage from 8 GB → 100 GB
```

---

### Snapshots for Backup

EBS supports **snapshots**, which are backups stored in Amazon S3.

Snapshots can be used to:

* Restore volumes
* Create new volumes
* Create AMIs

---

### Encryption

EBS volumes support **encryption using AWS Key Management Service (KMS)**.

Encrypted EBS protects:

* Data at rest
* Data in transit

---

## 12.5 Types of EBS Volumes

Amazon EBS provides different volume types designed for various workload requirements. Each type offers different performance characteristics such as **IOPS, throughput, latency, and cost**.

EBS volumes are **created in a specific Availability Zone (AZ)** and must be attached to EC2 instances **within the same Availability Zone**.

Example:

```
EC2 Instance (ap-south-1a)
       │
       ▼
EBS Volume (ap-south-1a)
```

If an EC2 instance is in another AZ, the volume **cannot be directly attached**. In that case, you must create a **snapshot and restore it in the required AZ**.

---

# 12.5.1 General Purpose SSD (gp3 / gp2)

General Purpose SSD volumes provide a balance between **performance, cost, and reliability**.

These volumes are suitable for:

* Boot volumes
* Web servers
* Small databases
* Development environments
* Application servers

### gp3 Performance

| Feature            | gp3        |
| ------------------ | ---------- |
| Maximum IOPS       | 16,000     |
| Maximum Throughput | 1,000 MB/s |
| Minimum Size       | 1 GB       |
| Maximum Size       | 16 TB      |

Advantages:

* Lower cost than gp2
* Independent IOPS configuration
* Consistent performance

---

# 12.5.2 Provisioned IOPS SSD (io1 / io2)

Provisioned IOPS SSD volumes are designed for **high-performance workloads that require consistent and predictable I/O performance**.

Typical use cases:

* Enterprise databases
* High transaction systems
* SAP workloads
* Large-scale relational databases

### io2 Performance

| Feature             | io2     |
| ------------------- | ------- |
| Maximum IOPS        | 256,000 |
| Maximum Volume Size | 64 TB   |
| Durability          | 99.999% |

These volumes are commonly used in **mission-critical applications**.

---

# 12.5.3 Throughput Optimized HDD (st1)

Throughput Optimized HDD volumes provide **low-cost magnetic storage with high throughput performance**.

Best suited for:

* Big data analytics
* Log processing
* Data warehouses
* Streaming workloads

### st1 Performance

| Feature            | st1         |
| ------------------ | ----------- |
| Maximum Throughput | 500 MB/s    |
| Volume Size        | Up to 16 TB |

---

# 12.5.4 Cold HDD (sc1)

Cold HDD volumes are the **lowest-cost EBS storage option**.

Designed for **infrequently accessed data**.

Common use cases:

* Archive storage
* Backup storage
* Long-term data retention

### sc1 Performance

| Feature                     | sc1 |
| --------------------------- | --- |
| Low cost storage            | Yes |
| High latency                | Yes |
| Ideal for archive workloads | Yes |

---

# 12.6 EBS Volume Attachment Types

EBS volumes support two types of attachment methods.

---

# 12.6.1 Single Instance Attachment

By default, an EBS volume can be attached to **only one EC2 instance at a time**.

Example architecture:

```
EC2 Instance
      │
      ▼
EBS Volume
```

Characteristics:

* Used in most workloads
* Simple storage model
* Suitable for applications requiring exclusive disk access

---

# 12.6.2 Multi-Attach (Multiple Instances)

Certain EBS volumes support **multi-attach**, allowing the same volume to be attached to **multiple EC2 instances simultaneously**.

Currently supported only for:

```
io1
io2
```

Example architecture:

```
EC2 Instance 1
      │
      ├── Shared EBS Volume
      │
EC2 Instance 2
```

Requirements:

* Instances must be in the **same Availability Zone**
* Instances must support **Nitro system**
* Applications must handle concurrent access

Use cases:

* Clustered file systems
* High availability databases
* Distributed applications

---

# 12.7 EBS Availability Zone Requirement

EBS volumes are **AZ-specific resources**.

Rules:

1. Volume must be created in the **same AZ as the EC2 instance**
2. Volumes cannot be attached across AZs
3. Snapshots must be used to move volumes across AZs

Example:

```
EC2 (ap-south-1a)
      │
      ▼
EBS Volume (ap-south-1a)   ✓ Allowed
```

```
EC2 (ap-south-1a)
      │
      ▼
EBS Volume (ap-south-1b)   ✗ Not allowed
```

---

# 12.8 Steps to Create an EBS Volume

## Step 1 – Open AWS Console

Navigate to:

```
AWS Console → EC2
```

---

## Step 2 – Open Volumes Section

Select:

```
Elastic Block Store → Volumes
```

Click:

```
Create Volume
```

---

## Step 3 – Configure Volume

Example configuration:

| Parameter         | Example     |
| ----------------- | ----------- |
| Volume Type       | gp3         |
| Size              | 20 GB       |
| Availability Zone | ap-south-1a |

---

## Step 4 – Create Volume

Click:

```
Create Volume
```

The volume will appear in the **Available state**.

---

# 12.9 Steps to Attach EBS Volume to EC2

## Step 1 – Select Volume

Go to:

```
EC2 → Volumes
```

Select the created volume.

---

## Step 2 – Attach Volume

Click:

```
Actions → Attach Volume
```

---

## Step 3 – Select Instance

Choose the EC2 instance.

Example:

```
Instance ID: i-0abc123456
Device Name: /dev/xvdf
```

Click:

```
Attach
```

---

# 12.10 Mounting the Volume (Linux)

After attaching the volume, it must be mounted.

List devices:

```bash
lsblk
```

Create file system:

```bash
sudo mkfs -t ext4 /dev/xvdf
```

Create mount directory:

```bash
sudo mkdir /data
```

Mount volume:

```bash
sudo mount /dev/xvdf /data
```

Verify mount:

```bash
df -h
```

---
## 12.11 Permanent Mount of EBS Volume (Linux)

When an **EBS volume is mounted manually**, the mount exists only until the instance is rebooted.
After a restart, the mount will disappear.

To ensure that the EBS volume **automatically mounts every time the EC2 instance starts**, we configure a **permanent mount using the `/etc/fstab` file**.

---

# 12.11.1 Why Permanent Mount is Required

By default:

```
mount /dev/xvdf /data
```

This mount is **temporary**.

If the instance reboots:

```
Reboot EC2 Instance
      │
      ▼
Volume not mounted
```

To solve this problem, we configure the volume in:

```
/etc/fstab
```

This ensures the volume mounts automatically during system startup.

---

# 12.11.2 Steps for Permanent Mount

Follow these steps after attaching the EBS volume.

---

## Step 1 – Check Attached Volumes

Run the following command to list storage devices:

```bash
lsblk
```

Example output:

```
NAME    MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
xvda    202:0    0   8G  0 disk /
xvdf    202:80   0  20G  0 disk
```

Here:

```
xvdf → Newly attached EBS volume
```

---

## Step 2 – Create File System

If the volume is new, create a file system.

Example:

```bash
sudo mkfs -t ext4 /dev/xvdf
```

Supported file systems include:

| File System | Use Case                |
| ----------- | ----------------------- |
| ext4        | Most common             |
| xfs         | Large storage workloads |

Example for XFS:

```bash
sudo mkfs -t xfs /dev/xvdf
```

---

## Step 3 – Create Mount Directory

Create a directory where the volume will be mounted.

Example:

```bash
sudo mkdir /data
```

---

## Step 4 – Mount the Volume Temporarily

Mount the volume:

```bash
sudo mount /dev/xvdf /data
```

Verify mount:

```bash
df -h
```

Example output:

```
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvdf        20G   24M   19G   1% /data
```

---

## Step 5 – Get the UUID of the Volume

Using **UUID** instead of device name prevents mount failures if device names change.

Run:

```bash
sudo blkid
```

Example output:

```
/dev/xvdf: UUID="6f1e2c3a-1234-5678-abcd-123456789abc" TYPE="ext4"
```

Copy the **UUID value**.

---

## Step 6 – Edit `/etc/fstab`

Open the file:

```bash
sudo nano /etc/fstab
```

Add the following entry at the end.

Example:

```
UUID=6f1e2c3a-1234-5678-abcd-123456789abc /data ext4 defaults,nofail 0 2
```

Explanation:

| Field    | Meaning                                 |
| -------- | --------------------------------------- |
| UUID     | Unique identifier of the volume         |
| /data    | Mount directory                         |
| ext4     | File system type                        |
| defaults | Default mount options                   |
| nofail   | System continues boot if volume missing |
| 0        | Dump backup option                      |
| 2        | File system check order                 |

---

## Step 7 – Test the Configuration

Before rebooting, test the configuration.

Run:

```bash
sudo mount -a
```

If there are no errors, the configuration is correct.

---

## Step 8 – Reboot the Instance

Restart the EC2 instance:

```bash
sudo reboot
```

---

## Step 9 – Verify Permanent Mount

After reboot, check:

```bash
df -h
```

Example output:

```
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvdf        20G   24M   19G   1% /data
```

The volume is now **permanently mounted**.

---

# 12.11.3 Example Mount Architecture

Example EC2 storage setup:

```
EC2 Instance
      │
      ├── Root Volume (EBS)
      │       /
      │
      └── Data Volume (EBS)
              /data
```

* `/` → Operating system volume
* `/data` → Application storage volume

---

# 12.12 EBS Snapshots

## 12.12.1 Introduction to EBS Snapshots

An **EBS Snapshot** is a **backup of an Amazon EBS volume** stored in Amazon S3.
Snapshots capture the state of an EBS volume at a specific point in time and allow you to **restore data, create new volumes, or recover from failures**.

Snapshots are widely used for:

* Data backup
* Disaster recovery
* Creating new EBS volumes
* Creating custom AMIs
* Migrating data between Availability Zones or Regions

Example concept:

```
EBS Volume
     │
     ▼
Snapshot (Stored in S3)
     │
     ▼
Restore → New EBS Volume
```

---

# 12.12.2 How EBS Snapshots Work

EBS snapshots are **incremental backups**.

This means:

* The first snapshot stores **all data blocks**.
* Subsequent snapshots store **only changed blocks**.

Example:

```
Snapshot 1 → Full backup
Snapshot 2 → Only changed data
Snapshot 3 → Only changed data
```

Benefits:

* Reduced storage cost
* Faster snapshot creation
* Efficient storage usage

---

# 12.12.3 Snapshot Architecture

Example architecture:

```
EC2 Instance
      │
      ▼
EBS Volume
      │
Create Snapshot
      │
      ▼
Stored in Amazon S3
```

Snapshots are stored in **Amazon S3 internally**, but users manage them through the **EBS service interface**.

---

# 12.12.4 Snapshot Use Cases

Snapshots are used in several scenarios.

### Backup and Recovery

Snapshots provide reliable backups of EBS volumes.

Example:

```
Application Data → Snapshot → Restore if failure occurs
```

---

### Disaster Recovery

Snapshots can be used to recreate volumes in case of system failure.

Example:

```
System failure
      │
      ▼
Restore volume from snapshot
```

---

### Create New EBS Volumes

Snapshots allow you to create multiple volumes from the same backup.

Example:

```
Snapshot
   │
   ├── Volume 1
   ├── Volume 2
   └── Volume 3
```

---

### Create Custom AMIs

Snapshots are used when creating **custom Amazon Machine Images (AMI)**.

Process:

```
EC2 Instance
      │
Create Snapshot
      │
Create AMI
```

---

# 12.12.5 Creating an EBS Snapshot

## Step 1 – Open AWS Console

Navigate to:

```
AWS Console → EC2
```

---

## Step 2 – Open Volumes

Select:

```
Elastic Block Store → Volumes
```

---

## Step 3 – Select Volume

Choose the EBS volume you want to back up.

---

## Step 4 – Create Snapshot

Click:

```
Actions → Create Snapshot
```

---

## Step 5 – Configure Snapshot

Provide details:

| Parameter   | Example                 |
| ----------- | ----------------------- |
| Description | Backup of web server    |
| Tags        | Environment: Production |

---

## Step 6 – Create Snapshot

Click:

```
Create Snapshot
```

The snapshot will appear in:

```
EC2 → Snapshots
```

---

# 12.12.6 Restoring an EBS Volume from Snapshot

Snapshots can be used to create new EBS volumes.

## Step 1 – Open Snapshots

Navigate to:

```
EC2 → Snapshots
```

---

## Step 2 – Select Snapshot

Choose the snapshot.

---

## Step 3 – Create Volume

Click:

```
Actions → Create Volume
```

---

## Step 4 – Configure Volume

Example configuration:

| Parameter         | Example     |
| ----------------- | ----------- |
| Volume Type       | gp3         |
| Size              | 20 GB       |
| Availability Zone | ap-south-1a |

---

## Step 5 – Create Volume

Click:

```
Create Volume
```

Attach the new volume to an EC2 instance.

---

# 12.12.7 Copying Snapshots Across Regions

Snapshots can be copied to another AWS region.

This is useful for **disaster recovery and cross-region backup**.

Example process:

```
Snapshot (Mumbai Region)
       │
Copy Snapshot
       │
       ▼
Snapshot (Singapore Region)
```

Steps:

```
Snapshots → Actions → Copy Snapshot
```

---

# 12.12.8 Snapshot Lifecycle Management

AWS provides **Amazon Data Lifecycle Manager (DLM)** to automate snapshot creation.

Features include:

* Automatic snapshot scheduling
* Automatic deletion of old snapshots
* Backup policies

Example policy:

```
Create snapshot every 24 hours
Keep last 7 snapshots
```

---

# 12.12.9 Snapshot Encryption

Snapshots support encryption using **AWS Key Management Service (KMS)**.

Encryption protects:

* Data at rest
* Snapshot backups

Example:

```
Encrypted EBS Volume → Encrypted Snapshot
```

---

# 12.12.10 Snapshot Pricing

EBS snapshot pricing is based on:

* Storage used by snapshot data
* Incremental storage changes

Example pricing model:

```
Pay for GB of snapshot storage
```

Because snapshots are incremental, storage costs are reduced.

---

# 12.13 EBS Volume Lifecycle

## 12.13.1 Introduction

The **EBS Volume Lifecycle** describes the different states an **Amazon Elastic Block Store (EBS) volume** goes through from creation to deletion.

Understanding the lifecycle is important for managing storage resources, troubleshooting issues, and ensuring proper data management.

An EBS volume typically goes through the following states:

1. Creating
2. Available
3. In-Use
4. Detaching
5. Deleting
6. Deleted

Example lifecycle flow:

```text
Create Volume → Available → Attach to EC2 → In-use → Detach → Delete
```

---

# 12.13.2 Creating State

When a new EBS volume is created, it enters the **Creating** state.

During this state:

* AWS provisions the storage volume
* The volume is prepared inside the selected **Availability Zone**
* The volume is not yet ready for attachment

Example process:

```text
User creates volume
        │
        ▼
Volume provisioning
        │
        ▼
State: Creating
```

Once the process finishes, the volume changes to **Available**.

---

# 12.13.3 Available State

When the volume is ready to be used, it enters the **Available** state.

Characteristics:

* The volume exists but is not attached to any EC2 instance
* It can be attached to an EC2 instance
* It can be deleted
* It can be used to create snapshots

Example:

```text
EBS Volume
     │
State: Available
     │
Ready to attach to EC2
```

---

# 12.13.4 In-Use State

When an EBS volume is attached to an EC2 instance, it enters the **In-Use** state.

Characteristics:

* The volume is actively connected to an EC2 instance
* The instance can read and write data to the volume
* Snapshots can still be created while the volume is in use

Example architecture:

```text
EC2 Instance
      │
      ▼
EBS Volume
(State: In-use)
```

Multiple EBS volumes can be attached to the same EC2 instance.

Example:

```text
EC2 Instance
     │
     ├── Root Volume
     ├── Data Volume
     └── Backup Volume
```

---

# 12.13.5 Detaching State

When an EBS volume is being removed from an EC2 instance, it enters the **Detaching** state.

During this state:

* AWS disconnects the volume from the instance
* Any ongoing disk operations are completed
* The volume becomes available again

Example:

```text
Detach Volume
      │
      ▼
State: Detaching
      │
      ▼
State: Available
```

It is recommended to **unmount the volume inside the operating system before detaching** to prevent data corruption.

Example command (Linux):

```bash
sudo umount /data
```

---

# 12.13.6 Deleting State

When a volume is deleted, it enters the **Deleting** state.

During this process:

* AWS removes the storage volume
* All data stored on the volume is permanently deleted

Example process:

```text
Delete Volume
      │
      ▼
State: Deleting
      │
      ▼
State: Deleted
```

Once deleted, the data cannot be recovered unless a **snapshot backup exists**.

---

# 12.13.7 Deleted State

After the deletion process completes, the volume enters the **Deleted** state.

Characteristics:

* The volume no longer exists
* Storage resources are released
* Billing for the volume stops

However, **snapshots created earlier remain available**.

Example:

```text
EBS Volume Deleted
       │
Snapshot Still Available
```

Snapshots can be used to recreate the volume.

---

# 12.13.8 Root Volume Lifecycle

When launching an EC2 instance, AWS automatically creates a **root EBS volume**.

Example:

```text
EC2 Instance
      │
      └── Root Volume (/)
```

If the instance is terminated, the root volume may also be deleted depending on the **Delete on Termination** setting.

| Setting  | Behavior              |
| -------- | --------------------- |
| Enabled  | Root volume deleted   |
| Disabled | Root volume preserved |

---

# 12.13.9 Example EBS Lifecycle Architecture

Example EC2 storage lifecycle:

```text
Create EBS Volume
       │
       ▼
State: Available
       │
Attach to EC2
       │
       ▼
State: In-use
       │
Detach Volume
       │
       ▼
State: Available
       │
Delete Volume
       │
       ▼
State: Deleted
```

---

# 12.14 EBS vs Instance Store


| Feature        | EBS                     | Instance Store           |
| -------------- | ----------------------- | ------------------------ |
| Persistence    | Persistent              | Temporary                |
| Data retention | Survives stop/start     | Lost when instance stops |
| Backup support | Snapshots available     | No backup                |
| Use cases      | Databases, applications | Temporary cache          |

---
