---
# 13.1 Introduction to Amazon VPC
---

## What is Amazon VPC

Amazon Virtual Private Cloud (VPC) is a networking service that allows you to create a **logically isolated virtual network inside the AWS cloud**. Within this network you can launch and manage AWS resources such as compute, databases, and load balancers in a controlled environment.

A VPC functions similarly to a **traditional data center network**, but it runs on AWS infrastructure. This means organizations can design their own network topology in the cloud without maintaining physical networking hardware.

Inside a VPC, you can configure:

* IP address ranges using CIDR blocks
* Subnets for network segmentation
* Route tables for traffic routing
* Internet gateways for external connectivity
* NAT gateways for controlled internet access
* Security groups and network ACLs for traffic filtering

This flexibility allows cloud engineers and DevOps teams to build **secure, scalable, and production-ready architectures**.

Example conceptual architecture:

```
AWS Cloud
   │
   └── VPC (10.0.0.0/16)
        │
        ├── Public Subnet
        │      └── Web Server (EC2)
        │
        └── Private Subnet
               └── Database Server (RDS)
```

In this architecture:

* Public subnet resources can communicate with the internet.
* Private subnet resources remain protected and isolated from direct internet access.

---

# Why VPC is Required

In the early days of AWS, instances were launched using a networking platform called **EC2-Classic**. This model had limitations in terms of security and network control.

Modern cloud infrastructure requires:

* Network isolation
* Flexible IP management
* Secure traffic control
* Hybrid connectivity

Amazon VPC was introduced to solve these challenges.

The main reasons VPC is required are described below.

---

## 1 Network Isolation

A VPC creates a **separate virtual network** for your AWS resources.

Each VPC is isolated from other VPCs by default. This ensures that applications from different organizations or environments cannot communicate unless explicitly configured.

For example:

```
AWS Account
   │
   ├── VPC 1 (Production)
   │
   ├── VPC 2 (Development)
   │
   └── VPC 3 (Testing)
```

Each environment can run independently without interfering with others.

---

## 2 Secure Application Deployment

Security is one of the primary reasons for using VPC.

VPC provides multiple security layers:

### Security Groups

Instance-level firewall controlling inbound and outbound traffic.

### Network ACLs

Subnet-level firewall controlling network traffic rules.

Together they provide **multi-layer security protection**.

---

## 3 Flexible Network Design

VPC allows engineers to design networks according to application needs.

For example:

* Public subnet for web servers
* Private subnet for application servers
* Isolated subnet for databases

Example architecture:

```
VPC (10.0.0.0/16)

 ├── Public Subnet
 │      └── Load Balancer
 │
 ├── Private Subnet
 │      └── Application Servers
 │
 └── Isolated Subnet
        └── Database Servers
```

This structure improves security and scalability.

---

## 4 Internet Connectivity Control

VPC allows full control over internet access.

Resources can connect to the internet using:

* Internet Gateway
* NAT Gateway

Example:

```
Internet
   │
Internet Gateway
   │
Public Subnet
   │
NAT Gateway
   │
Private Subnet
```

Private instances can access the internet for updates but remain unreachable from outside.

---

## 5 Hybrid Cloud Connectivity

Many companies still maintain on-premise data centers. VPC enables hybrid cloud architecture by connecting AWS infrastructure with on-premise networks.

This can be achieved using:

* VPN connections
* Dedicated network links through AWS Direct Connect

Example architecture:

```
On-Premise Data Center
        │
        │ VPN
        │
AWS VPC
```

This allows seamless integration between existing infrastructure and cloud services.

---

# Benefits of Using VPC

Using Amazon VPC provides several important advantages for modern cloud environments.

---

## 1 Complete Network Control

With VPC, you control:

* IP addressing
* Subnet creation
* Route tables
* Network gateways

This provides a high level of customization.

---

## 2 Improved Security

Security is improved through multiple layers:

| Security Layer  | Description               |
| --------------- | ------------------------- |
| Security Groups | Instance-level firewall   |
| Network ACLs    | Subnet-level firewall     |
| Private Subnets | No direct internet access |

This design protects sensitive workloads such as databases.

---

## 3 Scalable Infrastructure

VPC supports large address ranges, enabling thousands of instances within a single network.

Example CIDR block:

```
10.0.0.0/16
```

This allows creation of **65,536 private IP addresses**.

---

## 4 High Availability

VPC allows distribution of resources across multiple **Availability Zones**.

Example:

```
VPC
 ├── AZ-1
 │     └── Public Subnet
 │
 └── AZ-2
       └── Private Subnet
```

If one availability zone fails, applications can continue running in another zone.

---

## 5 Network Segmentation

Subnets allow logical separation of workloads.

Typical segmentation:

| Subnet Type     | Purpose                        |
| --------------- | ------------------------------ |
| Public Subnet   | Web servers and load balancers |
| Private Subnet  | Application servers            |
| Isolated Subnet | Databases                      |

This architecture improves both **security and management**.

---

# Default VPC vs Custom VPC

When a new AWS account is created, AWS automatically provides a **Default VPC**.

However, production environments generally use **Custom VPCs** for better control and security.

| Feature               | Default VPC          | Custom VPC              |
| --------------------- | -------------------- | ----------------------- |
| Created Automatically | Yes                  | No                      |
| Internet Gateway      | Already attached     | Must configure manually |
| Subnets               | Preconfigured        | Created by user         |
| Internet Access       | Enabled by default   | Controlled by user      |
| Use Case              | Learning and testing | Production environments |

---

## Default VPC Characteristics

A default VPC typically includes:

* A predefined CIDR block
* Public subnets in each availability zone
* An attached internet gateway
* Default route tables
* Default security groups

This allows users to launch instances quickly without complex networking configuration.

---

## Custom VPC Characteristics

Custom VPCs allow full network control, including:

* Custom CIDR ranges
* Public and private subnet design
* Advanced routing configuration
* Controlled internet access
* Multi-tier architecture

Custom VPCs are commonly used for **enterprise and production workloads**.

---

# Real World Architecture Overview

Most production applications follow a **multi-tier architecture** inside a VPC.

Example production architecture:

```
Internet
   │
Internet Gateway
   │
Public Subnet
   │
Application Load Balancer
   │
Private Subnet
   │
Application Servers
   │
Private Subnet
   │
Database Servers
```

Architecture layers:

| Layer              | Example Components            |
| ------------------ | ----------------------------- |
| Presentation Layer | Load balancer and web servers |
| Application Layer  | Backend application servers   |
| Data Layer         | Databases                     |

This architecture provides:

* Improved security
* High scalability
* Fault tolerance
* Production-ready deployment

---
# 13.2 VPC Architecture and Components

Amazon VPC architecture is built using several networking components that work together to create a **secure, scalable, and highly available cloud network**. These components allow engineers to design network infrastructure similar to a traditional on-premise data center but with the flexibility of the cloud.

A typical VPC architecture includes components such as:

* VPC
* Subnets
* Route Tables
* Internet Gateway
* NAT Gateway
* Security Groups
* Network ACLs
* Elastic IP
* DHCP Option Sets

Each component has a specific role in controlling **network communication, internet connectivity, and security** within the VPC.

---

# VPC Architecture Overview

A typical AWS VPC architecture for a production environment looks like this:

```
Internet
   │
Internet Gateway
   │
Public Subnet
   │
Load Balancer
   │
Private Subnet
   │
Application Servers
   │
Private Subnet
   │
Database Servers
```

This architecture follows a **multi-tier design**, which separates application layers to improve security and scalability.

| Layer             | Components                  |
| ----------------- | --------------------------- |
| Web Layer         | Load Balancer / Web Servers |
| Application Layer | Application Servers         |
| Data Layer        | Databases                   |

---

# Core Components of VPC Architecture

## 1 VPC (Virtual Private Cloud)

A **VPC** is the foundation of AWS networking. It defines the **network boundary** where all resources are deployed.

When creating a VPC, you must define a **CIDR block**, which determines the IP address range available inside the network.

Example CIDR block:

```
10.0.0.0/16
```

This allows approximately **65,536 private IP addresses**.

Example:

```
VPC: 10.0.0.0/16
```

Inside this network, multiple subnets can be created.

---

## 2 Subnets

A **Subnet** is a smaller network segment inside a VPC. Subnets help organize resources and control network access.

Subnets are created within a specific **Availability Zone**.

Example:

```
VPC: 10.0.0.0/16

Subnet 1 (Public)  : 10.0.1.0/24
Subnet 2 (Private) : 10.0.2.0/24
```

Types of Subnets:

### Public Subnet

A subnet that allows resources to access the internet through an Internet Gateway.

Typical resources:

* Web servers
* Load balancers
* Bastion hosts

### Private Subnet

A subnet that does not allow direct internet access.

Typical resources:

* Application servers
* Databases
* Internal services

Private subnets improve security by keeping critical infrastructure isolated.

---

## 3 Route Tables

A **Route Table** controls how network traffic flows inside a VPC.

It contains rules called **routes** that determine where traffic should be directed.

Example route table:

| Destination | Target           |
| ----------- | ---------------- |
| 10.0.0.0/16 | Local            |
| 0.0.0.0/0   | Internet Gateway |

Explanation:

* **Local route** allows communication within the VPC.
* **0.0.0.0/0 route** sends traffic to the internet.

Each subnet must be associated with a route table.

Types of route tables:

* Main Route Table
* Custom Route Tables

Custom route tables are commonly used in production environments.

---

## 4 Internet Gateway (IGW)

An **Internet Gateway** enables communication between a VPC and the public internet.

It performs two important functions:

* Provides internet connectivity
* Performs Network Address Translation (NAT) for public instances

Example architecture:

```
Internet
   │
Internet Gateway
   │
Public Subnet
   │
EC2 Instance
```

Without an Internet Gateway, instances inside the VPC cannot access the internet.

Steps to enable internet access:

1. Create Internet Gateway
2. Attach Internet Gateway to the VPC
3. Add route in the route table

---

## 5 NAT Gateway

A **NAT Gateway** allows instances in a private subnet to access the internet **without allowing inbound internet traffic**.

This is useful when private instances need to:

* Download software updates
* Access external APIs
* Install packages

Example architecture:

```
Internet
   │
Internet Gateway
   │
Public Subnet
   │
NAT Gateway
   │
Private Subnet
   │
Application Server
```

Key points:

* NAT Gateway must be placed in a **Public Subnet**
* It requires an **Elastic IP**
* Private subnet route tables must point to the NAT Gateway

Example route:

| Destination | Target      |
| ----------- | ----------- |
| 0.0.0.0/0   | NAT Gateway |

---

## 6 Security Groups

Security Groups act as **virtual firewalls for EC2 instances**.

They control:

* Inbound traffic
* Outbound traffic

Security groups are **stateful**, meaning if inbound traffic is allowed, the response traffic is automatically allowed.

Example security group rules:

| Type  | Port | Source    |
| ----- | ---- | --------- |
| SSH   | 22   | My IP     |
| HTTP  | 80   | 0.0.0.0/0 |
| HTTPS | 443  | 0.0.0.0/0 |

Security groups are applied at the **instance level**.

---

## 7 Network ACLs (NACLs)

Network Access Control Lists provide **subnet-level security**.

Unlike security groups, NACLs are **stateless**, meaning both inbound and outbound rules must be defined explicitly.

Example rules:

| Rule Number | Type | Allow/Deny | Source    |
| ----------- | ---- | ---------- | --------- |
| 100         | HTTP | Allow      | 0.0.0.0/0 |
| 200         | SSH  | Allow      | My IP     |

NACLs provide an additional layer of security.

---

## 8 Elastic IP

An **Elastic IP (EIP)** is a static public IP address assigned to an AWS resource.

Normally, public IP addresses change when an instance is stopped and started. Elastic IPs solve this problem by providing a **permanent public IP address**.

Example:

```
Elastic IP → EC2 Instance
```

Use cases:

* Web servers
* NAT Gateways
* Bastion hosts

---

## 9 DHCP Option Sets

DHCP (Dynamic Host Configuration Protocol) option sets control how instances receive network configuration.

They can define:

* DNS servers
* Domain names
* NTP servers

By default, AWS automatically assigns DNS settings to instances.

---

# Complete VPC Architecture Example

```
Internet
   │
Internet Gateway
   │
Public Subnet
   │
Load Balancer
   │
Private Subnet
   │
Application Servers
   │
Private Subnet
   │
Database Servers
```

This architecture is commonly used in **production AWS environments**.

Advantages:

* High security
* Scalable architecture
* High availability
* Fault tolerance

---

# 13.3 VPC CIDR Blocks and IP Addressing

--
IP addressing is a fundamental concept in AWS networking. When creating a VPC, the first step is defining a **CIDR block**, which determines the **range of IP addresses available within the VPC**.

Proper CIDR planning is important for:

* scalable infrastructure
* subnet creation
* hybrid cloud connectivity
* avoiding IP conflicts between networks

---

# What is CIDR

CIDR stands for **Classless Inter-Domain Routing**.

Classless Inter-Domain Routing is a method used to allocate IP addresses and route IP packets efficiently.

CIDR notation is written in the following format:

```
IP Address / Prefix Length
```

Example:

```
10.0.0.0/16
```

| Component | Description                            |
| --------- | -------------------------------------- |
| 10.0.0.0  | Network Address                        |
| /16       | Prefix length (number of network bits) |

The prefix length determines how many bits belong to the **network portion** and how many bits belong to the **host portion**.

---

# CIDR Bit Structure (Network Bits vs Host Bits)

An IPv4 address consists of **32 bits**.

CIDR divides these bits into:

* **Network bits**
* **Host bits**

Example:

```
10.0.0.0/16
```

| Field        | Bits |
| ------------ | ---- |
| Network bits | 16   |
| Host bits    | 16   |

Calculation:

```
Host bits = 32 − Network bits
```

```
Host bits = 32 − 16 = 16
```

Total available IP addresses:

```
2^16 = 65,536
```

---

# CIDR Block Size Examples

| CIDR | Network Bits | Host Bits | Total IPs |
| ---- | ------------ | --------- | --------- |
| /16  | 16           | 16        | 65,536    |
| /20  | 20           | 12        | 4,096     |
| /24  | 24           | 8         | 256       |
| /28  | 28           | 4         | 16        |

Example:

```
CIDR: 10.0.1.0/24
```

Host bits = **8**

```
2^8 = 256 IP addresses
```

---

# Binary Representation of CIDR

CIDR is based on the **binary representation of IP addresses**.

Example:

```
10.0.0.0/16
```

Binary format:

```
00001010.00000000.00000000.00000000
```

Prefix `/16` means the first **16 bits represent the network**.

```
Network bits: 00001010.00000000
Host bits   : 00000000.00000000
```

The host bits are used to assign IP addresses to resources inside the VPC.

---

# Private IP Address Ranges

When creating a VPC, AWS allows only **private IPv4 ranges** defined in:

RFC 1918

| Private Range                 | CIDR           |
| ----------------------------- | -------------- |
| 10.0.0.0 – 10.255.255.255     | 10.0.0.0/8     |
| 172.16.0.0 – 172.31.255.255   | 172.16.0.0/12  |
| 192.168.0.0 – 192.168.255.255 | 192.168.0.0/16 |

Most AWS architectures commonly use:

```
10.0.0.0/16
```

because it provides a large number of addresses.

---

# AWS Reserved IP Addresses in Subnets

In every subnet AWS reserves **5 IP addresses**.

Example subnet:

```
10.0.1.0/24
```

Reserved addresses:

| IP Address | Purpose           |
| ---------- | ----------------- |
| 10.0.1.0   | Network address   |
| 10.0.1.1   | VPC router        |
| 10.0.1.2   | AWS DNS           |
| 10.0.1.3   | Reserved          |
| 10.0.1.255 | Broadcast address |

Total IPs in `/24` subnet:

```
256
```

Usable IPs:

```
256 − 5 = 251
```

---

# VPC CIDR Block Limits

AWS allows VPC CIDR blocks between:

```
/16 to /28
```

| CIDR | Purpose                   |
| ---- | ------------------------- |
| /16  | Large enterprise networks |
| /20  | Medium networks           |
| /24  | Small networks            |
| /28  | Very small networks       |

Example:

```
VPC CIDR : 10.0.0.0/16
```

---

# Subnet CIDR Example

Example VPC:

```
VPC CIDR : 10.0.0.0/16
```

Subnet allocation:

| Subnet          | CIDR        |
| --------------- | ----------- |
| Public Subnet   | 10.0.1.0/24 |
| Private Subnet  | 10.0.2.0/24 |
| Database Subnet | 10.0.3.0/24 |

Architecture:

```
VPC (10.0.0.0/16)

 ├── Public Subnet
 │      10.0.1.0/24
 │
 ├── Private Subnet
 │      10.0.2.0/24
 │
 └── Database Subnet
        10.0.3.0/24
```

---

# Secondary CIDR Blocks

AWS allows attaching **multiple CIDR blocks** to the same VPC.

Example:

```
Primary CIDR  : 10.0.0.0/16
Secondary CIDR: 10.1.0.0/16
```

This expands the available IP address range when the network grows.

---

# CIDR Planning Best Practices

### Choose a Large CIDR Block

Start with a large CIDR block such as:

```
10.0.0.0/16
```

This allows future expansion.

---

### Avoid Overlapping Networks

CIDR ranges must not overlap with:

* other VPCs
* on-premise networks
* VPN networks

Otherwise routing conflicts will occur.

---

### Separate Application Layers

Use different subnets for different layers:

* Public subnet → web servers
* Private subnet → application servers
* Isolated subnet → databases

---

### Use Multiple Availability Zones

Distribute subnets across multiple **Availability Zones** for:

* high availability
* fault tolerance
* better scalability

---
# 13.4 Subnets in AWS VPC

Subnets are one of the most important components of a VPC network architecture. They allow you to divide a large VPC network into **smaller and manageable network segments**. This helps in organizing resources, improving security, and designing scalable cloud infrastructure.

In AWS networking, subnets are used to **separate different layers of an application**, such as web servers, application servers, and databases.

Subnets are created inside a **Amazon Virtual Private Cloud** and are associated with a specific **Availability Zone**.

---

# What is a Subnet

A **Subnet (Subnetwork)** is a logical subdivision of a VPC's IP address range.

When you create a VPC with a CIDR block, you can divide that range into multiple smaller CIDR blocks called subnets.

Example VPC:

```
VPC CIDR: 10.0.0.0/16
```

This VPC can be divided into multiple subnets.

Example:

```
VPC (10.0.0.0/16)

 ├── Subnet 1 : 10.0.1.0/24
 ├── Subnet 2 : 10.0.2.0/24
 ├── Subnet 3 : 10.0.3.0/24
 └── Subnet 4 : 10.0.4.0/24
```

Each subnet contains a specific number of IP addresses that can be assigned to resources such as:

* EC2 instances
* Load balancers
* Databases
* Containers

Subnets help organize resources within the network.

---

# Subnet Characteristics

Important characteristics of AWS subnets include:

### 1 Availability Zone Specific

Each subnet exists in only **one Availability Zone**.

Example:

```
Subnet 1 → ap-south-1a
Subnet 2 → ap-south-1b
```

This allows applications to run across multiple AZs for high availability.

---

### 2 Automatic Private IP Assignment

When an instance is launched in a subnet, AWS automatically assigns a **private IP address** from the subnet range.

Example:

```
Subnet: 10.0.1.0/24
Instance Private IP: 10.0.1.15
```

---

### 3 Subnet Routing

Each subnet must be associated with a **route table** that determines how traffic flows.

Example route:

| Destination | Target           |
| ----------- | ---------------- |
| 10.0.0.0/16 | Local            |
| 0.0.0.0/0   | Internet Gateway |

---

### 4 IP Address Allocation

Subnets allocate IP addresses to resources.

Example:

```
Subnet CIDR: 10.0.1.0/24
Total IPs: 256
Reserved by AWS: 5
Available: 251
```

---

# Types of Subnets

There are mainly two types of subnets used in AWS architecture.

---

## Public Subnet

A **Public Subnet** is a subnet that allows resources to communicate with the internet.

This happens when:

* The subnet route table contains a route to an **Internet Gateway**.
* Instances inside the subnet have a **public IP address**.

Example architecture:

```
Internet
   │
Internet Gateway
   │
Public Subnet
   │
Web Server (EC2)
```

Typical resources deployed in public subnets:

* Web servers
* Load balancers
* Bastion hosts

---

## Private Subnet

A **Private Subnet** does not allow direct internet access.

Instances inside private subnets cannot be accessed directly from the internet.

Example architecture:

```
Internet
   │
Internet Gateway
   │
Public Subnet
   │
NAT Gateway
   │
Private Subnet
   │
Application Server
```

Private subnets are commonly used for:

* Application servers
* Databases
* Internal services

---

# Subnet Architecture in Production

Most production architectures use **multiple subnets across multiple Availability Zones**.

Example architecture:

```
VPC (10.0.0.0/16)

AZ-1
 ├── Public Subnet
 ├── Private App Subnet
 └── Private DB Subnet

AZ-2
 ├── Public Subnet
 ├── Private App Subnet
 └── Private DB Subnet
```

This architecture provides:

* High availability
* Fault tolerance
* Security isolation

---

# Subnet CIDR Planning Example

Example production subnet structure:

| Subnet     | CIDR         | Purpose             |
| ---------- | ------------ | ------------------- |
| Public AZ1 | 10.0.1.0/24  | Load balancer       |
| Public AZ2 | 10.0.2.0/24  | Load balancer       |
| App AZ1    | 10.0.10.0/24 | Application servers |
| App AZ2    | 10.0.11.0/24 | Application servers |
| DB AZ1     | 10.0.20.0/24 | Database            |
| DB AZ2     | 10.0.21.0/24 | Database            |

---

# Steps to Create a Subnet in AWS

Steps to create a subnet in AWS Management Console.

1. Open AWS Console
2. Navigate to **VPC Dashboard**
3. Click **Subnets**
4. Click **Create Subnet**
5. Select VPC
6. Select Availability Zone
7. Enter Subnet CIDR block
8. Click **Create Subnet**

Example configuration:

| Setting           | Value       |
| ----------------- | ----------- |
| VPC               | 10.0.0.0/16 |
| Availability Zone | ap-south-1a |
| Subnet CIDR       | 10.0.1.0/24 |

---

# Public vs Private Subnet Comparison

| Feature           | Public Subnet | Private Subnet |
| ----------------- | ------------- | -------------- |
| Internet Access   | Yes           | No             |
| Route Table       | IGW Route     | NAT Route      |
| Public IP         | Required      | Not required   |
| Example Resources | Web servers   | Databases      |

---

# Best Practices for Subnet Design

### Use Multiple Availability Zones

Deploy subnets across multiple AZs to increase availability.

---

### Separate Application Layers

Use different subnets for:

* web servers
* application servers
* databases

---

### Avoid Very Small Subnets

Small subnets limit scalability.

Example recommended size:

```
/24
```

---

### Use Private Subnets for Sensitive Resources

Keep databases and internal services inside private subnets.

---

# Real DevOps Architecture Example

```
Internet
   │
Internet Gateway
   │
Public Subnets
   │
Application Load Balancer
   │
Private Application Subnets
   │
Application Servers
   │
Private Database Subnets
   │
Database Cluster
```

This architecture is widely used in **enterprise AWS environments**.

---
# 13.5 Route Tables in AWS VPC
---
Route tables are an essential component of AWS networking. They control how network traffic flows inside a VPC and determine where packets should be sent.

In AWS networking, every subnet must be associated with a route table. The route table contains rules that define the **destination network and the target through which traffic should be routed**.

Route tables are used to control communication between:

* subnets inside the VPC
* internet connectivity
* private networks
* other VPCs

They are a core feature of **Amazon Virtual Private Cloud** networking architecture.

---

# What is a Route Table

A **Route Table** is a set of rules (routes) that determine where network traffic should go.

Each route has two main parts:

| Field       | Description                   |
| ----------- | ----------------------------- |
| Destination | Network address or CIDR block |
| Target      | Where traffic should be sent  |

Example route table:

| Destination | Target           |
| ----------- | ---------------- |
| 10.0.0.0/16 | local            |
| 0.0.0.0/0   | Internet Gateway |

Explanation:

* **local route** allows communication within the VPC.
* **0.0.0.0/0 route** sends traffic to the internet.

---

# How Route Tables Work

When an instance sends a network packet, AWS checks the route table associated with the subnet.

Traffic flow process:

1. Instance sends traffic to a destination.
2. AWS checks the subnet route table.
3. The matching route is selected.
4. Traffic is forwarded to the target resource.

Example:

```
EC2 Instance
      │
      │
Route Table
      │
      ├── Local → Internal VPC traffic
      └── IGW → Internet traffic
```

This process ensures correct network routing inside the VPC.

---

# Default Route Table

When a VPC is created, AWS automatically creates a **Main Route Table**.

Characteristics of the main route table:

* Automatically associated with all subnets by default
* Contains a local route for VPC communication

Example:

| Destination | Target |
| ----------- | ------ |
| 10.0.0.0/16 | local  |

This route allows instances within the VPC to communicate with each other.

---

# Custom Route Tables

Custom route tables are created to control network traffic for specific subnets.

They allow engineers to define routes for:

* internet access
* NAT gateway access
* VPN connections
* VPC peering

Example architecture:

```
VPC
 │
 ├── Public Subnet
 │       └── Route Table → Internet Gateway
 │
 └── Private Subnet
         └── Route Table → NAT Gateway
```

This separation improves security and network control.

---

# Public Route Table

A **Public Route Table** allows internet access for resources in a subnet.

Example route table:

| Destination | Target           |
| ----------- | ---------------- |
| 10.0.0.0/16 | local            |
| 0.0.0.0/0   | Internet Gateway |

Traffic flow:

```
EC2 Instance
     │
Public Subnet
     │
Route Table
     │
Internet Gateway
     │
Internet
```

Instances must also have a **public IP address** to communicate with the internet.

---

# Private Route Table

A **Private Route Table** allows instances to access the internet through a NAT Gateway.

Example route table:

| Destination | Target      |
| ----------- | ----------- |
| 10.0.0.0/16 | local       |
| 0.0.0.0/0   | NAT Gateway |

Traffic flow:

```
Private Instance
       │
Private Subnet
       │
Route Table
       │
NAT Gateway
       │
Internet Gateway
       │
Internet
```

This allows outbound internet access while preventing inbound connections.

---

# Route Table Association

Each subnet must be associated with a route table.

Types of associations:

### Explicit Association

A subnet is manually associated with a custom route table.

Example:

```
Public Subnet → Public Route Table
```

### Implicit Association

If no route table is specified, the subnet automatically uses the **main route table**.

---

# Route Table Targets

Route tables can send traffic to different targets.

Common targets include:

| Target                  | Purpose                        |
| ----------------------- | ------------------------------ |
| Internet Gateway        | Internet access                |
| NAT Gateway             | Private subnet internet access |
| VPC Peering             | Connect two VPCs               |
| Virtual Private Gateway | VPN connection                 |
| Local                   | Internal VPC communication     |

Example route table:

| Destination   | Target           |
| ------------- | ---------------- |
| 10.0.0.0/16   | local            |
| 0.0.0.0/0     | Internet Gateway |
| 172.31.0.0/16 | VPC Peering      |

---

# Route Table Architecture Example

Example VPC design:

```
VPC (10.0.0.0/16)

 ├── Public Subnet
 │       │
 │       └── Route Table
 │              └── 0.0.0.0/0 → Internet Gateway
 │
 └── Private Subnet
         │
         └── Route Table
                └── 0.0.0.0/0 → NAT Gateway
```

This architecture is commonly used in production environments.

---

# Steps to Create a Route Table

Steps in AWS Management Console.

1. Open AWS Console
2. Go to VPC Dashboard
3. Click **Route Tables**
4. Click **Create Route Table**
5. Select VPC
6. Add routes
7. Associate subnet

Example configuration:

| Setting     | Value            |
| ----------- | ---------------- |
| VPC         | 10.0.0.0/16      |
| Destination | 0.0.0.0/0        |
| Target      | Internet Gateway |

---

# Best Practices for Route Tables

### Separate Public and Private Route Tables

Use different route tables for public and private subnets.

---

### Use NAT Gateway for Private Subnets

Private instances should access the internet using NAT Gateway instead of Internet Gateway.

---

### Avoid Complex Routing

Keep route tables simple to reduce network troubleshooting complexity.

---

### Use Clear Naming

Example naming:

```
Public-Route-Table
Private-Route-Table
Database-Route-Table
```

---

# Real Production Architecture Example

```
Internet
   │
Internet Gateway
   │
Public Route Table
   │
Public Subnets
   │
Load Balancer
   │
Private Route Table
   │
Private Subnets
   │
Application Servers
   │
Database Servers
```

This architecture ensures:

* secure application deployment
* controlled internet access
* scalable infrastructure

---
# 13.6 Internet Gateway (IGW)
---

An **Internet Gateway (IGW)** is a VPC component that enables communication between resources inside a VPC and the public internet. It allows instances in a **public subnet** to send and receive traffic from the internet.

In AWS networking, an Internet Gateway is attached to a **Amazon Virtual Private Cloud** and works together with route tables to provide internet connectivity.

Without an Internet Gateway, resources inside the VPC cannot communicate with the public internet.

---

# What is an Internet Gateway

An **Internet Gateway** is a horizontally scalable, redundant, and highly available AWS-managed gateway that connects a VPC to the internet.

It performs two main functions:

1. **Enables internet connectivity for instances with public IP addresses**
2. **Performs network address translation for instances with public IPs**

Example architecture:

```
Internet
   │
Internet Gateway
   │
Public Subnet
   │
EC2 Instance
```

In this setup:

* The Internet Gateway acts as the entry and exit point for internet traffic.
* Instances in the public subnet can communicate with external networks.

---

# Key Characteristics of Internet Gateway

### Highly Available

Internet Gateway is managed by AWS and automatically provides high availability across the region.

---

### Horizontally Scalable

It automatically scales to handle large volumes of traffic without requiring manual configuration.

---

### No Bandwidth Limitation

AWS automatically manages bandwidth for Internet Gateway.

---

### No Cost for Gateway

There is **no additional cost for using Internet Gateway**, but data transfer charges may apply.

---

# How Internet Gateway Works

Internet Gateway works together with:

* Public IP addresses
* Route tables
* Subnets

Traffic flow example:

```
User Browser
     │
Internet
     │
Internet Gateway
     │
Public Route Table
     │
Public Subnet
     │
EC2 Instance
```

Steps involved:

1. A user sends a request from the internet.
2. The request reaches the Internet Gateway.
3. The route table directs the traffic to the public subnet.
4. The EC2 instance receives the request.

The response follows the reverse path.

---

# Public Subnet Requirement

For a subnet to be considered a **public subnet**, two conditions must be met.

### 1 Internet Gateway Attached

The VPC must have an Internet Gateway attached.

---

### 2 Route Table Entry

The subnet route table must contain this route:

```
Destination: 0.0.0.0/0
Target: Internet Gateway
```

Example route table:

| Destination | Target           |
| ----------- | ---------------- |
| 10.0.0.0/16 | Local            |
| 0.0.0.0/0   | Internet Gateway |

---

# Public IP Requirement

Instances must have a **public IP address** to communicate with the internet through the Internet Gateway.

Example:

| Instance   | Private IP | Public IP    |
| ---------- | ---------- | ------------ |
| Web Server | 10.0.1.15  | 54.210.10.20 |

Private IP is used for internal communication, while the public IP allows internet access.

---

# Internet Gateway Architecture Example

Example AWS architecture:

```
Internet
   │
Internet Gateway
   │
Public Subnet
   │
Application Load Balancer
   │
Private Subnet
   │
Application Servers
```

In this architecture:

* The Load Balancer is placed in a public subnet.
* Application servers run in private subnets.
* Only the load balancer communicates with the internet.

---

# Steps to Create an Internet Gateway

Steps to create an Internet Gateway in AWS.

1. Open AWS Management Console
2. Navigate to **VPC Dashboard**
3. Click **Internet Gateways**
4. Click **Create Internet Gateway**
5. Enter a name tag
6. Click **Create Internet Gateway**

Example configuration:

| Setting | Value          |
| ------- | -------------- |
| Name    | production-igw |

---

# Attach Internet Gateway to VPC

After creation, the Internet Gateway must be attached to a VPC.

Steps:

1. Select Internet Gateway
2. Click **Actions**
3. Select **Attach to VPC**
4. Choose the VPC
5. Click **Attach**

Example:

```
Internet Gateway → VPC
```

---

# Add Route to Route Table

To enable internet connectivity, a route must be added.

Steps:

1. Go to **Route Tables**
2. Select the public route table
3. Click **Edit Routes**
4. Add route

Example route:

| Destination | Target           |
| ----------- | ---------------- |
| 0.0.0.0/0   | Internet Gateway |

---

# Complete Internet Access Architecture

Example setup:

```
Internet
   │
Internet Gateway
   │
Public Route Table
   │
Public Subnet
   │
EC2 Web Server
```

Requirements for internet access:

* Internet Gateway attached to VPC
* Route table entry (0.0.0.0/0 → IGW)
* Public IP assigned to instance

---

# Best Practices for Internet Gateway

### Use Internet Gateway Only for Public Subnets

Private subnets should not use Internet Gateway directly.

---

### Use NAT Gateway for Private Instances

Private instances should access the internet using a **NAT Gateway**.

---

### Restrict Access with Security Groups

Control inbound traffic using security group rules.

Example:

| Type  | Port | Source    |
| ----- | ---- | --------- |
| HTTP  | 80   | 0.0.0.0/0 |
| HTTPS | 443  | 0.0.0.0/0 |
| SSH   | 22   | My IP     |

---

# Real Production Architecture

```
Internet
   │
Internet Gateway
   │
Public Subnets
   │
Application Load Balancer
   │
Private Application Subnets
   │
Application Servers
   │
Private Database Subnets
   │
Database Cluster
```

This architecture provides:

* secure application design
* controlled internet access
* high availability

---
# 13.7 NAT Gateway
---

A **NAT Gateway (Network Address Translation Gateway)** is a networking service that allows instances in a **private subnet** to connect to the internet while preventing the internet from initiating connections with those instances.

It is commonly used when private instances need internet access for tasks such as:

* downloading software updates
* installing packages
* accessing external APIs
* pulling container images

NAT Gateway is a core networking component inside **Amazon Virtual Private Cloud** architecture.

---

# What is NAT (Network Address Translation)

Network Address Translation is a technique used to translate private IP addresses into public IP addresses so that devices inside a private network can communicate with external networks.

Example:

```
Private IP → Public IP → Internet
```

NAT hides the internal private IP address and replaces it with a public IP address.

This improves security because external systems cannot directly access private resources.

---

# What is a NAT Gateway

A **NAT Gateway** is an AWS-managed service that performs NAT for instances in private subnets.

It allows **outbound internet access only**.

Important characteristics:

* Instances can access the internet
* Internet cannot initiate inbound connections
* Managed and highly available service

Example architecture:

```
Internet
   │
Internet Gateway
   │
Public Subnet
   │
NAT Gateway
   │
Private Subnet
   │
EC2 Instance
```

---

# Why NAT Gateway is Required

Instances in private subnets cannot access the internet directly because they do not have public IP addresses.

Example:

```
Private Subnet
   │
EC2 Instance (10.0.2.15)
```

This instance cannot reach the internet without NAT.

Using a NAT Gateway allows outbound internet connectivity while maintaining security.

Example traffic flow:

```
Private Instance
      │
Private Route Table
      │
NAT Gateway
      │
Internet Gateway
      │
Internet
```

---

# NAT Gateway Architecture

Typical architecture in AWS:

```
Internet
   │
Internet Gateway
   │
Public Subnet
   │
NAT Gateway
   │
Private Subnet
   │
Application Server
```

Important points:

* NAT Gateway must be placed in a **Public Subnet**
* NAT Gateway must have an **Elastic IP**
* Private subnet route tables must point to NAT Gateway

---

# Traffic Flow Through NAT Gateway

Step-by-step traffic flow:

1. Private instance sends request to internet.
2. Route table directs traffic to NAT Gateway.
3. NAT Gateway translates private IP to Elastic IP.
4. Traffic goes through Internet Gateway.
5. Response returns to NAT Gateway.
6. NAT Gateway forwards traffic back to private instance.

Example:

```
Private Instance (10.0.2.15)
       │
Private Route Table
       │
NAT Gateway (Elastic IP)
       │
Internet Gateway
       │
Internet
```

---

# NAT Gateway vs Internet Gateway

| Feature            | NAT Gateway     | Internet Gateway   |
| ------------------ | --------------- | ------------------ |
| Used for           | Private subnets | Public subnets     |
| Internet access    | Outbound only   | Inbound + outbound |
| Public IP required | No              | Yes                |
| Security           | Higher          | Lower              |

---

# NAT Gateway vs NAT Instance

Before NAT Gateway existed, AWS used NAT instances.

| Feature           | NAT Gateway | NAT Instance |
| ----------------- | ----------- | ------------ |
| Managed by AWS    | Yes         | No           |
| High Availability | Automatic   | Manual       |
| Scalability       | Automatic   | Limited      |
| Maintenance       | None        | Required     |

Today, NAT Gateway is recommended for production environments.

---

# Steps to Create a NAT Gateway

Steps in AWS Management Console.

### Step 1 Create Elastic IP

1. Open AWS Console
2. Go to VPC Dashboard
3. Click **Elastic IPs**
4. Click **Allocate Elastic IP**

Elastic IP is required for NAT Gateway.

---

### Step 2 Create NAT Gateway

1. Go to **NAT Gateways**
2. Click **Create NAT Gateway**
3. Select **Public Subnet**
4. Attach Elastic IP
5. Click **Create**

Example configuration:

| Setting    | Value         |
| ---------- | ------------- |
| Subnet     | Public Subnet |
| Elastic IP | Allocated EIP |

---

### Step 3 Update Private Route Table

Add route in private route table.

Example route:

| Destination | Target      |
| ----------- | ----------- |
| 0.0.0.0/0   | NAT Gateway |

This allows private instances to access the internet.

---

# Complete NAT Gateway Architecture

```
Internet
   │
Internet Gateway
   │
Public Subnet
   │
NAT Gateway
   │
Private Route Table
   │
Private Subnet
   │
Application Servers
```

This architecture is widely used in production AWS environments.

---

# Best Practices for NAT Gateway

### Place NAT Gateway in Public Subnet

NAT Gateway must always be created in a public subnet.

---

### Use One NAT Gateway Per Availability Zone

This improves high availability.

Example:

```
AZ-1 → NAT Gateway 1
AZ-2 → NAT Gateway 2
```

---

### Use Private Subnets for Sensitive Resources

Databases and application servers should run in private subnets.

---

### Monitor NAT Gateway Costs

NAT Gateway has hourly and data processing charges.

---

# Real Production Architecture Example

```
Internet
   │
Internet Gateway
   │
Public Subnets
   │
Load Balancer
   │
Private Subnets
   │
Application Servers
   │
NAT Gateway
   │
Internet
```

Benefits:

* secure architecture
* controlled internet access
* scalable infrastructure

---
# 13.8 Elastic IP (EIP)
---

An **Elastic IP (EIP)** is a static public IPv4 address provided by AWS that can be assigned to resources such as EC2 instances or NAT Gateways. Unlike regular public IP addresses, an Elastic IP remains the same even if the instance is stopped and started.

Elastic IPs are commonly used in cloud architectures where a **permanent public IP address** is required.

Elastic IP is part of the networking services within **Amazon Virtual Private Cloud**.

---

# What is an Elastic IP

An **Elastic IP** is a **static public IP address** that can be allocated to your AWS account and then associated with a specific AWS resource.

Normally when an instance is stopped and started:

* The **public IP changes**
* The **private IP remains the same**

Elastic IP solves this issue by providing a **fixed public IP**.

Example:

```
EC2 Instance
Private IP → 10.0.1.15
Elastic IP → 52.14.210.35
```

Even if the instance restarts, the Elastic IP remains the same.

---

# Why Elastic IP is Required

Elastic IPs are required when applications need a **consistent public endpoint**.

Common use cases include:

* Production web servers
* NAT Gateway configuration
* Bastion hosts
* DNS mapping to a fixed IP

Without Elastic IP, public IP addresses would change frequently, which could break external connectivity.

---

# How Elastic IP Works

When an Elastic IP is associated with a resource, AWS maps the **public Elastic IP to the private IP address** of that resource.

Example architecture:

```
Internet
   │
Elastic IP
   │
EC2 Instance
Private IP: 10.0.1.15
```

Traffic flow:

1. User sends request to Elastic IP.
2. AWS maps Elastic IP to the private IP.
3. Instance receives the request.
4. Response is sent back through the Elastic IP.

---

# Elastic IP Association

Elastic IP can be associated with different AWS resources.

Common associations:

| Resource          | Use Case                       |
| ----------------- | ------------------------------ |
| EC2 Instance      | Web servers                    |
| NAT Gateway       | Private subnet internet access |
| Network Interface | Advanced networking            |

Example:

```
Elastic IP → NAT Gateway
Elastic IP → Bastion Host
```

---

# Elastic IP Allocation

Elastic IP must first be **allocated to the AWS account** before it can be used.

Once allocated, it remains reserved until released.

Important points:

* Elastic IP belongs to a specific AWS region
* It can be remapped between instances
* It provides a static public endpoint

---

# Steps to Allocate an Elastic IP

Steps in AWS Management Console.

1. Open AWS Console
2. Navigate to **VPC Dashboard**
3. Click **Elastic IPs**
4. Click **Allocate Elastic IP Address**
5. Choose allocation settings
6. Click **Allocate**

Example configuration:

| Setting              | Value  |
| -------------------- | ------ |
| Network Border Group | Region |
| IP Type              | IPv4   |

After allocation, the Elastic IP appears in the dashboard.

---

# Associate Elastic IP to EC2 Instance

Steps:

1. Go to **Elastic IPs**
2. Select the allocated IP
3. Click **Actions → Associate Elastic IP Address**
4. Select resource type (EC2 instance)
5. Choose instance
6. Click **Associate**

Example:

```
Elastic IP → EC2 Instance
```

The instance now has a static public IP.

---

# Disassociate Elastic IP

Elastic IP can also be detached from a resource.

Steps:

1. Select Elastic IP
2. Click **Actions → Disassociate Elastic IP**

After disassociation, the IP remains allocated but not attached.

---

# Release Elastic IP

If an Elastic IP is no longer required, it should be released.

Steps:

1. Select Elastic IP
2. Click **Actions → Release Elastic IP**

This returns the IP address to AWS.

---

# Elastic IP Pricing

Elastic IP is **free when associated with a running instance**.

However charges apply in the following cases:

| Scenario                            | Cost    |
| ----------------------------------- | ------- |
| Elastic IP not attached to instance | Charged |
| Multiple Elastic IPs per instance   | Charged |

AWS encourages efficient use of Elastic IP addresses.

---

# Elastic IP Architecture Example

Example AWS architecture:

```
Internet
   │
Elastic IP
   │
Load Balancer / EC2
   │
Private Subnet
   │
Application Servers
```

Elastic IP ensures a stable external endpoint for internet communication.

---

# Elastic IP with NAT Gateway

Elastic IP is required for NAT Gateway.

Example architecture:

```
Internet
   │
Internet Gateway
   │
Elastic IP
   │
NAT Gateway
   │
Private Subnet
   │
Application Server
```

The NAT Gateway uses Elastic IP to communicate with the internet on behalf of private instances.

---

# Best Practices for Elastic IP

### Use Only When Required

Elastic IP addresses are limited resources, so they should be used only when necessary.

---

### Release Unused Elastic IPs

Unused Elastic IPs incur charges, so they should be released.

---

### Use for Critical Infrastructure

Typical resources that require Elastic IP:

* NAT Gateway
* Bastion host
* Production web server

---

# Real Production Architecture

```
Internet
   │
Elastic IP
   │
Application Load Balancer
   │
Public Subnet
   │
NAT Gateway
   │
Private Subnet
   │
Application Servers
```

This architecture provides:

* stable public endpoint
* secure private infrastructure
* scalable cloud networking

---
# 13.9 DHCP Option Sets
---

In AWS networking, when an instance launches inside a VPC, it automatically receives network configuration such as IP address, DNS server, and domain name. This configuration is provided using **DHCP Option Sets**.

DHCP Option Sets allow administrators to define how instances receive network settings automatically.

This feature is part of the networking capabilities of **Amazon Virtual Private Cloud**.

---

# What is DHCP

DHCP stands for **Dynamic Host Configuration Protocol**.

Dynamic Host Configuration Protocol is a protocol used to automatically assign network configuration to devices when they join a network.

DHCP automatically provides:

* IP address
* Subnet mask
* DNS server
* Default gateway
* Domain name

Example:

```
EC2 Instance
     │
DHCP Server
     │
Receives Network Configuration
```

Without DHCP, network configuration would need to be assigned manually to each instance.

---

# What is a DHCP Option Set

A **DHCP Option Set** is a collection of network configuration settings that can be applied to a VPC.

These settings define what configuration instances receive when they start.

Example DHCP settings include:

| Setting              | Purpose                      |
| -------------------- | ---------------------------- |
| Domain Name          | Default domain for instances |
| DNS Servers          | DNS resolution               |
| NTP Servers          | Time synchronization         |
| NetBIOS Name Servers | Windows networking           |

Once created, a DHCP option set is **associated with a VPC**.

All instances launched in that VPC automatically receive these settings.

---

# Default DHCP Option Set

Every VPC automatically has a **default DHCP option set**.

Typical default configuration:

| Setting     | Default Value           |
| ----------- | ----------------------- |
| Domain Name | region.compute.internal |
| DNS Server  | AmazonProvidedDNS       |

Example:

```
ap-south-1.compute.internal
```

AWS provides a built-in DNS resolver called **AmazonProvidedDNS**.

This DNS allows instances to resolve:

* AWS service endpoints
* internal hostnames
* private DNS names

---

# How DHCP Option Sets Work

When an instance launches inside a VPC, it requests network configuration.

The process works as follows:

```
EC2 Instance
     │
DHCP Request
     │
DHCP Option Set
     │
Network Configuration Assigned
```

The instance automatically receives:

* private IP address
* DNS server
* domain name

This simplifies network configuration.

---

# Example DHCP Configuration

Example configuration inside a DHCP option set:

| Parameter           | Value             |
| ------------------- | ----------------- |
| Domain Name         | example.internal  |
| Domain Name Servers | AmazonProvidedDNS |
| NTP Servers         | time.aws.com      |

This configuration will be applied to all instances in the VPC.

---

# DHCP Option Set Architecture

Example AWS architecture:

```
VPC
 │
 ├── DHCP Option Set
 │
 ├── Subnet
 │     │
 │     └── EC2 Instance
 │            │
 │            └── Receives DNS + Domain Settings
```

This ensures consistent network configuration across instances.

---

# Steps to Create DHCP Option Set

Steps in AWS Management Console.

1. Open AWS Console
2. Navigate to **VPC Dashboard**
3. Click **DHCP Option Sets**
4. Click **Create DHCP Option Set**
5. Configure options
6. Click **Create**

Example configuration:

| Setting             | Value             |
| ------------------- | ----------------- |
| Domain Name         | example.internal  |
| Domain Name Servers | AmazonProvidedDNS |

---

# Associate DHCP Option Set with VPC

After creating a DHCP option set, it must be associated with a VPC.

Steps:

1. Select DHCP Option Set
2. Click **Actions → Associate DHCP Options Set**
3. Select VPC
4. Click **Save**

Example:

```
DHCP Option Set → VPC
```

All instances in the VPC will now receive these settings.

---

# Common Use Cases of DHCP Option Sets

DHCP option sets are commonly used for:

### Custom DNS Servers

Organizations may use their own DNS servers instead of AWS DNS.

Example:

```
DNS Server → 10.0.0.10
```

---

### Active Directory Integration

Windows environments may require specific DNS configuration for domain services.

---

### Internal Domain Naming

Organizations may define internal domain names.

Example:

```
company.internal
```

---

# Best Practices for DHCP Option Sets

### Use Default AWS DNS When Possible

AWS DNS is optimized for VPC networking and provides better performance.

---

### Configure Custom DNS Only When Required

Custom DNS servers should be used only when necessary.

---

### Test DNS Resolution

Ensure instances can resolve hostnames correctly after configuration changes.

---

# Example Production Architecture

```
VPC
 │
DHCP Option Set
 │
 ├── Public Subnet
 │       └── Web Servers
 │
 └── Private Subnet
         └── Application Servers
```

All instances automatically receive consistent network configuration.

---
# 13.10 Network ACLs (NACLs)
---

A **Network Access Control List (NACL)** is a security layer in AWS that controls inbound and outbound traffic at the **subnet level**. It acts as a firewall that allows or denies specific network traffic based on defined rules.

NACLs provide an additional layer of security in **Amazon Virtual Private Cloud** and are commonly used together with security groups to protect cloud infrastructure.

---

# What is a Network ACL

A **Network ACL (Access Control List)** is a set of rules that determine which traffic is allowed or denied to enter or leave a subnet.

It filters traffic based on:

* IP address
* protocol
* port number

Example architecture:

```
Internet
   │
Internet Gateway
   │
Network ACL
   │
Subnet
   │
EC2 Instance
```

In this setup, the Network ACL checks traffic before it reaches instances in the subnet.

---

# Key Characteristics of NACLs

### Subnet-Level Security

NACLs are applied to **subnets**, not individual instances.

All resources inside the subnet are affected by the same NACL rules.

---

### Stateless Firewall

Network ACLs are **stateless**.

Stateless firewall means that inbound and outbound rules must both be defined explicitly.

Example:

If inbound traffic on port 80 is allowed, the outbound response must also be allowed.

---

### Allow and Deny Rules

Unlike security groups, NACLs support both **allow and deny rules**.

Example:

| Rule             | Action  |
| ---------------- | ------- |
| Allow HTTP       | Allowed |
| Deny specific IP | Blocked |

---

### Rule Evaluation Order

NACL rules are evaluated in **numerical order from lowest to highest**.

Example:

| Rule Number | Type        | Action |
| ----------- | ----------- | ------ |
| 100         | Allow HTTP  | Allow  |
| 200         | Allow HTTPS | Allow  |
| 300         | Deny All    | Deny   |

The first matching rule is applied.

---

# Default Network ACL

Every VPC has a **default Network ACL** automatically created.

Characteristics:

* Allows all inbound traffic
* Allows all outbound traffic

Example rules:

| Rule Number | Type        | Action |
| ----------- | ----------- | ------ |
| 100         | All Traffic | Allow  |

This means resources are not restricted unless custom rules are added.

---

# Custom Network ACL

A **custom NACL** allows administrators to define specific security rules.

Example rules:

Inbound rules:

| Rule Number | Protocol | Port | Source    | Action |
| ----------- | -------- | ---- | --------- | ------ |
| 100         | TCP      | 80   | 0.0.0.0/0 | Allow  |
| 110         | TCP      | 443  | 0.0.0.0/0 | Allow  |
| 120         | TCP      | 22   | My IP     | Allow  |

Outbound rules:

| Rule Number | Protocol | Port | Destination | Action |
| ----------- | -------- | ---- | ----------- | ------ |
| 100         | All      | All  | 0.0.0.0/0   | Allow  |

---

# How NACL Works

Traffic flow with NACL:

```
Internet
   │
Internet Gateway
   │
Network ACL
   │
Subnet
   │
EC2 Instance
```

Traffic process:

1. Request enters subnet.
2. NACL inbound rules are checked.
3. If allowed, traffic reaches instance.
4. Instance sends response.
5. NACL outbound rules are checked.

If outbound rules do not allow the response, communication fails.

---

# NACL Rule Structure

A typical NACL rule contains the following fields:

| Field              | Description      |
| ------------------ | ---------------- |
| Rule Number        | Priority order   |
| Protocol           | TCP / UDP / ICMP |
| Port Range         | Network port     |
| Source/Destination | IP address       |
| Allow/Deny         | Traffic action   |

Example:

| Rule | Protocol | Port | Source    | Action |
| ---- | -------- | ---- | --------- | ------ |
| 100  | TCP      | 80   | 0.0.0.0/0 | Allow  |

---

# Steps to Create a Network ACL

Steps in AWS Management Console:

1. Open AWS Console
2. Navigate to **VPC Dashboard**
3. Click **Network ACLs**
4. Click **Create Network ACL**
5. Select VPC
6. Add inbound and outbound rules

Example configuration:

| Setting | Value       |
| ------- | ----------- |
| VPC     | 10.0.0.0/16 |

---

# Associate NACL with Subnet

After creating a NACL, it must be associated with a subnet.

Steps:

1. Select Network ACL
2. Click **Subnet Associations**
3. Choose subnet
4. Click **Save**

Example:

```
Network ACL → Subnet
```

---

# NACL vs Security Groups

Both NACLs and security groups provide security, but they operate differently.

| Feature          | NACL         | Security Group      |
| ---------------- | ------------ | ------------------- |
| Level            | Subnet       | Instance            |
| Firewall Type    | Stateless    | Stateful            |
| Allow/Deny Rules | Yes          | Allow only          |
| Rule Evaluation  | Number order | All rules evaluated |

In most architectures:

* NACL provides **coarse security control**
* Security groups provide **fine-grained instance security**

---

# NACL Architecture Example

Example AWS architecture:

```
Internet
   │
Internet Gateway
   │
Public Subnet
   │
Network ACL
   │
EC2 Web Server
```

Private subnet architecture:

```
Public Subnet
   │
Application Load Balancer
   │
Private Subnet
   │
Network ACL
   │
Application Servers
```

---

# Best Practices for NACL

### Use NACL for Additional Security Layer

Combine NACL with security groups for stronger protection.

---

### Use Low Rule Numbers for Important Rules

Lower rule numbers are evaluated first.

Example:

```
100 → Allow HTTP
110 → Allow HTTPS
120 → Allow SSH
```

---

### Avoid Overly Complex Rules

Complex rule sets make troubleshooting difficult.

---

### Restrict SSH Access

Limit SSH access to specific IP addresses.

Example:

```
Port: 22
Source: My IP
```

---

# Real Production Architecture

```
Internet
   │
Internet Gateway
   │
Public Subnet
   │
Network ACL
   │
Load Balancer
   │
Private Subnet
   │
Network ACL
   │
Application Servers
```

This architecture provides:

* layered security
* controlled network access
* protection against unauthorized traffic

---
# 13.11 Security Groups
---

A **Security Group** is a virtual firewall that controls inbound and outbound traffic for AWS resources such as EC2 instances. It is one of the primary security mechanisms used to protect cloud infrastructure in AWS.

Security groups operate at the **instance level** and define rules that allow traffic to reach the resource.

Security groups are an important networking security feature of **Amazon Virtual Private Cloud**.

---

# What is a Security Group

A **Security Group** is a set of rules that controls network traffic to and from an AWS resource.

It filters traffic based on:

* Protocol (TCP, UDP, ICMP)
* Port number
* Source or destination IP address

Example architecture:

```
Internet
   │
Internet Gateway
   │
Security Group
   │
EC2 Instance
```

The security group acts like a firewall that allows only specific traffic to reach the instance.

---

# Key Characteristics of Security Groups

### Instance-Level Firewall

Security groups are applied directly to resources such as:

* EC2 instances
* Load balancers
* databases

Each instance can have one or multiple security groups.

---

### Stateful Firewall

Security groups are **stateful firewalls**.

Stateful firewall means that if inbound traffic is allowed, the response traffic is automatically allowed.

Example:

```
Inbound rule → Allow HTTP
Response → Automatically allowed
```

You do not need to create separate outbound rules for responses.

---

### Allow Rules Only

Security groups allow **only allow rules**.

They do not support explicit deny rules.

Traffic that is not allowed by any rule is automatically blocked.

---

### Default Deny Behavior

If no rule allows the traffic, it is denied by default.

Example:

| Traffic             | Result  |
| ------------------- | ------- |
| Port 80 allowed     | Allowed |
| Port 22 not allowed | Blocked |

---

# Security Group Rule Components

Each security group rule includes:

| Component            | Description                |
| -------------------- | -------------------------- |
| Protocol             | TCP, UDP, ICMP             |
| Port Range           | Network port               |
| Source / Destination | IP range or security group |
| Description          | Rule explanation           |

Example rule:

| Type | Protocol | Port | Source    |
| ---- | -------- | ---- | --------- |
| HTTP | TCP      | 80   | 0.0.0.0/0 |

---

# Inbound Rules

Inbound rules control traffic entering the instance.

Example inbound rules:

| Type  | Protocol | Port | Source    |
| ----- | -------- | ---- | --------- |
| SSH   | TCP      | 22   | My IP     |
| HTTP  | TCP      | 80   | 0.0.0.0/0 |
| HTTPS | TCP      | 443  | 0.0.0.0/0 |

Explanation:

* SSH allows remote login
* HTTP allows web traffic
* HTTPS allows secure web traffic

---

# Outbound Rules

Outbound rules control traffic leaving the instance.

Default outbound rule:

| Type        | Destination |
| ----------- | ----------- |
| All Traffic | 0.0.0.0/0   |

This allows instances to communicate with external networks.

---

# Default Security Group

Every VPC automatically includes a **default security group**.

Characteristics:

* Allows inbound traffic from resources within the same security group
* Allows all outbound traffic

Example:

| Rule             | Description            |
| ---------------- | ---------------------- |
| Allow SG traffic | Internal communication |

This allows instances in the same security group to communicate.

---

# Security Group Architecture Example

Example AWS architecture:

```
Internet
   │
Internet Gateway
   │
Public Subnet
   │
Security Group
   │
EC2 Web Server
```

Example rules:

| Type  | Port | Source    |
| ----- | ---- | --------- |
| HTTP  | 80   | 0.0.0.0/0 |
| HTTPS | 443  | 0.0.0.0/0 |
| SSH   | 22   | My IP     |

---

# Security Groups for Multi-Tier Architecture

In production architectures, different security groups are used for different application layers.

Example:

```
Internet
   │
Load Balancer SG
   │
Application Server SG
   │
Database SG
```

Example rules:

### Load Balancer Security Group

| Port | Source   |
| ---- | -------- |
| 80   | Internet |
| 443  | Internet |

---

### Application Server Security Group

| Port | Source           |
| ---- | ---------------- |
| 8080 | Load Balancer SG |

---

### Database Security Group

| Port | Source                |
| ---- | --------------------- |
| 3306 | Application Server SG |

This design improves security by limiting access between layers.

---

# Steps to Create Security Group

Steps in AWS Management Console:

1. Open AWS Console
2. Navigate to **VPC Dashboard**
3. Click **Security Groups**
4. Click **Create Security Group**
5. Enter name and description
6. Select VPC
7. Add inbound and outbound rules
8. Click **Create Security Group**

Example configuration:

| Setting | Value          |
| ------- | -------------- |
| Name    | Web-SG         |
| VPC     | Production VPC |

---

# Attach Security Group to Instance

Security groups can be attached when launching an instance or modified later.

Steps:

1. Select EC2 instance
2. Click **Actions → Security → Change Security Groups**
3. Select security group
4. Save

Example:

```
EC2 Instance → Web-SG
```

---

# Security Group Best Practices

### Restrict SSH Access

Allow SSH access only from trusted IP addresses.

Example:

```
Port: 22
Source: My IP
```

---

### Use Security Group Referencing

Allow traffic from another security group instead of open IP ranges.

Example:

```
Application SG → Database SG
```

---

### Follow Least Privilege Principle

Allow only the necessary ports and traffic required by the application.

---

### Separate Security Groups by Role

Example:

```
Web-SG
App-SG
DB-SG
```

This improves security and management.

---

# Security Group vs Network ACL

| Feature         | Security Group | Network ACL  |
| --------------- | -------------- | ------------ |
| Level           | Instance       | Subnet       |
| Firewall Type   | Stateful       | Stateless    |
| Allow Rules     | Yes            | Allow + Deny |
| Rule Evaluation | All rules      | Number order |

Both security groups and NACLs are used together for layered security.

---

# Real Production Architecture

```
Internet
   │
Internet Gateway
   │
Public Subnet
   │
Load Balancer
   │
Security Group
   │
Private Subnet
   │
Application Servers
   │
Database Servers
```

This architecture provides:

* secure traffic filtering
* layered security model
* controlled access between application layers

---
# 13.12 VPC Peering

VPC Peering is a networking feature that allows two VPCs to communicate with each other privately using their private IP addresses. This enables resources in different VPCs to interact as if they were within the same network.

VPC Peering is commonly used in multi-VPC architectures for sharing services, connecting environments, and building scalable cloud networks.

This feature is part of **Amazon Virtual Private Cloud**.

---

# What is VPC Peering

**VPC Peering** is a connection between two VPCs that allows them to route traffic using private IP addresses.

Once the peering connection is established, resources such as EC2 instances in both VPCs can communicate with each other.

Example architecture:

```
VPC A (10.0.0.0/16)
      │
      │  VPC Peering Connection
      │
VPC B (192.168.0.0/16)
```

Instances in both VPCs can communicate through private networking.

Example communication:

```
EC2 (10.0.1.10)  ↔  EC2 (192.168.1.10)
```

No internet gateway or NAT gateway is required.

---

# Why VPC Peering is Required

Organizations often create multiple VPCs for different environments such as development, testing, and production.

Example environments:

```
VPC 1 → Development
VPC 2 → Testing
VPC 3 → Production
```

Sometimes services in one VPC need to communicate with services in another VPC.

Example:

* Application servers in one VPC need access to a database in another VPC.
* Microservices running in different VPCs need to communicate.

VPC Peering provides a secure and private connection between these networks.

---

# Key Characteristics of VPC Peering

### Private Communication

Traffic between VPCs uses private IP addresses and does not traverse the public internet.

---

### High Performance

VPC Peering provides high bandwidth and low latency communication because traffic remains within AWS infrastructure.

---

### No Single Point of Failure

AWS manages the infrastructure for the peering connection.

---

### Regional or Cross-Region

VPC Peering supports:

* same-region VPC peering
* cross-region VPC peering

---

# Types of VPC Peering

## Same Region Peering

Both VPCs exist in the same AWS region.

Example:

```
Region: ap-south-1

VPC A (10.0.0.0/16)
       │
       │ Peering
       │
VPC B (172.16.0.0/16)
```

This is the most common configuration.

---

## Cross Region Peering

VPCs exist in different AWS regions.

Example:

```
Region: ap-south-1
VPC A

      │
      │ Peering
      │

Region: us-east-1
VPC B
```

Used for global architectures and disaster recovery.

---

# VPC Peering Architecture

Example architecture:

```
VPC A (10.0.0.0/16)
   │
   │  VPC Peering Connection
   │
VPC B (192.168.0.0/16)
```

Example instances:

```
EC2 Instance (10.0.1.15)
         │
         │
EC2 Instance (192.168.1.20)
```

Both instances can communicate directly using private IPs.

---

# Steps to Create VPC Peering

Steps in AWS Management Console:

1. Open AWS Console
2. Navigate to **VPC Dashboard**
3. Click **Peering Connections**
4. Click **Create Peering Connection**
5. Select requester VPC
6. Select accepter VPC
7. Click **Create**

Example configuration:

| Setting       | Value |
| ------------- | ----- |
| Requester VPC | VPC-A |
| Accepter VPC  | VPC-B |

---

# Accept VPC Peering Request

After creating the request, the owner of the accepter VPC must approve the connection.

Steps:

1. Open VPC Dashboard
2. Go to **Peering Connections**
3. Select pending request
4. Click **Accept Request**

The peering connection becomes active.

---

# Update Route Tables

After creating the peering connection, route tables must be updated.

Example:

VPC A Route Table:

| Destination    | Target             |
| -------------- | ------------------ |
| 192.168.0.0/16 | Peering Connection |

VPC B Route Table:

| Destination | Target             |
| ----------- | ------------------ |
| 10.0.0.0/16 | Peering Connection |

This allows traffic between both VPCs.

---

# VPC Peering Limitations

VPC Peering has some important limitations.

### No Transitive Peering

If:

```
VPC A ↔ VPC B
VPC B ↔ VPC C
```

Then:

```
VPC A cannot communicate with VPC C
```

This is called **no transitive routing**.

---

### Overlapping CIDR Blocks Not Allowed

Both VPCs must have **non-overlapping CIDR ranges**.

Example:

Allowed:

```
VPC A → 10.0.0.0/16
VPC B → 192.168.0.0/16
```

Not allowed:

```
VPC A → 10.0.0.0/16
VPC B → 10.0.1.0/24
```

---

# Security Considerations

Security groups and NACLs still control traffic between VPCs.

Example:

| Layer           | Control        |
| --------------- | -------------- |
| Security Groups | Instance level |
| Network ACL     | Subnet level   |

This ensures secure communication between VPCs.

---

# Real Production Architecture Example

```
Production VPC
     │
     │
VPC Peering
     │
Shared Services VPC
     │
     │
Database Servers
```

Example use cases:

* shared database services
* centralized logging infrastructure
* monitoring services

---

# Best Practices for VPC Peering

### Use Clear CIDR Planning

Ensure VPC CIDR ranges do not overlap.

---

### Update Route Tables Carefully

Both VPCs must have correct routing rules.

---

### Use Security Groups for Access Control

Restrict traffic between VPCs using security groups.

---

### Use for Small Architectures

For large multi-VPC architectures, AWS **Transit Gateway** is recommended instead of multiple peering connections.

---

# VPC Peering Architecture Example (Production)

```
VPC A (Application VPC)
        │
        │
VPC Peering
        │
        │
VPC B (Database VPC)
```

This architecture provides:

* private communication
* secure resource sharing
* scalable multi-VPC design

---
# 13.13 Transit Gateway
---

A **Transit Gateway** is a networking service that allows you to connect multiple VPCs and on-premises networks through a **central hub**. It simplifies complex network architectures where many VPCs need to communicate with each other.

Instead of creating multiple VPC peering connections, Transit Gateway provides a **hub-and-spoke network architecture**, making it easier to manage large cloud environments.

Transit Gateway is a networking feature of **Amazon Virtual Private Cloud**.

---

# What is Transit Gateway

A **Transit Gateway (TGW)** acts as a **central router** that connects multiple VPCs, VPN connections, and Direct Connect gateways.

Example architecture:

```
                VPC-A
                   │
                   │
VPC-B ───── Transit Gateway ───── VPC-C
                   │
                   │
                VPC-D
```

In this architecture:

* All VPCs connect to the Transit Gateway.
* Communication between VPCs happens through the central gateway.

This model greatly simplifies networking compared to multiple VPC peering connections.

---

# Why Transit Gateway is Required

When organizations use multiple VPCs, networking becomes complex.

Example with VPC Peering:

```
VPC-A ↔ VPC-B
VPC-A ↔ VPC-C
VPC-B ↔ VPC-C
```

This creates a **mesh network** that becomes difficult to manage.

With Transit Gateway:

```
VPC-A
   │
VPC-B ── Transit Gateway ── VPC-C
   │
VPC-D
```

Benefits:

* simpler architecture
* centralized routing
* easier management

---

# Hub and Spoke Architecture

Transit Gateway follows a **hub-and-spoke network design**.

Hub and Spoke Network Topology is a model where a central hub connects multiple networks.

Example:

```
            VPC-A
              │
              │
VPC-B ── Transit Gateway ── VPC-C
              │
              │
            VPC-D
```

The Transit Gateway acts as the **hub**, and VPCs act as **spokes**.

---

# Key Features of Transit Gateway

### Centralized Connectivity

All networks connect to a single gateway, simplifying network design.

---

### High Scalability

Transit Gateway can support **thousands of VPC connections**.

---

### High Performance

Traffic between VPCs flows through AWS’s private network infrastructure.

---

### Hybrid Cloud Connectivity

Transit Gateway can connect:

* multiple VPCs
* on-premises networks via VPN
* dedicated connections via Direct Connect

---

# Transit Gateway Architecture

Example architecture:

```
On-Premise Data Center
        │
        │ VPN
        │
    Transit Gateway
        │
   ┌────┼────┐
   │    │    │
 VPC-A VPC-B VPC-C
```

This architecture connects both cloud and on-premise networks.

---

# Components of Transit Gateway

### Transit Gateway

Central routing hub connecting multiple networks.

---

### Attachments

Attachments connect resources to the Transit Gateway.

Examples:

| Attachment Type           | Purpose                      |
| ------------------------- | ---------------------------- |
| VPC Attachment            | Connect VPC                  |
| VPN Attachment            | Connect on-premise VPN       |
| Direct Connect Attachment | Dedicated network connection |

---

### Route Tables

Transit Gateway uses route tables to control traffic between connected networks.

Example:

| Destination   | Target |
| ------------- | ------ |
| 10.0.0.0/16   | VPC-A  |
| 172.16.0.0/16 | VPC-B  |

---

# Transit Gateway Traffic Flow

Example traffic flow:

```
EC2 Instance (VPC-A)
        │
        │
Transit Gateway
        │
        │
EC2 Instance (VPC-B)
```

Traffic travels through the Transit Gateway between VPCs.

---

# Steps to Create Transit Gateway

Steps in AWS Management Console:

1. Open AWS Console
2. Navigate to **VPC Dashboard**
3. Click **Transit Gateways**
4. Click **Create Transit Gateway**
5. Configure settings
6. Click **Create**

Example configuration:

| Setting | Value          |
| ------- | -------------- |
| Name    | Production-TGW |
| ASN     | Default        |

---

# Attach VPC to Transit Gateway

Steps:

1. Go to **Transit Gateway Attachments**
2. Click **Create Attachment**
3. Select VPC
4. Select subnet
5. Click **Create Attachment**

Example:

```
Transit Gateway → VPC-A
Transit Gateway → VPC-B
```

---

# Update Route Tables

After attaching VPCs, route tables must be updated.

Example:

VPC Route Table:

| Destination   | Target          |
| ------------- | --------------- |
| 172.16.0.0/16 | Transit Gateway |

Transit Gateway Route Table:

| Destination   | Attachment |
| ------------- | ---------- |
| 10.0.0.0/16   | VPC-A      |
| 172.16.0.0/16 | VPC-B      |

---

# Transit Gateway vs VPC Peering

| Feature            | Transit Gateway | VPC Peering   |
| ------------------ | --------------- | ------------- |
| Architecture       | Hub and Spoke   | Mesh          |
| Scalability        | Very High       | Limited       |
| Transitive Routing | Supported       | Not Supported |
| Management         | Centralized     | Distributed   |

Transit Gateway is recommended for **large enterprise architectures**.

---

# Real Production Architecture Example

```
              On-Premise
                   │
                   │ VPN
                   │
            Transit Gateway
             │      │      │
             │      │      │
         VPC-App  VPC-DB  VPC-Logging
```

Example use cases:

* centralized networking
* hybrid cloud connectivity
* shared services VPC
* large multi-VPC architectures

---

# Best Practices for Transit Gateway

### Use Hub-and-Spoke Design

Centralize connectivity using Transit Gateway.

---

### Plan CIDR Ranges Carefully

Avoid overlapping CIDR blocks across VPCs.

---

### Use Route Tables for Traffic Control

Control communication between VPCs using Transit Gateway route tables.

---

### Monitor Network Traffic

Use monitoring tools such as **Amazon CloudWatch** to track network performance.

---

# Production Architecture Example

```
Internet
   │
Internet Gateway
   │
Public Subnet
   │
Transit Gateway
   │
Private Subnets
   │
Application Services
```

Benefits:

* centralized network management
* scalable architecture
* secure VPC communication

---
# 13.14 VPN (Virtual Private Network)
---

A **Virtual Private Network (VPN)** allows secure communication between an on-premises network (such as a company data center) and AWS cloud resources. It creates an encrypted connection over the internet so that private network traffic can safely travel between the two environments.

VPN connectivity is widely used in hybrid cloud architectures built with **Amazon Virtual Private Cloud**.

---

# What is a VPN

A **VPN** creates a **secure and encrypted tunnel** between two networks.

This tunnel allows private data to travel through the public internet while remaining protected from unauthorized access.

Example:

```
On-Premise Network
       │
       │  Encrypted Tunnel
       │
AWS VPC
```

In this setup:

* company servers in the data center
* AWS cloud resources

can communicate securely.

---

# Why VPN is Required

Organizations often need to connect their existing infrastructure with cloud services.

Common scenarios include:

* migrating applications from on-premise to AWS
* hybrid cloud environments
* secure remote network access
* backup and disaster recovery systems

VPN enables these connections without exposing internal systems to the public internet.

---

# Types of AWS VPN

AWS provides two main VPN solutions.

## 1 Site-to-Site VPN

A **Site-to-Site VPN** connects an entire on-premise network to an AWS VPC.

Example architecture:

```
On-Premise Network
        │
        │ VPN Tunnel
        │
Virtual Private Gateway
        │
        │
VPC
```

All machines in the on-premise network can communicate with resources inside the VPC.

Typical use cases:

* hybrid cloud connectivity
* enterprise networks
* data center integration

---

## 2 Client VPN

A **Client VPN** allows individual users to securely connect to AWS resources.

Example architecture:

```
User Laptop
      │
      │ Secure VPN Connection
      │
Client VPN Endpoint
      │
      │
VPC Resources
```

This is commonly used for:

* remote employees
* secure developer access
* private application access

---

# Components of AWS Site-to-Site VPN

A typical AWS VPN setup contains the following components.

## Customer Gateway

Represents the **on-premise VPN device** such as a firewall or router.

Example devices:

* Cisco router
* Fortinet firewall
* Palo Alto firewall

---

## Virtual Private Gateway

A **Virtual Private Gateway** is an AWS component attached to a VPC that allows VPN connections.

It acts as the AWS side of the VPN tunnel.

Example architecture:

```
On-Premise Router
        │
Customer Gateway
        │
VPN Tunnel
        │
Virtual Private Gateway
        │
VPC
```

---

## VPN Connection

The encrypted connection between the customer gateway and virtual private gateway.

It typically includes **two VPN tunnels** for high availability.

---

# VPN Architecture Example

Example hybrid cloud architecture:

```
On-Premise Data Center
       │
Customer Gateway
       │
VPN Tunnel
       │
Virtual Private Gateway
       │
VPC
       │
EC2 Instances
```

This architecture allows internal company systems to access AWS resources securely.

---

# VPN Traffic Flow

Traffic flow between on-premise network and AWS.

```
On-Premise Server
        │
Customer Gateway
        │
Encrypted VPN Tunnel
        │
Virtual Private Gateway
        │
Route Table
        │
EC2 Instance
```

All traffic passing through the VPN is encrypted.

---

# Steps to Create Site-to-Site VPN

Steps in AWS Management Console.

### Step 1 Create Customer Gateway

1. Open AWS Console
2. Navigate to **VPC Dashboard**
3. Click **Customer Gateways**
4. Click **Create Customer Gateway**

Example configuration:

| Setting    | Value               |
| ---------- | ------------------- |
| IP Address | Public IP of router |
| Routing    | Static / Dynamic    |

---

### Step 2 Create Virtual Private Gateway

1. Go to **Virtual Private Gateways**
2. Click **Create Virtual Private Gateway**
3. Attach it to the VPC

Example:

```
Virtual Private Gateway → VPC
```

---

### Step 3 Create VPN Connection

1. Go to **Site-to-Site VPN Connections**
2. Click **Create VPN Connection**
3. Select Customer Gateway
4. Select Virtual Private Gateway

Example:

| Setting                 | Value             |
| ----------------------- | ----------------- |
| Customer Gateway        | On-premise router |
| Virtual Private Gateway | Attached to VPC   |

---

### Step 4 Update Route Tables

Add route in VPC route table.

Example:

| Destination    | Target                  |
| -------------- | ----------------------- |
| 192.168.0.0/16 | Virtual Private Gateway |

This allows traffic between the VPC and on-premise network.

---

# VPN vs Direct Connect

| Feature         | VPN       | Direct Connect     |
| --------------- | --------- | ------------------ |
| Connection Type | Internet  | Dedicated network  |
| Cost            | Lower     | Higher             |
| Performance     | Moderate  | High               |
| Security        | Encrypted | Private connection |

VPN is typically used for **hybrid cloud connectivity**, while Direct Connect is used for high-performance enterprise networking.

---

# Best Practices for AWS VPN

### Use Two VPN Tunnels

AWS automatically creates two tunnels for redundancy.

---

### Use Dynamic Routing

Dynamic routing using **BGP** improves network management.

---

### Monitor VPN Health

Use monitoring tools such as **Amazon CloudWatch** to monitor tunnel status.

---

### Plan Network CIDR Carefully

Avoid overlapping IP ranges between on-premise network and AWS VPC.

---

# Real Production Architecture

```
Corporate Data Center
        │
Customer Gateway
        │
VPN Tunnel
        │
Virtual Private Gateway
        │
Transit Gateway
        │
Multiple VPCs
```

This architecture provides:

* hybrid cloud connectivity
* secure network communication
* scalable enterprise infrastructure

---
# 13.15 VPC Endpoints
---

A **VPC Endpoint** allows resources inside a VPC to privately connect to AWS services without using the public internet. This means traffic stays within the AWS network and does not pass through an Internet Gateway, NAT Gateway, or VPN.

VPC Endpoints improve **security, performance, and network efficiency** in cloud architectures built using **Amazon Virtual Private Cloud**.

---

# What is a VPC Endpoint

A **VPC Endpoint** is a private connection between a VPC and supported AWS services.

Normally when a private instance needs to access AWS services like S3, the traffic goes through the internet.

Example without VPC Endpoint:

```
EC2 Instance
     │
NAT Gateway
     │
Internet
     │
AWS Service (S3)
```

With a VPC Endpoint, traffic stays inside AWS:

```
EC2 Instance
     │
VPC Endpoint
     │
AWS Service (S3)
```

This improves both security and performance.

---

# Why VPC Endpoints are Required

In many architectures, instances inside **private subnets** need to access AWS services such as:

* S3
* DynamoDB
* EC2 APIs
* CloudWatch
* Systems Manager

Without VPC endpoints, private instances must use:

* NAT Gateway
* Internet Gateway

This introduces additional cost and exposes traffic to the public internet.

VPC endpoints solve this by providing **private connectivity to AWS services**.

---

# Types of VPC Endpoints

AWS provides two main types of VPC endpoints.

---

# 1 Gateway Endpoint

A **Gateway Endpoint** is used to privately connect a VPC to specific AWS services.

Currently supported services:

* Amazon S3
* Amazon DynamoDB

Gateway endpoints are implemented using **route tables**.

Example architecture:

```
VPC
 │
 │
Gateway Endpoint
 │
 │
Amazon S3
```

Traffic between the VPC and S3 stays inside the AWS network.

Example route table entry:

| Destination    | Target           |
| -------------- | ---------------- |
| S3 Prefix List | Gateway Endpoint |

---

# 2 Interface Endpoint

An **Interface Endpoint** provides private connectivity using an **Elastic Network Interface (ENI)**.

It creates a private IP address inside the subnet.

Interface endpoints support many AWS services.

Examples:

* CloudWatch
* EC2
* SNS
* SQS
* Systems Manager

Example architecture:

```
VPC
 │
 │
Interface Endpoint (ENI)
 │
 │
AWS Service
```

This allows resources inside the VPC to access AWS services using private IP addresses.

---

# Gateway Endpoint vs Interface Endpoint

| Feature            | Gateway Endpoint | Interface Endpoint        |
| ------------------ | ---------------- | ------------------------- |
| Connection Method  | Route Table      | Elastic Network Interface |
| Supported Services | S3, DynamoDB     | Many AWS services         |
| Cost               | Free             | Hourly charges            |
| Security Control   | Endpoint Policy  | Security Groups           |

---

# VPC Endpoint Architecture Example

Example AWS architecture:

```
Private Subnet
      │
EC2 Instance
      │
VPC Endpoint
      │
Amazon S3
```

In this setup:

* Private instance accesses S3
* No internet connection required

---

# Gateway Endpoint Architecture

Example with S3:

```
VPC
 │
Route Table
 │
Gateway Endpoint
 │
Amazon S3
```

Traffic flows directly between VPC and S3.

---

# Interface Endpoint Architecture

Example with CloudWatch:

```
VPC
 │
Private Subnet
 │
Interface Endpoint (ENI)
 │
AWS Service
```

Each interface endpoint receives a private IP address.

---

# Steps to Create a VPC Endpoint

Steps in AWS Management Console.

1. Open AWS Console
2. Navigate to **VPC Dashboard**
3. Click **Endpoints**
4. Click **Create Endpoint**

Example configuration:

| Setting          | Value          |
| ---------------- | -------------- |
| Service Category | AWS Services   |
| Service Name     | S3             |
| VPC              | Production VPC |

---

# Configure Route Tables

For gateway endpoints, update the route table.

Example:

| Destination | Target           |
| ----------- | ---------------- |
| S3 Prefix   | Gateway Endpoint |

This ensures S3 traffic goes through the endpoint.

---

# Configure Security Groups

Interface endpoints support security groups.

Example rules:

| Type  | Port | Source   |
| ----- | ---- | -------- |
| HTTPS | 443  | VPC CIDR |

This controls which resources can access the endpoint.

---

# Benefits of VPC Endpoints

### Improved Security

Traffic remains inside AWS private network.

---

### Reduced Internet Exposure

No need for Internet Gateway or NAT Gateway.

---

### Lower Cost

Gateway endpoints eliminate NAT gateway data charges.

---

### Improved Performance

Direct connectivity to AWS services reduces latency.

---

# Best Practices for VPC Endpoints

### Use Gateway Endpoints for S3

This reduces NAT gateway traffic and costs.

---

### Use Interface Endpoints for AWS APIs

This ensures private access to AWS services.

---

### Restrict Access Using Endpoint Policies

Use policies to control which resources can use the endpoint.

---

### Deploy Endpoints in Multiple AZs

Improves high availability.

---

# Real Production Architecture

```
Private Subnet
     │
Application Servers
     │
VPC Endpoint
     │
Amazon S3
     │
Data Storage
```

Another example:

```
Private Subnet
     │
Application Servers
     │
Interface Endpoint
     │
AWS Services (CloudWatch, SQS)
```

Benefits:

* secure AWS service access
* no public internet exposure
* optimized network performance

---
# 13.16 VPC Best Practices
---

Designing a VPC correctly is very important for building **secure, scalable, and highly available cloud infrastructure**. Following best practices ensures better performance, security, and easier network management in AWS environments.

These practices apply when designing networks using **Amazon Virtual Private Cloud**.

---

# Plan CIDR Blocks Carefully

CIDR planning is one of the most important steps when designing a VPC.

Choose a CIDR block that provides enough IP addresses for future expansion.

Example recommended CIDR:

```
10.0.0.0/16
```

Benefits of large CIDR blocks:

* supports thousands of instances
* allows multiple subnet creation
* avoids network redesign later

Also ensure CIDR ranges do **not overlap** with:

* other VPCs
* on-premise networks
* VPN networks

---

# Use Multiple Availability Zones

Deploy resources across multiple **Availability Zone** to increase reliability and availability.

Example architecture:

```
VPC (10.0.0.0/16)

AZ-1
 ├── Public Subnet
 └── Private Subnet

AZ-2
 ├── Public Subnet
 └── Private Subnet
```

Benefits:

* fault tolerance
* disaster recovery
* high availability

If one Availability Zone fails, applications can continue running in another zone.

---

# Separate Public and Private Subnets

A good VPC architecture separates resources based on their exposure to the internet.

Example design:

```
Public Subnet
   │
Load Balancer
   │
Private Subnet
   │
Application Servers
   │
Private Subnet
   │
Database Servers
```

Typical placement:

| Subnet Type     | Resources                    |
| --------------- | ---------------------------- |
| Public Subnet   | Load Balancers, Bastion Host |
| Private Subnet  | Application Servers          |
| Isolated Subnet | Databases                    |

This improves security by restricting direct internet access to sensitive resources.

---

# Use NAT Gateway for Private Instances

Private instances should not have direct internet access.

Instead use a NAT Gateway placed in a public subnet.

Example architecture:

```
Internet
   │
Internet Gateway
   │
Public Subnet
   │
NAT Gateway
   │
Private Subnet
   │
Application Servers
```

Benefits:

* private instances can download updates
* inbound internet access is blocked

---

# Implement Layered Security

AWS networking security should use multiple layers.

Common security layers:

| Layer          | Security Tool   |
| -------------- | --------------- |
| Instance Level | Security Groups |
| Subnet Level   | Network ACL     |
| Network Level  | Route Tables    |

Example layered architecture:

```
Internet
   │
Security Group
   │
Network ACL
   │
EC2 Instance
```

This defense-in-depth approach improves security.

---

# Use Least Privilege Security Rules

Security rules should allow only required traffic.

Example security group rules:

| Type  | Port | Source        |
| ----- | ---- | ------------- |
| HTTP  | 80   | 0.0.0.0/0     |
| HTTPS | 443  | 0.0.0.0/0     |
| SSH   | 22   | Admin IP only |

Avoid open rules such as:

```
0.0.0.0/0 for SSH
```

because they expose infrastructure to the internet.

---

# Use Private Access to AWS Services

Use **VPC Endpoints** to access AWS services privately.

Example architecture:

```
Private Subnet
     │
Application Server
     │
VPC Endpoint
     │
Amazon S3
```

Benefits:

* traffic stays inside AWS network
* improves security
* reduces NAT Gateway cost

---

# Monitor Network Traffic

Monitoring network activity helps detect issues and security threats.

Use tools such as:

* **Amazon CloudWatch**
* **AWS VPC Flow Logs**

These tools allow you to analyze:

* traffic patterns
* rejected connections
* network performance

---

# Use Consistent Naming and Tagging

Use proper naming conventions for networking resources.

Example:

| Resource       | Name Example        |
| -------------- | ------------------- |
| VPC            | Production-VPC      |
| Subnet         | Public-Subnet-AZ1   |
| Route Table    | Private-Route-Table |
| Security Group | Web-SG              |

Tagging resources helps in:

* cost management
* infrastructure organization
* automation tools

---

# Design for Scalability

Your VPC should support future growth.

Best practices:

* use large CIDR ranges
* create additional subnets for future services
* design modular network architecture

Example scalable design:

```
VPC (10.0.0.0/16)

 ├── Web Subnets
 ├── App Subnets
 ├── Database Subnets
 └── Future Services
```

---

# Use Transit Gateway for Large Architectures

When connecting many VPCs, use **AWS Transit Gateway** instead of multiple VPC peering connections.

Example architecture:

```
           Transit Gateway
           │     │     │
        VPC-A  VPC-B  VPC-C
```

This simplifies routing and network management.

---

# Backup and Disaster Recovery Planning

Design the network to support disaster recovery.

Example strategies:

* multi-AZ deployment
* cross-region replication
* redundant VPN connections

Example architecture:

```
Region 1
   │
Primary VPC

Region 2
   │
Backup VPC
```

---

# Real Production VPC Architecture

Typical enterprise architecture:

```
Internet
   │
Internet Gateway
   │
Public Subnets
   │
Application Load Balancer
   │
Private Application Subnets
   │
Application Servers
   │
Private Database Subnets
   │
Database Cluster
```

Features:

* high availability
* network isolation
* scalable architecture
* strong security controls

---

# Summary

Following VPC best practices ensures:

* secure networking
* scalable infrastructure
* high availability
* simplified network management

A well-designed VPC architecture forms the **foundation of a reliable AWS cloud environment**.

---
# 13.17 Real Production VPC Architecture
---

A **production VPC architecture** is designed to support real-world applications with high availability, scalability, and strong security. Modern cloud applications usually follow a **multi-tier architecture** where different application layers are isolated into separate subnets.

This architecture is built using services within **Amazon Virtual Private Cloud** and other AWS compute and database services.

A typical production VPC includes:

* Public Subnets
* Private Application Subnets
* Private Database Subnets
* Internet Gateway
* NAT Gateway
* Load Balancer
* Security Groups and Network ACLs

---

# Production VPC Architecture Overview

A common real-world architecture looks like this:

```id="k32v31"
                      Internet
                         │
                  Internet Gateway
                         │
                ┌────────┴────────┐
                │                 │
        Public Subnet AZ-1   Public Subnet AZ-2
                │                 │
      Application Load Balancer
                │
        ┌───────┴────────┐
        │                │
 Private App Subnet   Private App Subnet
        │                │
   Application Servers (Auto Scaling)
        │
        ┌───────────────┐
        │               │
 Private DB Subnet   Private DB Subnet
        │               │
      Database Cluster (RDS)
```

This architecture ensures:

* secure infrastructure
* high availability
* scalable application deployment

---

# Components of Production VPC Architecture

## VPC

The VPC acts as the **network boundary** for all cloud resources.

Example CIDR:

```
10.0.0.0/16
```

This CIDR block allows enough IP addresses for large infrastructures.

---

## Public Subnets

Public subnets contain resources that must communicate directly with the internet.

Example resources:

* Application Load Balancer
* Bastion Host
* NAT Gateway

Example CIDR:

| Subnet             | CIDR        |
| ------------------ | ----------- |
| Public Subnet AZ-1 | 10.0.1.0/24 |
| Public Subnet AZ-2 | 10.0.2.0/24 |

Public subnets have a route to the **Internet Gateway**.

---

## Private Application Subnets

Application servers are deployed in private subnets to prevent direct internet access.

Example resources:

* application servers
* backend APIs
* container workloads

Example CIDR:

| Subnet          | CIDR         |
| --------------- | ------------ |
| App Subnet AZ-1 | 10.0.10.0/24 |
| App Subnet AZ-2 | 10.0.11.0/24 |

These subnets use **NAT Gateway** for outbound internet access.

---

## Private Database Subnets

Databases are placed in isolated subnets with no direct internet access.

Example services:

* Amazon RDS
* database clusters

Example CIDR:

| Subnet         | CIDR         |
| -------------- | ------------ |
| DB Subnet AZ-1 | 10.0.20.0/24 |
| DB Subnet AZ-2 | 10.0.21.0/24 |

These subnets usually do not have internet routes.

---

# Internet Gateway

An **Internet Gateway** allows communication between public subnets and the internet.

Traffic flow:

```
Internet
   │
Internet Gateway
   │
Public Subnet
```

Only resources with **public IP addresses** can communicate with the internet.

---

# NAT Gateway

Private instances need internet access for tasks such as:

* downloading updates
* installing packages

A NAT Gateway enables this while keeping instances private.

Example:

```
Private Instance
     │
NAT Gateway
     │
Internet Gateway
     │
Internet
```

NAT Gateway is usually deployed in a public subnet.

---

# Load Balancer

Production systems use a load balancer to distribute traffic across multiple servers.

Example:

```
Internet
   │
Application Load Balancer
   │
Application Servers
```

Benefits:

* load distribution
* fault tolerance
* improved performance

---

# Auto Scaling

Application servers are usually deployed using **Auto Scaling groups**.

Example architecture:

```
Application Load Balancer
        │
Auto Scaling Group
        │
EC2 Instances
```

Benefits:

* automatic scaling based on demand
* improved reliability
* cost optimization

---

# Security Architecture

Security is implemented using multiple layers.

Example security model:

| Layer          | Security Tool   |
| -------------- | --------------- |
| Instance Level | Security Groups |
| Subnet Level   | Network ACL     |
| Network Level  | Route Tables    |

Example architecture:

```
Internet
   │
Security Group
   │
Network ACL
   │
Application Server
```

This layered security approach protects production infrastructure.

---

# High Availability Design

Production architectures distribute resources across multiple **Availability Zones**.

Example:

```
AZ-1
 ├── Public Subnet
 ├── App Subnet
 └── DB Subnet

AZ-2
 ├── Public Subnet
 ├── App Subnet
 └── DB Subnet
```

Benefits:

* fault tolerance
* disaster resilience
* continuous application availability

---

# Monitoring and Logging

Production systems require monitoring and logging tools.

Example monitoring services:

* **Amazon CloudWatch**
* **AWS VPC Flow Logs**

These tools help monitor:

* network traffic
* application performance
* security events

---

# Real Enterprise Architecture Example

Example enterprise VPC architecture:

```
Internet
   │
Internet Gateway
   │
Public Subnets
   │
Application Load Balancer
   │
Private Application Subnets
   │
Application Servers
   │
Private Database Subnets
   │
Database Cluster
```

Optional integrations:

* Transit Gateway for multi-VPC architecture
* VPN for hybrid cloud connectivity
* VPC Endpoints for private AWS service access

---

# Benefits of Production VPC Architecture

This architecture provides:

* strong security isolation
* scalable infrastructure
* high availability
* optimized network performance

It is the **standard architecture used by most real-world AWS production environments**.

---
