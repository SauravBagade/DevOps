---
# 📌 1️⃣ Terraform Introduction (Foundation)
---
This section explains **Terraform from zero level**, exactly like **official documentation**, but in **simple DevOps language** with **real-world meaning**.

---

## 1️⃣ What is Terraform

**Terraform** is an **Infrastructure as Code (IaC)** tool used to **create, update, and manage infrastructure automatically** using configuration files.

Instead of:

* Clicking in cloud consoles
* Creating servers manually
* Remembering steps

👉 You **write code**, and Terraform **builds the infrastructure for you**.

### In simple words

> Terraform is a tool that turns **code into real infrastructure**.

### Example

Using Terraform, you can create:

* EC2 instances
* VPCs
* Load balancers
* Kubernetes clusters
* Databases

with **one command**:

```bash
terraform apply
```

---

## 2️⃣ What is Infrastructure as Code (IaC)

**Infrastructure as Code (IaC)** means:

> Managing infrastructure using **code instead of manual actions**

### Traditional (Without IaC)

* Login to AWS Console
* Click → Create EC2
* Select options manually
* No record of what was created

### With IaC

* Infrastructure is written in files (`.tf`)
* Version controlled (Git)
* Reproducible
* Automated

### Example IaC file (Terraform)

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "my_ec2" {
  ami           = "ami-12345678"
  instance_type = "t2.micro"
}
```

Provider → Defines which cloud/service you are using (AWS, Azure, GCP).
Resource → Defines what infra you want (EC2, VPC, S3, etc.).
Arguments → Settings inside resources (ami, instance_type).
👉 It’s declarative → you say what you want, Terraform figures out how to do it.

---

## 3️⃣ Why Terraform is Used (Real DevOps Problems It Solves)

Terraform exists because **manual infrastructure fails at scale**.

### ❌ Real problems without Terraform

| Problem        | Reality                       |
| -------------- | ----------------------------- |
| Manual errors  | Wrong instance, wrong region  |
| No tracking    | Nobody knows what was created |
| No consistency | Dev ≠ Prod                    |
| No automation  | Slow deployments              |
| Hard rollback  | No history                    |

### ✅ What Terraform solves

* Automation of infrastructure
* Same infra across Dev / QA / Prod
* Version control (Git)
* Easy rollback
* Repeatable deployments

### Real DevOps Example

> “We need **20 EC2 servers**, **3 environments**, **same config**”

Without Terraform → weeks
With Terraform → minutes

---

## 4️⃣ Terraform Use Cases (Cloud, DevOps, Multi-Cloud)

### ☁️ Cloud Infrastructure

* AWS EC2, VPC, IAM
* Azure VM, VNet
* GCP Compute Engine

### ⚙️ DevOps Automation

* CI/CD infra
* Kubernetes clusters (EKS, AKS, GKE)
* Load balancers
* Auto Scaling

### 🌍 Multi-Cloud

* AWS + Azure + GCP together
* Same language for all clouds

### 🧪 Environments

* Dev
* Stage
* Production

Terraform allows **same code, different environments**.

---

## 5️⃣ Terraform vs Manual Infrastructure

| Feature         | Manual Setup | Terraform |
| --------------- | ------------ | --------- |
| Speed           | Slow         | Fast      |
| Errors          | High         | Low       |
| Repeatability   | ❌            | ✅         |
| Version control | ❌            | ✅         |
| Rollback        | Hard         | Easy      |
| Automation      | ❌            | ✅         |

### Reality

Manual infra **does not scale**
Terraform **is mandatory in real DevOps jobs**

---

## 6️⃣ Terraform vs CloudFormation vs ARM vs Ansible

### Comparison Table

| Tool           | Type               | Scope              | Cloud       |
| -------------- | ------------------ | ------------------ | ----------- |
| Terraform      | IaC                | Infra provisioning | Multi-cloud |
| CloudFormation | IaC                | Infra provisioning | AWS only    |
| ARM Templates  | IaC                | Infra provisioning | Azure only  |
| Ansible        | Configuration Mgmt | Software & config  | Any         |

### Key Differences

#### Terraform

* Multi-cloud
* Declarative
* Best for infrastructure

#### CloudFormation

* AWS native
* AWS only
* Deep AWS integration

#### ARM

* Azure native
* Azure only
* Complex syntax

#### Ansible

* Server configuration
* App deployment
* Not infra-focused

### Real DevOps Usage

> Terraform + Ansible together
> Terraform → create infra
> Ansible → configure servers

---

## 7️⃣ Terraform Advantages & Limitations

### ✅ Advantages

* Multi-cloud support
* Simple language (HCL)
* State management
* Large provider ecosystem
* Strong community
* Production-ready

### ❌ Limitations

* State file must be protected
* Not ideal for config management
* Learning curve for beginners
* Complex debugging sometimes

👉 Still, **Terraform is industry standard**

---

## 8️⃣ Who Maintains Terraform

Terraform is developed and maintained by:

### 🏢 **HashiCorp**

HashiCorp also created:

* Vault (Secrets)
* Consul (Service Discovery)
* Nomad (Workload Orchestration)
* Packer (Image building)

Terraform is **enterprise-grade** and widely used by:

* AWS
* Google
* Microsoft
* Netflix
* Uber
* Startups & enterprises

---
![Image](https://cms.cloudoptimo.com/uploads/terraform_eaa800441c.png)

![Image](https://media.beehiiv.com/cdn-cgi/image/fit%3Dscale-down%2Cformat%3Dauto%2Conerror%3Dredirect%2Cquality%3D80/uploads/asset/file/a70941e1-5fb2-4a29-a70b-a671150e9298/directory_2.png?t=1730702773)

![Image](https://k21academy.com/wp-content/uploads/2020/11/terraform-lifecycle.png)

# 📌 2️⃣ Terraform Setup

This section explains **Terraform CLI usage** and **project directory structure** exactly how it is used in **real DevOps projects** (not theory).

---

## 1️⃣ Terraform CLI Basics

The **Terraform CLI (Command Line Interface)** is the main way you interact with Terraform.
Every real Terraform action happens through CLI commands.

### 🔹 What Terraform CLI Does

* Reads `.tf` files
* Downloads providers
* Creates execution plans
* Applies infrastructure
* Manages state files

You never click UI buttons — **CLI is mandatory**.

---

### 🔹 Core Terraform CLI Commands (Foundation)

| Command              | Purpose                         |
| -------------------- | ------------------------------- |
| `terraform init`     | Initialize working directory    |
| `terraform plan`     | Show what Terraform will change |
| `terraform apply`    | Create / update infrastructure  |
| `terraform destroy`  | Delete infrastructure           |
| `terraform validate` | Validate configuration          |
| `terraform fmt`      | Format `.tf` files              |
| `terraform show`     | Show current state              |
| `terraform output`   | Read output values              |

---

### 🔹 Command Flow (Real Usage)

```bash
terraform init
terraform plan
terraform apply
```

This flow is **non-negotiable** in real projects.

---

### 🔹 terraform init (Most Important)

What it does:

* Downloads providers
* Initializes backend
* Creates `.terraform/` directory
* Locks provider versions

Without `init`, **nothing works**.

---

### 🔹 terraform plan

* Shows execution plan
* No real changes
* Used for review & approval

DevOps teams **must review plan** before apply.

---

### 🔹 terraform apply

* Executes changes
* Creates real resources
* Updates state file

Can be interactive or auto-approved:

```bash
terraform apply -auto-approve
```

---

### 🔹 terraform destroy

* Deletes all resources defined in code
* Dangerous in production

```bash
terraform destroy
```

---

### 🔹 terraform validate & fmt

* `validate` → syntax check
* `fmt` → formatting standard

Used in CI/CD pipelines.

---

### 🔹 Important Hidden Files

| File/Dir              | Purpose               |
| --------------------- | --------------------- |
| `.terraform/`         | Providers & plugins   |
| `.terraform.lock.hcl` | Provider version lock |
| `terraform.tfstate`   | Actual infra record   |

👉 **Never delete state files blindly**

---

## 2️⃣ Directory Structure Best Practices

### ❌ Bad Practice (Beginner Mistake)

```
terraform/
 ├─ main.tf
```

Problems:

* No clarity
* Not scalable
* Breaks in real projects

---

### ✅ Standard Terraform Project Structure (Single Environment)

```
terraform/
 ├─ main.tf
 ├─ variables.tf
 ├─ outputs.tf
 ├─ providers.tf
 ├─ versions.tf
 └─ terraform.tfvars
```

### Purpose of Each File

| File               | Purpose                       |
| ------------------ | ----------------------------- |
| `main.tf`          | Resource definitions          |
| `variables.tf`     | Input variables               |
| `outputs.tf`       | Output values                 |
| `providers.tf`     | Provider config               |
| `versions.tf`      | Terraform & provider versions |
| `terraform.tfvars` | Environment values            |

---

### ✅ Multi-Environment Structure (Real DevOps)

```
terraform/
 ├─ modules/
 │   ├─ vpc/
 │   ├─ ec2/
 │   └─ eks/
 │
 ├─ env/
 │   ├─ dev/
 │   │   ├─ main.tf
 │   │   ├─ terraform.tfvars
 │   │   └─ backend.tf
 │   ├─ stage/
 │   └─ prod/
```

### Why This Structure Works

* Reusable modules
* Separate environments
* Safe production deployments
* Easy CI/CD integration

---

### ✅ Module Folder Structure

```
modules/ec2/
 ├─ main.tf
 ├─ variables.tf
 ├─ outputs.tf
```

This is **industry standard**.

---

## 🔐 Directory Rules (Very Important)

### ❌ Never Commit

```
terraform.tfstate
terraform.tfstate.backup
.terraform/
```

Add to `.gitignore`.

---

![Image](https://miro.medium.com/0%2AbJzMGdZBo0zKfbvQ)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2AazlDiCZlFfytmHqEF3reyw.png)

# 📌 3️⃣ Terraform Architecture (Must Know)

This section explains **how Terraform actually works internally**.
If you understand this, **debugging + real projects become easy**.
This is written **like official documentation**, but in **clear DevOps language**.

---

## 1️⃣ Terraform CLI

The **Terraform CLI** is the **entry point** for everything.

### What Terraform CLI does

* Reads `.tf` configuration files
* Communicates with Terraform Core
* Downloads providers & plugins
* Executes plan and apply
* Manages state

### Reality

* No UI
* No dashboard
* **CLI is mandatory**

### Common CLI commands

* `terraform init`
* `terraform plan`
* `terraform apply`
* `terraform destroy`

👉 CLI **does not create infrastructure by itself**
It **delegates work to Terraform Core**

---

## 2️⃣ Terraform Core (Brain of Terraform)

**Terraform Core** is the **main engine**.

### Terraform Core responsibilities

* Parse `.tf` files (HCL)
* Build dependency graph
* Compare desired vs actual state
* Create execution plan
* Decide what to create / update / delete

### Core does NOT:

* Talk directly to AWS/Azure/GCP
* Create infrastructure itself

👉 Terraform Core always works **with providers**

---

## 3️⃣ Providers

A **Provider** is what allows Terraform to **talk to external APIs**.

### Example providers

* AWS provider → AWS API
* AzureRM provider → Azure API
* Google provider → GCP API
* Kubernetes provider → K8s API
* Docker provider → Docker API

### What providers do

* Authenticate with cloud/service
* Create, update, delete resources
* Read current infrastructure state

### Example (concept)

```
Terraform Core → AWS Provider → AWS API → EC2 Created
```

👉 Without providers, Terraform is useless.

---

## 4️⃣ Plugins

**Plugins** are **binary executables** downloaded by Terraform.

### Types of plugins

* Provider plugins
* Provisioner plugins (legacy)

### Where plugins live

```
.terraform/providers/
```

### Why plugins exist

* Terraform Core stays generic
* Providers are independent
* Easy updates & version control

### Important fact

Plugins run as **separate processes** for security and stability.

---

## 5️⃣ State File Concept (Very Important)

The **state file** is Terraform’s **single source of truth**.

### State file contains

* What resources exist
* Resource IDs
* Dependencies
* Metadata

File name:

```
terraform.tfstate
```

### Why state is critical

Terraform **does NOT query cloud every time**
It compares:

```
Desired State (code)
VS
Current State (state file)
```

### If state is lost

* Terraform forgets infrastructure
* Duplicate resources may be created
* Production damage possible

👉 **State file = Production data**

---

## 6️⃣ Backend (Local vs Remote)

A **backend** defines **where state is stored**.

---

### 🔹 Local Backend (Default)

* State stored locally
* Good for learning
* Bad for teams

```
terraform.tfstate (local machine)
```

❌ Problems:

* No locking
* No collaboration
* Risk of corruption

---

### 🔹 Remote Backend (Production)

* State stored remotely
* Supports locking
* Team-safe

Common remote backends:

* AWS S3 + DynamoDB
* Terraform Cloud
* Azure Storage
* GCS

### Benefits

* State locking
* Versioning
* Team collaboration
* CI/CD support

👉 **Production = Remote backend only**

---

## 7️⃣ Dependency Graph

Terraform automatically builds a **dependency graph**.

### What it is

A **directed graph** that decides:

* What to create first
* What depends on what

### Example

```
VPC → Subnet → EC2 → Load Balancer
```

Terraform **automatically understands this**, even if you don’t specify it.

### Explicit dependency

Used only when needed:

* `depends_on`

👉 Dependency graph enables **parallel execution**

---

## 8️⃣ Execution Plan

The **execution plan** is Terraform’s **dry-run output**.

### What happens during `terraform plan`

* Reads configuration
* Reads state
* Queries providers
* Calculates differences

### Plan shows

* `+` Create
* `~` Modify
* `-` Destroy

Example meaning:

* `+ aws_instance` → new resource
* `~ aws_instance` → change
* `- aws_instance` → delete

### Why execution plan matters

* Prevents accidents
* Mandatory review step
* Used in approvals & CI/CD

👉 **Never apply without reviewing plan**

---

## 🔁 Terraform Architecture Flow (End-to-End)

```
Terraform CLI
     ↓
Terraform Core
     ↓
Dependency Graph
     ↓
Execution Plan
     ↓
Providers & Plugins
     ↓
Cloud APIs
     ↓
State Updated
```

---

## 🏢 Who Designed This Architecture

Terraform is designed and maintained by:

**HashiCorp**

This architecture is why Terraform:

* Scales
* Works with any cloud
* Is production-safe

---
# 📌 4️⃣ Terraform Configuration Language (HCL) –

This section is **core Terraform**.
Everything you do in Terraform is written in **HCL**.
Below is **official-style explanation + real examples** used in DevOps projects.

---

## 1️⃣ HCL Syntax Basics

### 🔹 What is HCL

**HCL (HashiCorp Configuration Language)** is:

* Declarative
* Human-readable
* Designed for infrastructure

👉 You define **desired state**, Terraform decides **how to reach it**.

---

### 🔹 Basic Syntax Structure

```hcl
block_type "label1" "label2" {
  argument = value
}
```

### Example

```hcl
resource "aws_instance" "web" {
  instance_type = "t2.micro"
}
```

* `resource` → block type
* `aws_instance` → resource type
* `web` → resource name
* `{}` → block body

---

### 🔹 Value Types

```hcl
string  = "dev"
number  = 2
bool    = true
list    = ["a", "b"]
map     = { env = "dev" }
```

---

## 2️⃣ Blocks, Arguments & Identifiers

### 🔹 Blocks

Blocks define **what you are declaring**.

Common blocks:

* `resource`
* `provider`
* `variable`
* `output`
* `locals`
* `data`
* `module`

Example:

```hcl
provider "aws" {
  region = "ap-south-1"
}
```

---

### 🔹 Arguments

Arguments are **key = value** pairs inside blocks.

```hcl
region = "ap-south-1"
```

---

### 🔹 Identifiers

Identifiers are how Terraform **references objects**.

```hcl
aws_instance.web
```

Breakdown:

* `aws_instance` → type
* `web` → name

Used everywhere:

```hcl
value = aws_instance.web.public_ip
```

---

## 3️⃣ Comments & Formatting

### 🔹 Single-line comments

```hcl
# This is a comment
// This is also a comment
```

### 🔹 Multi-line comments

```hcl
/*
This is
a multi-line
comment
*/
```

---

### 🔹 Formatting Rules

Terraform enforces formatting:

* 2 spaces indentation
* Clean alignment
* No tabs

Run formatter:

```bash
terraform fmt
```

👉 **In companies, unformatted code = rejected PR**

---

## 4️⃣ Resource Blocks (MOST IMPORTANT)

### 🔹 What is a Resource

A **resource block** creates or manages **real infrastructure**.

### Syntax

```hcl
resource "<provider>_<type>" "<name>" {
  arguments
}
```

---

### Example: EC2 Instance

```hcl
resource "aws_instance" "app" {
  ami           = "ami-0abcdef"
  instance_type = "t2.micro"

  tags = {
    Name = "app-server"
  }
}
```

### Lifecycle

Terraform manages:

* Create
* Update
* Destroy

👉 **If resource block is deleted → infra is destroyed**

---

## 5️⃣ Data Sources

### 🔹 What is a Data Source

Data sources **READ existing infrastructure**
They **do not create anything**.

---

### Syntax

```hcl
data "<provider>_<type>" "<name>" {
}
```

---

### Example: Existing AMI

```hcl
data "aws_ami" "amazon_linux" {
  most_recent = true
  owners      = ["amazon"]
}
```

Usage:

```hcl
ami = data.aws_ami.amazon_linux.id
```

---

### Resource vs Data

| Resource      | Data Source  |
| ------------- | ------------ |
| Creates infra | Reads infra  |
| Managed by TF | Read-only    |
| Has lifecycle | No lifecycle |

---

## 6️⃣ Variables

Variables make Terraform **reusable & dynamic**.

---

### 🔹 Variable Declaration

```hcl
variable "instance_type" {
  type    = string
  default = "t2.micro"
}
```

---

### 🔹 Variable Usage

```hcl
instance_type = var.instance_type
```

---

### 🔹 Variable Types

```hcl
string
number
bool
list(string)
map(string)
object({...})
```

---

### 🔹 tfvars Example

`terraform.tfvars`

```hcl
instance_type = "t3.micro"
```

---

### 🔹 Variable Priority (High → Low)

1. CLI `-var`
2. `.tfvars`
3. Default value

👉 **Hardcoding values = bad DevOps practice**

---

## 7️⃣ Output Values

Outputs show **results after apply**.

---

### Example

```hcl
output "public_ip" {
  value = aws_instance.app.public_ip
}
```

After apply:

```bash
terraform output
```

---

### Sensitive Output

```hcl
output "db_password" {
  value     = var.db_password
  sensitive = true
}
```

👉 Outputs are used in:

* Debugging
* CI/CD
* Cross-module references

---

## 8️⃣ Locals

Locals are **internal calculated values**.

---

### Example

```hcl
locals {
  env      = "dev"
  app_name = "web-${local.env}"
}
```

Usage:

```hcl
tags = {
  Name = local.app_name
}
```

---

### Locals vs Variables

| Variables     | Locals   |
| ------------- | -------- |
| Input         | Internal |
| User-provided | Computed |
| Changeable    | Fixed    |

---

## 9️⃣ Files & Directories

### 🔹 Terraform File Loading Rule

> Terraform loads **ALL `.tf` files** in a directory automatically

File name **does not matter**, content does.

---

### Standard Structure

```
terraform/
 ├─ main.tf
 ├─ variables.tf
 ├─ outputs.tf
 ├─ providers.tf
 ├─ locals.tf
 └─ terraform.tfvars
```

---

### Important Files

| File         | Purpose         |
| ------------ | --------------- |
| main.tf      | Resources       |
| variables.tf | Variables       |
| outputs.tf   | Outputs         |
| providers.tf | Provider config |
| locals.tf    | Locals          |
| tfvars       | Values          |

---

## 🔟 `terraform fmt` & `terraform validate`

### 🔹 terraform fmt

```bash
terraform fmt
```

* Formats code
* Fixes spacing
* Mandatory in CI/CD

---

### 🔹 terraform validate

```bash
terraform validate
```

* Syntax check
* Logical validation
* No cloud API calls

❌ Does NOT:

* Create infra
* Check credentials

---
![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2Ael-spbCECAOdp06Iiun-ug.png)

![Image](https://phiptech.com/content/images/2023/05/Approval-Workflow.drawio--2-.png)


# 📌 5️⃣ Terraform Workflow

Terraform workflow is the **daily routine of every DevOps engineer**.
If you don’t follow this workflow correctly, **production mistakes happen**.

Terraform workflow is **NOT optional** — it is **discipline**.

---

## 🔁 Terraform Standard Workflow (Overview)

```
Write Code → init → plan → apply → (update) → destroy
```

Terraform **always follows this order**.

---

## 1️⃣ `terraform init`

### 🔹 What is `terraform init`

`terraform init` **initializes your Terraform project**.

Without this command, **Terraform will not work**.

---

### 🔹 What happens internally

When you run:

```bash
terraform init
```

Terraform does:

1. Downloads required providers
2. Initializes backend (state storage)
3. Creates `.terraform/` directory
4. Creates `.terraform.lock.hcl`
5. Prepares project for execution

---

### 🔹 When to run `terraform init`

* First time in a project ✅
* After adding a provider ✅
* After changing backend ✅
* After pulling code from Git ✅

---

### 🔹 Example

```bash
terraform init
```

Output (simplified):

```
Initializing the backend...
Initializing provider plugins...
Terraform has been successfully initialized!
```

👉 **Every Terraform project starts with `init`**

---

## 2️⃣ `terraform plan`

### 🔹 What is `terraform plan`

`terraform plan` is a **dry run**.

It shows:

* What Terraform WILL create
* What Terraform WILL change
* What Terraform WILL destroy

❌ No real infrastructure change happens.

---

### 🔹 Why plan is critical

* Prevents accidental deletion
* Mandatory review step
* Used in approvals & CI/CD

---

### 🔹 Example

```bash
terraform plan
```

Example output:

```
+ aws_instance.app
~ aws_security_group.web
- aws_s3_bucket.old
```

### 🔹 Symbols Meaning

| Symbol | Meaning |
| ------ | ------- |
| `+`    | Create  |
| `~`    | Update  |
| `-`    | Destroy |

👉 **Never skip plan in real projects**

---

## 3️⃣ `terraform apply`

### 🔹 What is `terraform apply`

This command **creates or modifies real infrastructure**.

---

### 🔹 What happens internally

1. Reads configuration
2. Reads state file
3. Talks to provider APIs
4. Creates/updates resources
5. Updates state file

---

### 🔹 Example (Interactive)

```bash
terraform apply
```

Terraform asks:

```
Do you want to perform these actions?
  Enter a value: yes
```

---

### 🔹 Auto approval (CI/CD)

```bash
terraform apply -auto-approve
```

⚠️ Used only in:

* CI/CD pipelines
* Non-interactive environments

---

### 🔹 Reality Check

* `apply` = **real money cost**
* Mistake here = **production outage**

---

## 4️⃣ `terraform destroy`

### 🔹 What is `terraform destroy`

Deletes **ALL infrastructure** managed by Terraform.

---

### 🔹 Example

```bash
terraform destroy
```

Terraform will:

* Read state file
* Destroy resources in correct order
* Update state

---

### 🔹 Auto destroy

```bash
terraform destroy -auto-approve
```

⚠️ **Extremely dangerous in production**

---

### 🔹 Real Usage

Used for:

* Dev / Test environments
* Cleanup unused infra
* Cost control

---

## 5️⃣ `.terraform` Directory

### 🔹 What is `.terraform/`

A **hidden directory** created after `terraform init`.

---

### 🔹 Contains

* Provider binaries
* Module downloads
* Plugin cache

Structure example:

```
.terraform/
 ├─ providers/
 ├─ modules/
```

---

### 🔹 Important Rules

❌ Never edit manually
❌ Never commit to Git
❌ Never delete randomly

Add to `.gitignore`:

```
.terraform/
```

---

## 6️⃣ `.terraform.lock.hcl`

### 🔹 What is this file

This file **locks provider versions**.

Example:

```hcl
provider "registry.terraform.io/hashicorp/aws" {
  version = "5.10.0"
}
```

---

### 🔹 Why it exists

* Ensures same provider version for all team members
* Prevents breaking changes
* Improves reproducibility

---

### 🔹 Git Rule

✅ **Commit this file to Git**
(It is safe and required)

---

## 7️⃣ Real-Life Terraform Workflow (Dev → Stage → Prod)

This is how Terraform is used in **real companies**.

---

### 🔹 Folder Structure

```
terraform/
 ├─ modules/
 │   ├─ vpc/
 │   ├─ ec2/
 │   └─ rds/
 │
 ├─ env/
 │   ├─ dev/
 │   ├─ stage/
 │   └─ prod/
```

---

### 🔹 Dev Environment

```bash
cd env/dev
terraform init
terraform plan
terraform apply
```

* Fast changes
* Destroy allowed
* Testing happens here

---

### 🔹 Stage Environment

```bash
cd env/stage
terraform plan
```

* Production-like
* Approval required
* Limited access

---

### 🔹 Production Environment

```bash
cd env/prod
terraform plan
terraform apply
```

Rules:

* Mandatory code review
* Plan approval
* No destroy without approval
* Remote backend only

---

### 🔹 CI/CD Workflow

```
Git Commit
 → terraform init
 → terraform plan
 → Manual Approval
 → terraform apply
```

---

![Image](https://miro.medium.com/1%2A9-FhseZZXa4BDduWV_ikkg.png)

# 📌 6️⃣ Providers (Core Concept)

Providers are the **backbone of Terraform**.
Without providers, Terraform **cannot talk to the real world**.

Think of it like this:

> **Terraform Core = Brain**
> **Providers = Hands (API connectors)**

---

## 1️⃣ What is a Provider

A **provider** is a plugin that allows Terraform to:

* Authenticate with a service
* Call its API
* Create, update, read, delete resources

### Simple definition

> A Terraform provider is a **bridge between Terraform and external systems**.

---

### Examples

* AWS provider → talks to AWS APIs
* Azure provider → talks to Azure APIs
* Kubernetes provider → talks to Kubernetes API
* Docker provider → talks to Docker Engine API

Flow:

```
Terraform Core → Provider → Cloud / Tool API → Resource
```

👉 Terraform **never** creates infra directly.
Providers do that job.

---

## 2️⃣ Provider Configuration

Before creating resources, Terraform must know:

* Which provider to use
* How to authenticate
* Which region / endpoint

---

### Basic Provider Syntax

```hcl
provider "aws" {
  region = "ap-south-1"
}
```

This tells Terraform:

* Use AWS provider
* Operate in Mumbai region

---

### Provider Authentication (Example: AWS)

Terraform **does not store credentials** itself.
It uses standard mechanisms.

Common AWS auth methods:

* Environment variables
* AWS CLI config
* IAM role (recommended)

Example (env vars):

```bash
export AWS_ACCESS_KEY_ID=xxxx
export AWS_SECRET_ACCESS_KEY=xxxx
```

👉 In production, **IAM roles** are mandatory.

---

## 3️⃣ Multiple Providers

Terraform can use **more than one provider** in the same project.

### Why this is needed

* Multi-cloud architecture
* Infra + Kubernetes
* Cloud + Docker local testing

---

### Example: AWS + Kubernetes

```hcl
provider "aws" {
  region = "ap-south-1"
}

provider "kubernetes" {
  config_path = "~/.kube/config"
}
```

Now Terraform can:

* Create EC2 / EKS in AWS
* Deploy pods in Kubernetes

👉 This is **very common in DevOps projects**.

---

## 4️⃣ Provider Versions

Providers change over time.
Terraform **locks provider versions** to avoid breaking changes.

---

### Version Constraint Example

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}
```

Meaning:

* Allow any `5.x`
* Block `6.x` (breaking changes)

---

### Where version is locked

File created automatically:

```
.terraform.lock.hcl
```

This ensures:

* Same provider version for all team members
* Same behavior in CI/CD

👉 **Never delete lock file casually**

---

## 5️⃣ Alias Providers

Alias providers are used when:

* Multiple regions
* Multiple accounts
* Same provider, different configs

---

### Example: AWS Multi-Region

```hcl
provider "aws" {
  region = "ap-south-1"
}

provider "aws" {
  alias  = "us"
  region = "us-east-1"
}
```

Using alias in resource:

```hcl
resource "aws_instance" "india_server" {
  ami           = "ami-xxxx"
  instance_type = "t2.micro"
}

resource "aws_instance" "us_server" {
  provider      = aws.us
  ami           = "ami-yyyy"
  instance_type = "t2.micro"
}
```

👉 Alias = **advanced but very important**

---

## 6️⃣ Popular Terraform Providers (Industry Standard)

Below are the **most used providers in real DevOps jobs**.

---

### ☁️ AWS Provider

* EC2, VPC, IAM, S3, RDS, EKS
* Most widely used provider

Used by:

* Startups
* Enterprises
* Almost every DevOps role

👉 **Must-know provider**

---

### ☁️ Azure Provider

* Virtual Machines
* VNets
* Azure Kubernetes Service (AKS)
* Storage accounts

Used in Microsoft ecosystem & enterprises.

---

### ☁️ GCP Provider

* Compute Engine
* GKE
* Cloud Storage
* IAM

Popular in data & Kubernetes-heavy workloads.

---

### ☸ Kubernetes Provider

* Pods
* Deployments
* Services
* ConfigMaps
* Secrets

Example:

```hcl
resource "kubernetes_namespace" "dev" {
  metadata {
    name = "dev"
  }
}
```

👉 Terraform + Kubernetes is **very common**.

---

### 🐳 Docker Provider

* Images
* Containers
* Networks
* Volumes

Used mainly for:

* Learning
* Local testing
* CI environments

Example:

```hcl
resource "docker_container" "nginx" {
  image = "nginx"
  name  = "web"
}
```

---

# 📌 7️⃣ Resources (Real Infrastructure)

Resources are **the heart of Terraform**.
If providers are *hands*, then **resources are the actual things being built**.

Servers, networks, databases, load balancers — **everything is a resource**.

---

## 1️⃣ What is a Resource

A **resource** represents **real infrastructure** managed by Terraform.

### Simple definition

> A Terraform resource is a block that **creates, updates, or deletes** infrastructure via a provider.

---

### Basic Resource Syntax

```hcl
resource "<provider>_<type>" "<name>" {
  arguments
}
```

### Example (AWS EC2)

```hcl
resource "aws_instance" "web" {
  ami           = "ami-0abcd1234"
  instance_type = "t2.micro"
}
```

### Breakdown

* `aws_instance` → resource type
* `web` → logical name (Terraform internal)
* Block body → configuration

👉 **If resource block exists → infra exists**
👉 **If resource block is removed → infra is destroyed**

---

## 2️⃣ Resource Lifecycle

Every Terraform resource goes through a **lifecycle**.

### Terraform Resource Lifecycle States

1. **Create**
2. **Read**
3. **Update**
4. **Delete**

Terraform decides the action by comparing:

```
Desired State (HCL code)
VS
Current State (terraform.tfstate)
```

---

### Example Scenario

You change:

```hcl
instance_type = "t2.micro"
```

to:

```hcl
instance_type = "t3.micro"
```

Terraform will:

* Detect change
* Update resource (or recreate if required)
* Update state file

👉 Lifecycle behavior depends on **resource type**

---

## 3️⃣ Resource Dependencies

Resources often **depend on other resources**.

### Example

* EC2 needs a VPC
* Subnet needs a VPC
* Load Balancer needs subnets

---

### Implicit Dependency (Automatic)

Terraform automatically detects dependencies when you reference another resource.

```hcl
resource "aws_subnet" "subnet" {
  vpc_id = aws_vpc.main.id
}
```

Here:

* `aws_subnet.subnet` depends on `aws_vpc.main`
* Terraform **automatically knows order**

👉 This is called **implicit dependency**

---

### Execution Order (Auto)

```
VPC → Subnet → EC2
```

Terraform also runs **parallel operations** when possible.

---

## 4️⃣ `depends_on` (Explicit Dependency)

Sometimes Terraform **cannot detect dependency automatically**.

In such cases, you must **explicitly define it**.

---

### Syntax

```hcl
depends_on = [resource.reference]
```

---

### Example

```hcl
resource "aws_instance" "app" {
  ami           = "ami-0abcd"
  instance_type = "t2.micro"

  depends_on = [
    aws_security_group.web
  ]
}
```

### When to use `depends_on`

* IAM roles & policies
* Null resources
* External scripts
* Hidden dependencies

⚠️ **Do not overuse `depends_on`**
Implicit dependencies are preferred.

---

## 5️⃣ `lifecycle` Block (Advanced & Critical)

The `lifecycle` block controls **how Terraform handles changes**.

This is **very important in production**.

---

### 🔹 Lifecycle Block Syntax

```hcl
lifecycle {
  create_before_destroy = true
  prevent_destroy       = true
  ignore_changes        = []
}
```

---

## 5.1️⃣ `create_before_destroy`

### Problem it Solves

Normally Terraform:

```
Destroy old → Create new
```

This can cause **downtime**.

---

### Solution

```hcl
lifecycle {
  create_before_destroy = true
}
```

### Result

```
Create new → Switch → Destroy old
```

---

### Real Example (Load Balancer / ASG)

```hcl
resource "aws_launch_template" "app" {
  name_prefix = "app-"

  lifecycle {
    create_before_destroy = true
  }
}
```

👉 **Used to avoid downtime**

---

## 5.2️⃣ `prevent_destroy`

### Problem it Solves

Accidental deletion of:

* Production DB
* S3 buckets
* Critical infra

---

### Example

```hcl
resource "aws_db_instance" "prod_db" {
  allocated_storage = 20
  engine            = "mysql"

  lifecycle {
    prevent_destroy = true
  }
}
```

### Result

```bash
terraform destroy
```

❌ **Fails with error**

👉 **Production safety feature**

---

## 5.3️⃣ `ignore_changes`

### Problem it Solves

Some attributes change **outside Terraform**:

* Auto-scaling
* Manual console changes
* Provider-managed fields

Terraform keeps detecting changes again and again.

---

### Example

```hcl
resource "aws_instance" "app" {
  ami           = "ami-0abcd"
  instance_type = "t2.micro"

  lifecycle {
    ignore_changes = [
      tags,
      instance_type
    ]
  }
}
```

### Result

* Terraform ignores those fields
* No unnecessary updates

👉 Useful but **dangerous if misused**

---

# 📌 8️⃣ Variables & Input Management

Variables are what make Terraform **reusable, environment-friendly, and production-ready**.
Without variables, Terraform becomes **hard-coded and useless in real DevOps work**.

---

## 1️⃣ Variable Types

Terraform variables define **what kind of data** is allowed.

### 🔹 General Syntax

```hcl
variable "name" {
  type        = <TYPE>
  description = "..."
  default     = <VALUE>
}
```

---

### 🔸 1. `string`

Used for text values.

```hcl
variable "env" {
  type    = string
  default = "dev"
}
```

Usage:

```hcl
tags = {
  Environment = var.env
}
```

---

### 🔸 2. `number`

Used for numeric values.

```hcl
variable "disk_size" {
  type    = number
  default = 20
}
```

---

### 🔸 3. `bool`

Used for true / false conditions.

```hcl
variable "enable_monitoring" {
  type    = bool
  default = true
}
```

---

### 🔸 4. `list`

Ordered collection of values.

```hcl
variable "subnet_ids" {
  type    = list(string)
}
```

Usage:

```hcl
subnet_id = var.subnet_ids[0]
```

---

### 🔸 5. `map`

Key-value pairs.

```hcl
variable "tags" {
  type = map(string)
}
```

Usage:

```hcl
tags = var.tags
```

Example value:

```hcl
tags = {
  Name = "web"
  Env  = "dev"
}
```

---

### 🔸 6. `object`

Structured complex data.

```hcl
variable "server" {
  type = object({
    name  = string
    size  = string
    count = number
  })
}
```

Usage:

```hcl
instance_type = var.server.size
```

👉 **Object type is common in modules**

---

## 2️⃣ Default Values

Default values make variables **optional**.

```hcl
variable "instance_type" {
  type    = string
  default = "t2.micro"
}
```

If user doesn’t pass value → default is used.

---

### ❌ Without Default

Terraform will ask during `apply`:

```
Enter a value:
```

👉 In CI/CD, defaults or tfvars are required.

---

## 3️⃣ Variable Precedence (Very Important)

Terraform follows a **strict order** when reading variables.

### 🔹 Precedence Order (High → Low)

1. `-var` (CLI)
2. `-var-file`
3. `terraform.tfvars`
4. `*.auto.tfvars`
5. Environment variables
6. Default values

---

### Example

```bash
terraform apply -var="env=prod"
```

This overrides everything else.

👉 Highest precedence **always wins**.

---

## 4️⃣ `.tfvars` Files

`.tfvars` files store **environment-specific values**.

---

### Example: `terraform.tfvars`

```hcl
env           = "dev"
instance_type = "t3.micro"
```

Terraform automatically loads:

* `terraform.tfvars`
* `*.auto.tfvars`

---

### Multiple Environments

```
dev.tfvars
stage.tfvars
prod.tfvars
```

Usage:

```bash
terraform apply -var-file=prod.tfvars
```

👉 **Best practice for Dev / Stage / Prod**

---

## 5️⃣ Environment Variables

Terraform supports environment variables using:

```
TF_VAR_<variable_name>
```

---

### Example

```bash
export TF_VAR_env=prod
export TF_VAR_instance_type=t3.large
```

Terraform automatically reads them.

---

### When to use env vars

* CI/CD pipelines
* Secrets
* Dynamic values

👉 Very common in GitHub Actions / Jenkins.

---

## 6️⃣ Sensitive Variables

Sensitive variables hide values from:

* CLI output
* Logs
* State display

---

### Example

```hcl
variable "db_password" {
  type      = string
  sensitive = true
}
```

Usage:

```hcl
password = var.db_password
```

---

## 🔹 What is “multi-environment with .tfvars” (EC2)?

👉 **One Terraform codebase**
👉 **Multiple environments (dev, staging, prod)**
👉 **Different values via `.tfvars` files**
👉 **Same infra logic, different configurations**

Example:

* Dev → small EC2
* Prod → large EC2
* Same `.tf` files

---

## 🧱 Folder Structure (Recommended)

```
terraform-ec2/
├── main.tf
├── provider.tf
├── variables.tf
├── outputs.tf
├── dev.tfvars
├── stage.tfvars
└── prod.tfvars
```

---

## 1️⃣ provider.tf

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}

provider "aws" {
  region = var.aws_region
}
```

---

## 2️⃣ variables.tf

```hcl
variable "aws_region" {
  type = string
}

variable "environment" {
  type = string
}

variable "instance_type" {
  type = string
}

variable "ami_id" {
  type = string
}

variable "key_name" {
  type = string
}

variable "instance_name" {
  type = string
}
```

---

## 3️⃣ main.tf (EC2 Resource)

```hcl
resource "aws_instance" "ec2" {
  ami           = var.ami_id
  instance_type = var.instance_type
  key_name      = var.key_name

  tags = {
    Name        = var.instance_name
    Environment = var.environment
  }
}
```

---

## 4️⃣ outputs.tf

```hcl
output "ec2_public_ip" {
  value = aws_instance.ec2.public_ip
}
```

---

## 5️⃣ dev.tfvars (Development)

```hcl
aws_region    = "ap-south-1"
environment   = "dev"
instance_type = "t2.micro"
ami_id        = "ami-0f5ee92e2d63afc18"
key_name      = "dev-key"
instance_name = "dev-ec2"
```

---

## 6️⃣ stage.tfvars (Staging)

```hcl
aws_region    = "ap-south-1"
environment   = "stage"
instance_type = "t2.small"
ami_id        = "ami-0f5ee92e2d63afc18"
key_name      = "stage-key"
instance_name = "stage-ec2"
```

---

## 7️⃣ prod.tfvars (Production)

```hcl
aws_region    = "ap-south-1"
environment   = "prod"
instance_type = "t2.medium"
ami_id        = "ami-0f5ee92e2d63afc18"
key_name      = "prod-key"
instance_name = "prod-ec2"
```

---

## 8️⃣ How to Apply (Very Important)

### 🔹 Dev

```bash
terraform init
terraform apply -var-file="dev.tfvars"
```

### 🔹 Stage

```bash
terraform apply -var-file="stage.tfvars"
```

### 🔹 Prod

```bash
terraform apply -var-file="prod.tfvars"
```

---

## ✅ What Happens Internally

| Environment | EC2 Type  | Tags              |
| ----------- | --------- | ----------------- |
| dev         | t2.micro  | Environment=dev   |
| stage       | t2.small  | Environment=stage |
| prod        | t2.medium | Environment=prod  |

Same code ✔
Different infra ✔
Safe & scalable ✔

---


# 📌 9️⃣ Outputs

Outputs are Terraform’s way to **return values after infrastructure is created**.
Think of outputs as **the final result** of `terraform apply`.

In real DevOps work, outputs are used for:

* Debugging
* CI/CD pipelines
* Passing values between modules
* Automation scripts

---

## 1️⃣ Output Blocks

### 🔹 What is an Output Block

An **output block** exposes a value from Terraform configuration.

### Basic Syntax

```hcl
output "name" {
  value = expression
}
```

---

### Example: EC2 Public IP

```hcl
output "ec2_public_ip" {
  value = aws_instance.web.public_ip
}
```

After `terraform apply`, Terraform prints:

```
ec2_public_ip = "13.235.xx.xx"
```

👉 Output blocks **do not create infrastructure**
They only **display or expose information**.

---

## 2️⃣ Output Usage (Real-Life Scenarios)

### 🔹 View Outputs

```bash
terraform output
```

Output:

```
ec2_public_ip = "13.235.xx.xx"
```

---

### 🔹 Get Single Output

```bash
terraform output ec2_public_ip
```

Useful in:

* Shell scripts
* CI/CD jobs

---

### 🔹 JSON Format (Automation)

```bash
terraform output -json
```

Used by:

* Jenkins
* GitHub Actions
* Python / Bash scripts

---

### 🔹 Common Real Uses

| Use Case   | Example                 |
| ---------- | ----------------------- |
| Debugging  | Check IP, DNS           |
| CI/CD      | Pass values to next job |
| Monitoring | Expose endpoint         |
| Automation | Feed data to scripts    |

👉 Outputs connect Terraform with **other tools**.

---

## 3️⃣ Sensitive Outputs

Some outputs should **not be displayed openly**.

Examples:

* Passwords
* Tokens
* Secrets

---

### Sensitive Output Example

```hcl
output "db_password" {
  value     = var.db_password
  sensitive = true
}
```

Result:

```bash
terraform output
```

```
db_password = <sensitive>
```

---

### Important Reality (Very Important ⚠️)

* Sensitive outputs are **hidden only in CLI**
* Value is still stored in:

  ```
  terraform.tfstate
  ```

👉 **State file security is mandatory**

Sensitive ≠ encrypted
Sensitive = hidden from screen only

---

## 4️⃣ Using Outputs Across Modules (Very Important)

This is **core Terraform design**.

### 🔹 Why Cross-Module Outputs Are Needed

* VPC module creates VPC
* EC2 module needs VPC ID
* Load Balancer module needs subnet IDs

Modules communicate via **outputs + inputs**.

---

### Example: VPC Module

**modules/vpc/outputs.tf**

```hcl
output "vpc_id" {
  value = aws_vpc.main.id
}
```

---

### Root Module Uses Output

**main.tf**

```hcl
module "vpc" {
  source = "./modules/vpc"
}

module "ec2" {
  source = "./modules/ec2"
  vpc_id = module.vpc.vpc_id
}
```

---

### How This Works

* `module.vpc.vpc_id` → output from VPC module
* Passed as input variable to EC2 module

👉 This is how **large Terraform projects are built**

---

## 🔁 Output Flow (Visual Logic)

```
Resource → Output → Module → Another Module → Resource
```

Terraform enforces:

* Strong typing
* Clear dependencies
* Safe ordering

---

# 📌 🔟 Terraform State Management (Very Important)

Terraform **state management** is the **most critical and dangerous part** of Terraform.
Most **production outages, data loss, and duplicate resources** happen due to **bad state handling**.

If you understand this section properly → **you are production-ready**.

---

## 1️⃣ What is `terraform.tfstate`

### 🔹 Definition

`terraform.tfstate` is a **JSON file** that stores the **current known state of infrastructure** managed by Terraform.

### In simple words

> State file is Terraform’s **memory**.

---

### 🔹 What state file contains

* Resource IDs (EC2 ID, VPC ID, etc.)
* Resource attributes
* Dependencies
* Metadata
* Provider info

Example (simplified):

```json
{
  "resources": [
    {
      "type": "aws_instance",
      "name": "web",
      "instances": [
        {
          "attributes": {
            "id": "i-012345",
            "instance_type": "t2.micro"
          }
        }
      ]
    }
  ]
}
```

👉 Terraform **does not rely only on cloud APIs**
It relies on **state file first**

---

## 2️⃣ Why State File is Critical

Terraform works by comparing:

```
Desired State (HCL code)
VS
Current State (terraform.tfstate)
```

### 🔹 What happens if state is missing

* Terraform thinks **nothing exists**
* Creates **duplicate infrastructure**
* Causes **billing & outages**

### 🔹 What happens if state is wrong

* Wrong resources destroyed
* Wrong updates
* Production damage

👉 **State file = production data**

---

## 3️⃣ Local State

### 🔹 What is Local State

Default behavior:

* State stored on **local machine**
* File name:

  ```
  terraform.tfstate
  ```

### 🔹 Example

```
project/
 ├─ main.tf
 ├─ terraform.tfstate
```

### ❌ Problems with Local State

| Issue            | Reality                 |
| ---------------- | ----------------------- |
| No locking       | Two users = corruption  |
| No backup        | File lost = infra lost  |
| No collaboration | Team cannot work        |
| Unsafe           | Laptop crash = disaster |

👉 Local state is **ONLY for learning**

---

## 4️⃣ Remote State (Production Mandatory)

### 🔹 What is Remote State

State stored in **remote, centralized storage**.

### Common Remote Backends

* AWS S3
* Azure Storage
* GCS
* Terraform Cloud

---

### 🔹 Example: S3 Backend

```hcl
terraform {
  backend "s3" {
    bucket = "my-tf-state"
    key    = "prod/terraform.tfstate"
    region = "ap-south-1"
  }
}
```

### ✅ Benefits

* Centralized state
* Team collaboration
* Versioning
* Locking support
* CI/CD friendly

👉 **Production = Remote state only**

---

## 5️⃣ State Locking

### 🔹 What is State Locking

State locking prevents **multiple Terraform runs at the same time**.

Without locking:

* Two applies run together
* State corruption happens

---

### 🔹 Example: S3 + DynamoDB Locking

```hcl
backend "s3" {
  bucket         = "my-tf-state"
  key            = "prod/terraform.tfstate"
  region         = "ap-south-1"
  dynamodb_table = "terraform-lock"
}
```

### What happens

* Terraform acquires lock
* Other users must wait
* Lock released after apply

👉 **Locking = safety**

---

## 6️⃣ State Backup

### 🔹 Automatic Backups

Terraform automatically creates:

```
terraform.tfstate.backup
```

This happens when:

* State changes
* Apply runs

---

### 🔹 Remote Backend Backup

Remote backends provide:

* S3 versioning
* Terraform Cloud history

👉 Always enable **versioning** on backend storage.

---

## 7️⃣ `terraform state` Commands

Used for **advanced troubleshooting**.

---

### 🔹 List Resources

```bash
terraform state list
```

Shows all resources in state.

---

### 🔹 Show Resource

```bash
terraform state show aws_instance.web
```

Shows exact state data.

---

### 🔹 Remove Resource from State

```bash
terraform state rm aws_instance.web
```

⚠️ Resource still exists in cloud
Only removed from Terraform tracking.

Used when:

* Resource deleted manually
* Import cleanup

---

### 🔹 Move Resource

```bash
terraform state mv aws_instance.old aws_instance.new
```

Used during:

* Refactoring
* Module restructuring

---

👉 `terraform state` commands are **dangerous but powerful**

---

## 8️⃣ State Corruption & Recovery

### 🔹 How State Corruption Happens

* Two applies at same time
* Manual editing of state
* Force kill Terraform
* Network failures
* Bad backend config

---

### 🔹 Symptoms

* Terraform shows wrong plan
* Duplicate resource creation
* Missing resources
* Apply failures

---

### 🔹 Recovery Steps (Real World)

#### Step 1: Stop All Applies

* No one runs Terraform

#### Step 2: Restore Backup

* Use `.backup` file
* Or backend version

#### Step 3: Validate State

```bash
terraform plan
```

#### Step 4: Import Missing Resources

```bash
terraform import
```

---

### ❌ Never Do This

* Manually edit state (unless expert)
* Ignore state issues
* Run apply blindly

---

# 📌 1️⃣1️⃣ Backends (Remote State)

Backends decide **where and how Terraform state is stored**.
In real production, **backend configuration is more important than resource code**.

If backend is wrong → **state corruption, outages, data loss**.

---

## 1️⃣ Backend Concept

### 🔹 What is a Backend?

A **backend** defines:

* Where Terraform stores the state file
* How state is locked
* How multiple users collaborate

### Simple definition

> Backend = **State storage + state access rules**

---

### 🔹 Default Backend

* Local backend (default)
* State stored as:

```
terraform.tfstate (local machine)
```

❌ Not safe for teams
❌ Not safe for production

---

### 🔹 Why Remote Backend is Mandatory

* Centralized state
* Locking support
* Team collaboration
* CI/CD compatibility
* Disaster recovery

👉 **Production without remote backend = unsafe**

---

## 2️⃣ S3 Backend (Most Common – Industry Standard)

### 🔹 What is S3 Backend?

* Stores state in **AWS S3**
* Uses **DynamoDB** for locking (optional but required in prod)

---

### 🔹 S3 Backend Architecture

```
Terraform
   ↓
S3 (state file)
   ↓
DynamoDB (lock)
```

---

### 🔹 S3 Backend Configuration (Example)

Create `backend.tf`:

```hcl
terraform {
  backend "s3" {
    bucket         = "my-terraform-state-bucket"
    key            = "prod/terraform.tfstate"
    region         = "ap-south-1"
    dynamodb_table = "terraform-lock"
    encrypt        = true
  }
}
```

---

### 🔹 Explanation of Each Field

| Field            | Meaning             |
| ---------------- | ------------------- |
| `bucket`         | S3 bucket for state |
| `key`            | Path inside bucket  |
| `region`         | AWS region          |
| `dynamodb_table` | Locking table       |
| `encrypt`        | Enable encryption   |

---

### 🔹 S3 Best Practices (REAL)

✔ Enable S3 versioning
✔ Block public access
✔ Use SSE encryption
✔ Restrict IAM access
✔ Separate bucket for prod

---

## 3️⃣ DynamoDB Locking

### 🔹 Why Locking is Needed

Without locking:

* Two `terraform apply` run together
* State file corruption happens

---

### 🔹 DynamoDB Lock Table Setup

| Setting       | Value           |
| ------------- | --------------- |
| Table name    | terraform-lock  |
| Partition key | LockID (String) |
| Capacity      | On-demand       |

---

### 🔹 How Locking Works

1. Terraform requests lock
2. DynamoDB grants lock
3. Apply runs
4. Lock released

If another user runs Terraform:

```
Error: state is locked
```

👉 **Locking = production safety belt**

---

## 4️⃣ Terraform Cloud Backend

### 🔹 What is Terraform Cloud Backend?

Terraform Cloud provides:

* Managed state
* Locking
* UI dashboard
* Access control
* Remote runs

---

### 🔹 When to Use Terraform Cloud

✔ Small to medium teams
✔ No need to manage S3/DynamoDB
✔ SaaS preference

---

### 🔹 Terraform Cloud Backend Example

```hcl
terraform {
  cloud {
    organization = "my-org"

    workspaces {
      name = "prod"
    }
  }
}
```

---

### 🔹 Terraform Cloud vs S3

| Feature | S3 Backend | Terraform Cloud |
| ------- | ---------- | --------------- |
| Setup   | Manual     | Easy            |
| Cost    | AWS cost   | SaaS cost       |
| Locking | DynamoDB   | Built-in        |
| UI      | ❌          | ✅               |
| Control | Full       | Limited         |

👉 **Enterprises often use S3**
👉 **Startups often use Terraform Cloud**

---

## 5️⃣ Backend Migration (Very Important)

Backend migration happens when:

* Local → S3
* S3 → Terraform Cloud
* Bucket or key change

---

### 🔹 How Migration Works

Terraform **moves state safely** if done correctly.

---

### 🔹 Example: Local → S3 Migration

1️⃣ Add backend config:

```hcl
terraform {
  backend "s3" {
    bucket = "my-terraform-state"
    key    = "dev/terraform.tfstate"
    region = "ap-south-1"
  }
}
```

2️⃣ Run:

```bash
terraform init
```

3️⃣ Terraform asks:

```
Do you want to migrate existing state?
```

✔ Type: `yes`

---

### 🔹 Important Migration Rules

✔ Take backup before migration
✔ No parallel Terraform runs
✔ Verify after migration:

```bash
terraform plan
```

---

# 📌 1️⃣2️⃣ Terraform Modules

(**Theory + Examples + Real DevOps Practice – Full Detail**)

Terraform **modules** are what turn Terraform from **small scripts** into **enterprise-grade infrastructure systems**.
If you don’t understand modules → you **cannot scale Terraform**.

> **Real rule:**
> ❌ No modules = beginner
> ✅ Proper modules = production DevOps engineer

---

## 1️⃣ What is a Module

### 🔹 Definition

A **module** is a **container for Terraform configuration** that is:

* Reusable
* Parameterized
* Isolated
* Versionable

### Simple words

> A module is a **reusable Terraform blueprint**.

---

### Example Analogy

* Module = **class**
* Variables = **constructor arguments**
* Outputs = **return values**

---

### Example

Instead of repeating EC2 code 10 times:

```hcl
resource "aws_instance" "web" { ... }
```

You write it **once** as a module and reuse it everywhere.

---

## 2️⃣ Root Module vs Child Module

### 🔹 Root Module

* The **main working directory**
* Where you run:

  ```bash
  terraform init
  terraform apply
  ```

📁 Example:

```
env/dev/
```

Everything in this directory is the **root module**.

---

### 🔹 Child Module

* A module **called by the root module**
* Lives inside `modules/`

📁 Example:

```
modules/ec2/
```

---

### 🔁 Relationship

```
Root Module
   ↓ calls
Child Module
```

---

### Example

```hcl
module "ec2" {
  source = "../modules/ec2"
}
```

👉 Root module **orchestrates**
👉 Child module **implements**

---

## 3️⃣ Module Structure (Industry Standard)

### 🔹 Minimum Required Structure

```
modules/ec2/
 ├─ main.tf
 ├─ variables.tf
 └─ outputs.tf
```

---

### 🔹 Purpose of Each File

| File           | Purpose              |
| -------------- | -------------------- |
| `main.tf`      | Resource definitions |
| `variables.tf` | Inputs to module     |
| `outputs.tf`   | Values exported      |

---

### Example: `main.tf`

```hcl
resource "aws_instance" "this" {
  ami           = var.ami
  instance_type = var.instance_type
}
```

---

### Example: `variables.tf`

```hcl
variable "ami" {
  type = string
}

variable "instance_type" {
  type = string
}
```

---

### Example: `outputs.tf`

```hcl
output "instance_id" {
  value = aws_instance.this.id
}
```

---

## 4️⃣ Reusable Modules (MOST IMPORTANT)

### 🔹 What Makes a Module Reusable

✔ No hard-coded values
✔ Everything configurable via variables
✔ Clear outputs
✔ No environment-specific logic

---

### ❌ Bad Module (Not Reusable)

```hcl
instance_type = "t2.micro"
```

---

### ✅ Good Module (Reusable)

```hcl
instance_type = var.instance_type
```

---

### Example: Using Same Module in Multiple Envs

```hcl
module "ec2_dev" {
  source        = "../../modules/ec2"
  instance_type = "t2.micro"
}

module "ec2_prod" {
  source        = "../../modules/ec2"
  instance_type = "t3.large"
}
```

👉 Same module, different behavior.

---

## 5️⃣ Module Versioning

Module versioning prevents **breaking changes**.

---

### 🔹 Local Module (No Version)

```hcl
source = "../../modules/ec2"
```

Used during:

* Development
* Same repository

---

### 🔹 Git Module with Version

```hcl
module "ec2" {
  source = "git::https://github.com/org/terraform-aws-ec2.git?ref=v1.0.0"
}
```

---

### Why Versioning Matters

* Safe upgrades
* Rollback possible
* Reproducible infra

👉 **Never use `main` branch in production**

---

## 6️⃣ Public vs Private Modules

### 🔹 Public Modules

* Available to everyone
* Hosted on Terraform Registry
* Community or vendor maintained

Examples:

* VPC modules
* EKS modules
* IAM modules

---

### 🔹 Private Modules

* Internal company modules
* Hosted on:

  * GitHub
  * GitLab
  * Bitbucket
  * Terraform Cloud private registry

Used when:

* Company standards
* Security rules
* Custom infra

---

### Comparison

| Feature       | Public   | Private    |
| ------------- | -------- | ---------- |
| Access        | Everyone | Restricted |
| Customization | Limited  | Full       |
| Security      | Depends  | Controlled |
| Usage         | Fast     | Safer      |

👉 Enterprises prefer **private modules**

---

## 7️⃣ Terraform Registry

### 🔹 What is Terraform Registry

Terraform Registry is the **official module & provider hub**.

Contains:

* Providers
* Modules
* Documentation
* Versioning info

---

### 🔹 Module Usage Example

```hcl
module "vpc" {
  source  = "terraform-aws-modules/vpc/aws"
  version = "5.1.0"
}
```

Terraform automatically:

* Downloads module
* Manages version
* Integrates it

---

# 📌 1️⃣3️⃣ Meta-Arguments

**Meta-arguments** are special arguments that **change how Terraform creates and manages resources**, not *what* the resource is.
They are essential for **scaling**, **ordering**, and **safety** in real infrastructure.

> **Rule of thumb:**
> Resources define *what* to build.
> Meta-arguments define *how* Terraform builds and manages them.

---

## 1️⃣ `count`

### 🔹 What is `count`

`count` creates **multiple instances of the same resource** using a number.

### Syntax

```hcl
resource "aws_instance" "web" {
  count = 3
  ami   = "ami-0abcd"
  instance_type = "t2.micro"
}
```

### Result

Terraform creates:

```
aws_instance.web[0]
aws_instance.web[1]
aws_instance.web[2]
```

---

### 🔹 Accessing with `count.index`

```hcl
tags = {
  Name = "web-${count.index}"
}
```

---

### 🔹 Conditional Creation (Very Common)

```hcl
count = var.create_instance ? 1 : 0
```

If `false` → resource not created.

---

### ❌ Limitations of `count`

* Index-based → fragile
* Removing one item shifts indexes
* Can cause **unexpected destroy/recreate**

👉 Use `count` for **simple, identical resources only**.

---

## 2️⃣ `for_each`

### 🔹 What is `for_each`

`for_each` creates resources from:

* map
* set
* object

Each instance has a **stable key** (safer than `count`).

---

### Example: Using a Map

```hcl
variable "instances" {
  type = map(string)
  default = {
    web  = "t2.micro"
    api  = "t3.micro"
  }
}

resource "aws_instance" "app" {
  for_each      = var.instances
  instance_type = each.value
  ami           = "ami-0abcd"

  tags = {
    Name = each.key
  }
}
```

### Result

```
aws_instance.app["web"]
aws_instance.app["api"]
```

---

### 🔹 Access Values

* `each.key`   → map key
* `each.value` → map value

---

### ✅ Why `for_each` is Better

✔ Stable addressing
✔ Safer updates
✔ Better for real projects

👉 **Preferred over `count` in production**

---

### ❌ When NOT to use `for_each`

* When you only need simple numeric repetition
* When order matters strictly

---

## 3️⃣ `depends_on`

### 🔹 What is `depends_on`

Forces Terraform to **create resources in a specific order**.

Terraform usually detects dependencies automatically, but **not always**.

---

### Syntax

```hcl
depends_on = [aws_iam_role.policy]
```

---

### Example: IAM Role Dependency

```hcl
resource "aws_iam_role_policy_attachment" "attach" {
  role       = aws_iam_role.role.name
  policy_arn = aws_iam_policy.policy.arn
}

resource "aws_instance" "app" {
  ami           = "ami-0abcd"
  instance_type = "t2.micro"

  depends_on = [
    aws_iam_role_policy_attachment.attach
  ]
}
```

---

### When to Use `depends_on`

✔ IAM policies & roles
✔ External scripts
✔ `null_resource`
✔ Hidden dependencies

⚠️ **Do not overuse** — prefer implicit dependencies.

---

## 4️⃣ `provider` (Meta-Argument)

### 🔹 What it Does

Allows a resource to use a **specific provider configuration**, often with **aliases**.

---

### Example: Multi-Region AWS

```hcl
provider "aws" {
  region = "ap-south-1"
}

provider "aws" {
  alias  = "us"
  region = "us-east-1"
}
```

Using provider meta-argument:

```hcl
resource "aws_instance" "india" {
  ami           = "ami-aaa"
  instance_type = "t2.micro"
}

resource "aws_instance" "usa" {
  provider      = aws.us
  ami           = "ami-bbb"
  instance_type = "t2.micro"
}
```

---

### Real Use Cases

✔ Multi-region deployments
✔ Multi-account setups
✔ Blue/Green infra

---

## 5️⃣ `lifecycle`

### 🔹 What is `lifecycle`

Controls **how Terraform reacts to changes**.

This is **critical for production safety**.

---

### Lifecycle Block Syntax

```hcl
lifecycle {
  create_before_destroy = true
  prevent_destroy       = true
  ignore_changes        = []
}
```

---

## 5.1️⃣ `create_before_destroy`

### Problem

Default behavior:

```
Destroy old → Create new
```

Causes downtime.

---

### Solution

```hcl
lifecycle {
  create_before_destroy = true
}
```

### Result

```
Create new → Switch → Destroy old
```

👉 Used for:

* Load balancers
* Launch templates
* ASGs

---

## 5.2️⃣ `prevent_destroy`

### Purpose

Prevents **accidental deletion**.

---

### Example

```hcl
resource "aws_db_instance" "prod" {
  engine = "mysql"

  lifecycle {
    prevent_destroy = true
  }
}
```

If someone runs:

```bash
terraform destroy
```

❌ Terraform blocks it.

👉 **Mandatory for prod DBs**

---

## 5.3️⃣ `ignore_changes`

### Purpose

Ignore changes Terraform **should not manage**.

---

### Example

```hcl
lifecycle {
  ignore_changes = [
    tags,
    desired_capacity
  ]
}
```

Used when:

* Auto-scaling modifies values
* Manual changes are expected

⚠️ Dangerous if misused — Terraform may stop managing important changes.

---

# 📌 1️⃣4️⃣ Terraform Functions

Terraform **functions** are used to **transform data**, **make decisions**, and **write dynamic infrastructure code**.

If modules are structure,
👉 **functions are the logic**.

Real-world Terraform **cannot survive without functions**.

---

# 🔹 What Are Terraform Functions?

Terraform functions:

* Take input values
* Perform operations
* Return output values

They are used inside:

* Variables
* Resources
* Outputs
* Locals
* Meta-arguments

Syntax:

```hcl
function_name(arg1, arg2)
```

---

# 1️⃣ String Functions

Used to manipulate **text values**.

---

## 🔹 Common String Functions

### `upper()` / `lower()`

```hcl
upper("dev")   # DEV
lower("PROD")  # prod
```

---

### `length()`

```hcl
length("terraform")  # 9
```

---

### `substr()`

```hcl
substr("terraform", 0, 4)  # terra
```

---

### `replace()`

```hcl
replace("web-dev", "dev", "prod")  # web-prod
```

---

### `format()`

```hcl
format("app-%s-%s", var.env, var.region)
```

Result:

```
app-dev-ap-south-1
```

---

### ✅ Real Use Case

Naming resources consistently:

```hcl
tags = {
  Name = format("%s-%s", var.app, var.env)
}
```

---

# 2️⃣ Numeric Functions

Used for **numbers and calculations**.

---

## 🔹 Common Numeric Functions

### `min()` / `max()`

```hcl
min(1, 5, 3)  # 1
max(1, 5, 3)  # 5
```

---

### `ceil()` / `floor()`

```hcl
ceil(2.3)   # 3
floor(2.9)  # 2
```

---

### `abs()`

```hcl
abs(-10)  # 10
```

---

### ✅ Real Use Case

Disk size calculation:

```hcl
volume_size = max(var.disk_size, 20)
```

Ensures minimum size = 20 GB.

---

# 3️⃣ Collection Functions (Lists & Maps)

Used heavily in **real Terraform projects**.

---

## 🔹 `length()`

```hcl
length(var.subnet_ids)
```

---

## 🔹 `element()`

```hcl
element(var.subnet_ids, 0)
```

---

## 🔹 `lookup()`

```hcl
lookup(var.tags, "env", "dev")
```

If key not found → default used.

---

## 🔹 `keys()` / `values()`

```hcl
keys(var.tags)
values(var.tags)
```

---

## 🔹 `merge()`

```hcl
merge(
  { env = "dev" },
  { owner = "ops" }
)
```

Result:

```hcl
{ env = "dev", owner = "ops" }
```

---

## 🔹 `flatten()`

```hcl
flatten([[1,2],[3,4]])
```

Result:

```
[1,2,3,4]
```

---

### ✅ Real Use Case

Combining tags:

```hcl
tags = merge(
  var.common_tags,
  { Name = "web-${var.env}" }
)
```

---

# 4️⃣ File Functions

Used to **read external files**.

---

## 🔹 `file()`

```hcl
file("user-data.sh")
```

Common for EC2 user data:

```hcl
user_data = file("userdata.sh")
```

---

## 🔹 `templatefile()`

```hcl
templatefile("config.tpl", {
  env  = var.env
  port = 8080
})
```

`config.tpl`

```text
ENV=${env}
PORT=${port}
```

---

### ✅ Real Use Case

Dynamic config injection into servers.

---

# 5️⃣ Conditional Expressions

Used for **decision making**.

---

## 🔹 Syntax

```hcl
condition ? true_value : false_value
```

---

### Example

```hcl
instance_type = var.env == "prod" ? "t3.large" : "t2.micro"
```

---

### Boolean Toggle Example

```hcl
count = var.create_instance ? 1 : 0
```

---

### Nested Condition (Avoid if possible)

```hcl
var.env == "prod" ? "t3.large" :
var.env == "stage" ? "t3.micro" :
"t2.micro"
```

---

### ✅ Best Practice

* Use **locals** to keep conditions clean
* Avoid deeply nested conditions

---

# 6️⃣ Loops & Dynamic Blocks

Terraform supports **loops for data** and **dynamic blocks for nested configs**.

---

## 🔹 `for` Expressions (Loops)

### Example: List Transformation

```hcl
[for subnet in var.subnets : subnet.id]
```

---

### Map Transformation

```hcl
{
  for k, v in var.tags :
  k => upper(v)
}
```

---

### Filtering

```hcl
[for s in var.subnets : s if s.public]
```

---

## 🔹 Dynamic Blocks (Advanced & Powerful)

Used when:

* Nested blocks are optional
* Count of blocks is dynamic

---

### Example: Security Group Rules

```hcl
dynamic "ingress" {
  for_each = var.ingress_rules
  content {
    from_port   = ingress.value.from
    to_port     = ingress.value.to
    protocol    = ingress.value.protocol
    cidr_blocks = ingress.value.cidr
  }
}
```

---

### Variable Example

```hcl
ingress_rules = [
  {
    from = 80
    to   = 80
    protocol = "tcp"
    cidr = ["0.0.0.0/0"]
  },
  {
    from = 22
    to   = 22
    protocol = "tcp"
    cidr = ["10.0.0.0/16"]
  }
]
```

---

# 📌 1️⃣5️⃣ Terraform Workspaces

Terraform **workspaces** allow you to manage **multiple states from the same configuration**.
They are simple, powerful—and **often misunderstood**.

> **Important truth (no sugarcoating):**
> Workspaces are useful, but **not a replacement** for proper multi-environment architecture.

---

## 1️⃣ What Are Terraform Workspaces

### 🔹 Definition

A **workspace** is a **separate instance of Terraform state** associated with the **same configuration code**.

### Simple words

> Same Terraform code
> ➜ Multiple isolated state files
> ➜ Selected using a workspace name

---

### 🔹 Default Workspace

When you start Terraform:

```
default
```

Terraform automatically creates a workspace called **default**.

State path (conceptual):

```
terraform.tfstate.d/default/terraform.tfstate
```

---

### 🔹 Multiple Workspaces

If you create workspaces:

```
dev
stage
prod
```

Each one has:

* Its **own state**
* Same `.tf` files
* Different infrastructure

👉 **Code is shared, state is isolated**

---

## 2️⃣ Workspace Use Cases (Where They Actually Make Sense)

### ✅ Good Use Cases

#### 1. Small projects

* One Terraform repo
* Few resources
* Low risk

#### 2. Temporary environments

* Feature testing
* POCs
* Sandboxes

#### 3. Same infra, different scale

```hcl
instance_type = terraform.workspace == "prod"
  ? "t3.large"
  : "t2.micro"
```

---

### ❌ Bad Use Cases (Very Common Mistake)

| Scenario                     | Why Workspaces Fail |
| ---------------------------- | ------------------- |
| Large production systems     | Too risky           |
| Different backends per env   | Not supported       |
| Different providers/accounts | Complex & unsafe    |
| Strict prod isolation        | Poor visibility     |

👉 **Most enterprises do NOT use workspaces for prod**

---

## 3️⃣ Create, List, Switch Workspaces (Commands)

### 🔹 List Workspaces

```bash
terraform workspace list
```

Output:

```
* default
```

---

### 🔹 Create a Workspace

```bash
terraform workspace new dev
```

Output:

```
Created and switched to workspace "dev"
```

---

### 🔹 Switch Workspace

```bash
terraform workspace select prod
```

---

### 🔹 Show Current Workspace

```bash
terraform workspace show
```

Output:

```
prod
```

---

### 🔹 Delete Workspace

```bash
terraform workspace delete dev
```

⚠️ Only allowed if:

* Workspace not active
* State is empty or force removed

---

## 4️⃣ Using Workspaces in Code

Terraform exposes the current workspace via:

```hcl
terraform.workspace
```

---

### Example: Environment-Based Naming

```hcl
resource "aws_instance" "web" {
  ami           = "ami-0abcd"
  instance_type = terraform.workspace == "prod"
    ? "t3.large"
    : "t2.micro"

  tags = {
    Environment = terraform.workspace
  }
}
```

---

### Result

| Workspace | Instance Type |
| --------- | ------------- |
| dev       | t2.micro      |
| stage     | t2.micro      |
| prod      | t3.large      |

---

## 5️⃣ Workspace State Behavior (Important)

### 🔹 State Isolation

Each workspace has **its own state file**.

Conceptually:

```
terraform.tfstate.d/
 ├─ dev/terraform.tfstate
 ├─ stage/terraform.tfstate
 └─ prod/terraform.tfstate
```

---

### 🔹 Backend Interaction

* Same backend
* Same bucket
* Different **state keys**

Example (S3 backend):

```
env:/terraform.tfstate
```

becomes:

```
env:/terraform.tfstate.d/dev
env:/terraform.tfstate.d/prod
```

👉 You **cannot** change backend config per workspace.

---

## 6️⃣ Workspace Best Practices (REAL WORLD)

### ✅ DO

✔ Use workspaces for **small / non-critical setups**
✔ Use workspaces for **temporary environments**
✔ Use `terraform.workspace` only for **simple conditionals**
✔ Keep workspace logic minimal

---

### ❌ DON’T

❌ Don’t use workspaces for large production systems
❌ Don’t mix many conditionals everywhere
❌ Don’t rely on workspaces for account isolation
❌ Don’t use workspaces to replace folder-based environments

---

## 🆚 Workspaces vs Folder-Based Environments (Reality Check)

| Feature            | Workspaces | Folder-Based |
| ------------------ | ---------- | ------------ |
| Setup              | Easy       | More files   |
| State isolation    | ✅          | ✅            |
| Backend per env    | ❌          | ✅            |
| Account separation | ❌          | ✅            |
| Production safety  | ⚠️         | ✅            |
| Industry usage     | Medium     | **High**     |

👉 **Production standard = folder-based environments**
👉 Workspaces = convenience tool, not architecture

---

# 📌 1️⃣6️⃣ Terraform Import

Terraform **import** is used when **infrastructure already exists**, but Terraform **does not know about it yet**.

This is extremely common in real companies where:

* Infra was created manually
* Old teams didn’t use Terraform
* You are migrating to IaC

> **Truth:**
> Terraform import is **not optional** in real DevOps jobs.

---

## 1️⃣ Why Import Is Needed

### 🔹 The Problem

Terraform manages **only what is in its state file**.

If a resource:

* Exists in cloud
* But not in Terraform state

👉 Terraform thinks it **does not exist**

---

### 🔹 What Happens Without Import

Example:

* EC2 already exists (manual)
* You write Terraform code for EC2
* Run `terraform apply`

❌ Terraform tries to **create a duplicate EC2**

💥 Billing issues
💥 Conflicts
💥 Outages

---

### 🔹 Solution → Terraform Import

> Import tells Terraform:
> “This resource already exists — start managing it.”

---

## 2️⃣ Import Existing Resources (Step-by-Step)

### 🔹 Important Rule (Very Important)

Terraform import:

* **Only updates state**
* **Does NOT create configuration code**

You must:

1. Write the resource block first
2. Then import the real resource into state

---

### ✅ Step 1: Identify Existing Resource

Example: Existing EC2 instance

* Instance ID: `i-0abc12345`

---

### ✅ Step 2: Write Matching Resource Block

`main.tf`

```hcl
resource "aws_instance" "existing" {
  ami           = "ami-0abcd1234"
  instance_type = "t2.micro"
}
```

⚠️ Values can be approximate at first
Terraform will sync real values after import.

---

### ✅ Step 3: Run Terraform Import

```bash
terraform import aws_instance.existing i-0abc12345
```

Output:

```
Import successful!
```

---

### ✅ Step 4: Verify State

```bash
terraform state list
```

You should see:

```
aws_instance.existing
```

---

### ✅ Step 5: Sync Configuration (CRITICAL)

Now run:

```bash
terraform plan
```

Terraform will show differences between:

* Code
* Actual resource

👉 Update your `.tf` code until:

```
No changes. Infrastructure is up-to-date.
```

This step is **mandatory**.

---

## 3️⃣ Import Limitations (Very Important)

Terraform import has **serious limitations**.

---

### ❌ What Import DOES NOT Do

❌ Does not generate `.tf` code
❌ Does not import child resources automatically
❌ Does not fix bad architecture
❌ Does not guess dependencies

---

### ❌ Common Beginner Mistake

> “Terraform import will write the code for me”

🚫 **WRONG**

Terraform import only:

* Links existing resource → Terraform state

---

### ❌ Complex Resources

Some resources require:

* Multiple imports
* Manual dependency mapping

Examples:

* Load balancers
* IAM roles + policies
* EKS clusters

---

## 4️⃣ Real-World Import Scenarios

These are **actual situations DevOps engineers face**.

---

### 🔹 Scenario 1: Company Migrating to Terraform

**Situation**

* Infra created manually for years
* No IaC
* Now want Terraform

**Solution**

1. Write Terraform code
2. Import all existing resources
3. Clean plans
4. Lock state in remote backend

👉 This is the **most common import use case**

---

### 🔹 Scenario 2: Lost State File (Disaster Recovery)

**Situation**

* State file deleted
* Infra still exists

**Solution**

* Re-import all resources
* Rebuild state

👉 Painful but possible

---

### 🔹 Scenario 3: Manual Resource Created by Mistake

**Situation**

* Someone created EC2 manually in prod

**Solution**

* Add resource block
* Import it
* Prevent future drift

---

### 🔹 Scenario 4: Split Ownership

**Situation**

* Network team created VPC
* App team uses Terraform

**Solution**

* Import VPC
* Use outputs
* Share state safely

---

# 📌 1️⃣7️⃣ Terraform Security

Terraform is powerful — and that means **dangerous if unsecured**.
Most real incidents happen due to **leaked secrets, exposed state files, or over-permissive IAM**.

> **Reality (no sugarcoating):**
> Terraform security mistakes = **cloud account compromise**.

---

## 1️⃣ Secrets Handling

### 🔹 What Are Secrets in Terraform

* Cloud access keys
* Database passwords
* API tokens
* TLS private keys

### ❌ What NOT to Do

```hcl
password = "MySecret123"
```

❌ Hardcoded
❌ Visible in Git
❌ Stored in state
❌ Permanent leak

---

### ✅ Correct Ways to Handle Secrets

#### 1. Environment Variables (Preferred)

```bash
export TF_VAR_db_password="SuperSecret"
```

```hcl
variable "db_password" {
  type      = string
  sensitive = true
}
```

---

#### 2. Secret Managers (Best Practice)

Use:

* AWS Secrets Manager
* Azure Key Vault
* GCP Secret Manager
* Vault

Example (concept):

```hcl
data "aws_secretsmanager_secret_version" "db" {
  secret_id = "prod/db/password"
}
```

👉 Terraform **reads**, never stores plaintext in code.

---

#### 3. CI/CD Secret Stores

* GitHub Actions secrets
* GitLab CI variables
* Jenkins credentials

👉 Injected at runtime, not stored in repo.

---

## 2️⃣ Sensitive Variables

### 🔹 What Are Sensitive Variables

Sensitive variables **hide values from CLI output and logs**.

---

### Example

```hcl
variable "db_password" {
  type      = string
  sensitive = true
}
```

Usage:

```hcl
password = var.db_password
```

Output:

```bash
terraform output
db_password = <sensitive>
```

---

### ⚠️ Important Reality

Sensitive variables:

* ❌ Are **still stored in state**
* ✅ Are only hidden from terminal output

👉 Sensitive ≠ encrypted

---

## 3️⃣ State File Security (CRITICAL)

### 🔹 Why State File Is Dangerous

State file contains:

* Resource IDs
* Passwords
* Tokens
* Private IPs
* Metadata

> **If attacker gets state file → game over**

---

### ❌ Common State Security Mistakes

* Committing `terraform.tfstate` to Git
* Public S3 bucket
* No encryption
* No access control

---

### ✅ State Security Best Practices

#### 1. Use Remote Backend Only

Never local state in prod.

---

#### 2. Encrypt State Storage

For S3 backend:

* Enable SSE-S3 or SSE-KMS
* Enable bucket encryption

---

#### 3. Restrict Access (IAM)

* Only Terraform role can read/write state
* No public access
* No wildcard permissions

---

#### 4. Enable Versioning

* Protects from accidental overwrite
* Enables rollback

---

#### 5. Separate State Per Environment

```
dev/terraform.tfstate
stage/terraform.tfstate
prod/terraform.tfstate
```

👉 **Prod state deserves highest protection**

---

## 4️⃣ IAM Best Practices (MOST IMPORTANT)

Terraform security is **mostly IAM security**.

---

### 🔹 Principle of Least Privilege

Terraform should have:

* Only required permissions
* Nothing more

❌ Avoid:

```json
"Action": "*",
"Resource": "*"
```

---

### ✅ Correct IAM Design

#### 1. One Role per Environment

* terraform-dev-role
* terraform-stage-role
* terraform-prod-role

---

#### 2. Separate Human vs Terraform Access

* Humans → read-only / limited
* Terraform → controlled write access

---

#### 3. Use IAM Roles, Not Keys

❌ Long-lived access keys
✅ IAM roles + STS

---

#### 4. Protect Production

* MFA required
* Approval gates
* Separate AWS account (best)

---

### 🔥 Real Incident Pattern

> “Terraform had admin access →
> State leaked →
> Attacker created crypto miners”

This happens **a lot**.

---

## 5️⃣ Policy as Code (OPA / Sentinel)

### 🔹 What Is Policy as Code

Policy as Code enforces **rules before infrastructure is created**.

> “Just because you can create it, doesn’t mean you should.”

---

### 🔹 What Policies Can Enforce

✔ No public S3 buckets
✔ No open `0.0.0.0/0` on SSH
✔ Mandatory tags
✔ Approved regions only
✔ Approved instance sizes
✔ No destroy in prod

---

### 🔹 Where Policies Run

* Before `terraform apply`
* In CI/CD
* In Terraform Cloud / Enterprise

---

### 🔹 Example Policy Logic (Concept)

```
Deny if:
- Resource = aws_security_group
- Port = 22
- CIDR = 0.0.0.0/0
```

Terraform apply → ❌ BLOCKED

---

### 🔹 When to Use Which

| Tool     | Best For                       |
| -------- | ------------------------------ |
| OPA      | Open-source, CI/CD, Kubernetes |
| Sentinel | Terraform Cloud / Enterprise   |

👉 Enterprises **always** use policy enforcement.

---

# 📌 1️⃣8️⃣ Terraform Testing & Validation

Terraform **testing & validation** is about **preventing damage before it happens**.
In real companies, **most Terraform runs never reach `apply`** unless they pass strict checks.

> **Hard truth:**
> If you skip validation → you’re gambling with production.

---

## 1️⃣ `terraform validate`

### 🔹 What it Does

`terraform validate` checks:

* Syntax correctness
* Internal consistency
* Required arguments
* Variable types & references

❌ It does NOT:

* Contact cloud providers
* Check credentials
* Create infrastructure

---

### 🔹 How to Run

```bash
terraform validate
```

### Example Output

```
Success! The configuration is valid.
```

---

### ❌ Failure Example

```
Error: Unsupported argument
```

---

### 🔹 When to Use

✔ After writing/modifying code
✔ Before `terraform plan`
✔ In every CI pipeline

👉 **Fast, local, mandatory**

---

## 2️⃣ `terraform plan` Review (MOST IMPORTANT)

### 🔹 What Plan Review Is

`terraform plan` is Terraform’s **change proposal**.

It shows:

* What will be created
* What will be modified
* What will be destroyed

---

### 🔹 Why Review Is Critical

Most production outages happen because:

* Plan was not reviewed
* Destroy action went unnoticed
* Wrong environment was targeted

---

### 🔹 Symbols You Must Understand

| Symbol | Meaning |
| ------ | ------- |
| `+`    | Create  |
| `~`    | Modify  |
| `-`    | Destroy |

---

### 🔹 Safe Plan Workflow

```bash
terraform plan -out=tfplan
terraform show tfplan
```

Benefits:

* Immutable plan file
* Exact plan applied later
* Prevents “plan drift”

---

### 🔹 Production Rule

> **Never run `terraform apply` without reviewing plan output**

---

## 3️⃣ Pre-Commit Hooks

### 🔹 What Are Pre-Commit Hooks

Pre-commit hooks run **before `git commit`**.

They block:

* Bad formatting
* Invalid Terraform
* Dangerous patterns

---

### 🔹 Why They Matter

They stop problems:

* Before PR
* Before CI
* Before prod

👉 Cheapest place to catch mistakes.

---

### 🔹 Common Terraform Pre-Commit Checks

✔ `terraform fmt`
✔ `terraform validate`
✔ TFLint
✔ Security scans

---

### 🔹 Example `.pre-commit-config.yaml`

```yaml
repos:
  - repo: https://github.com/antonbabenko/pre-commit-terraform
    rev: v1.83.0
    hooks:
      - id: terraform_fmt
      - id: terraform_validate
```

---

### 🔹 Result

```bash
git commit -m "terraform change"
```

❌ Commit blocked if checks fail
✅ Commit allowed only if clean

---

## 4️⃣ CI/CD Validation (REAL ENTERPRISE FLOW)

### 🔹 Why CI/CD Validation Exists

* Humans make mistakes
* CI is neutral and strict
* Prevents accidental prod changes

---

### 🔹 Typical CI/CD Terraform Pipeline

```
Code Push
  ↓
terraform fmt -check
  ↓
terraform validate
  ↓
terraform plan
  ↓
Manual Approval
  ↓
terraform apply
```

---

### 🔹 What CI/CD Usually Enforces

✔ No formatting issues
✔ Valid syntax
✔ Clean plan
✔ No destroy in prod
✔ Approved changes only

---

### 🔹 Example CI Rules

* ❌ Destroy in prod → pipeline fails
* ❌ Open security group → blocked
* ❌ Missing tags → blocked

---

### 🔹 Plan as Artifact

CI stores:

```
tfplan
```

Apply stage uses **same plan**, not a new one.

👉 This prevents last-minute surprises.

---

# 📌 1️⃣9️⃣ Terraform with CI/CD

Terraform + CI/CD is **mandatory in real DevOps jobs**.
Manual `terraform apply` on laptops **does not scale and is unsafe**.

> **Reality:**
> In production, Terraform runs **only through CI/CD**, not humans.

---

# 🔁 Why Terraform Must Run in CI/CD

Without CI/CD:

* Wrong environment applied ❌
* No review ❌
* No audit trail ❌
* Accidental destroy ❌

With CI/CD:

* Predictable
* Auditable
* Safe
* Approved

---

# 1️⃣ Terraform in GitHub Actions

### 🔹 When GitHub Actions Is Used

* GitHub repositories
* Small → large teams
* Very common in startups & mid-size orgs

---

## ✅ Basic GitHub Actions Workflow

### `.github/workflows/terraform.yml`

```yaml
name: Terraform CI

on:
  pull_request:
  push:
    branches: [ "main" ]

jobs:
  terraform:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout
      uses: actions/checkout@v4

    - name: Setup Terraform
      uses: hashicorp/setup-terraform@v3

    - name: Terraform Init
      run: terraform init

    - name: Terraform Validate
      run: terraform validate

    - name: Terraform Plan
      run: terraform plan
```

---

### 🔹 How This Works

* PR → plan only
* Main branch → plan + apply (with approval)

👉 **Secrets are stored in GitHub Secrets**, not code.

---

## 🔐 GitHub Secrets Example

```
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
```

---

# 2️⃣ Terraform in GitLab CI

### 🔹 When GitLab CI Is Used

* GitLab repositories
* Strong enterprise usage
* Built-in approvals

---

## ✅ GitLab CI Pipeline Example

### `.gitlab-ci.yml`

```yaml
stages:
  - validate
  - plan
  - apply

terraform_validate:
  stage: validate
  script:
    - terraform init
    - terraform validate

terraform_plan:
  stage: plan
  script:
    - terraform plan
  artifacts:
    paths:
      - tfplan

terraform_apply:
  stage: apply
  when: manual
  script:
    - terraform apply -auto-approve
```

---

### 🔹 Key Features

✔ `when: manual` = approval
✔ Artifacts store plan
✔ Environment-based rules

👉 GitLab CI is **very strong for regulated environments**.

---

# 3️⃣ Terraform in Jenkins

### 🔹 When Jenkins Is Used

* Legacy environments
* On-prem
* Highly customized pipelines

---

## ✅ Jenkinsfile Example

```groovy
pipeline {
  agent any

  stages {
    stage('Init') {
      steps {
        sh 'terraform init'
      }
    }

    stage('Validate') {
      steps {
        sh 'terraform validate'
      }
    }

    stage('Plan') {
      steps {
        sh 'terraform plan -out=tfplan'
      }
    }

    stage('Apply') {
      input {
        message "Approve Terraform Apply?"
      }
      steps {
        sh 'terraform apply tfplan'
      }
    }
  }
}
```

---

### 🔹 Jenkins Strength

✔ Manual approvals
✔ Full control
✔ Integrates with everything

❌ More maintenance
❌ Less cloud-native

---

# 4️⃣ Automated Plan & Apply (Safe Way)

### 🔹 Golden Rule

> **Plan and Apply must use the SAME plan file**

---

### ✅ Correct Pattern

```bash
terraform plan -out=tfplan
terraform apply tfplan
```

---

### ❌ Wrong Pattern

```bash
terraform plan
terraform apply
```

Why wrong?

* Code may change
* Drift may occur
* Unsafe

---

### 🔹 CI/CD Reality

* Plan runs automatically
* Apply is **manual / gated**
* Prod never auto-applies

---

# 5️⃣ Approval Workflows (MOST IMPORTANT)

Approval workflows **protect production**.

---

## 🔹 Common Approval Models

### 1️⃣ Pull Request Approval

* Code review
* Terraform plan visible
* Merge allowed only after approval

---

### 2️⃣ Manual Apply Step

* Pipeline pauses
* Human approves
* Apply runs

---

### 3️⃣ Environment-Based Rules

| Env   | Apply                    |
| ----- | ------------------------ |
| Dev   | Auto                     |
| Stage | Manual                   |
| Prod  | Manual + senior approval |

---

### 🔹 Example Rule

> ❌ Destroy in prod → pipeline fails
> ❌ No approval → no apply

---
