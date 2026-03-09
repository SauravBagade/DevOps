## 🔐 1. AWS IAM (Identity and Access Management)

### 1.1 What is AWS IAM?

**AWS IAM (Identity and Access Management)** is a security service provided by **Amazon Web Services (AWS)** that helps you **securely control access to AWS resources**.

It allows you to manage:

* **Who can access AWS**
* **What actions they can perform**
* **Which AWS resources they can use**

IAM is the **central security system of AWS** used to manage **authentication and authorization**.

---

## 🔑 Simple Definition

> **AWS IAM is a service that helps you control who can access your AWS account and what they can do inside it.**

Example:

| User            | Permission              |
| --------------- | ----------------------- |
| DevOps Engineer | Can create EC2, VPC     |
| Developer       | Can access S3 only      |
| Security Team   | Can manage IAM policies |
| Intern          | Read-only access        |

---

# 🧠 Core Concepts of AWS IAM

IAM works using **five main components**:

1. IAM Users
2. IAM Groups
3. IAM Roles
4. IAM Policies
5. Permissions

Let's understand each one.

---

# 👤 1. IAM User

An **IAM User** represents a **person or application** that needs access to AWS.

Example users:

* DevOps Engineer
* Developer
* Administrator
* Application service

Each IAM user has:

* **Username**
* **Password (for AWS Console)**
* **Access Keys (for CLI / API)**

### Example

```
User: devops-user
Password: Login to AWS Console
Access Key: Use AWS CLI
```

---

# 👥 2. IAM Group

An **IAM Group** is a collection of IAM users.

Instead of giving permissions to users individually, you can assign permissions to a **group**.

Example:

| Group Name | Users            | Permission      |
| ---------- | ---------------- | --------------- |
| Developers | dev1, dev2       | S3 access       |
| DevOps     | devops1, devops2 | EC2, VPC        |
| Admins     | admin1           | Full AWS access |

### Benefit

Easier permission management.

If a new developer joins:

```
Add user → Developers group
```

No need to assign permissions again.

---

# 🎭 3. IAM Role

An **IAM Role** is used to **grant temporary permissions to AWS services or users**.

Roles are mainly used when:

* EC2 needs access to S3
* Lambda needs access to DynamoDB
* Cross account access
* Temporary security credentials

### Example

EC2 instance needs to upload logs to S3.

Instead of storing access keys inside the server:

```
Create IAM Role
Attach S3 permission
Attach role to EC2 instance
```

EC2 will automatically get permissions.

---

# 📜 4. IAM Policy

A **Policy** is a **JSON document that defines permissions**.

Policies specify:

* **Which service**
* **Which actions**
* **Which resources**
* **Allow or Deny**

Example IAM Policy:

```json
{
 "Version": "2012-10-17",
 "Statement": [
   {
     "Effect": "Allow",
     "Action": "s3:ListBucket",
     "Resource": "*"
   }
 ]
}
```

Meaning:

```
User can list S3 buckets
```

---

# 🔐 5. Permissions

Permissions determine **what actions a user can perform in AWS**.

Example actions:

| Service | Action         |
| ------- | -------------- |
| EC2     | Start instance |
| EC2     | Stop instance  |
| S3      | Upload file    |
| VPC     | Create subnet  |

Example permission:

```
Allow: ec2:StartInstances
```

---

# 🔑 Authentication vs Authorization

| Concept        | Meaning          |
| -------------- | ---------------- |
| Authentication | Who are you?     |
| Authorization  | What can you do? |

Example:

```
Login with username/password → Authentication
Allowed to create EC2 → Authorization
```

IAM manages **both**.

---

# 🔐 Types of IAM Access

### 1️⃣ AWS Management Console Access

Login via browser.

Example:

```
https://aws.amazon.com/console
```

Use:

```
Username + Password
```

---

### 2️⃣ Programmatic Access

Used for:

* AWS CLI
* SDK
* Terraform
* Applications

Uses:

```
Access Key ID
Secret Access Key
```

Example CLI command:

```bash
aws s3 ls
```

---

# 🔐 IAM Security Best Practices

### 1. Never use root account

Root user has **full access to AWS**.

Use it only for:

* Billing
* Account settings

---

### 2. Enable MFA (Multi Factor Authentication)

Add extra security layer.

Example:

```
Password + OTP
```

---

### 3. Use IAM Roles instead of Access Keys

Roles provide **temporary credentials**.

More secure.

---

### 4. Follow Least Privilege Principle

Give only required permissions.

Example:

❌ Bad

```
AdministratorAccess
```

✔ Good

```
Only S3 read access
```

---

### 5. Rotate Access Keys

Change keys regularly.

---

# 🏗 IAM Architecture Example

```
AWS Account
     │
     ├── IAM Users
     │     ├── dev1
     │     ├── dev2
     │
     ├── IAM Groups
     │     ├── Developers
     │     ├── DevOps
     │
     ├── IAM Roles
     │     ├── EC2-S3-Role
     │     ├── Lambda-DynamoDB-Role
     │
     └── IAM Policies
           ├── S3ReadPolicy
           ├── EC2FullAccess
```

---

# 🧾 IAM Example Scenario (Real DevOps Use Case)

### DevOps Team Access

```
DevOps Group
    │
    ├── Permission
    │     ├── EC2 Full Access
    │     ├── VPC Full Access
    │     ├── CloudWatch Access
```

Users:

```
devops1
devops2
devops3
```

---

# ⚡ Advantages of AWS IAM

* Centralized access control
* High security
* Fine-grained permissions
* Temporary credentials
* Integration with all AWS services

---

# 📊 Summary

| IAM Component | Purpose             |
| ------------- | ------------------- |
| IAM User      | Individual identity |
| IAM Group     | Collection of users |
| IAM Role      | Temporary access    |
| IAM Policy    | Permission rules    |
| Permissions   | Allowed actions     |

---
