---
AWS Lambda
---
## 1. Introduction to AWS Lambda
---
### What is AWS Lambda

**AWS Lambda** is a **serverless computing service provided by Amazon Web Services** that allows developers to run code **without provisioning or managing servers**.

You simply upload your code, and Lambda automatically runs it when an **event trigger** occurs.

Lambda automatically:

* Allocates compute resources
* Scales the application
* Runs the code
* Stops execution when finished

You only pay for the **compute time used**.

---

### Simple Definition

**AWS Lambda is a serverless service that executes code in response to events and automatically manages the underlying infrastructure.**

---

### Example

Example scenario:

1. A user uploads an image to **Amazon S3**
2. The upload event triggers a Lambda function
3. Lambda resizes the image
4. The processed image is stored back in S3

This entire process happens **without managing any servers**.

---

### Traditional Server vs Lambda

| Traditional Server      | AWS Lambda             |
| ----------------------- | ---------------------- |
| Need to create server   | No server management   |
| Manual scaling          | Automatic scaling      |
| Pay for server uptime   | Pay only for execution |
| OS maintenance required | Fully managed by AWS   |

---

### Why AWS Lambda Was Created

Before serverless computing:

Developers had to:

* Launch servers
* Install operating systems
* Manage scaling
* Monitor infrastructure
* Patch systems

This caused:

* Higher operational overhead
* Infrastructure complexity
* Higher cost

**Lambda solves these problems by removing server management completely.**

---

### Key Characteristics of AWS Lambda

1️⃣ **Serverless**
No server provisioning or management.

2️⃣ **Event Driven**
Runs only when triggered by an event.

3️⃣ **Auto Scaling**
Automatically scales from **1 request to thousands of requests**.

4️⃣ **Fully Managed**
AWS manages:

* OS
* Patching
* Scaling
* Availability

5️⃣ **Short-lived execution**
Lambda functions run for a **maximum of 15 minutes**.

---

### Programming Languages Supported

AWS Lambda supports multiple runtimes:

* Python
* Node.js
* Java
* Go
* .NET
* Ruby
* Custom Runtime

---

### AWS Services That Trigger Lambda

Lambda integrates with many AWS services:

* **Amazon S3**
* **Amazon DynamoDB**
* **Amazon API Gateway**
* **Amazon EventBridge**
* **Amazon SNS**
* **Amazon SQS**

These services can automatically **trigger Lambda functions**.

---

### AWS Lambda Execution Flow

Typical workflow:

```
Event Source
   ↓
Trigger
   ↓
AWS Lambda Function
   ↓
Process Logic
   ↓
Response / Output
```

Example:

```
User Upload File → S3 Event → Lambda → Process File
```

---

### When to Use AWS Lambda

Lambda is best used for:

* Event-driven applications
* Microservices
* Real-time file processing
* API backends
* Automation tasks
* Scheduled jobs
* Data transformation

---
---
## 2. Serverless Architecture Overview
---
Serverless architecture is the core concept behind **AWS Lambda** and many modern cloud applications. It allows developers to build and run applications **without managing servers or infrastructure**.

In this model, the cloud provider such as **Amazon Web Services** automatically handles:

* Server provisioning
* Scaling
* Infrastructure maintenance
* Availability
* Patching and updates

Developers only focus on **writing application logic**.

---

## What is Serverless Architecture

**Serverless Architecture** is a cloud computing model where the cloud provider manages the infrastructure, and applications run as **small event-driven functions**.

Even though it is called **serverless**, servers still exist, but **developers do not manage them**.

Instead of running an application continuously on a server, code runs **only when triggered by an event**.

---

## Key Characteristics of Serverless Architecture

### 1. No Server Management

Developers do not manage:

* Operating systems
* Virtual machines
* Hardware
* Scaling infrastructure

All infrastructure is managed by AWS.

---

### 2. Event Driven Execution

Serverless applications run **in response to events**.

Examples of events:

* File uploaded to **Amazon S3**
* HTTP request through **Amazon API Gateway**
* Database update in **Amazon DynamoDB**
* Message from **Amazon SQS**

---

### 3. Stateless Compute

Serverless functions do **not maintain state between executions**.

Each execution is independent.

If state needs to be stored, external services are used such as:

* **Amazon DynamoDB**
* **Amazon S3**
* **Amazon ElastiCache**

---

### 4. Automatic Scaling

Serverless applications scale automatically.

Example:

| Requests        | Lambda Instances |
| --------------- | ---------------- |
| 1 request       | 1 instance       |
| 100 requests    | 100 instances    |
| 10,000 requests | 10,000 instances |

Scaling happens automatically without manual configuration.

---

### 5. Pay Per Use Pricing

You only pay for:

* Number of requests
* Execution time
* Memory used

When the function is not running, **no cost is incurred**.

---

## Traditional Architecture vs Serverless Architecture

| Feature                    | Traditional Architecture | Serverless Architecture |
| -------------------------- | ------------------------ | ----------------------- |
| Server Management          | Required                 | Not required            |
| Scaling                    | Manual                   | Automatic               |
| Infrastructure Maintenance | Required                 | Managed by AWS          |
| Billing                    | Pay for uptime           | Pay per execution       |
| Deployment                 | Complex                  | Simple                  |

---

## Serverless Architecture Workflow

Typical serverless application architecture:

```
User Request
     ↓
API Gateway
     ↓
AWS Lambda
     ↓
Database / Storage
```

Example services used:

* **Amazon API Gateway**
* **AWS Lambda**
* **Amazon DynamoDB**
* **Amazon S3**

---

## Example: Image Processing Serverless Architecture

```
User Upload Image
        ↓
     Amazon S3
        ↓
    S3 Event Trigger
        ↓
     AWS Lambda
        ↓
 Resize / Compress Image
        ↓
 Save Image to S3
```

No servers are required for this workflow.

---

## Core AWS Services Used in Serverless Architecture

| AWS Service            | Purpose              |
| ---------------------- | -------------------- |
| **AWS Lambda**         | Run application code |
| **Amazon API Gateway** | Create APIs          |
| **Amazon DynamoDB**    | Store data           |
| **Amazon S3**          | File storage         |
| **Amazon EventBridge** | Event routing        |

---

## Real Production Serverless Architecture

Example DevOps production architecture:

```
Users
   ↓
CloudFront
   ↓
API Gateway
   ↓
AWS Lambda
   ↓
DynamoDB
   ↓
S3
```

Benefits:

* Fully scalable
* Highly available
* Low operational overhead
* Cost efficient

---
---
## 3. Benefits of AWS Lambda
---

**AWS Lambda** provides many advantages compared to traditional server-based computing. It is designed to simplify application development by removing infrastructure management and enabling event-driven execution.

Below are the major benefits of using AWS Lambda in cloud architectures.

---

## 3.1 No Server Management

One of the biggest advantages of AWS Lambda is that **developers do not need to manage servers**.

In traditional infrastructure you must:

* Launch servers
* Install operating systems
* Configure runtime environments
* Apply security patches
* Monitor server health

With AWS Lambda, all infrastructure is managed by **Amazon Web Services**.

Developers only need to:

* Write code
* Upload the function
* Configure triggers

AWS automatically handles server provisioning and maintenance.

---

## 3.2 Automatic Scaling

AWS Lambda automatically scales based on incoming requests.

For example:

| Number of Requests | Lambda Instances        |
| ------------------ | ----------------------- |
| 1 request          | 1 execution environment |
| 100 requests       | 100 parallel executions |
| 10,000 requests    | 10,000 executions       |

Scaling happens automatically without manual configuration.

This makes Lambda ideal for applications with **unpredictable traffic patterns**.

---

## 3.3 Pay-Per-Use Pricing

AWS Lambda follows a **pay-as-you-go model**.

You only pay for:

* Number of function invocations
* Execution duration
* Memory allocated

If your function is not running, **you pay nothing**.

This is very different from traditional servers where you pay for the instance even if it is idle.

Example:

| Scenario                   | Traditional Server         | Lambda                |
| -------------------------- | -------------------------- | --------------------- |
| Server running but idle    | Cost incurred              | No cost               |
| Code executed for 1 second | Pay for full server uptime | Pay only for 1 second |

---

## 3.4 High Availability

AWS Lambda is built on AWS global infrastructure.

Functions automatically run across multiple **Availability Zones** within a region.

This provides:

* Fault tolerance
* High availability
* Automatic recovery

If one server fails, AWS automatically runs the function on another server.

---

## 3.5 Built-In Fault Tolerance

Lambda automatically handles failures.

Features include:

* Automatic retries
* Dead Letter Queue (DLQ)
* Event replay

Lambda integrates with services such as:

* **Amazon SQS**
* **Amazon SNS**
* **Amazon EventBridge**

This helps ensure reliable event processing.

---

## 3.6 Fast Development and Deployment

Developers can quickly deploy applications without managing infrastructure.

Lambda functions can be deployed using:

* AWS Console
* AWS CLI
* Infrastructure as Code tools like **Terraform**
* **AWS CloudFormation**

This enables rapid application development and continuous deployment.

---

## 3.7 Deep Integration with AWS Services

AWS Lambda integrates with many AWS services, enabling powerful architectures.

Common integrations include:

* **Amazon S3** – file upload triggers
* **Amazon DynamoDB** – database events
* **Amazon API Gateway** – REST APIs
* **Amazon EventBridge** – event routing
* **Amazon Kinesis** – stream processing

These integrations allow developers to build **event-driven cloud architectures** easily.

---

## 3.8 Reduced Operational Complexity

Because AWS manages the infrastructure, teams do not need to worry about:

* Server maintenance
* Capacity planning
* OS updates
* Hardware management

This reduces operational overhead and allows teams to focus on **application logic**.

---

## 3.9 Improved Resource Efficiency

Traditional servers often remain idle when traffic is low.

Lambda only runs when needed, which improves resource utilization and reduces waste.

Example:

```
Traditional Server:
Server runs 24 hours even if used only 10 minutes.

AWS Lambda:
Function runs only when triggered.
```

---

## 3.10 Supports Microservices Architecture

AWS Lambda is ideal for building **microservices-based applications**.

Each Lambda function can perform a single task.

Example microservices architecture:

```
User Request
      ↓
API Gateway
      ↓
Lambda Function
      ↓
DynamoDB / S3
```

Each service is independent and scalable.

---
---
## 4. AWS Lambda Global Infrastructure
---

**AWS Lambda** runs on the global infrastructure of **Amazon Web Services**.
This infrastructure is designed to provide **high availability, scalability, and low latency** for applications running Lambda functions.

AWS deploys Lambda across multiple **Regions, Availability Zones, and Edge Locations**, ensuring that applications remain highly reliable and globally accessible.

---

# 4.1 AWS Regions

An **AWS Region** is a geographical area that contains multiple isolated data centers where AWS services run.

Lambda functions are deployed inside a **specific region**, and the function execution occurs within that region.

Examples of AWS regions:

| Region Name              | Region Code    |
| ------------------------ | -------------- |
| US East (N. Virginia)    | us-east-1      |
| US West (Oregon)         | us-west-2      |
| Europe (Ireland)         | eu-west-1      |
| Asia Pacific (Mumbai)    | ap-south-1     |
| Asia Pacific (Singapore) | ap-southeast-1 |

For example, if you deploy a Lambda function in the **Mumbai region**, it runs in:

```
ap-south-1
```

Choosing the correct region helps reduce **network latency for users**.

---

# 4.2 Availability Zones

Each AWS region contains multiple **Availability Zones (AZs)**.

An Availability Zone is a **separate data center with independent power, networking, and cooling**.

Example:

```
Region (ap-south-1)
   ├── AZ-a
   ├── AZ-b
   └── AZ-c
```

Lambda automatically distributes function execution across multiple AZs to provide:

* High availability
* Fault tolerance
* Automatic failover

If one data center fails, Lambda continues running in another AZ.

---

# 4.3 AWS Edge Locations

AWS also operates **Edge Locations**, which are smaller data centers located close to users worldwide.

These are primarily used by **Amazon CloudFront** and **Lambda@Edge**.

Edge locations help:

* Reduce latency
* Deliver content faster
* Process requests closer to users

Example:

```
User
   ↓
Nearest Edge Location
   ↓
AWS Region
   ↓
Lambda Function
```

---

# 4.4 Lambda@Edge

**Lambda@Edge** allows Lambda functions to run at **CloudFront edge locations** instead of AWS regions.

It is commonly used with **Amazon CloudFront**.

This enables developers to execute code closer to users.

### Use Cases

* Modify HTTP headers
* Authentication
* Redirect users
* Personalize content
* Security filtering

Example workflow:

```
User Request
      ↓
CloudFront Edge Location
      ↓
Lambda@Edge
      ↓
Origin Server
```

This improves **response time and performance**.

---

# 4.5 Lambda Global Availability

AWS Lambda is available in **almost all AWS regions worldwide**.

This allows organizations to deploy applications:

* Near their users
* Across multiple regions
* With global redundancy

Example global deployment:

```
Users Worldwide
      ↓
Multiple AWS Regions
      ↓
Lambda Functions
      ↓
Distributed Application
```

Benefits:

* Global application availability
* Reduced latency
* Disaster recovery capability

---

# 4.6 Multi-Region Architecture with Lambda

For high availability, organizations often deploy Lambda functions in **multiple regions**.

Example architecture:

```
Users
   ↓
Route53 (DNS Routing)
   ↓
Region 1 (Primary)
   ↓
Lambda Functions

If failure occurs

Users
   ↓
Route53
   ↓
Region 2 (Failover)
   ↓
Lambda Functions
```

Example AWS services used:

* **Amazon Route 53**
* **AWS Lambda**
* **Amazon DynamoDB Global Tables**

This architecture ensures **business continuity**.

---

# 4.7 Global Infrastructure Benefits for Lambda

AWS global infrastructure provides the following benefits:

### High Availability

Lambda runs across multiple Availability Zones automatically.

### Fault Tolerance

Failures in one data center do not affect the application.

### Low Latency

Users can access services from nearby regions or edge locations.

### Scalability

Lambda can handle millions of requests globally.

---
---
## 5. AWS Lambda Architecture

**AWS Lambda** architecture is designed to execute code **in response to events without managing servers**.
The architecture automatically handles **execution environments, scaling, request processing, and resource allocation**.

Lambda functions run inside **isolated containers** managed by **Amazon Web Services**, ensuring security, scalability, and high availability.

---

# 5.1 High-Level AWS Lambda Architecture

A typical Lambda architecture includes:

* Event source
* Trigger
* Lambda function
* Execution environment
* Output service

Example architecture:

```id="n24m9g"
Event Source
     ↓
Trigger
     ↓
AWS Lambda
     ↓
Processing Logic
     ↓
Storage / Database / Response
```

Example services that trigger Lambda:

* **Amazon S3**
* **Amazon API Gateway**
* **Amazon DynamoDB**
* **Amazon EventBridge**

---

# 5.2 Core Components of Lambda Architecture

## 1. Event Source

An **event source** is the AWS service that generates an event to trigger the Lambda function.

Examples:

| Event Source           | Example Event      |
| ---------------------- | ------------------ |
| **Amazon S3**          | File upload        |
| **Amazon DynamoDB**    | Database update    |
| **Amazon API Gateway** | HTTP request       |
| **Amazon SQS**         | New message        |
| **Amazon SNS**         | Notification event |

These events automatically invoke Lambda functions.

---

## 2. Trigger

A **trigger** connects an AWS service to a Lambda function.

When the event occurs, the trigger automatically invokes the function.

Example:

```id="v5j9um"
Image Uploaded to S3
        ↓
S3 Trigger
        ↓
Lambda Function Executes
```

---

## 3. Lambda Function

A **Lambda function** is the actual code that runs when triggered.

It contains:

* Business logic
* Application code
* Dependencies

Example structure:

```id="8cjbcr"
Lambda Function
   ├── Handler
   ├── Code
   └── Dependencies
```

Supported languages include:

* Python
* Node.js
* Java
* Go
* .NET
* Ruby

---

## 4. Execution Environment

When Lambda is triggered, AWS creates an **execution environment**.

This environment includes:

* Runtime (Python, Node.js, etc.)
* Memory allocation
* Temporary storage
* Network configuration

Execution environments are isolated containers that run your code.

Example:

```id="5m00hi"
Event
  ↓
Lambda Service
  ↓
Execution Environment Created
  ↓
Function Code Runs
```

---

# 5.3 Lambda Internal Architecture

Internally, Lambda works with multiple components:

```id="80nbde"
Event Source
     ↓
Lambda Service
     ↓
Function Invocation
     ↓
Execution Environment
     ↓
Function Code Execution
     ↓
Return Response
```

Lambda automatically manages:

* Container creation
* Runtime initialization
* Code execution
* Resource cleanup

---

# 5.4 Lambda Execution Environment

The execution environment contains:

| Component         | Description                             |
| ----------------- | --------------------------------------- |
| Runtime           | Programming language runtime            |
| Handler           | Entry point of the function             |
| Memory            | RAM allocated to function               |
| CPU               | Automatically allocated based on memory |
| Temporary Storage | `/tmp` storage (up to 10 GB)            |

Each Lambda execution environment runs **one function instance at a time**.

---

# 5.5 Lambda Function Invocation Flow

Example invocation process:

```id="7m7yy7"
1. Event occurs
2. Lambda receives event
3. Lambda creates execution environment
4. Runtime loads
5. Function code runs
6. Result returned
```

---

# 5.6 Lambda Cold Start

A **cold start** happens when Lambda runs a function for the first time or after a long idle period.

Steps during cold start:

```id="j3uzsn"
Create container
   ↓
Initialize runtime
   ↓
Load function code
   ↓
Execute function
```

Cold starts can add **extra latency**.

---

# 5.7 Lambda Warm Start

If the function is invoked again quickly, Lambda reuses the existing environment.

This is called a **warm start**.

Advantages:

* Faster execution
* No container creation
* No runtime initialization

Example:

```id="qys5rd"
Previous execution environment reused
       ↓
Function executes immediately
```

---

# 5.8 Lambda Scaling Architecture

Lambda automatically scales by creating multiple execution environments.

Example:

```id="4xmb0l"
Request 1 → Execution Environment 1
Request 2 → Execution Environment 2
Request 3 → Execution Environment 3
```

Each request runs independently.

---

# 5.9 Example Serverless Architecture

Real-world serverless architecture:

```id="cz36n2"
User
   ↓
CloudFront
   ↓
API Gateway
   ↓
AWS Lambda
   ↓
DynamoDB / S3
```

AWS services used:

* **Amazon CloudFront**
* **Amazon API Gateway**
* **AWS Lambda**
* **Amazon DynamoDB**

---
---
## 6. AWS Lambda Core Components
---

The functionality of **AWS Lambda** is built around several core components that work together to execute code when an event occurs. These components define **how the function runs, what triggers it, and how it processes data**.

Understanding these core components is important for building serverless applications on **Amazon Web Services**.

---

# 6.1 Lambda Function

A **Lambda Function** is the main unit of execution in AWS Lambda.
It contains the code that runs when the function is triggered.

A function includes:

* Application code
* Dependencies
* Runtime configuration
* Handler method

Example structure:

```text
Lambda Function
   ├── Source Code
   ├── Libraries / Dependencies
   ├── Handler
   └── Configuration
```

Example Python Lambda function:

```python
def lambda_handler(event, context):
    return "Hello from AWS Lambda"
```

Here:

* `lambda_handler` → function entry point
* `event` → data passed to the function
* `context` → runtime information

---

# 6.2 Runtime

A **runtime** provides the environment required to run Lambda functions.

It includes:

* Programming language interpreter
* Libraries
* Execution environment

AWS Lambda supports multiple runtimes.

| Runtime         | Language   |
| --------------- | ---------- |
| Python Runtime  | Python     |
| Node.js Runtime | JavaScript |
| Java Runtime    | Java       |
| Go Runtime      | Go         |
| .NET Runtime    | C#         |
| Ruby Runtime    | Ruby       |

Example:

If a function is written in Python, Lambda loads the **Python runtime** to execute it.

---

# 6.3 Handler

The **handler** is the **entry point** for a Lambda function.

When the function is invoked, AWS Lambda calls the handler method.

Handler format depends on the programming language.

Example Python handler:

```python
def lambda_handler(event, context):
    print("Lambda function executed")
```

Example Node.js handler:

```javascript
exports.handler = async (event) => {
    return "Hello Lambda";
};
```

Handler responsibilities:

* Process incoming event data
* Execute business logic
* Return output

---

# 6.4 Event Object

The **event object** contains the data sent to the Lambda function when it is triggered.

Different AWS services send different event structures.

Example:

If a file is uploaded to **Amazon S3**, the event contains information about the uploaded object.

Example event JSON:

```json
{
  "bucket": "my-bucket",
  "file": "image.jpg"
}
```

Example Python code accessing event data:

```python
def lambda_handler(event, context):
    bucket = event['bucket']
    file = event['file']
    print(bucket, file)
```

Common event sources:

* **Amazon S3**
* **Amazon DynamoDB**
* **Amazon API Gateway**
* **Amazon SQS**

---

# 6.5 Context Object

The **context object** provides runtime information about the Lambda execution environment.

It contains metadata such as:

| Property       | Description             |
| -------------- | ----------------------- |
| Request ID     | Unique ID of invocation |
| Function Name  | Lambda function name    |
| Memory Limit   | Allocated memory        |
| Remaining Time | Time before timeout     |

Example Python usage:

```python
def lambda_handler(event, context):
    print(context.function_name)
    print(context.memory_limit_in_mb)
```

The context object helps in **logging, debugging, and monitoring**.

---

# 6.6 Execution Role (IAM Role)

A Lambda function needs permissions to access AWS resources.

This is provided using an **execution role** from **AWS Identity and Access Management**.

The execution role defines **what the Lambda function is allowed to do**.

Example permissions:

* Read files from **Amazon S3**
* Write data to **Amazon DynamoDB**
* Send logs to **Amazon CloudWatch**

Example architecture:

```text
Lambda Function
       ↓
Execution Role (IAM)
       ↓
Access AWS Services
```

Without proper permissions, Lambda cannot access other AWS services.

---

# 6.7 Environment Variables

Environment variables allow developers to store configuration values for Lambda functions.

Example values:

* Database URL
* API keys
* Configuration settings

Example Python code:

```python
import os

def lambda_handler(event, context):
    db_url = os.environ['DATABASE_URL']
    print(db_url)
```

Environment variables make applications **more flexible and secure**.

---

# 6.8 Lambda Layers

Lambda layers allow you to **share libraries and dependencies across multiple Lambda functions**.

Benefits:

* Reduce deployment package size
* Reuse common libraries
* Improve code management

Example use cases:

* Python packages
* Node.js libraries
* Machine learning models

---

# Core Components Interaction

All Lambda core components work together during function execution.

Example workflow:

```text
Event Source
     ↓
Trigger
     ↓
Lambda Function
     ↓
Handler
     ↓
Runtime Execution
     ↓
Return Response
```

---
---
## 7. Lambda Function Creation Methods
---

A function in **AWS Lambda** can be created using several methods depending on the workflow and automation level. In real DevOps environments, Lambda functions are often created using **Infrastructure as Code (IaC)** tools rather than manually.

Below are the most common ways to create Lambda functions on **Amazon Web Services**.

---

# 7.1 Create Lambda Function using AWS Console

The AWS Management Console provides a **graphical interface** to create Lambda functions easily.

### Steps

1. Login to AWS Console
2. Open **AWS Lambda**
3. Click **Create function**
4. Select **Author from scratch**
5. Enter configuration details

Example configuration:

| Setting       | Example            |
| ------------- | ------------------ |
| Function name | my-lambda-function |
| Runtime       | Python 3.12        |
| Architecture  | x86_64             |
| Permissions   | Create new role    |

6. Click **Create function**

After creation, you can write code directly in the console editor.

Example code:

```python
def lambda_handler(event, context):
    return "Hello AWS Lambda"
```

---

# 7.2 Create Lambda Function using AWS CLI

Lambda functions can also be created using the **AWS Command Line Interface (CLI)**.

CLI is useful for:

* automation
* scripting
* DevOps workflows

Example command:

```bash
aws lambda create-function \
--function-name myLambdaFunction \
--runtime python3.12 \
--role arn:aws:iam::123456789012:role/lambda-role \
--handler lambda_function.lambda_handler \
--zip-file fileb://function.zip
```

Explanation:

| Parameter     | Description          |
| ------------- | -------------------- |
| function-name | Lambda function name |
| runtime       | Programming runtime  |
| role          | IAM execution role   |
| handler       | Entry point function |
| zip-file      | Deployment package   |

---

# 7.3 Create Lambda Function using Terraform

In DevOps environments, Lambda functions are commonly created using **Terraform**.

Terraform allows infrastructure to be defined as code and deployed automatically.

Example Terraform configuration:

```hcl
provider "aws" {
  region = "ap-south-1"
}

resource "aws_lambda_function" "example" {
  function_name = "example_lambda"

  runtime = "python3.12"
  handler = "lambda_function.lambda_handler"

  role = aws_iam_role.lambda_role.arn

  filename = "lambda_function.zip"
}
```

Advantages:

* Infrastructure version control
* Repeatable deployments
* Automation friendly

---

# 7.4 Create Lambda Function using AWS CloudFormation

**AWS CloudFormation** allows infrastructure to be defined using JSON or YAML templates.

Example YAML template:

```yaml
Resources:
  MyLambdaFunction:
    Type: AWS::Lambda::Function
    Properties:
      FunctionName: MyLambdaFunction
      Runtime: python3.12
      Handler: lambda_function.lambda_handler
      Role: arn:aws:iam::123456789012:role/lambda-role
      Code:
        S3Bucket: my-bucket
        S3Key: lambda_function.zip
```

CloudFormation automatically creates the Lambda function and its resources.

---

# 7.5 Create Lambda using AWS SAM

**AWS Serverless Application Model** (SAM) is used to simplify serverless application development.

SAM templates extend CloudFormation to provide serverless-specific features.

Example SAM template:

```yaml
Resources:
  HelloWorldFunction:
    Type: AWS::Serverless::Function
    Properties:
      Handler: app.lambda_handler
      Runtime: python3.12
      CodeUri: .
      MemorySize: 128
      Timeout: 10
```

SAM makes it easier to deploy serverless applications.

---

# 7.6 Create Lambda using AWS CDK

**AWS Cloud Development Kit** allows developers to define cloud infrastructure using programming languages.

Supported languages:

* TypeScript
* Python
* Java
* C#

Example CDK (Python):

```python
from aws_cdk import aws_lambda as lambda_

lambda_.Function(
    self,
    "MyFunction",
    runtime=lambda_.Runtime.PYTHON_3_12,
    handler="lambda_function.lambda_handler",
    code=lambda_.Code.from_asset("lambda")
)
```

CDK converts the code into CloudFormation templates automatically.

---

# Comparison of Lambda Creation Methods

| Method         | Use Case                                   |
| -------------- | ------------------------------------------ |
| AWS Console    | Beginners and manual testing               |
| AWS CLI        | Automation and scripting                   |
| Terraform      | DevOps Infrastructure as Code              |
| CloudFormation | AWS native IaC                             |
| AWS SAM        | Serverless application deployment          |
| AWS CDK        | Infrastructure using programming languages |

---
---
## 9. Lambda Execution Role (IAM)
---

A Lambda function needs permission to interact with other AWS services. These permissions are provided through an **execution role** created using **AWS Identity and Access Management** and attached to **AWS Lambda**.

The execution role defines **what resources the Lambda function can access** when it runs on **Amazon Web Services**.

Without an execution role, a Lambda function **cannot access AWS services** such as storage, databases, or logging services.

---

# 9.1 What is a Lambda Execution Role

A **Lambda Execution Role** is an IAM role that grants permissions to a Lambda function so it can perform actions on AWS services.

Example actions:

* Read files from **Amazon S3**
* Write data to **Amazon DynamoDB**
* Send logs to **Amazon CloudWatch**

Example architecture:

```
Lambda Function
      ↓
Execution Role (IAM)
      ↓
Access AWS Resources
```

The role acts as a **security identity for the Lambda function**.

---

# 9.2 Why Lambda Execution Role is Required

Lambda functions often interact with multiple AWS services.

Example workflow:

```
User Upload File
       ↓
Amazon S3
       ↓
Trigger Lambda Function
       ↓
Lambda Processes File
       ↓
Save Output to DynamoDB
```

To perform these actions, Lambda must have permission to:

* Read from **Amazon S3**
* Write to **Amazon DynamoDB**

These permissions are defined in the **execution role policy**.

---

# 9.3 IAM Role Structure

An IAM role for Lambda contains three main components.

### 1 Trust Policy

Defines **which service can assume the role**.

Example trust policy:

```json
{
 "Version": "2012-10-17",
 "Statement": [
  {
   "Effect": "Allow",
   "Principal": {
    "Service": "lambda.amazonaws.com"
   },
   "Action": "sts:AssumeRole"
  }
 ]
}
```

This policy allows the **Lambda service** to assume the role.

---

### 2 Permission Policy

Defines **what actions the Lambda function can perform**.

Example permission policy:

```json
{
 "Version": "2012-10-17",
 "Statement": [
  {
   "Effect": "Allow",
   "Action": [
    "s3:GetObject"
   ],
   "Resource": "arn:aws:s3:::my-bucket/*"
  }
 ]
}
```

This policy allows Lambda to read objects from an S3 bucket.

---

### 3 Role Attachment

The role must be attached to the Lambda function.

Example:

```
Lambda Function
      ↓
Attached IAM Role
      ↓
Access AWS Services
```

---

# 9.4 Default Lambda Permissions

When creating a Lambda function from the AWS console, AWS automatically creates a role with basic permissions.

Typical default permission:

```
AWSLambdaBasicExecutionRole
```

This allows Lambda to write logs to **Amazon CloudWatch**.

---

# 9.5 Example Lambda Execution Role Policy

Example policy allowing Lambda to access S3 and CloudWatch.

```json
{
 "Version": "2012-10-17",
 "Statement": [
  {
   "Effect": "Allow",
   "Action": [
    "logs:CreateLogGroup",
    "logs:CreateLogStream",
    "logs:PutLogEvents"
   ],
   "Resource": "*"
  },
  {
   "Effect": "Allow",
   "Action": [
    "s3:GetObject"
   ],
   "Resource": "arn:aws:s3:::example-bucket/*"
  }
 ]
}
```

This policy allows:

* Logging to CloudWatch
* Reading files from S3

---

# 9.6 How to Create Lambda Execution Role (Steps)

### Step 1

Open **IAM Console**

### Step 2

Select **Roles**

### Step 3

Click **Create Role**

### Step 4

Choose trusted entity

```
AWS Service
```

### Step 5

Select service

```
Lambda
```

### Step 6

Attach policies such as:

* AWSLambdaBasicExecutionRole
* S3 access policy

### Step 7

Create the role.

---

# 9.7 Lambda Role Example Architecture

Example architecture using execution roles.

```
User
  ↓
API Gateway
  ↓
Lambda Function
  ↓
IAM Execution Role
  ↓
Access S3 / DynamoDB / CloudWatch
```

Services involved:

* **Amazon API Gateway**
* **Amazon S3**
* **Amazon DynamoDB**
* **Amazon CloudWatch**

---

# 9.8 Lambda IAM Best Practices

### Follow Least Privilege Principle

Grant only the permissions required.

Example:

Instead of:

```
s3:*
```

Use:

```
s3:GetObject
```

---

### Use Separate Roles for Different Functions

Each Lambda function should have its **own IAM role**.

---

### Avoid Using Administrator Access

Never attach **AdministratorAccess** policy to Lambda.

---

### Monitor IAM Activity

Use **AWS CloudTrail** to track IAM actions.

---
---
## 10. Lambda Event Sources
---
In **AWS Lambda**, an **event source** is a service or application that generates an event which triggers the Lambda function to run.

Lambda follows an **event-driven architecture**, meaning functions execute automatically when a specific event occurs in **Amazon Web Services**.

Example events:

* File upload
* HTTP request
* Database update
* Message in queue
* Scheduled task

---

# 10.1 What is an Event Source

An **event source** is any AWS service or external application that sends an event to Lambda.

Example flow:

```text
Event Source
     ↓
Trigger
     ↓
Lambda Function
     ↓
Process Event
```

Example:

```text
File uploaded to S3
        ↓
Lambda Trigger
        ↓
Lambda processes the file
```

---

# 10.2 Types of Lambda Event Sources

Lambda supports multiple event sources. These can be grouped into three main categories:

| Category          | Description                         |
| ----------------- | ----------------------------------- |
| Push-based events | Service directly invokes Lambda     |
| Poll-based events | Lambda polls the service for events |
| Scheduled events  | Lambda runs on a defined schedule   |

---

# 10.3 Push-Based Event Sources

In push-based events, AWS services **directly invoke Lambda when an event occurs**.

Example services:

| AWS Service            | Example Event        |
| ---------------------- | -------------------- |
| **Amazon S3**          | File upload          |
| **Amazon SNS**         | Notification message |
| **Amazon EventBridge** | Event trigger        |
| **Amazon API Gateway** | HTTP request         |

Example architecture:

```text
User Upload File
      ↓
Amazon S3
      ↓
S3 Event Trigger
      ↓
Lambda Function
```

---

# 10.4 Poll-Based Event Sources

In poll-based architecture, Lambda continuously polls a service for new messages or data.

Example services:

| Service                     | Purpose                  |
| --------------------------- | ------------------------ |
| **Amazon SQS**              | Process messages         |
| **Amazon Kinesis**          | Process data streams     |
| **Amazon DynamoDB** Streams | Capture database changes |

Example architecture:

```text
Application sends message
       ↓
Amazon SQS
       ↓
Lambda polls queue
       ↓
Lambda processes message
```

---

# 10.5 Scheduled Event Sources

Lambda functions can also run on a **schedule** using **Amazon EventBridge**.

This works similar to **cron jobs**.

Example use cases:

* Daily reports
* Backup tasks
* Data synchronization
* Scheduled maintenance

Example schedule:

```text
Cron Schedule
      ↓
EventBridge Rule
      ↓
Lambda Function
```

Example cron expression:

```text
cron(0 12 * * ? *)
```

This runs the Lambda function **every day at 12 PM**.

---

# 10.6 Common Lambda Event Sources

Below are the most commonly used event sources.

### 1. Amazon S3 Trigger

**Amazon S3** can trigger Lambda when objects are uploaded, deleted, or modified.

Example:

```text
Upload Image
      ↓
Amazon S3 Bucket
      ↓
S3 Event Trigger
      ↓
Lambda Resizes Image
```

Use cases:

* Image processing
* File validation
* Video processing

---

### 2. API Gateway Trigger

**Amazon API Gateway** can trigger Lambda for HTTP requests.

Example architecture:

```text
User Request
      ↓
API Gateway
      ↓
Lambda Function
      ↓
Database
```

Use cases:

* REST APIs
* Web applications
* Backend services

---

### 3. DynamoDB Stream Trigger

**Amazon DynamoDB** streams capture database changes.

Example:

```text
Database Update
      ↓
DynamoDB Stream
      ↓
Lambda Function
```

Use cases:

* Real-time analytics
* Data replication
* Notifications

---

### 4. SQS Trigger

**Amazon SQS** triggers Lambda when new messages arrive in a queue.

Example architecture:

```text
Application
      ↓
SQS Queue
      ↓
Lambda Function
      ↓
Process Messages
```

Use cases:

* Background job processing
* Microservices communication

---

### 5. SNS Trigger

**Amazon SNS** sends notifications to Lambda functions.

Example:

```text
SNS Topic
      ↓
Lambda Function
      ↓
Send Email / Process Data
```

Use cases:

* Alerts
* Notifications
* Event processing

---

# 10.7 Real Production Serverless Architecture

Example production architecture using multiple event sources.

```text
User Upload Image
        ↓
Amazon S3
        ↓
Lambda Function
        ↓
Store Metadata
        ↓
DynamoDB
```

Another architecture:

```text
User Request
      ↓
CloudFront
      ↓
API Gateway
      ↓
Lambda Function
      ↓
DynamoDB / S3
```

Services used:

* **Amazon CloudFront**
* **Amazon API Gateway**
* **AWS Lambda**

---

# 10.8 Benefits of Lambda Event Sources

* Automatic execution
* Event-driven architecture
* Highly scalable
* Reduced operational overhead
* Real-time processing

---
---
## 11. Lambda Execution Lifecycle
---

The **execution lifecycle** of **AWS Lambda** describes what happens internally when a Lambda function is invoked.
Each time a function runs, AWS creates or reuses an **execution environment** where the code executes.

Understanding the lifecycle is important for optimizing performance, reducing latency, and designing efficient serverless applications on **Amazon Web Services**.

---

# 11.1 Overview of Lambda Execution Lifecycle

The Lambda execution lifecycle consists of three main phases:

| Phase                | Description                                  |
| -------------------- | -------------------------------------------- |
| Initialization Phase | Environment setup and runtime initialization |
| Invocation Phase     | Lambda function execution                    |
| Shutdown Phase       | Environment cleanup                          |

Execution flow:

```text
Event Occurs
     ↓
Initialization Phase
     ↓
Invocation Phase
     ↓
Response Returned
     ↓
Shutdown / Environment Reuse
```

---

# 11.2 Initialization Phase (Init Phase)

The **Initialization Phase** occurs when Lambda creates a **new execution environment** for the function.

This usually happens during a **cold start**.

During this phase, Lambda performs the following steps:

1. Container creation
2. Runtime initialization
3. Load function code
4. Load dependencies
5. Run initialization code

Example process:

```text
Event Trigger
      ↓
Create Execution Environment
      ↓
Load Runtime (Python / Node.js)
      ↓
Load Function Code
      ↓
Initialize Function
```

Example event sources that trigger initialization:

* **Amazon API Gateway**
* **Amazon S3**
* **Amazon EventBridge**

Initialization happens **only once per environment**, unless a new environment is required.

---

# 11.3 Invocation Phase

The **Invocation Phase** occurs when the Lambda function processes the event.

During this phase:

1. Lambda receives event data
2. Handler function is executed
3. Business logic runs
4. Result is returned

Example workflow:

```text
Event Received
      ↓
Lambda Handler Executed
      ↓
Application Logic Runs
      ↓
Return Response
```

Example Python Lambda code:

```python
def lambda_handler(event, context):
    print("Lambda function executed")
    return "Success"
```

This phase represents the **actual function execution**.

---

# 11.4 Shutdown Phase

After the function execution finishes, Lambda may either:

* **Reuse the execution environment**
* **Terminate the environment**

If the environment is reused, future requests will run faster.

Example process:

```text
Function Execution Completed
        ↓
Environment Idle
        ↓
Reuse or Terminate
```

---

# 11.5 Cold Start

A **cold start** occurs when Lambda creates a **new execution environment**.

Cold starts happen when:

* The function is invoked for the first time
* The function has been idle for a long time
* Lambda needs to scale to handle more requests

Cold start steps:

```text
Create Container
      ↓
Initialize Runtime
      ↓
Load Code
      ↓
Execute Function
```

Cold starts may introduce **extra latency**.

---

# 11.6 Warm Start

A **warm start** occurs when Lambda reuses an existing execution environment.

Because the environment already exists:

* No container creation
* No runtime initialization
* Faster execution

Example:

```text
Previous Execution Environment
         ↓
Receive Event
         ↓
Execute Function Immediately
```

Warm starts significantly reduce response time.

---

# 11.7 Lambda Execution Environment Reuse

Lambda may reuse the execution environment for multiple invocations.

This allows:

* Faster performance
* Cached resources
* Reuse of initialized variables

Example:

```text
Invocation 1 → Environment Created
Invocation 2 → Environment Reused
Invocation 3 → Environment Reused
```

Developers can use this behavior for caching resources like database connections.

---

# 11.8 Lambda Scaling Lifecycle

Lambda automatically creates multiple execution environments to handle concurrent requests.

Example:

```text
Request 1 → Environment 1
Request 2 → Environment 2
Request 3 → Environment 3
```

Each environment runs independently.

---

# 11.9 Example Execution Lifecycle Architecture

Example architecture using Lambda lifecycle:

```text
User Request
      ↓
CloudFront
      ↓
API Gateway
      ↓
Lambda Execution Lifecycle
      ↓
Database / Storage
```

AWS services involved:

* **Amazon CloudFront**
* **Amazon API Gateway**
* **AWS Lambda**
* **Amazon DynamoDB**

---

# 11.10 Best Practices for Lambda Lifecycle

### Minimize Cold Starts

Reduce deployment package size.

### Use Provisioned Concurrency

Pre-warm Lambda environments.

### Initialize Resources Outside Handler

Reuse resources between executions.

Example:

```python
import boto3

s3 = boto3.client("s3")

def lambda_handler(event, context):
    print("Using reused S3 client")
```

---
## 12. Lambda Scaling and Concurrency
---

**AWS Lambda** automatically scales to handle incoming requests. When multiple events trigger a function at the same time, Lambda runs **multiple instances of the function concurrently**. This ability to handle parallel executions is known as **concurrency**.

Scaling and concurrency are important concepts for designing **high-performance serverless applications** on **Amazon Web Services**.

---

# 12.1 What is Concurrency in Lambda

Concurrency refers to the **number of Lambda function instances running simultaneously**.

Example:

If 5 users send requests at the same time:

```text
Request 1 → Lambda Instance 1
Request 2 → Lambda Instance 2
Request 3 → Lambda Instance 3
Request 4 → Lambda Instance 4
Request 5 → Lambda Instance 5
```

Total concurrency = **5**

Each request runs in a **separate execution environment**.

---

# 12.2 Automatic Scaling

Lambda automatically scales based on the number of incoming events.

Example scaling scenario:

| Requests        | Lambda Instances |
| --------------- | ---------------- |
| 1 request       | 1 instance       |
| 100 requests    | 100 instances    |
| 10,000 requests | 10,000 instances |

Scaling happens automatically without manual configuration.

Example event sources that trigger scaling:

* **Amazon API Gateway**
* **Amazon S3**
* **Amazon SQS**

---

# 12.3 Default Lambda Concurrency Limit

AWS sets a **default concurrency limit per account per region**.

Typical default limit:

```text
1000 concurrent executions
```

This means only **1000 Lambda functions can run simultaneously** in a region.

If the limit is exceeded, Lambda will **throttle additional requests**.

The limit can be increased by requesting a quota increase.

---

# 12.4 Reserved Concurrency

Reserved concurrency guarantees a specific number of concurrent executions for a Lambda function.

Example:

```text
Reserved Concurrency = 100
```

This means:

* Lambda reserves **100 execution environments**
* No other functions can use these resources

Benefits:

* Prevents resource starvation
* Ensures critical functions always run

Example architecture:

```text
Account Concurrency = 1000

Function A → Reserved 300
Function B → Reserved 200
Remaining → 500
```

---

# 12.5 Provisioned Concurrency

Provisioned concurrency keeps Lambda execution environments **pre-initialized and ready**.

This reduces **cold start latency**.

Normal Lambda execution:

```text
Request
   ↓
Create Environment
   ↓
Initialize Runtime
   ↓
Run Function
```

Provisioned concurrency execution:

```text
Pre-initialized Environment
        ↓
Request
        ↓
Immediate Execution
```

Provisioned concurrency is useful for:

* APIs
* Low latency applications
* Real-time systems

Common integration:

* **Amazon API Gateway**
* **Amazon CloudFront**

---

# 12.6 Lambda Throttling

Throttling occurs when the concurrency limit is exceeded.

Example:

```text
Concurrent Limit = 1000

Requests = 1200
```

Result:

```text
1000 → Executed
200 → Throttled
```

Throttled requests may:

* Fail immediately
* Retry automatically depending on the event source

Example services with retry behavior:

* **Amazon SQS**
* **Amazon EventBridge**

---

# 12.7 Concurrency with Event Sources

Different event sources scale Lambda differently.

### API Gateway

Each request creates a new Lambda execution.

```text
User Requests
      ↓
API Gateway
      ↓
Multiple Lambda Instances
```

---

### SQS Event Source

Lambda polls the queue and processes messages in batches.

```text
Messages in Queue
        ↓
Lambda Polling
        ↓
Process Messages
```

---

### DynamoDB Streams

Lambda processes database changes in real time.

```text
Database Update
      ↓
DynamoDB Stream
      ↓
Lambda Function
```

---

# 12.8 Real Production Scaling Architecture

Example serverless production architecture:

```text
Users
   ↓
CloudFront
   ↓
API Gateway
   ↓
Lambda (Auto Scaling)
   ↓
DynamoDB / S3
```

AWS services involved:

* **Amazon CloudFront**
* **Amazon API Gateway**
* **AWS Lambda**
* **Amazon DynamoDB**

This architecture allows applications to handle **millions of requests automatically**.

---

# 12.9 Monitoring Lambda Concurrency

Lambda concurrency can be monitored using **Amazon CloudWatch**.

Important metrics:

| Metric               | Description                  |
| -------------------- | ---------------------------- |
| ConcurrentExecutions | Active Lambda executions     |
| Throttles            | Number of throttled requests |
| Invocations          | Total function calls         |
| Duration             | Execution time               |

---

# Best Practices

### Set Reserved Concurrency for Critical Functions

Prevents important functions from being throttled.

### Monitor Concurrency Metrics

Use CloudWatch alarms.

### Use Provisioned Concurrency for APIs

Reduces cold start latency.

### Optimize Function Execution Time

Shorter execution time improves concurrency handling.

---
---
## 13. Lambda Configuration Options
---

When creating a function in **AWS Lambda**, several configuration options control how the function runs. These settings affect **performance, cost, security, and resource allocation**.

Proper configuration is important for building efficient serverless applications on **Amazon Web Services**.

---

# 13.1 Memory Configuration

Lambda allows you to configure the **amount of memory allocated to the function**.

Memory directly impacts:

* CPU power
* Network throughput
* Execution performance

Memory range:

```text
128 MB – 10,240 MB (10 GB)
```

Example configuration:

| Memory   | CPU Power |
| -------- | --------- |
| 128 MB   | Low       |
| 512 MB   | Medium    |
| 1024 MB  | High      |
| 3008 MB+ | Very high |

Example:

```text
Lambda Memory = 512 MB
```

The function receives more CPU power as memory increases.

---

# 13.2 CPU Allocation

In Lambda, CPU power is **automatically allocated based on memory size**.

Higher memory = higher CPU performance.

Example:

| Memory  | CPU           |
| ------- | ------------- |
| 128 MB  | Minimal CPU   |
| 1024 MB | Moderate CPU  |
| 3008 MB | Full CPU core |

Example architecture:

```text
Lambda Function
       ↓
Memory Allocation
       ↓
CPU Automatically Assigned
```

This allows performance tuning by adjusting memory settings.

---

# 13.3 Timeout Configuration

Timeout defines **how long a Lambda function is allowed to run before AWS stops it**.

Default timeout:

```text
3 seconds
```

Maximum timeout:

```text
15 minutes (900 seconds)
```

Example:

```text
Timeout = 60 seconds
```

If the function runs longer than the timeout, AWS terminates the execution.

Example use cases:

| Application     | Recommended Timeout |
| --------------- | ------------------- |
| API request     | 3–10 seconds        |
| Data processing | 30–120 seconds      |
| Batch jobs      | Several minutes     |

---

# 13.4 Environment Variables

Environment variables allow you to store configuration data used by Lambda functions.

Common uses:

* Database connection strings
* API keys
* Configuration values

Example environment variables:

```text
DATABASE_URL = mydatabase
API_KEY = abc123
```

Example Python code:

```python
import os

def lambda_handler(event, context):
    db = os.environ['DATABASE_URL']
    print(db)
```

Environment variables help separate **configuration from code**.

---

# 13.5 Ephemeral Storage

Lambda provides temporary storage inside the execution environment.

This storage is available in the `/tmp` directory.

Default size:

```text
512 MB
```

Maximum configurable storage:

```text
10 GB
```

Example:

```text
/tmp/file.txt
```

Use cases:

* Temporary file processing
* Image processing
* Data transformation

Example workflow:

```text
Upload File
     ↓
Lambda Function
     ↓
Temporary Processing (/tmp)
     ↓
Upload Result to S3
```

Common storage integration:

* **Amazon S3**

---

# 13.6 Runtime Configuration

Runtime configuration specifies the **programming language environment** used to run Lambda functions.

Supported runtimes include:

| Runtime | Language   |
| ------- | ---------- |
| Python  | Python 3.x |
| Node.js | JavaScript |
| Java    | Java       |
| Go      | Go         |
| .NET    | C#         |
| Ruby    | Ruby       |

Example runtime setting:

```text
Runtime = Python 3.12
```

Lambda loads the appropriate runtime when the function executes.

---

# 13.7 Architecture Configuration

Lambda supports two processor architectures.

| Architecture | Description             |
| ------------ | ----------------------- |
| x86_64       | Standard architecture   |
| arm64        | AWS Graviton processors |

Example configuration:

```text
Architecture = arm64
```

Benefits of ARM architecture:

* Lower cost
* Better performance for some workloads

---

# 13.8 File System Configuration

Lambda can connect to a shared file system using **Amazon Elastic File System**.

Example architecture:

```text
Lambda Function
       ↓
Amazon EFS
       ↓
Shared Storage
```

Benefits:

* Persistent storage
* Shared data between Lambda functions
* Large data processing

---

# 13.9 Logging Configuration

Lambda automatically sends logs to **Amazon CloudWatch**.

Logs include:

* Function execution logs
* Error messages
* Debug information

Example log:

```text
START RequestId: 12345
Processing request
END RequestId: 12345
```

These logs help monitor and debug Lambda functions.

---

# 13.10 Configuration Example Architecture

Example configuration architecture:

```text
User Request
      ↓
API Gateway
      ↓
Lambda Function
   ├── Memory
   ├── Timeout
   ├── Environment Variables
   ├── Runtime
   └── Ephemeral Storage
      ↓
Database / Storage
```

Services involved:

* **Amazon API Gateway**
* **AWS Lambda**
* **Amazon DynamoDB**
* **Amazon S3**

---

# Best Practices

### Optimize Memory Settings

Higher memory improves CPU performance.

### Set Proper Timeout

Avoid very high timeout values.

### Use Environment Variables

Store configuration outside code.

### Monitor Logs

Use **CloudWatch logs** for debugging.

---
---
## 14. Lambda Networking
---

Networking in **AWS Lambda** determines how a Lambda function communicates with other resources such as databases, APIs, and storage services inside **Amazon Web Services**.

Lambda functions can run:

* **Outside a VPC (default)**
* **Inside a VPC**

Choosing the correct networking configuration is important for **security, connectivity, and performance**.

---

# 14.1 Default Lambda Networking (Without VPC)

By default, Lambda functions run **outside of a VPC** in an AWS-managed network.

In this mode:

* Lambda automatically has **internet access**
* No VPC configuration is required
* AWS manages the networking infrastructure

Example architecture:

```text
User Request
     ↓
API Gateway
     ↓
Lambda Function
     ↓
Access AWS Services
```

Example services accessed:

* **Amazon S3**
* **Amazon DynamoDB**
* **Amazon API Gateway**

This is the **simplest configuration**.

---

# 14.2 Lambda Inside a VPC

Lambda functions can also run inside a **Virtual Private Cloud**.

A VPC is a logically isolated network provided by **Amazon Virtual Private Cloud**.

Running Lambda inside a VPC is useful when accessing:

* Private databases
* Internal services
* Private APIs

Example architecture:

```text
User Request
     ↓
API Gateway
     ↓
Lambda Function
     ↓
VPC
     ↓
Private Database
```

Example database:

* **Amazon RDS**

---

# 14.3 Lambda VPC Components

When Lambda runs inside a VPC, it must be connected to:

* Subnets
* Security Groups

Example architecture:

```text
Lambda Function
      ↓
VPC
   ├── Subnet
   └── Security Group
```

These components control **network routing and security**.

---

# 14.4 Subnets

A subnet is a **segment of a VPC network**.

Lambda functions must be assigned to one or more subnets.

Types of subnets:

| Subnet Type    | Description               |
| -------------- | ------------------------- |
| Public Subnet  | Has internet access       |
| Private Subnet | No direct internet access |

Example VPC architecture:

```text
VPC
 ├── Public Subnet
 │      └── NAT Gateway
 └── Private Subnet
        └── Lambda Function
```

Lambda usually runs inside **private subnets** for security.

---

# 14.5 Security Groups

A **security group** acts as a **virtual firewall** for Lambda functions.

Security groups control:

* Incoming traffic
* Outgoing traffic

Example rule:

```text
Allow outbound traffic to database port 3306
```

Example architecture:

```text
Lambda Function
      ↓
Security Group
      ↓
Database
```

Example database:

* **Amazon RDS**

---

# 14.6 Internet Access from Lambda in VPC

If Lambda runs inside a **private subnet**, it cannot access the internet directly.

To allow internet access, a **NAT Gateway** must be used.

Example architecture:

```text
Lambda Function
      ↓
Private Subnet
      ↓
NAT Gateway
      ↓
Internet Gateway
      ↓
Internet
```

Important services:

* **NAT Gateway**
* **Internet Gateway**

---

# 14.7 Lambda Access to AWS Services in VPC

Lambda functions inside a VPC can still access AWS services using **VPC endpoints**.

Example:

```text
Lambda Function
      ↓
VPC Endpoint
      ↓
Amazon S3
```

Example services:

* **Amazon S3**
* **Amazon DynamoDB**

Using VPC endpoints avoids internet traffic and improves security.

---

# 14.8 Real Production Lambda Networking Architecture

Example production serverless architecture:

```text
Users
   ↓
CloudFront
   ↓
API Gateway
   ↓
Lambda Function
   ↓
VPC
 ├── Private Subnet
 │     └── RDS Database
 └── Public Subnet
       └── NAT Gateway
```

Services used:

* **Amazon CloudFront**
* **Amazon API Gateway**
* **AWS Lambda**
* **Amazon RDS**

This architecture ensures:

* Secure networking
* Private database access
* Internet connectivity through NAT Gateway

---

# 14.9 Best Practices for Lambda Networking

### Use Private Subnets

Improves security for backend services.

### Use NAT Gateway Carefully

NAT Gateway has additional cost.

### Use VPC Endpoints

Direct access to AWS services without internet.

### Configure Security Groups Properly

Allow only required traffic.

---
---
## 15. Lambda Monitoring and Logging
---

Monitoring and logging are essential for tracking the performance, errors, and behavior of **AWS Lambda** functions. AWS provides built-in monitoring tools that help developers observe function execution, debug issues, and optimize performance on **Amazon Web Services**.

The primary services used for Lambda monitoring are:

* **Amazon CloudWatch**
* **AWS X-Ray**
* **AWS CloudTrail**

---

# 15.1 Amazon CloudWatch Logs

When a Lambda function runs, it automatically sends logs to **Amazon CloudWatch**.

Logs include:

* Execution start time
* Execution end time
* Application output
* Error messages

Example log output:

```text
START RequestId: 8a9b2c
Processing request
END RequestId: 8a9b2c
REPORT Duration: 120 ms
```

Logs help developers:

* Debug errors
* Track execution behavior
* Monitor function performance

---

# 15.2 CloudWatch Log Groups and Log Streams

Lambda logs are organized into:

| Component  | Description                              |
| ---------- | ---------------------------------------- |
| Log Group  | Collection of logs for a Lambda function |
| Log Stream | Logs for a specific execution instance   |

Example structure:

```text
CloudWatch Logs
   ↓
Log Group
   ↓
Log Stream
   ↓
Lambda Execution Logs
```

Log group naming format:

```text
/aws/lambda/function-name
```

---

# 15.3 Lambda Metrics in CloudWatch

Lambda automatically publishes metrics to **CloudWatch**.

Important metrics include:

| Metric               | Description                                |
| -------------------- | ------------------------------------------ |
| Invocations          | Number of function calls                   |
| Duration             | Time taken to execute function             |
| Errors               | Number of failed executions                |
| Throttles            | Requests blocked due to concurrency limits |
| ConcurrentExecutions | Number of active executions                |

Example architecture:

```text
Lambda Function
      ↓
CloudWatch Metrics
      ↓
Monitoring Dashboard
```

These metrics help monitor **application performance and reliability**.

---

# 15.4 CloudWatch Alarms

CloudWatch alarms notify administrators when certain conditions occur.

Example conditions:

* High error rate
* High execution time
* Too many throttled requests

Example architecture:

```text
Lambda Metrics
      ↓
CloudWatch Alarm
      ↓
Notification
```

Notifications are usually sent using:

* **Amazon SNS**

Example alert workflow:

```text
Lambda Error
      ↓
CloudWatch Alarm
      ↓
SNS Notification
      ↓
Email / SMS Alert
```

---

# 15.5 AWS X-Ray for Lambda Tracing

**AWS X-Ray** helps trace requests through serverless applications.

It provides detailed information about:

* Execution time
* Service dependencies
* Latency
* Bottlenecks

Example architecture:

```text
User Request
      ↓
API Gateway
      ↓
Lambda Function
      ↓
Database
```

With X-Ray enabled, developers can see the entire request path.

Services commonly traced:

* **Amazon API Gateway**
* **AWS Lambda**
* **Amazon DynamoDB**

---

# 15.6 Lambda Error Logging

Lambda logs errors automatically in CloudWatch.

Example error log:

```text
ERROR: Unable to connect to database
```

Common errors:

* Timeout errors
* Permission errors
* Memory limit exceeded
* Runtime errors

Logs help identify and resolve issues quickly.

---

# 15.7 Lambda Monitoring Dashboard

CloudWatch dashboards allow visual monitoring of Lambda functions.

Example dashboard metrics:

* Invocation rate
* Error rate
* Average execution duration
* Throttling events

Example architecture:

```text
Lambda Function
      ↓
CloudWatch Metrics
      ↓
CloudWatch Dashboard
```

This provides a **centralized monitoring interface**.

---

# 15.8 AWS CloudTrail for Lambda

**AWS CloudTrail** records all API calls related to Lambda.

Examples of tracked events:

* Create function
* Update function
* Delete function
* Change permissions

Example workflow:

```text
Admin modifies Lambda
       ↓
CloudTrail records API call
       ↓
Audit logs stored
```

This helps with **security auditing and compliance**.

---

# 15.9 Real Production Monitoring Architecture

Example monitoring architecture for serverless applications:

```text
Users
   ↓
API Gateway
   ↓
Lambda Function
   ↓
Application Logic
```

Monitoring services:

```text
Lambda Execution
      ↓
CloudWatch Logs
      ↓
CloudWatch Metrics
      ↓
CloudWatch Alarms
      ↓
SNS Notifications
```

Additional tracing:

```text
Request Flow
      ↓
AWS X-Ray
```

---

# 15.10 Best Practices for Lambda Monitoring

### Enable CloudWatch Logging

Always monitor execution logs.

### Use CloudWatch Alarms

Automatically detect failures.

### Enable X-Ray Tracing

Identify performance bottlenecks.

### Monitor Error and Throttle Metrics

Ensure application reliability.

### Use Structured Logging

Improve debugging and log analysis.

---
---
## 16. Lambda Error Handling
---

Error handling is an important part of building reliable applications using **AWS Lambda**. When a Lambda function fails, AWS provides several mechanisms to retry, capture, or process failed events so that no data is lost.

Proper error handling ensures **high reliability and fault tolerance** for serverless applications running on **Amazon Web Services**.

---

# 16.1 Types of Lambda Errors

Lambda errors generally fall into two categories.

| Error Type      | Description                         |
| --------------- | ----------------------------------- |
| Function Errors | Errors inside the application code  |
| Service Errors  | Errors caused by AWS infrastructure |

Example function error:

```text
Division by zero
Database connection failed
Invalid input data
```

Example service error:

```text
Lambda timeout
Memory exceeded
Throttling
```

---

# 16.2 Synchronous Invocation Error Handling

In synchronous invocation, the caller waits for the Lambda response.

Example services:

* **Amazon API Gateway**
* **AWS SDK**

Example workflow:

```text
User Request
      ↓
API Gateway
      ↓
Lambda Function
      ↓
Return Response
```

If the function fails:

* The error is returned directly to the client.

Example response:

```text
500 Internal Server Error
```

---

# 16.3 Asynchronous Invocation Error Handling

In asynchronous invocation, the event is placed in a queue and Lambda processes it later.

Example services:

* **Amazon S3**
* **Amazon EventBridge**
* **Amazon SNS**

Example workflow:

```text
S3 Event
     ↓
Lambda Function
     ↓
Process Event
```

If the function fails, Lambda automatically retries the event.

Default retry behavior:

```text
Retry 1
Retry 2
Retry 3
```

After retries fail, the event can be sent to a **dead letter queue**.

---

# 16.4 Poll-Based Invocation Error Handling

Some services use polling to invoke Lambda.

Examples:

* **Amazon SQS**
* **Amazon DynamoDB** Streams
* **Amazon Kinesis**

Example workflow:

```text
Message in Queue
      ↓
Lambda polls queue
      ↓
Lambda processes message
```

If processing fails:

* Message remains in the queue
* Lambda retries processing

---

# 16.5 Dead Letter Queue (DLQ)

A **Dead Letter Queue (DLQ)** stores events that could not be processed successfully by Lambda.

Supported services for DLQ:

* **Amazon SQS**
* **Amazon SNS**

Example architecture:

```text
Event
  ↓
Lambda Function
  ↓
Failure
  ↓
Dead Letter Queue
```

Example workflow:

```text
S3 Upload
      ↓
Lambda Function
      ↓
Error
      ↓
DLQ (SQS)
```

This allows developers to analyze failed events later.

---

# 16.6 Lambda Destinations

Lambda Destinations allow sending execution results to other services.

Two types:

| Destination         | Purpose                 |
| ------------------- | ----------------------- |
| Success destination | When execution succeeds |
| Failure destination | When execution fails    |

Example services used:

* **Amazon SQS**
* **Amazon EventBridge**
* **Amazon SNS**

Example architecture:

```text
Lambda Execution
     ↓
Success → EventBridge
Failure → SQS Queue
```

---

# 16.7 Logging Errors

All Lambda errors are automatically logged in:

* **Amazon CloudWatch**

Example log:

```text
ERROR: Database connection failed
```

Logs help identify issues such as:

* Runtime errors
* Permission errors
* Timeout failures

---

# 16.8 Common Lambda Errors

### Timeout Error

Occurs when execution exceeds the configured timeout.

Example:

```text
Task timed out after 30 seconds
```

---

### Memory Limit Exceeded

Occurs when function memory usage exceeds configured memory.

Example:

```text
Memory limit exceeded
```

---

### Permission Error

Occurs when Lambda lacks permission to access a resource.

Example:

```text
AccessDenied: S3 bucket access denied
```

---

# 16.9 Real Production Error Handling Architecture

Example serverless architecture with error handling.

```text
Users
   ↓
API Gateway
   ↓
Lambda Function
```

Failure handling:

```text
Lambda Error
     ↓
CloudWatch Logs
     ↓
CloudWatch Alarm
     ↓
SNS Notification
```

Failed events:

```text
Lambda Failure
      ↓
Dead Letter Queue
      ↓
SQS Queue
```

Services involved:

* **Amazon CloudWatch**
* **Amazon SNS**
* **Amazon SQS**

---

# 16.10 Best Practices for Lambda Error Handling

### Use Dead Letter Queues

Store failed events for later processing.

### Enable CloudWatch Logging

Monitor errors and debugging information.

### Configure Retry Policies

Prevent infinite retry loops.

### Use CloudWatch Alarms

Get notified when failures occur.

### Validate Input Data

Prevent application errors.

---
---
## 17. Lambda Layers
---

**Lambda Layers** are a feature of **AWS Lambda** that allow developers to package and share common code, libraries, and dependencies across multiple Lambda functions. This helps keep functions smaller and easier to maintain while running on **Amazon Web Services**.

Instead of including the same libraries in every function deployment package, you can store them in a **layer** and attach the layer to multiple Lambda functions.

---

# 17.1 What is a Lambda Layer

A **Lambda Layer** is a reusable package that contains:

* Libraries
* Custom runtimes
* Dependencies
* Shared code

Example architecture:

```text
Lambda Function
   ├── Application Code
   └── Lambda Layer
         ├── Libraries
         └── Dependencies
```

This allows multiple functions to share the same dependencies.

---

# 17.2 Why Use Lambda Layers

Without layers, each Lambda function must include its own dependencies.

Example problem:

```text
Function A → Includes library
Function B → Includes same library
Function C → Includes same library
```

This increases:

* Deployment package size
* Duplicate code
* Maintenance complexity

With Lambda layers:

```text
Lambda Layer
      ↓
Shared Libraries
      ↓
Used by Multiple Lambda Functions
```

Benefits:

* Code reuse
* Smaller deployment packages
* Faster deployments
* Easier dependency management

---

# 17.3 Lambda Layer Architecture

Example architecture using layers:

```text
Application
     ↓
API Gateway
     ↓
Lambda Function
     ↓
Lambda Layer
     ↓
Shared Libraries
```

Services involved:

* **Amazon API Gateway**
* **AWS Lambda**

---

# 17.4 Lambda Layer Structure

A Lambda layer must follow a specific folder structure depending on the runtime.

Example structure for Python:

```text
layer/
 └── python/
      └── lib/
           └── python3.x/
                └── site-packages/
                     └── libraries
```

Example:

```text
layer/
 └── python/
      └── requests/
      └── numpy/
```

These libraries become available to the Lambda function.

---

# 17.5 Creating a Lambda Layer

Steps to create a layer:

### Step 1

Create a directory for the layer.

```bash
mkdir python
```

### Step 2

Install dependencies.

Example:

```bash
pip install requests -t python/
```

### Step 3

Create a zip file.

```bash
zip -r layer.zip python
```

### Step 4

Upload the layer in **AWS Lambda** console.

---

# 17.6 Attaching Layer to Lambda Function

After creating the layer, it must be attached to a Lambda function.

Example process:

```text
Lambda Function
      ↓
Add Layer
      ↓
Layer Attached
      ↓
Libraries Available in Function
```

Multiple layers can be attached to a single Lambda function.

Maximum allowed:

```text
5 layers per function
```

---

# 17.7 Layer Versioning

Lambda layers support **versioning**.

Each time a layer is updated, a **new version** is created.

Example:

| Layer Name     | Version   |
| -------------- | --------- |
| shared-library | version 1 |
| shared-library | version 2 |
| shared-library | version 3 |

This allows safe updates without breaking existing functions.

---

# 17.8 Lambda Layers Use Cases

Common use cases include:

### Shared Libraries

Common libraries used across functions.

Example:

* Python libraries
* Node.js packages

---

### Security Libraries

Shared authentication or encryption modules.

---

### Machine Learning Libraries

Large ML libraries such as:

* TensorFlow
* PyTorch

---

### Custom Runtime

Developers can create custom runtimes and distribute them using layers.

---

# 17.9 Example Serverless Architecture with Layers

Example architecture:

```text
Users
   ↓
CloudFront
   ↓
API Gateway
   ↓
Lambda Functions
   ↓
Lambda Layer (Shared Libraries)
   ↓
Database / Storage
```

AWS services involved:

* **Amazon CloudFront**
* **Amazon API Gateway**
* **AWS Lambda**
* **Amazon DynamoDB**

---

# 17.10 Best Practices for Lambda Layers

### Use Layers for Large Libraries

Avoid large deployment packages.

### Version Layers Properly

Never modify existing versions.

### Limit Number of Layers

Use only necessary layers to avoid complexity.

### Share Layers Across Functions

Reduce duplication.

---
---
## 18. Lambda Versions and Aliases
---
In **AWS Lambda**, **versions and aliases** help manage different releases of a Lambda function. They allow developers to deploy updates safely and control traffic between different function versions when building applications on **Amazon Web Services**.

This feature is very important for **production deployments, DevOps pipelines, and zero-downtime updates**.

---

# 18.1 What are Lambda Versions

A **version** is a **snapshot of a Lambda function at a specific point in time**.

When you publish a version, AWS creates an **immutable copy** of the function that cannot be modified.

Example:

| Version   | Description             |
| --------- | ----------------------- |
| $LATEST   | Current working version |
| Version 1 | First published version |
| Version 2 | Updated version         |
| Version 3 | Latest stable release   |

Example workflow:

```text
Lambda Function
      ↓
Publish Version
      ↓
Version 1 Created
```

---

# 18.2 $LATEST Version

Every Lambda function has a default version called:

```text
$LATEST
```

This version represents the **most recent code and configuration changes**.

Example workflow:

```text
Developer updates code
       ↓
Changes applied to $LATEST
       ↓
Publish version
       ↓
Immutable version created
```

Important points:

* `$LATEST` is editable
* Published versions are **read-only**

---

# 18.3 Publishing a Lambda Version

To create a new version:

1. Update Lambda function code
2. Test the function
3. Click **Publish version**

Example architecture:

```text
Lambda Function ($LATEST)
        ↓
Publish Version
        ↓
Version 1 Created
```

Each version contains:

* Code
* Runtime configuration
* Memory settings
* Environment variables

---

# 18.4 What are Lambda Aliases

An **alias** is a pointer to a specific Lambda version.

Aliases allow developers to create **environment names** for different versions.

Example aliases:

| Alias | Version   |
| ----- | --------- |
| dev   | Version 1 |
| test  | Version 2 |
| prod  | Version 3 |

Example architecture:

```text
Client Request
       ↓
Alias (prod)
       ↓
Lambda Version 3
```

This allows applications to call the alias instead of a specific version.

---

# 18.5 Why Use Lambda Aliases

Aliases provide several benefits:

* Environment management
* Safer deployments
* Traffic control
* Easier rollbacks

Example architecture:

```text
API Gateway
      ↓
Lambda Alias
      ↓
Lambda Version
```

Service example:

* **Amazon API Gateway**

---

# 18.6 Traffic Shifting with Aliases

Lambda aliases can split traffic between different versions.

Example configuration:

```text
Version 1 → 90% traffic
Version 2 → 10% traffic
```

Example architecture:

```text
User Requests
       ↓
Lambda Alias
       ↓
Traffic Split
   ├── Version 1 (90%)
   └── Version 2 (10%)
```

This technique is used for **gradual deployments**.

---

# 18.7 Canary Deployment

A **canary deployment** gradually shifts traffic from an old version to a new version.

Example:

```text
Initial traffic
Version 1 → 100%

Test phase
Version 1 → 90%
Version 2 → 10%

Final deployment
Version 2 → 100%
```

This allows testing new code with a small number of users.

---

# 18.8 Blue-Green Deployment

Blue-Green deployment is a safe release strategy.

Example:

| Environment | Version   |
| ----------- | --------- |
| Blue        | Version 1 |
| Green       | Version 2 |

Deployment workflow:

```text
Users
   ↓
Alias (Production)
   ↓
Version 1
```

After testing:

```text
Users
   ↓
Alias (Production)
   ↓
Version 2
```

Benefits:

* Zero downtime deployment
* Easy rollback

---

# 18.9 Example Production Architecture

Example serverless deployment architecture:

```text
Users
   ↓
CloudFront
   ↓
API Gateway
   ↓
Lambda Alias (prod)
   ↓
Lambda Version
```

AWS services used:

* **Amazon CloudFront**
* **Amazon API Gateway**
* **AWS Lambda**

---

# 18.10 Best Practices

### Always Use Versions in Production

Avoid invoking `$LATEST` directly.

### Use Aliases for Environments

Example: dev, test, prod.

### Implement Canary Deployments

Gradually test new versions.

### Maintain Rollback Strategy

Keep previous stable versions available.

---
---
## 19. Lambda Security
---

Security is a critical aspect when running applications using **AWS Lambda**. AWS provides multiple security mechanisms to control access, protect data, and secure communication between services on **Amazon Web Services**.

Lambda security mainly focuses on:

* Access control
* Data protection
* Network security
* Monitoring and auditing

---

# 19.1 Identity and Access Management (IAM)

Access to Lambda functions is controlled using **AWS Identity and Access Management**.

IAM allows administrators to define:

* Who can access Lambda
* What actions they can perform
* Which resources they can access

Example IAM actions:

| Action                | Description            |
| --------------------- | ---------------------- |
| lambda:CreateFunction | Create Lambda function |
| lambda:InvokeFunction | Run Lambda function    |
| lambda:DeleteFunction | Delete Lambda function |

Example architecture:

```text
User
   ↓
IAM Policy
   ↓
Lambda Function
```

IAM ensures **secure and controlled access**.

---

# 19.2 Lambda Execution Role

Each Lambda function runs with an **execution role** that grants permissions to access AWS resources.

Example resources:

* **Amazon S3**
* **Amazon DynamoDB**
* **Amazon CloudWatch**

Example architecture:

```text
Lambda Function
      ↓
IAM Execution Role
      ↓
Access AWS Services
```

Without proper permissions, Lambda cannot interact with other AWS services.

---

# 19.3 Resource-Based Policies

Lambda also supports **resource-based policies**.

These policies define **who can invoke the Lambda function**.

Example use case:

Allow **Amazon API Gateway** to invoke Lambda.

Example architecture:

```text
API Gateway
      ↓
Resource Policy
      ↓
Lambda Function
```

Resource-based policies allow **cross-account access** as well.

---

# 19.4 Encryption in Lambda

AWS Lambda supports encryption to protect sensitive data.

Two types of encryption are used:

| Type                  | Description                  |
| --------------------- | ---------------------------- |
| Encryption at Rest    | Protect stored data          |
| Encryption in Transit | Protect data during transfer |

AWS uses **AWS Key Management Service** to manage encryption keys.

Example architecture:

```text
Lambda Function
      ↓
KMS Encryption
      ↓
Secure Data Storage
```

This protects environment variables and sensitive data.

---

# 19.5 Secrets Management

Sensitive information such as passwords and API keys should not be stored directly in Lambda code.

Instead, developers should use:

* **AWS Secrets Manager**
* **AWS Systems Manager Parameter Store**

Example architecture:

```text
Lambda Function
      ↓
Secrets Manager
      ↓
Retrieve Credentials
```

This approach improves security and simplifies credential management.

---

# 19.6 Lambda Network Security

Lambda networking security can be enhanced using **Amazon Virtual Private Cloud**.

Lambda functions can run inside a VPC to access private resources.

Example architecture:

```text
Lambda Function
      ↓
VPC
      ↓
Private Database
```

Example database:

* **Amazon RDS**

Security groups and subnets control network access.

---

# 19.7 Logging and Auditing

Security monitoring is performed using:

* **Amazon CloudWatch**
* **AWS CloudTrail**

Example architecture:

```text
Lambda Function
      ↓
CloudWatch Logs
      ↓
Security Monitoring
```

CloudTrail records:

* API calls
* Configuration changes
* Access events

This helps track unauthorized access.

---

# 19.8 Code Security

Lambda code security should follow best practices.

Recommendations:

* Avoid storing credentials in code
* Validate input data
* Use dependency scanning
* Keep libraries updated

Example workflow:

```text
Code
   ↓
Security Scan
   ↓
Deploy Lambda
```

---

# 19.9 Security Architecture Example

Example secure serverless architecture:

```text
Users
   ↓
CloudFront
   ↓
API Gateway
   ↓
Lambda Function
   ↓
Database
```

Security services used:

* **Amazon CloudFront**
* **Amazon API Gateway**
* **AWS Lambda**
* **Amazon DynamoDB**

Additional security tools:

* **AWS WAF**
* **AWS Shield**

---

# 19.10 Best Practices for Lambda Security

### Follow Least Privilege Principle

Grant only necessary permissions.

### Encrypt Sensitive Data

Use **AWS KMS** encryption.

### Store Secrets Securely

Use **Secrets Manager** instead of environment variables.

### Monitor Logs

Enable **CloudWatch and CloudTrail** monitoring.

### Use VPC for Private Resources

Protect internal services like databases.

---
---
## 20. Lambda Pricing Model
---

The pricing for **AWS Lambda** is based on a **pay-as-you-go model**. Instead of paying for servers running continuously, you only pay when your function executes on **Amazon Web Services**.

Lambda pricing mainly depends on:

* Number of requests
* Execution duration
* Memory allocation

This makes Lambda cost-efficient for **event-driven and serverless applications**.

---

# 20.1 Lambda Pricing Components

Lambda pricing is calculated using three main components.

| Component | Description                           |
| --------- | ------------------------------------- |
| Requests  | Number of times a function is invoked |
| Duration  | Time taken for function execution     |
| Memory    | Memory allocated to the function      |

Example workflow:

```text
User Request
     ↓
Lambda Function
     ↓
Execution Time
     ↓
Billing Calculated
```

---

# 20.2 Request Pricing

Every time a Lambda function is triggered, it counts as **one request**.

Example triggers:

* **Amazon API Gateway**
* **Amazon S3**
* **Amazon EventBridge**

Pricing rule:

```text
$0.20 per 1 million requests
```

Example:

| Requests   | Cost  |
| ---------- | ----- |
| 1 million  | $0.20 |
| 5 million  | $1.00 |
| 10 million | $2.00 |

---

# 20.3 Duration Pricing

Duration pricing is based on how long the function runs.

Measured in:

```text
Milliseconds (ms)
```

Duration depends on:

* Function execution time
* Memory allocation

Example:

```text
Execution time = 500 ms
Memory = 512 MB
```

Billing is calculated using **GB-seconds**.

Example architecture:

```text
Lambda Function
      ↓
Execution Duration
      ↓
Compute Cost
```

---

# 20.4 Memory Pricing Impact

Lambda cost increases as memory allocation increases.

Example memory settings:

| Memory  | Usage            |
| ------- | ---------------- |
| 128 MB  | Small workloads  |
| 512 MB  | Medium workloads |
| 1024 MB | Heavy workloads  |

Higher memory provides:

* More CPU power
* Faster execution

Example:

```text
Memory = 128 MB → lower cost
Memory = 1024 MB → higher cost
```

However, higher memory may reduce execution time.

---

# 20.5 Free Tier

AWS provides a **free tier** for Lambda.

Free tier includes:

```text
1 million free requests per month
400,000 GB-seconds compute time
```

Example:

| Usage           | Cost                     |
| --------------- | ------------------------ |
| Under free tier | $0                       |
| Above free tier | Standard pricing applies |

This makes Lambda ideal for:

* small applications
* development environments
* testing projects

---

# 20.6 Example Cost Calculation

Example scenario:

Lambda configuration:

```text
Memory = 512 MB
Execution time = 1 second
Requests = 1 million
```

Calculation:

```text
Request cost = $0.20
Compute cost ≈ based on GB-seconds
```

Approximate total:

```text
Very low cost compared to running servers
```

---

# 20.7 Additional Costs

Lambda may incur additional costs when integrated with other services.

Example services:

* **Amazon API Gateway**
* **Amazon S3**
* **Amazon DynamoDB**
* **Amazon CloudWatch**

Example architecture:

```text
User
  ↓
API Gateway
  ↓
Lambda Function
  ↓
DynamoDB
```

Each service has its own pricing model.

---

# 20.8 Provisioned Concurrency Pricing

If **Provisioned Concurrency** is enabled, additional cost applies.

Provisioned concurrency keeps Lambda environments **pre-initialized**.

Example architecture:

```text
Provisioned Environment
        ↓
Immediate Execution
```

Benefits:

* Reduced cold start latency
* Better performance for APIs

However, it increases cost.

---

# 20.9 Cost Optimization Strategies

### Reduce Execution Time

Optimize code to finish faster.

### Choose Proper Memory

Balance between speed and cost.

### Use Event-Driven Architecture

Avoid unnecessary executions.

### Monitor Usage

Use **Amazon CloudWatch** metrics to track usage.

### Use Free Tier

Take advantage of free requests.

---

# 20.10 Real Serverless Cost Architecture

Example production architecture:

```text
Users
   ↓
CloudFront
   ↓
API Gateway
   ↓
Lambda Function
   ↓
Database
```

Services involved:

* **Amazon CloudFront**
* **Amazon API Gateway**
* **AWS Lambda**
* **Amazon DynamoDB**

This architecture is **cost-efficient because compute runs only when needed**.

---
---
## 21. Lambda Limits and Quotas
---

Like all AWS services, **AWS Lambda** has certain **limits and quotas** that define how functions can run and scale on **Amazon Web Services**.

These limits help maintain system stability, performance, and fair resource usage across AWS customers.

Some limits are **soft limits** (can be increased), while others are **hard limits** (cannot be changed).

---

# 21.1 Lambda Memory Limits

Lambda allows configuration of memory allocated to a function.

Memory range:

```text
128 MB → 10,240 MB (10 GB)
```

Memory affects:

* CPU power
* Network performance
* Execution speed

Example:

| Memory   | CPU Power              |
| -------- | ---------------------- |
| 128 MB   | Low                    |
| 512 MB   | Medium                 |
| 1024 MB  | High                   |
| 3008 MB+ | Maximum CPU allocation |

---

# 21.2 Lambda Execution Timeout Limit

Timeout defines how long a Lambda function can run before AWS terminates it.

Default timeout:

```text
3 seconds
```

Maximum timeout:

```text
15 minutes (900 seconds)
```

Example use cases:

| Workload        | Timeout         |
| --------------- | --------------- |
| API requests    | 3–10 seconds    |
| Data processing | 30–120 seconds  |
| Batch jobs      | Several minutes |

---

# 21.3 Deployment Package Size Limits

Lambda has limits for deployment package size.

ZIP package limits:

| Type            | Limit  |
| --------------- | ------ |
| Direct upload   | 50 MB  |
| Uploaded via S3 | 250 MB |

Example:

```text
lambda_function.zip → uploaded to S3
```

For larger applications, Lambda supports **container images** stored in **Amazon Elastic Container Registry**.

Container image limit:

```text
10 GB
```

---

# 21.4 Lambda Concurrency Limits

Concurrency defines how many Lambda functions can run simultaneously.

Default concurrency limit:

```text
1000 concurrent executions per region
```

Example:

```text
Requests = 1200
Allowed = 1000
Throttled = 200
```

This limit can be increased by requesting a quota increase.

---

# 21.5 Environment Variable Limits

Lambda allows storing configuration using environment variables.

Limit:

```text
Maximum size = 4 KB
```

Example environment variables:

```text
DATABASE_URL=mydatabase
API_KEY=abc123
```

These values are encrypted using **AWS Key Management Service**.

---

# 21.6 Lambda Layers Limits

Lambda layers also have size limits.

| Limit                       | Value       |
| --------------------------- | ----------- |
| Maximum layers per function | 5           |
| Maximum layer size          | 50 MB (zip) |
| Maximum uncompressed size   | 250 MB      |

Layers are commonly used to store shared libraries.

---

# 21.7 Temporary Storage Limit

Lambda provides temporary storage in:

```text
/tmp
```

Default storage:

```text
512 MB
```

Maximum configurable storage:

```text
10 GB
```

Use cases:

* File processing
* Image transformation
* Data analysis

---

# 21.8 File Descriptor and Process Limits

Lambda execution environments have system-level limits.

Example:

| Resource         | Limit |
| ---------------- | ----- |
| File descriptors | 1024  |
| Processes        | 1024  |

These limits help maintain system stability.

---

# 21.9 API Request Limits

When Lambda is invoked through **Amazon API Gateway**, payload size limits apply.

Example:

| Invocation Type      | Limit  |
| -------------------- | ------ |
| Synchronous payload  | 6 MB   |
| Asynchronous payload | 256 KB |

These limits ensure efficient request processing.

---

# 21.10 Real Production Architecture Example

Example serverless architecture with Lambda limits considered:

```text
Users
   ↓
CloudFront
   ↓
API Gateway
   ↓
Lambda Function
   ↓
Database / Storage
```

AWS services used:

* **Amazon CloudFront**
* **Amazon API Gateway**
* **AWS Lambda**
* **Amazon DynamoDB**

Proper architecture design helps avoid hitting service limits.

---

# 21.11 Monitoring Lambda Limits

Lambda limits and usage can be monitored using:

* **Amazon CloudWatch**
* AWS Service Quotas dashboard

Important metrics:

* Concurrent executions
* Throttled requests
* Function errors

---

# Best Practices

### Monitor Concurrency Usage

Avoid throttling.

### Optimize Package Size

Reduce deployment package size.

### Use Layers for Dependencies

Share libraries efficiently.

### Request Limit Increases

Increase concurrency when required.

---
---
## 22. Lambda Integration with AWS Services
---

One of the biggest strengths of **AWS Lambda** is its deep integration with many services in **Amazon Web Services**. These integrations allow developers to build **event-driven serverless architectures** where Lambda automatically reacts to events from other AWS services.

Lambda can integrate with storage, databases, messaging systems, APIs, and monitoring tools to build scalable cloud applications.

---

# 22.1 Lambda + Amazon S3

**Amazon S3** can trigger Lambda functions whenever objects are created, deleted, or modified in a bucket.

### Example Workflow

```text
User Upload File
      ↓
Amazon S3 Bucket
      ↓
S3 Event Trigger
      ↓
Lambda Function
      ↓
Process File
```

### Use Cases

* Image resizing
* Video processing
* File validation
* Data transformation

---

# 22.2 Lambda + API Gateway

**Amazon API Gateway** allows Lambda to act as a backend for REST or HTTP APIs.

### Architecture

```text
Client Application
        ↓
API Gateway
        ↓
Lambda Function
        ↓
Database / Storage
```

### Use Cases

* Serverless REST APIs
* Mobile application backends
* Microservices architecture

Example services used with Lambda APIs:

* **Amazon DynamoDB**
* **Amazon RDS**

---

# 22.3 Lambda + DynamoDB

**Amazon DynamoDB** integrates with Lambda using **DynamoDB Streams**.

Streams capture changes to database tables and trigger Lambda functions.

### Architecture

```text
Database Update
      ↓
DynamoDB Stream
      ↓
Lambda Function
      ↓
Process Data
```

### Use Cases

* Real-time analytics
* Data synchronization
* Event-driven processing

---

# 22.4 Lambda + Amazon SQS

**Amazon SQS** allows Lambda to process messages asynchronously.

Lambda automatically polls the queue and processes messages.

### Architecture

```text
Application
     ↓
SQS Queue
     ↓
Lambda Polling
     ↓
Process Messages
```

### Use Cases

* Background job processing
* Microservice communication
* Event-driven workloads

---

# 22.5 Lambda + Amazon SNS

**Amazon SNS** sends notifications that can trigger Lambda functions.

### Architecture

```text
Application Event
       ↓
SNS Topic
       ↓
Lambda Function
       ↓
Process Notification
```

### Use Cases

* Alert processing
* Notification handling
* Event broadcasting

---

# 22.6 Lambda + EventBridge

**Amazon EventBridge** allows applications to send and route events to Lambda.

### Architecture

```text
Event Source
      ↓
EventBridge Rule
      ↓
Lambda Function
      ↓
Process Event
```

### Use Cases

* Event-driven applications
* Scheduled tasks
* Microservices communication

Example scheduled event:

```text
Daily Job
   ↓
EventBridge
   ↓
Lambda Function
```

---

# 22.7 Lambda + Step Functions

**AWS Step Functions** helps coordinate multiple Lambda functions into workflows.

### Architecture

```text
Step Functions Workflow
        ↓
Lambda Function 1
        ↓
Lambda Function 2
        ↓
Lambda Function 3
```

### Use Cases

* Complex business workflows
* Data processing pipelines
* Microservice orchestration

---

# 22.8 Lambda + CloudWatch

Lambda integrates with **Amazon CloudWatch** for logging and monitoring.

### Architecture

```text
Lambda Function
      ↓
CloudWatch Logs
      ↓
Monitoring Dashboard
```

### Features

* Execution logs
* Performance metrics
* Alerts and alarms

---

# 22.9 Lambda + Kinesis

**Amazon Kinesis** streams data that Lambda can process in real time.

### Architecture

```text
Data Stream
      ↓
Kinesis Stream
      ↓
Lambda Function
      ↓
Data Processing
```

### Use Cases

* Real-time analytics
* IoT data processing
* Log processing

---

# 22.10 Real Serverless Architecture Example

Example production architecture integrating multiple AWS services.

```text
Users
   ↓
CloudFront
   ↓
API Gateway
   ↓
Lambda Function
   ↓
DynamoDB
   ↓
S3 Storage
```

Services used:

* **Amazon CloudFront**
* **Amazon API Gateway**
* **AWS Lambda**
* **Amazon DynamoDB**
* **Amazon S3**

This architecture is **fully serverless, scalable, and event-driven**.

---

# Best Practices for Lambda Integration

### Use Event-Driven Architecture

Trigger functions only when events occur.

### Avoid Tight Coupling

Use messaging services like SQS or EventBridge.

### Monitor Integration Points

Use CloudWatch for logs and metrics.

### Handle Failures Properly

Use DLQ and retry mechanisms.

---
---
## 23. AWS Lambda vs Other Compute Services
---

When building applications on **Amazon Web Services**, developers can choose from multiple compute services. Each service is designed for different workloads.
**AWS Lambda** is mainly used for **event-driven, serverless applications**, while other compute services provide different levels of control and flexibility.

Understanding the differences helps architects choose the **right compute service for each use case**.

---

# 23.1 Overview of AWS Compute Services

AWS provides several compute options:

| Service         | Type                  |
| --------------- | --------------------- |
| **AWS Lambda**  | Serverless compute    |
| **Amazon EC2**  | Virtual machines      |
| **Amazon ECS**  | Container management  |
| **Amazon EKS**  | Kubernetes clusters   |
| **AWS Fargate** | Serverless containers |

Each service differs in **server management, scaling, pricing, and use cases**.

---

# 23.2 AWS Lambda vs Amazon EC2

**Amazon EC2** provides virtual servers where users control the operating system and environment.

### Comparison

| Feature           | AWS Lambda        | Amazon EC2               |
| ----------------- | ----------------- | ------------------------ |
| Server management | No servers        | Full server management   |
| Scaling           | Automatic         | Manual or Auto Scaling   |
| Pricing           | Pay per execution | Pay per running instance |
| OS control        | No                | Full control             |
| Execution time    | Max 15 minutes    | Unlimited                |

### Architecture Comparison

**Lambda architecture**

```text
User Request
      ↓
API Gateway
      ↓
Lambda Function
      ↓
Database
```

**EC2 architecture**

```text
User Request
      ↓
Load Balancer
      ↓
EC2 Instances
      ↓
Application Server
```

### When to Use

Use Lambda for:

* Event-driven workloads
* Serverless APIs
* Automation tasks

Use EC2 for:

* Long-running applications
* Custom operating systems
* Full infrastructure control

---

# 23.3 AWS Lambda vs Amazon ECS

**Amazon ECS** is used to run Docker containers.

### Comparison

| Feature           | Lambda        | ECS                             |
| ----------------- | ------------- | ------------------------------- |
| Compute type      | Functions     | Containers                      |
| Server management | No servers    | Managed container orchestration |
| Scaling           | Automatic     | Auto Scaling                    |
| Deployment        | Function code | Docker container images         |

### Architecture Example

```text
Application
     ↓
ECS Cluster
     ↓
Containers
```

Lambda runs **short-lived functions**, while ECS runs **long-running containers**.

---

# 23.4 AWS Lambda vs Amazon EKS

**Amazon EKS** runs Kubernetes clusters on AWS.

### Comparison

| Feature        | Lambda           | EKS                         |
| -------------- | ---------------- | --------------------------- |
| Infrastructure | Fully serverless | Kubernetes cluster          |
| Management     | Minimal          | Requires cluster management |
| Scaling        | Automatic        | Kubernetes auto scaling     |
| Complexity     | Low              | High                        |

### When to Use

Use Lambda for:

* Simple serverless workloads
* Event-driven processing

Use EKS for:

* Large microservices platforms
* Kubernetes-based applications

---

# 23.5 AWS Lambda vs AWS Fargate

**AWS Fargate** runs containers without managing servers.

### Comparison

| Feature        | Lambda         | Fargate            |
| -------------- | -------------- | ------------------ |
| Workload type  | Functions      | Containers         |
| Execution time | Max 15 minutes | Long-running tasks |
| Deployment     | Code package   | Docker image       |
| Scaling        | Automatic      | Task-based scaling |

### Architecture Example

```text
Application
     ↓
Fargate Task
     ↓
Container
```

Lambda is better for **short events**, while Fargate is better for **container workloads**.

---

# 23.6 Serverless vs Container vs VM Model

| Model            | Service Example              |
| ---------------- | ---------------------------- |
| Serverless       | **AWS Lambda**               |
| Containers       | **Amazon ECS / AWS Fargate** |
| Kubernetes       | **Amazon EKS**               |
| Virtual Machines | **Amazon EC2**               |

Example compute hierarchy:

```text
Application
   ↓
Choose Compute Service
   ├── Lambda (serverless)
   ├── ECS / Fargate (containers)
   ├── EKS (Kubernetes)
   └── EC2 (virtual machines)
```

---

# 23.7 Real Production Architecture Example

Modern applications often combine multiple compute services.

Example architecture:

```text
Users
   ↓
CloudFront
   ↓
API Gateway
   ↓
Lambda (API logic)
   ↓
SQS Queue
   ↓
ECS / Fargate (background processing)
```

Services used:

* **Amazon CloudFront**
* **Amazon API Gateway**
* **AWS Lambda**
* **Amazon SQS**
* **Amazon ECS**

This hybrid architecture is common in **modern DevOps environments**.

---

# 23.8 When to Choose AWS Lambda

Use Lambda when:

* Application is event-driven
* Execution time is short
* No server management required
* Automatic scaling is needed

Example workloads:

* File processing
* APIs
* Data transformation
* Automation tasks

---
---
# AWS Lambda Interview Questions and Answers 
---

## 1. What is AWS Lambda?

**AWS Lambda** is a serverless compute service from **Amazon Web Services** that allows you to run code without managing servers. It automatically scales and executes code in response to events.

---

## 2. What is Serverless Computing?

Serverless computing is a cloud model where the cloud provider manages infrastructure and the developer focuses only on application code.

---

## 3. What languages are supported by Lambda?

Supported runtimes include:

* Python
* Node.js
* Java
* Go
* .NET
* Ruby

---

## 4. What is a Lambda function?

A Lambda function is a piece of code that runs in response to an event.

---

## 5. What is the maximum execution time of Lambda?

Maximum execution time is:

```
15 minutes (900 seconds)
```

---

## 6. What triggers a Lambda function?

Lambda functions can be triggered by services such as:

* **Amazon S3**
* **Amazon API Gateway**
* **Amazon SQS**
* **Amazon EventBridge**

---

## 7. What is the Lambda handler?

The handler is the **entry point of a Lambda function** where execution starts.

---

## 8. What is the event object in Lambda?

The event object contains input data passed to the Lambda function.

---

## 9. What is the context object?

The context object contains runtime information about the function execution.

---

## 10. What is a cold start in Lambda?

A cold start occurs when Lambda creates a **new execution environment** for a function.

---

## 11. What is a warm start?

A warm start occurs when Lambda **reuses an existing execution environment**.

---

## 12. What is Lambda concurrency?

Concurrency refers to the **number of Lambda executions running simultaneously**.

---

## 13. What is reserved concurrency?

Reserved concurrency guarantees a fixed number of execution environments for a function.

---

## 14. What is provisioned concurrency?

Provisioned concurrency keeps Lambda environments **pre-initialized** to reduce cold start latency.

---

## 15. What is the default Lambda concurrency limit?

Default limit:

```
1000 concurrent executions per region
```

---

## 16. What is the Lambda deployment package?

A deployment package contains:

* Function code
* Dependencies
* Libraries

---

## 17. What are Lambda layers?

Lambda layers allow sharing libraries and dependencies across multiple Lambda functions.

---

## 18. How many layers can be attached to a Lambda function?

Maximum:

```
5 layers
```

---

## 19. What is the Lambda execution role?

Lambda execution role is an **IAM role** that grants permission to access AWS services.

Example service:

* **AWS Identity and Access Management**

---

## 20. What is Lambda timeout?

Timeout defines the maximum time a function can run before AWS terminates it.

---

## 21. What is the Lambda memory limit?

Lambda memory range:

```
128 MB – 10 GB
```

---

## 22. How does Lambda scale?

Lambda automatically scales by creating multiple execution environments.

---

## 23. What is Lambda environment variable?

Environment variables store configuration values used by Lambda functions.

---

## 24. What is Lambda ephemeral storage?

Temporary storage available in:

```
/tmp directory
```

Default size:

```
512 MB
```

---

## 25. What is Lambda versioning?

Lambda versioning creates immutable snapshots of a function.

---

## 26. What is Lambda alias?

An alias is a pointer to a specific Lambda version.

---

## 27. What is traffic shifting in Lambda?

Traffic shifting allows routing traffic between multiple Lambda versions.

---

## 28. What is a Canary deployment?

A canary deployment gradually releases a new version to a small percentage of users.

---

## 29. What is Blue-Green deployment?

Blue-Green deployment switches traffic between two environments.

---

## 30. What is Lambda pricing model?

Lambda pricing depends on:

* Number of requests
* Execution duration
* Memory allocation

---

## 31. What is Lambda free tier?

AWS free tier provides:

```
1 million requests per month
400,000 GB-seconds compute time
```

---

## 32. What is Lambda DLQ?

A **Dead Letter Queue (DLQ)** stores failed events.

Supported services:

* **Amazon SQS**
* **Amazon SNS**

---

## 33. What is Lambda destination?

Lambda destination sends success or failure results to another AWS service.

---

## 34. How does Lambda integrate with API Gateway?

API Gateway sends HTTP requests to Lambda to build serverless APIs.

---

## 35. What is Lambda monitoring service?

Lambda monitoring is done using:

* **Amazon CloudWatch**

---

## 36. What is AWS X-Ray used for?

**AWS X-Ray** traces requests through Lambda applications.

---

## 37. What is Lambda VPC integration?

Lambda can run inside **Amazon Virtual Private Cloud** to access private resources.

---

## 38. Why use Lambda with S3?

Lambda processes files automatically when uploaded to S3.

---

## 39. What is Lambda + DynamoDB Streams?

DynamoDB streams trigger Lambda when database data changes.

---

## 40. What is Lambda + SQS integration?

Lambda processes messages from SQS queues.

---

## 41. What is Lambda + EventBridge?

EventBridge triggers Lambda based on scheduled or application events.

---

## 42. What is Lambda + Step Functions?

**AWS Step Functions** coordinate multiple Lambda functions into workflows.

---

## 43. What is Lambda container image deployment?

Lambda supports container images stored in:

* **Amazon Elastic Container Registry**

Maximum image size:

```
10 GB
```

---

## 44. What is Lambda throttling?

Throttling occurs when concurrency limits are exceeded.

---

## 45. What is Lambda logging?

Logs are automatically stored in:

* **Amazon CloudWatch**

---

## 46. What is Lambda event-driven architecture?

Lambda executes code in response to events generated by AWS services.

---

## 47. What is Lambda@Edge?

**Lambda@Edge** runs Lambda functions at CloudFront edge locations.

---

## 48. What are Lambda limits?

Examples:

* 15 min execution time
* 10 GB memory
* 1000 concurrency

---

## 49. What is Lambda best use case?

Lambda is best for:

* APIs
* Automation
* File processing
* Event-driven workloads

---

## 50. When should you not use Lambda?

Avoid Lambda when:

* Long-running processes
* Large monolithic applications
* Applications requiring full OS control

---

