---

# ☁️ Introduction to AWS

---

# 1. Introduction

## 1.1 What is Cloud Computing

**Cloud Computing** is the delivery of computing services over the internet. Instead of owning physical servers or data centers, organizations can use cloud providers to access resources like servers, storage, databases, networking, and software on demand.

Cloud computing allows businesses to scale infrastructure quickly, reduce hardware costs, and deploy applications globally.

### Why Cloud Computing Was Introduced

Before cloud computing, companies needed to **buy and maintain physical infrastructure**. This required large investments and long setup times.

Cloud computing solved these problems by allowing organizations to **rent infrastructure instead of owning it**.

This made IT infrastructure:

* More flexible
* Faster to deploy
* Cost efficient
* Globally accessible

### Key Characteristics of Cloud Computing

* **On-Demand Self Service** – Users can provision resources automatically without human interaction.
* **Broad Network Access** – Services are accessible over the internet from anywhere.
* **Resource Pooling** – Cloud providers share infrastructure among multiple customers.
* **Rapid Elasticity** – Resources can scale up or down automatically.
* **Pay-As-You-Go Pricing** – Pay only for the resources you use.

---

## 1.2 What is AWS

**Amazon Web Services (AWS)** is a cloud computing platform provided by **Amazon** that offers a wide range of infrastructure services such as computing power, storage, databases, networking, security, and machine learning.

AWS launched its first service **Amazon S3 in 2006**, and since then it has become the **largest cloud provider in the world**.

AWS is used by:

* Startups
* Enterprises
* Government organizations
* Universities
* Large technology companies

Examples of companies using AWS:

* Netflix
* Airbnb
* NASA
* Samsung
* Adobe

AWS provides **200+ cloud services** that help organizations build, deploy, and scale applications globally.

### Major Categories of AWS Services

| Category   | Description                            |
| ---------- | -------------------------------------- |
| Compute    | Virtual servers and container services |
| Storage    | Object and block storage services      |
| Database   | Managed databases                      |
| Networking | Networking and CDN services            |
| Security   | Identity and security management       |
| DevOps     | CI/CD and automation tools             |
| Monitoring | Logging and monitoring services        |

---

## 1.3 Benefits of Using AWS

### 1.3.1 Cost Effective

AWS follows a **pay-as-you-go pricing model**, which means you only pay for the resources you use.

Example:

If you run a server for **3 hours**, you only pay for those **3 hours**.

This eliminates the need for expensive hardware purchases.

---

### 1.3.2 Global Infrastructure

AWS has **data centers across the world**.

This allows applications to run closer to users, improving performance and reducing latency.

Example:

* Users in India → Mumbai Region
* Users in USA → Virginia Region

---

### 1.3.3 High Scalability

AWS allows applications to scale automatically.

Example:

If a website receives high traffic, AWS can automatically **add more servers** to handle the load.

This ensures applications remain stable during peak traffic.

---

### 1.3.4 High Availability

AWS infrastructure is designed to minimize downtime.

Applications can run across **multiple Availability Zones**, ensuring services remain available even if one data center fails.

---

### 1.3.5 Security

AWS provides enterprise-grade security with services like:

* IAM (Identity and Access Management)
* Encryption
* Network isolation
* Compliance certifications

Security in AWS follows the **Shared Responsibility Model**.

### Shared Responsibility Model

AWS and the customer both share security responsibilities.

| Responsibility            | AWS | Customer |
| ------------------------- | --- | -------- |
| Physical Data Centers     | ✔   |          |
| Hardware                  | ✔   |          |
| Networking Infrastructure | ✔   |          |
| Operating System          |     | ✔        |
| Applications              |     | ✔        |
| Data Security             |     | ✔        |

---

## 1.4 AWS Global Infrastructure

AWS cloud infrastructure is built using multiple components that work together to provide **high availability and low latency**.

These components include:

* Regions
* Availability Zones
* Edge Locations
* Local Zones
* Wavelength Zones

Each component helps AWS deliver services **reliably across the world**.

---

## 1.5 Why AWS is Popular in DevOps

AWS is widely used in **DevOps environments** because it provides automation-friendly services.

DevOps requires:

* Automation
* Continuous Integration
* Continuous Deployment
* Infrastructure as Code
* Monitoring and logging

AWS provides services that support all these practices.

### DevOps Capabilities in AWS

* Infrastructure as Code using **CloudFormation / Terraform**
* Continuous Integration using **CodeBuild**
* Continuous Delivery using **CodePipeline**
* Container orchestration using **ECS / EKS**
* Monitoring using **CloudWatch**
* Logging using **CloudTrail**

---

## 1.6 Traditional Infrastructure Problem

Before cloud computing companies had to build their own IT infrastructure.

This required:

1. Purchasing physical servers
2. Building data centers
3. Managing cooling and electricity
4. Handling hardware failures
5. Maintaining network infrastructure

### Major Challenges

* High capital investment
* Long setup times
* Hardware maintenance
* Difficult scaling
* Limited global availability

Cloud computing solved these problems by providing **on-demand infrastructure over the internet**.

---
## 2. Traditional Infrastructure vs Cloud Computing

Understanding the difference between **Traditional Infrastructure (On-Premise)** and **Cloud Computing** is important to understand **why cloud platforms like AWS became popular**.

In traditional environments, companies manage their own hardware and data centers.
In cloud computing, infrastructure is provided by **cloud service providers over the internet**.

---

## 2.1 Traditional Infrastructure (On-Premise)

**Traditional Infrastructure**, also called **On-Premise Infrastructure**, refers to IT infrastructure that is **owned, installed, and managed by the organization itself**.

The company builds and maintains its own **data center**.

### Components in Traditional Infrastructure

A typical company data center includes:

* Physical servers
* Storage systems
* Networking devices
* Cooling systems
* Power backup systems
* Security systems

### Steps to Build Traditional Infrastructure

1. Purchase physical servers
2. Setup data center environment
3. Install operating systems
4. Configure networking
5. Install applications
6. Maintain and monitor hardware

### Problems with Traditional Infrastructure

#### High Initial Cost

Companies must invest large amounts of money to purchase hardware.

Examples:

* Servers
* Storage devices
* Networking equipment

#### Slow Infrastructure Setup

Setting up infrastructure may take **weeks or even months**.

Example process:

```
Requirement → Purchase hardware → Delivery → Installation → Configuration
```

#### Hardware Maintenance

Companies must handle:

* Hardware failures
* Power supply issues
* Cooling systems
* Security management
* System updates

#### Scaling Difficulties

If application traffic increases:

* Company must purchase additional servers.

If traffic decreases:

* Servers remain unused → **wasted investment**.

---

## 2.2 Cloud Computing

**Cloud Computing** provides computing resources **over the internet** instead of requiring companies to own physical infrastructure.

Organizations can rent resources from **cloud providers** and scale them as needed.

### Major Cloud Providers

Some of the largest cloud providers include:

* Amazon Web Services (AWS)
* Microsoft Azure
* Google Cloud Platform (GCP)

### Cloud Services Provided

Cloud providers offer many services including:

* Virtual machines
* Storage systems
* Managed databases
* Networking services
* Security tools
* Monitoring systems

---

## 2.3 Advantages of Cloud Computing

### Pay-As-You-Go Pricing

You only pay for the resources you use.

Example:

If a server runs for **3 hours**, you only pay for **3 hours of usage**.

---

### Fast Infrastructure Deployment

Cloud infrastructure can be created in **minutes**.

Example:

Creating an **EC2 instance in AWS** takes only a few minutes.

---

### Scalability

Cloud infrastructure can scale automatically based on demand.

Types of scaling:

* **Vertical Scaling** → Increasing CPU or RAM
* **Horizontal Scaling** → Adding more servers

---

### High Availability

Cloud providers operate **multiple data centers worldwide**.

If one server fails, another can automatically handle the workload.

---

### Global Application Deployment

Applications can be deployed closer to users around the world.

Example:

* Users in India → Mumbai region
* Users in USA → US region

---

## 2.4 Traditional Infrastructure vs Cloud Comparison

| Feature                  | Traditional Infrastructure | Cloud Computing      |
| ------------------------ | -------------------------- | -------------------- |
| Infrastructure Ownership | Company owned              | Cloud provider owned |
| Setup Time               | Weeks / Months             | Minutes              |
| Initial Cost             | High capital investment    | Pay as you go        |
| Maintenance              | Managed by company         | Managed by provider  |
| Scalability              | Difficult                  | Easy                 |
| Global Availability      | Limited                    | Global               |
| Reliability              | Limited                    | High                 |

---

## 2.5 Example Scenario

### Traditional Infrastructure

A startup wants to launch a website.

Steps required:

1. Purchase servers
2. Setup data center
3. Install operating systems
4. Configure networking
5. Deploy application

Total time required: **Weeks or months**

---

### Cloud Infrastructure (AWS)

Startup launches the same website using cloud services:

* **EC2** → Compute server
* **S3** → Storage
* **RDS** → Database

Total setup time: **Minutes**

---

## 2.6 Why Companies Prefer Cloud

Organizations prefer cloud platforms because they provide:

* Faster infrastructure deployment
* Lower upfront investment
* Automatic scalability
* Global infrastructure
* High availability and reliability
* Managed services

---

## Virtualization vs Cloud Computing

**Virtualization** and **Cloud Computing** are closely related technologies, but they are **not the same**.
Virtualization is a **technology**, while cloud computing is a **service model built on top of virtualization and other technologies**.

Understanding the difference helps in learning **AWS, DevOps, and modern infrastructure architectures**.

---

# 1. What is Virtualization

## Definition

**Virtualization** is a technology that allows **multiple virtual machines (VMs) to run on a single physical server**.

Instead of one operating system running directly on hardware, a **hypervisor** creates multiple isolated virtual environments.

Each virtual machine behaves like an **independent computer with its own operating system, CPU, memory, and storage**.

---

## How Virtualization Works

A software layer called a **Hypervisor** sits between the hardware and virtual machines.

```
Physical Server
      │
      ▼
Hypervisor
      │
 ├── Virtual Machine 1 (Linux)
 ├── Virtual Machine 2 (Windows)
 └── Virtual Machine 3 (Ubuntu)
```

Each VM runs independently but shares the same physical hardware.

---

## Types of Hypervisors

### Type 1 Hypervisor (Bare Metal)

Runs directly on hardware.

Examples:

* VMware ESXi
* Microsoft Hyper-V
* Xen

---

### Type 2 Hypervisor

Runs on top of an operating system.

Examples:

* VirtualBox
* VMware Workstation

---

## Benefits of Virtualization

* Better hardware utilization
* Reduced hardware costs
* Ability to run multiple operating systems
* Easy testing environments
* Faster deployment of servers

---

## Example

Without virtualization:

```
1 Server → 1 Operating System → 1 Application
```

With virtualization:

```
1 Server
   │
   ├── VM1 → Linux Server
   ├── VM2 → Windows Server
   └── VM3 → Ubuntu Server
```

---

# 2. What is Cloud Computing

## Definition

**Cloud Computing** is the delivery of **computing services over the internet**.

Instead of running infrastructure locally, users access cloud resources such as:

* Virtual servers
* Storage
* Databases
* Networking
* Machine learning services

Cloud providers manage the infrastructure while users consume services on demand.

Examples of cloud providers:

* AWS
* Microsoft Azure
* Google Cloud Platform

---

## Cloud Architecture Example

```
User
 │
 ▼
Internet
 │
 ▼
Cloud Provider
 │
 ├── Compute (EC2)
 ├── Storage (S3)
 ├── Database (RDS)
 └── Networking (VPC)
```

Cloud platforms allow users to create infrastructure **within minutes instead of weeks**.

---

# 3. Relationship Between Virtualization and Cloud

Virtualization is the **foundation technology** used by many cloud providers.

Cloud computing uses virtualization to:

* Create virtual machines
* Isolate customers
* Efficiently use hardware
* Provide scalable infrastructure

Example:

AWS **EC2 instances** are virtual machines created using virtualization technology.

---

# 4. Virtualization vs Cloud Computing Comparison

| Feature        | Virtualization                           | Cloud Computing                                  |
| -------------- | ---------------------------------------- | ------------------------------------------------ |
| Definition     | Technology to create virtual machines    | Delivery of computing services over the internet |
| Infrastructure | Usually on local servers                 | Provided by cloud providers                      |
| Access         | Local network or internal infrastructure | Internet based                                   |
| Scalability    | Limited by local hardware                | Highly scalable                                  |
| Cost Model     | Hardware purchase required               | Pay-as-you-go                                    |
| Management     | Managed by organization                  | Managed by cloud provider                        |

---

# 5. Example Scenario

## Virtualization Example

A company has one physical server and installs a hypervisor.

```
Physical Server
 ├── VM1 → Web Server
 ├── VM2 → Database Server
 └── VM3 → Testing Environment
```

The company still owns and manages the hardware.

---

## Cloud Computing Example

A startup launches an application using cloud services:

```
AWS
 ├── EC2 → Application Server
 ├── S3 → File Storage
 └── RDS → Database
```

The cloud provider manages the infrastructure.

---



---

# 3 🌍 AWS Global Infrastructure

---
## 3.1 Introduction

**AWS Global Infrastructure** refers to the worldwide network of **data centers, networking systems, and edge locations** that Amazon Web Services uses to deliver cloud services across the globe.

AWS builds its infrastructure in multiple geographic locations to provide:

* **High availability**
* **Fault tolerance**
* **Low latency**
* **Global scalability**
* **Reliable cloud services**

This global infrastructure allows organizations to deploy applications **closer to users**, improving performance and reducing delays in data transfer.

The AWS Global Infrastructure is composed of several key components:

1. Regions
2. Availability Zones (AZs)
3. Edge Locations
4. Regional Edge Caches
5. Local Zones
6. Wavelength Zones

Each component plays a different role in delivering cloud services efficiently.

---

# 3.2 AWS Regions

![Image](https://res.cloudinary.com/hy4kyit2a/f_auto%2Cfl_lossy%2Cq_70/learn/modules/aws-cloud-technical-professionals/explore-the-aws-global-infrastructure-technical-professionals/images/d88d2fecf52142786da539be437e50df_d-11-f-53-af-b-76-f-482-d-8492-73-be-2-a-630-f-1-b.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1200/1%2AQOhqCn0g7lY3aTVBeT__cw.png)

![Image](https://intellipaat.com/mediaFiles/2016/05/AWS-Global-Infrastructure.jpg)

![Image](https://content-media-cdn.codefinity.com/courses/fd3863f4-2fa9-43d7-9b7a-27c305b40141/Section1/images/third_image.png)

## Definition

An **AWS Region** is a **physical geographic location** where AWS operates multiple data centers.

Each region is completely **independent and isolated from other regions** to improve security, fault tolerance, and reliability.

AWS regions allow organizations to deploy applications in **different parts of the world** depending on their user base and compliance requirements.

---

## Example AWS Regions

Some commonly used AWS regions include:

* **Asia Pacific (Mumbai)** – ap-south-1
* **Asia Pacific (Singapore)** – ap-southeast-1
* **US East (N. Virginia)** – us-east-1
* **US East (Ohio)** – us-east-2
* **US West (Oregon)** – us-west-2
* **Europe (Frankfurt)** – eu-central-1

---

## Characteristics of AWS Regions

* Each region contains **multiple Availability Zones**
* Regions are connected through **high-speed private fiber networks**
* Regions operate **independently for fault isolation**
* Data is **not automatically replicated across regions**

Organizations choose regions based on:

* **Latency requirements**
* **Data compliance laws**
* **Disaster recovery strategy**
* **User location**

---

## Why AWS Regions Are Important

### Low Latency

Deploying applications closer to users reduces network delay.

Example:

Users in India should ideally use the **Mumbai region**.

---

### Data Residency and Compliance

Some countries require that **data must remain within their geographic boundaries**.

AWS regions help organizations comply with these regulations.

---

### Disaster Recovery

Applications can replicate data across regions to protect against:

* Natural disasters
* Infrastructure failures
* Regional outages

---

### Global Application Deployment

Companies can deploy applications in multiple regions to serve global users efficiently.

Example:

```
India Users → Mumbai Region
Europe Users → Frankfurt Region
USA Users → Virginia Region
```

---

# 3.3 Availability Zones (AZ)

![Image](https://www.techtarget.com/rms/onlineimages/aws_availability_zones_vs_regions-f_mobile.png)

![Image](https://d1tcczg8b21j1t.cloudfront.net/strapi-assets/ec2_simple_high_availability_architecture_238f1c256f.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2ACsx-1GwZ1zm0nFAYks1vZQ.png)

![Image](https://kodekloud.com/kk-media/image/upload/v1752860152/notes-assets/images/AWS-Certified-SysOps-Administrator-Associate-Multi-AZ-Architectures-for-Various-AWS-Services-Overview/multi-az-architecture-aws-vpc.jpg)


## Definition

An **Availability Zone (AZ)** is one or more **physically separate data centers within an AWS Region**.

Each Availability Zone is designed to operate **independently** but remains connected to other zones through **high-speed, low-latency networking**.

---

## Example

For the **Mumbai Region (ap-south-1)**:

* ap-south-1a
* ap-south-1b
* ap-south-1c

Each zone represents a **separate physical infrastructure**.

---

## Characteristics of Availability Zones

Availability Zones are designed with:

* Independent power supply
* Independent cooling systems
* Independent networking
* Physical separation from other zones
* High-speed fiber connections between zones

This design ensures that **failure in one AZ does not affect others**.

---

## High Availability Using Availability Zones

Applications can run across multiple Availability Zones to improve reliability.

Example architecture:

```
User
 │
 ▼
Load Balancer
 │
 ├── EC2 Instance (AZ-1)
 │
 └── EC2 Instance (AZ-2)
```

If **AZ-1 fails**, traffic automatically moves to **AZ-2**.

This architecture provides **high availability and fault tolerance**.

---

# 3.4 Edge Locations

![Image](https://awsfundamentals.com/_next/image?q=75\&url=%2Fassets%2Fblog%2Faws-edge-locations%2Fvisual-diagram-of-amazon-cloudfront-edge-locations-points-of-presence-and-its-connection-to-regional-edge-caches-and-the-origin-servers..webp\&w=3840)

![Image](https://d1.awsstatic.com/onedam/marketing-channels/website/aws/en_US/global-infrastructure/approved/images/cloudfront-pop-static-map.b64acf5738108c84936643c3dda57ae2e52a27e1.jpg)

![Image](https://d2908q01vomqb2.cloudfront.net/5b384ce32d8cdef02bc3a139d4cac0a22bb029e8/2020/02/05/image-2-1260x615.png)

![Image](https://d2908q01vomqb2.cloudfront.net/5b384ce32d8cdef02bc3a139d4cac0a22bb029e8/2019/07/03/image-3-1024x586.png)


## Definition

**Edge Locations** are AWS data centers used by **Content Delivery Networks (CDN)** such as **Amazon CloudFront**.

They store cached copies of content closer to users to reduce latency.

---

## How Edge Locations Work

Without edge locations:

```
User → Request → AWS Region
```

The request must travel long distances.

With edge locations:

```
User
 │
 ▼
Nearest Edge Location
 │
 ▼
Origin Server (AWS Region)
```

The content is delivered faster because it is cached closer to the user.

---

## Benefits of Edge Locations

* Faster content delivery
* Reduced network latency
* Lower load on origin servers
* Improved user experience

---

# 3.5 Regional Edge Caches

![Image](https://docs.aws.amazon.com/images/AmazonCloudFront/latest/DeveloperGuide/images/regional-edge-caches.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2ALLBDoPlg-iJGXuIOdEm-5w.png)

![Image](https://ervinszilagyi.dev/certified-aws-solutions-architect-professional/10-caching/images/CloudFrontArchitecture1.png)


**Regional Edge Caches** are larger caching locations placed between **Edge Locations and AWS Regions**.

They store content for longer periods and reduce requests to the origin server.

---

## Request Flow Example

```
User
 │
 ▼
Edge Location
 │
 ▼
Regional Edge Cache
 │
 ▼
Origin Server (EC2 / S3)
```

This architecture improves performance and reduces network traffic.

---

# 3.6 AWS Local Zones

![Image](https://docs.aws.amazon.com/images/local-zones/latest/ug/images/region-with-lzs.png)

![Image](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2023/06/27/Architecture-image.jpg)

![Image](https://docs.aws.amazon.com/images/local-zones/latest/ug/images/local-zones-direct-connect-internet-gateway.png)

![Image](https://media.licdn.com/dms/image/v2/D5612AQFsxUKiL_CX8A/article-cover_image-shrink_720_1280/article-cover_image-shrink_720_1280/0/1726579591402?e=2147483647\&t=jeMq7mR9M7Tkxp6U7OAKM3hXnwCHs4G6HF1GzfcdUyg\&v=beta)


**AWS Local Zones** extend AWS services closer to large metropolitan areas.

They allow applications to run with **very low latency** for local users.

---

## Example

```
AWS Region → Mumbai
Local Zone → Pune
```

Applications hosted in the **Pune Local Zone** will have lower latency for users in that city.

---

## Use Cases of Local Zones

* Online gaming
* Real-time video processing
* Media rendering
* Machine learning inference
* Financial trading systems

---

# 3.7 AWS Wavelength Zones

![Image](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2020/08/05/Screen-Shot-2020-08-05-at-10.27.53-AM.png)

![Image](https://d2908q01vomqb2.cloudfront.net/77de68daecd823babbb58edb1c8e14d7106e83bb/2022/11/10/Confluent-Wavelength-Data-in-Motion-1.png)


**AWS Wavelength Zones** integrate AWS infrastructure directly into **telecommunication providers’ 5G networks**.

This allows applications to run extremely close to mobile users.

---

## Architecture Example

```
Mobile Device
     │
     ▼
5G Network
     │
     ▼
AWS Wavelength Zone
     │
     ▼
AWS Region
```

Latency in wavelength zones can be **less than 10 milliseconds**, making them ideal for **ultra-low latency applications**.

---

## Use Cases

* Augmented Reality (AR)
* Virtual Reality (VR)
* Autonomous vehicles
* Smart cities
* Real-time gaming

---

# 3.8 AWS Global Infrastructure Scale

AWS operates one of the **largest cloud infrastructures in the world**.

### Current Infrastructure (2025–2026)

| Component                      | Approximate Count |
| ------------------------------ | ----------------- |
| AWS Regions                    | 39                |
| Availability Zones             | 120+              |
| Edge Locations                 | 700+              |
| Local Zones                    | 40+               |
| Countries / Territories Served | 245+              |

AWS continues expanding its infrastructure by launching **new regions and availability zones every year**.

---

# 4. Cloud Service Models (IaaS, PaaS, SaaS)

![Image](https://images.openai.com/static-rsc-3/gq-KMH4IBlq5X2V8vayuOFKQHpfdAN-5XVfxi0rK_9IQ3LEOE-k6x5SR3fXNkneUUTTHNR6ovc2fFbyqmStBMXXdL_BtDnN0lrSVfpP3_OA?purpose=fullsize\&v=1)

![Image](https://images.openai.com/static-rsc-3/UH4Eqr82pkQXV1twgD3YaCtWmYKI2gLXBN4Jc_PiWhsg7XRbJGub6TjdWm4IbdvGPHGyHVMZ-K0oTO3v5wbOSG8-3VnuSq7OGvkCOJIW5e4?purpose=fullsize\&v=1)

![Image](https://images.openai.com/static-rsc-3/ZA5tm91aNEAjjXPGhGyZF0dzCv55fg-7XtV5hPRJVi1qH2poNUESkbysoTJ6WdLyrOLkXWdk0MtIDr5rhXpoxaHnkn-BSeJZ-5AivGAxabs?purpose=fullsize\&v=1)

Cloud computing services are commonly delivered through **three main service models**:

1. **Infrastructure as a Service (IaaS)**
2. **Platform as a Service (PaaS)**
3. **Software as a Service (SaaS)**

These models define **how cloud services are provided and how responsibilities are shared between the cloud provider and the user**.

As we move from **IaaS → PaaS → SaaS**, the level of **management responsibility for the user decreases**, while the cloud provider manages more of the infrastructure.

---

# 4.1 Understanding the Cloud Service Model Concept

In traditional infrastructure, organizations must manage **every layer of the technology stack**.

These layers include:

* Networking
* Storage
* Servers
* Virtualization
* Operating System
* Middleware
* Runtime
* Applications
* Data

Cloud service models divide the responsibility for managing these layers between the **cloud provider** and the **customer**.

---

## Responsibility Model

| Layer            | On-Premise | IaaS     | PaaS     | SaaS     |
| ---------------- | ---------- | -------- | -------- | -------- |
| Applications     | You        | You      | You      | Provider |
| Data             | You        | You      | You      | Provider |
| Runtime          | You        | You      | Provider | Provider |
| Middleware       | You        | You      | Provider | Provider |
| Operating System | You        | You      | Provider | Provider |
| Virtualization   | You        | Provider | Provider | Provider |
| Servers          | You        | Provider | Provider | Provider |
| Storage          | You        | Provider | Provider | Provider |
| Networking       | You        | Provider | Provider | Provider |

This model shows **how much infrastructure the cloud provider manages** in each service model.

---

# 4.2 Infrastructure as a Service (IaaS)

## Definition

**Infrastructure as a Service (IaaS)** provides **virtualized computing infrastructure over the internet**.

In this model, the cloud provider manages the **physical infrastructure**, while the user is responsible for managing the **operating system, applications, and configurations**.

This service model gives users the **maximum level of control and flexibility**.

---

## What the Cloud Provider Manages

The provider manages:

* Physical data centers
* Servers
* Storage systems
* Networking infrastructure
* Virtualization layer

---

## What the User Manages

The user manages:

* Operating system
* Runtime environment
* Middleware
* Applications
* Data
* Security configurations

---

## Example AWS Services

Examples of IaaS services include:

* **Amazon EC2** – Virtual servers
* **Amazon EBS** – Block storage
* **Amazon VPC** – Virtual networking

---

## Example Use Cases

IaaS is commonly used for:

* Hosting websites
* Running enterprise applications
* Development and testing environments
* DevOps infrastructure
* Backup and disaster recovery

---

## Example Architecture

```
User Application
       │
Operating System
       │
Runtime / Middleware
       │
AWS Infrastructure
(Servers, Storage, Networking)
```

---

# 4.3 Platform as a Service (PaaS)

## Definition

**Platform as a Service (PaaS)** provides a **complete development and deployment environment in the cloud**.

Developers can build and deploy applications **without managing the underlying infrastructure**.

The cloud provider manages the **servers, operating systems, and runtime environments**, allowing developers to focus only on writing application code.

---

## What the Cloud Provider Manages

The provider manages:

* Infrastructure
* Operating systems
* Runtime environment
* Middleware
* Auto scaling
* Load balancing

---

## What the User Manages

The user manages:

* Application code
* Application configuration
* Data

---

## Example AWS Services

Examples of PaaS services include:

* **AWS Elastic Beanstalk**
* **AWS Lambda**
* **Amazon RDS**

---

## Example Use Cases

PaaS is commonly used for:

* Web application development
* API development
* Microservices architectures
* Rapid application deployment
* Serverless applications

---

## Example Workflow

```
Developer
   │
Upload Application Code
   │
Platform Automatically Handles:
   - Infrastructure
   - Scaling
   - OS Management
   - Runtime Environment
```

---

# 4.4 Software as a Service (SaaS)

## Definition

**Software as a Service (SaaS)** delivers **fully functional software applications over the internet**.

Users simply access the application through a **web browser**, without installing or managing infrastructure or software.

The cloud provider manages **everything**, including infrastructure, platform, and application updates.

---

## What the Cloud Provider Manages

The provider manages:

* Infrastructure
* Platform
* Application software
* Security updates
* Maintenance
* Scaling

---

## What the User Manages

The user is responsible only for:

* Using the application
* Managing data
* Configuring user settings

---

## Examples of SaaS Applications

Common SaaS applications include:

* Google Workspace
* Microsoft 365
* Salesforce
* Dropbox
* Slack

---

## Example Use Cases

SaaS applications are commonly used for:

* Email services
* Customer relationship management (CRM)
* Project management
* Online collaboration tools
* Document sharing platforms

---

# 4.5 Comparison of Cloud Service Models

| Feature                   | IaaS     | PaaS     | SaaS      |
| ------------------------- | -------- | -------- | --------- |
| Infrastructure Management | Provider | Provider | Provider  |
| Operating System          | User     | Provider | Provider  |
| Application Management    | User     | User     | Provider  |
| Control Level             | High     | Medium   | Low       |
| Ease of Use               | Moderate | Easy     | Very Easy |

---

# 4.6 Summary

Cloud service models define **how much infrastructure management responsibility is handled by the cloud provider versus the user**.

* **IaaS** provides infrastructure with maximum control.
* **PaaS** provides a platform for developers to build and deploy applications.
* **SaaS** provides fully managed software accessible through the internet.

Organizations choose the appropriate model based on **control requirements, development needs, and operational complexity**.

---
# 5. Cloud Deployment Models

Cloud **Deployment Models** define **how cloud infrastructure is deployed, who owns it, and who can access it**.

Different organizations choose different deployment models depending on their:

* Security requirements
* Budget
* Scalability needs
* Compliance regulations
* Infrastructure control

There are **three main cloud deployment models**:

1. **Public Cloud**
2. **Private Cloud**
3. **Hybrid Cloud**

Each model provides different levels of **control, flexibility, security, and cost efficiency**.

---

# 5.1 Public Cloud

## Definition

A **Public Cloud** is a cloud environment where infrastructure and services are **owned and operated by a third-party cloud provider** and delivered over the internet.

Multiple organizations share the same cloud infrastructure, but **each customer's data and applications remain isolated and secure**.

Users access cloud services through the **internet using web consoles, APIs, or command line tools**.

---

## Characteristics of Public Cloud

* Infrastructure owned by cloud provider
* Accessible over the internet
* Multi-tenant environment (shared infrastructure)
* Highly scalable
* Pay-as-you-go pricing model

---

## Examples of Public Cloud Providers

Major public cloud providers include:

* Amazon Web Services (AWS)
* Microsoft Azure
* Google Cloud Platform (GCP)

---

## Advantages of Public Cloud

### Cost Efficient

Organizations do not need to purchase hardware or build data centers.

---

### High Scalability

Infrastructure can scale automatically based on workload demands.

---

### Global Infrastructure

Public cloud providers operate **data centers worldwide**, enabling global application deployment.

---

### Managed Infrastructure

The cloud provider manages:

* Hardware
* Networking
* Power
* Cooling
* Physical security

---

## Disadvantages of Public Cloud

* Less control over infrastructure
* Possible compliance limitations
* Shared infrastructure environment

---

## Common Use Cases

Public cloud is widely used for:

* Web applications
* Mobile applications
* DevOps pipelines
* SaaS platforms
* Data analytics
* Startups and modern applications

---

## Example Architecture

```text
User
 │
 ▼
Internet
 │
 ▼
Public Cloud Provider
 │
 ├── Virtual Servers
 ├── Storage
 ├── Databases
 └── Networking
```

---

# 5.2 Private Cloud

## Definition

A **Private Cloud** is a cloud infrastructure dedicated to **a single organization**.

It can be deployed in:

* The organization's **own data center**
* A **hosted private environment** managed by a service provider

Unlike public cloud, the infrastructure is **not shared with other organizations**.

---

## Characteristics of Private Cloud

* Dedicated infrastructure
* Single organization access
* High level of control
* Enhanced security
* Customizable environment

---

## Advantages of Private Cloud

### Higher Security

Sensitive data stays within the organization's infrastructure.

---

### Full Control

Organizations have full control over:

* Hardware configuration
* Network architecture
* Security policies

---

### Compliance Support

Private cloud is often required for industries with **strict regulatory requirements**.

Examples include:

* Banking
* Healthcare
* Government

---

## Disadvantages of Private Cloud

* High infrastructure cost
* Hardware management responsibility
* Limited scalability compared to public cloud

---

## Technologies Used in Private Cloud

Common technologies used to build private clouds include:

* OpenStack
* VMware vSphere
* Red Hat OpenShift

---

## Example Architecture

```text
Organization Data Center
 │
 ├── Private Servers
 ├── Private Storage
 ├── Private Network
 └── Virtual Machines
```

---

# 5.3 Hybrid Cloud

## Definition

A **Hybrid Cloud** combines **Public Cloud and Private Cloud environments**.

Organizations run some workloads in their **private infrastructure** while using **public cloud services for other workloads**.

Both environments are connected using **secure networking technologies**.

---

## Characteristics of Hybrid Cloud

* Combination of public and private infrastructure
* Secure connectivity between environments
* Flexible workload placement
* Data portability between environments

---

## Advantages of Hybrid Cloud

### Flexibility

Organizations can decide where applications should run.

---

### Security for Sensitive Data

Critical data can remain in private infrastructure while other workloads run in public cloud.

---

### Scalability

Public cloud can handle sudden spikes in demand.

---

### Cost Optimization

Organizations use public cloud resources only when needed.

---

## Disadvantages of Hybrid Cloud

* More complex architecture
* Requires advanced networking configuration
* More operational management

---

## Hybrid Cloud Architecture Example

```text
Private Cloud
   │
   │ Secure Connection (VPN / Direct Connect)
   │
   ▼
Public Cloud
   │
   ├── Web Applications
   ├── DevOps Infrastructure
   ├── Backup Storage
   └── Data Processing
```

---

# 5.4 Comparison of Deployment Models

| Feature        | Public Cloud   | Private Cloud | Hybrid Cloud |
| -------------- | -------------- | ------------- | ------------ |
| Ownership      | Cloud Provider | Organization  | Both         |
| Infrastructure | Shared         | Dedicated     | Mixed        |
| Cost           | Low            | High          | Medium       |
| Security       | Moderate       | High          | High         |
| Scalability    | Very High      | Limited       | High         |
| Maintenance    | Provider       | Organization  | Shared       |

---

# 5.5 Real-World Examples

### Public Cloud Example

A startup hosts its website using:

* EC2 for compute
* S3 for storage
* RDS for database

---

### Private Cloud Example

A bank stores sensitive financial data in its **internal data center** using private infrastructure.

---

### Hybrid Cloud Example

A company stores sensitive customer data in a **private cloud**, while running its **web servers and DevOps pipelines on AWS**.

---

# 5.6 Summary

Cloud deployment models determine **how cloud infrastructure is implemented and managed**.

* **Public Cloud** provides scalable infrastructure managed by cloud providers.
* **Private Cloud** offers dedicated infrastructure with greater control and security.
* **Hybrid Cloud** combines both environments for flexibility and scalability.

Organizations choose the appropriate deployment model based on **security requirements, cost considerations, scalability needs, and operational complexity**.

---
# 6. AWS Pricing Model

AWS follows a **flexible pricing model** that allows organizations to pay only for the resources they use. This approach helps businesses avoid large upfront investments in hardware and infrastructure.

Instead of purchasing servers and maintaining data centers, users can **rent cloud resources on demand** and pay based on usage.

AWS pricing is designed to provide **cost efficiency, scalability, and flexibility** for organizations of all sizes.

---

# 6.1 Pay-As-You-Go Pricing

## Definition

The **Pay-As-You-Go** pricing model means customers pay only for the resources they actually use.

There are **no long-term commitments or upfront infrastructure costs**.

Users are charged based on factors such as:

* Compute usage (hours or seconds)
* Storage usage (GB per month)
* Data transfer
* Number of requests
* Database usage

---

## Example

If an **EC2 instance** runs for:

```
3 hours → You pay only for 3 hours
```

If storage usage is:

```
100 GB in S3 → You pay for 100 GB storage
```

This model helps organizations **optimize costs and avoid unused infrastructure**.

---

# 6.2 AWS Free Tier

AWS provides a **Free Tier** that allows users to explore and test services at no cost within certain limits.

The Free Tier is especially useful for:

* Beginners learning AWS
* Developers testing applications
* Students practicing cloud services

---

## Types of AWS Free Tier

### 1. Always Free

Some services provide **limited free usage permanently**.

Examples:

* AWS Lambda – free requests per month
* DynamoDB – free storage and read/write capacity
* CloudWatch – limited monitoring metrics

---

### 2. 12-Month Free Tier

New AWS accounts receive **free usage limits for the first 12 months**.

Examples:

* 750 hours of EC2 instance usage per month
* 5 GB of S3 storage
* 750 hours of RDS database usage

---

### 3. Short-Term Free Trials

Some AWS services offer **temporary free trials**.

Example:

* Amazon SageMaker free trial
* Amazon Redshift free trial

---

# 6.3 On-Demand Pricing

## Definition

**On-Demand Pricing** allows users to pay for compute resources **without long-term commitments**.

You pay based on:

* Instance type
* Usage duration
* Region
* Operating system

---

## Characteristics

* No upfront payment
* No long-term contracts
* Pay per second or per hour
* Flexible and scalable

---

## Example

Running an EC2 instance for:

```
10 hours → pay for 10 hours
```

This model is ideal for:

* Short-term workloads
* Development environments
* Testing applications

---

# 6.4 Reserved Instances (RI)

## Definition

**Reserved Instances** allow users to reserve AWS compute capacity for a **1-year or 3-year term** in exchange for lower pricing.

This model provides **significant cost savings compared to On-Demand pricing**.

---

## Characteristics

* Long-term commitment
* Lower hourly cost
* Capacity reservation
* Predictable pricing

---

## Savings

Reserved Instances can provide **up to 70% cost savings** compared to On-Demand pricing.

---

## Example Use Cases

Reserved Instances are suitable for:

* Production servers
* Long-running applications
* Databases
* Enterprise workloads

---

# 6.5 Spot Instances

## Definition

**Spot Instances** allow users to use **unused AWS compute capacity** at a significantly lower price.

However, AWS can **terminate these instances at any time** when the capacity is needed.

---

## Characteristics

* Very low cost
* No guaranteed availability
* Can be interrupted
* Suitable for flexible workloads

---

## Cost Savings

Spot Instances can provide **up to 90% cost savings** compared to On-Demand pricing.

---

## Example Use Cases

Spot Instances are useful for:

* Batch processing
* Big data workloads
* Image rendering
* Machine learning training
* CI/CD pipelines

---

# 6.6 Savings Plans

## Definition

**AWS Savings Plans** provide flexible pricing by allowing users to commit to a **specific amount of compute usage per hour** for a **1-year or 3-year period**.

Savings Plans offer lower prices compared to On-Demand usage.

---

## Types of Savings Plans

### Compute Savings Plan

Applies to multiple compute services:

* EC2
* Lambda
* Fargate

Provides the most flexibility.

---

### EC2 Instance Savings Plan

Applies to specific EC2 instance types within a region.

Provides higher discounts but less flexibility.

---

## Benefits

* Up to **72% cost savings**
* Flexible usage across services
* Predictable billing

---

# 6.7 AWS Cost Management Tools

AWS provides tools to monitor and optimize cloud spending.

---

## AWS Cost Explorer

Used to analyze AWS spending patterns.

Features:

* Cost breakdown by service
* Usage trends
* Forecasting future costs

---

## AWS Budgets

Allows users to set **spending limits and alerts**.

Example:

```
Monthly budget: $100
Alert when usage reaches 80%
```

---

## AWS Pricing Calculator

Helps estimate the cost of AWS services before deployment.

Users can calculate:

* EC2 costs
* Storage costs
* Data transfer costs
* Database costs

---

# 6.8 Example Pricing Scenario

Example architecture:

```
Web Application
 │
 ├── EC2 → Web Server
 ├── S3 → File Storage
 └── RDS → Database
```

Estimated monthly costs depend on:

* Instance size
* Storage usage
* Network traffic
* Region

AWS pricing allows organizations to **scale infrastructure while controlling costs effectively**.

---

# 6.9 Summary

AWS provides multiple pricing models designed for **flexibility and cost optimization**.

| Pricing Model      | Description                                |
| ------------------ | ------------------------------------------ |
| Pay-As-You-Go      | Pay only for the resources used            |
| Free Tier          | Free usage limits for learning and testing |
| On-Demand          | Pay per use without commitment             |
| Reserved Instances | Lower pricing with long-term commitment    |
| Spot Instances     | Very low cost using unused capacity        |
| Savings Plans      | Flexible cost-saving commitment model      |

Organizations choose the appropriate pricing model based on **workload requirements, cost optimization strategies, and usage patterns**.

---
