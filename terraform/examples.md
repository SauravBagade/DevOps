# 📌Providers (Core Concept) — **Examples (Practical & Real-World)**

---

## 1️⃣ Basic Provider Example (AWS)

### 👉 Use case

Create infrastructure in **one AWS region**.

### `providers.tf`

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
  region = "ap-south-1"
}
```

### `main.tf`

```hcl
resource "aws_instance" "web" {
  ami           = "ami-0abcdef12345"
  instance_type = "t2.micro"

  tags = {
    Name = "web-server"
  }
}
```

📌 **What happens**

* Terraform uses AWS provider
* Auth via AWS CLI / IAM role
* EC2 is created in Mumbai region

---

## 2️⃣ Provider Authentication Example (Best Practice)

### 👉 Use case

Secure authentication **without hardcoding keys**

#### Option 1: AWS CLI (local)

```bash
aws configure
```

#### Option 2: Environment variables (CI/CD)

```bash
export AWS_ACCESS_KEY_ID=xxxx
export AWS_SECRET_ACCESS_KEY=xxxx
```

#### Option 3 (BEST – Production)

➡️ IAM Role attached to EC2 / CI runner
(No keys stored anywhere)

---

# 📌 Resources (Real Infrastructure) 

Below are **clear, exam + job-ready Terraform resource examples**.
These are **exactly how resources are used in real projects**, not theory.

---

## 1️⃣ Basic Resource Example (EC2 Instance)

### 👉 What is happening

Terraform creates **one real EC2 server**.

```hcl
resource "aws_instance" "web" {
  ami           = "ami-0abcd1234"
  instance_type = "t2.micro"

  tags = {
    Name = "web-server"
  }
}
```

### 🔍 Explanation

* `aws_instance` → resource type
* `web` → Terraform logical name
* If this block exists → EC2 exists
* If removed → EC2 destroyed

---

## 2️⃣ Multiple Resources Example (VPC → Subnet → EC2)

### 👉 Real dependency chain

```hcl
resource "aws_vpc" "main" {
  cidr_block = "10.0.0.0/16"
}

resource "aws_subnet" "public" {
  vpc_id     = aws_vpc.main.id
  cidr_block = "10.0.1.0/24"
}

resource "aws_instance" "app" {
  ami           = "ami-0abcd1234"
  instance_type = "t2.micro"
  subnet_id     = aws_subnet.public.id
}
```

### 🔍 What Terraform does automatically

```
VPC → Subnet → EC2
```

✔ No `depends_on` needed
✔ Terraform detects dependency from references

---

## 3️⃣ Resource Dependency Example (`depends_on`)

### 👉 When Terraform cannot auto-detect dependency

```hcl
resource "aws_iam_role" "role" {
  name = "app-role"
  assume_role_policy = "{}"
}

resource "aws_iam_role_policy_attachment" "attach" {
  role       = aws_iam_role.role.name
  policy_arn = "arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess"
}

resource "aws_instance" "app" {
  ami           = "ami-0abcd1234"
  instance_type = "t2.micro"

  depends_on = [
    aws_iam_role_policy_attachment.attach
  ]
}
```

### 🔍 Why `depends_on`

* IAM policy attachment has no direct reference
* Terraform must be forced to wait

⚠️ Use `depends_on` **only when required**

---

## 4️⃣ Resource with `count` Example

### 👉 Create multiple identical servers

```hcl
resource "aws_instance" "web" {
  count         = 2
  ami           = "ami-0abcd1234"
  instance_type = "t2.micro"

  tags = {
    Name = "web-${count.index}"
  }
}
```

### Result

```
aws_instance.web[0]
aws_instance.web[1]
```

✔ Good for **simple scaling**
❌ Risky if list order changes

---

## 5️⃣ Resource with `for_each` Example (Best Practice)

### 👉 Safer than `count`

```hcl
variable "servers" {
  default = {
    dev  = "t2.micro"
    prod = "t3.large"
  }
}

resource "aws_instance" "app" {
  for_each      = var.servers
  ami           = "ami-0abcd1234"
  instance_type = each.value

  tags = {
    Name = each.key
  }
}
```

### Result

```
aws_instance.app["dev"]
aws_instance.app["prod"]
```

✔ Stable
✔ Production-safe

---

## 6️⃣ Resource Lifecycle Example (`prevent_destroy`)

### 👉 Protect production resources

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

❌ **Terraform blocks deletion**

✔ Mandatory for:

* Databases
* S3 buckets
* Critical infra

---

# 📌 Variables & Input Management 

Below is a **complete, real-world EC2 example** showing **variables, tfvars, precedence, env vars, and sensitive values** exactly how DevOps engineers use them.

---

## ✅ Goal (What We Are Building)

We want to create an **EC2 instance** where:

* AMI, instance type, and environment are configurable
* Dev & Prod use different values
* Secrets are not hardcoded

---

## 1️⃣ Variable Definitions (`variables.tf`)

```hcl
variable "env" {
  type        = string
  description = "Environment name (dev/prod)"
}

variable "ami_id" {
  type        = string
  description = "AMI ID for EC2"
}

variable "instance_type" {
  type        = string
  description = "EC2 instance type"
  default     = "t2.micro"
}

variable "instance_count" {
  type        = number
  description = "Number of EC2 instances"
  default     = 1
}

variable "enable_monitoring" {
  type    = bool
  default = true
}

variable "tags" {
  type = map(string)
}

variable "db_password" {
  type      = string
  sensitive = true
}
```

📌 **Variable types used**

* `string` → env, ami
* `number` → count
* `bool` → monitoring
* `map` → tags
* `sensitive` → password

---

## 2️⃣ EC2 Resource Using Variables (`main.tf`)

```hcl
resource "aws_instance" "app" {
  count         = var.instance_count
  ami           = var.ami_id
  instance_type = var.instance_type
  monitoring    = var.enable_monitoring

  tags = merge(
    var.tags,
    {
      Name = "ec2-${var.env}-${count.index}"
    }
  )
}
```

### 🔍 What is happening

* EC2 count is dynamic
* Instance type changes per env
* Tags are merged dynamically
* No hardcoded values ✅

---

## 3️⃣ Environment-Specific Values (`terraform.tfvars`)

### 🔹 Dev Environment

```hcl
env             = "dev"
ami_id          = "ami-0dev12345"
instance_type   = "t2.micro"
instance_count  = 1

tags = {
  Project = "Terraform"
  Owner   = "DevTeam"
}
```

---

### 🔹 Prod Environment

```hcl
env             = "prod"
ami_id          = "ami-0prod6789"
instance_type   = "t3.large"
instance_count  = 2

tags = {
  Project = "Terraform"
  Owner   = "OpsTeam"
}
```

---

## 4️⃣ Using `.tfvars` Explicitly

```bash
terraform apply -var-file=prod.tfvars
```

✔ Clean
✔ Safe
✔ Industry standard

---

## 5️⃣ Environment Variables Example (CI/CD)

### 👉 No secrets in code or tfvars

```bash
export TF_VAR_db_password="SuperSecret123"
```

Terraform automatically picks it up.

---

## 6️⃣ Variable Precedence (Exam Question ⭐)

**Highest → Lowest**

1. CLI `-var`
2. `-var-file`
3. `terraform.tfvars`
4. `*.auto.tfvars`
5. Environment variables (`TF_VAR_`)
6. Default values

### Example

```bash
terraform apply -var="instance_type=t3.medium"
```

👉 This **overrides everything**

---

## 7️⃣ Sensitive Variable Reality (IMPORTANT ⚠️)

```hcl
variable "db_password" {
  sensitive = true
}
```

✔ Hidden in CLI output
❌ Still stored in `terraform.tfstate`

👉 **State file must be secured**

---

![Image](https://spaceliftio.wpcomstaging.com/wp-content/uploads/2022/04/image6.png)

![Image](https://substackcdn.com/image/fetch/%24s_%21undD%21%2Cf_auto%2Cq_auto%3Agood%2Cfl_progressive%3Asteep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff93f5234-c58f-466c-a60f-f55087ea991b_1370x932.png)

![Image](https://media2.dev.to/dynamic/image/width%3D800%2Cheight%3D%2Cfit%3Dscale-down%2Cgravity%3Dauto%2Cformat%3Dauto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2F60759qvjsecacoo29v57.png)

![Image](https://media2.dev.to/dynamic/image/width%3D800%2Cheight%3D%2Cfit%3Dscale-down%2Cgravity%3Dauto%2Cformat%3Dauto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fl1eu0470xts0l2mvgkr5.png)

# 📌 Outputs — **EC2 Example 

Below is a **complete, real-world EC2 outputs example** showing:

* Basic outputs
* How to read them
* Sensitive outputs
* Using outputs across modules

---

## ✅ Goal

After creating an **EC2 instance**, we want to **expose useful values** like:

* Instance ID
* Public IP
* Private IP
* DNS name
* (Optional) sensitive values

---

## 1️⃣ EC2 Resource (`main.tf`)

```hcl
resource "aws_instance" "web" {
  ami           = "ami-0abcd1234"
  instance_type = "t2.micro"

  tags = {
    Name = "web-server"
  }
}
```

---

## 2️⃣ Basic Output Blocks (`outputs.tf`)

### 🔹 EC2 Instance ID

```hcl
output "ec2_instance_id" {
  value = aws_instance.web.id
}
```

### 🔹 Public IP

```hcl
output "ec2_public_ip" {
  value = aws_instance.web.public_ip
}
```

### 🔹 Private IP

```hcl
output "ec2_private_ip" {
  value = aws_instance.web.private_ip
}
```

### 🔹 Public DNS

```hcl
output "ec2_public_dns" {
  value = aws_instance.web.public_dns
}
```

---

## 3️⃣ View Outputs (CLI)

After apply:

```bash
terraform apply
```

### Show all outputs

```bash
terraform output
```

Example result:

```
ec2_instance_id = "i-0a123456789"
ec2_public_ip   = "13.235.xx.xx"
ec2_private_ip  = "10.0.1.15"
ec2_public_dns  = "ec2-13-235-xx-xx.ap-south-1.compute.amazonaws.com"
```

---

### Get a single output

```bash
terraform output ec2_public_ip
```

---

### JSON format (CI/CD, scripts)

```bash
terraform output -json
```

Used in:

* GitHub Actions
* Jenkins
* Bash / Python automation

---
![Image](https://developer.hashicorp.com/_next/image?dpl=dpl_Esfip2Ttu82ZYhc2H3yjMRRBq8bm\&q=75\&url=https%3A%2F%2Fcontent.hashicorp.com%2Fapi%2Fassets%3Fproduct%3Dtutorials%26version%3Dmain%26asset%3Dpublic%252Fimg%252Fterraform%252Frecommended-patterns%252Farch-diag-overview.png%26width%3D1763%26height%3D961\&w=3840)

![Image](https://miro.medium.com/0%2APgKqKDKz8vQ5xhPs.png)

![Image](https://media.beehiiv.com/cdn-cgi/image/fit%3Dscale-down%2Cformat%3Dauto%2Conerror%3Dredirect%2Cquality%3D80/uploads/asset/file/a70941e1-5fb2-4a29-a70b-a671150e9298/directory_2.png?t=1730702773)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2A2Hv4lH0-1fhM3ZQ2tWcQ_g.png)

# 📌 Terraform Modules — **Complete Example (Practical & Exam-Ready)**

---

## 🗂️ Project Structure (Industry Standard)

```
terraform-project/
├── modules/
│   └── ec2/
│       ├── main.tf
│       ├── variables.tf
│       └── outputs.tf
│
├── env/
│   ├── dev/
│   │   ├── main.tf
│   │   └── terraform.tfvars
│   └── prod/
│       ├── main.tf
│       └── terraform.tfvars
```

👉 `modules/` = reusable logic
👉 `env/` = environment-specific usage

---

## 1️⃣ EC2 Child Module (Reusable)

## 📁 `modules/ec2/variables.tf`

```hcl
variable "ami_id" {
  type = string
}

variable "instance_type" {
  type = string
}

variable "env" {
  type = string
}

variable "tags" {
  type = map(string)
}
```

---

## 📁 `modules/ec2/main.tf`

```hcl
resource "aws_instance" "this" {
  ami           = var.ami_id
  instance_type = var.instance_type

  tags = merge(
    var.tags,
    {
      Name = "ec2-${var.env}"
    }
  )
}
```

---

## 📁 `modules/ec2/outputs.tf`

```hcl
output "instance_id" {
  value = aws_instance.this.id
}

output "public_ip" {
  value = aws_instance.this.public_ip
}
```

✅ No hardcoding
✅ Fully reusable
✅ Clean inputs & outputs

---

## 2️⃣ Root Module – Dev Environment

## 📁 `env/dev/main.tf`

```hcl
provider "aws" {
  region = "ap-south-1"
}

module "ec2" {
  source         = "../../modules/ec2"
  env            = "dev"
  ami_id         = "ami-0dev12345"
  instance_type  = "t2.micro"

  tags = {
    Project = "Terraform"
    Owner   = "DevTeam"
  }
}
```

---

## 📁 `env/dev/terraform.tfvars`

```hcl
# optional if values already in main.tf
```

Run:

```bash
cd env/dev
terraform init
terraform apply
```

---

## 3️⃣ Root Module – Prod Environment

## 📁 `env/prod/main.tf`

```hcl
provider "aws" {
  region = "ap-south-1"
}

module "ec2" {
  source         = "../../modules/ec2"
  env            = "prod"
  ami_id         = "ami-0prod67890"
  instance_type  = "t3.large"

  tags = {
    Project = "Terraform"
    Owner   = "OpsTeam"
  }
}
```

Run:

```bash
cd env/prod
terraform init
terraform apply
```

---

## 4️⃣ Using Module Outputs in Root Module

## 📁 `env/prod/outputs.tf`

```hcl
output "prod_ec2_public_ip" {
  value = module.ec2.public_ip
}
```

After apply:

```bash
terraform output
```

---
