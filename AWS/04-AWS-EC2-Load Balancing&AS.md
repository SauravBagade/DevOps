--

# 14. AWS EC2 Load Balancing and Target Group

---

## 14.1 Introduction to Load Balancing

![Image](https://d2908q01vomqb2.cloudfront.net/fc074d501302eb2b93e2554793fcaf50b3bf7291/2021/05/13/Figure-2.-Pilot-light-DR-strategy-1024x538.png)

![Image](https://miro.medium.com/1%2AuM9hKH4udB8MqTqHMFRYzQ.png)

![Image](https://d2908q01vomqb2.cloudfront.net/da4b9237bacccdf19c0760cab7aec4a8359010b0/2019/10/06/illustration-2-779x630.png)

![Image](https://docs.aws.amazon.com/images/elasticloadbalancing/latest/application/images/component_architecture.png)

### What is Load Balancing?

**Load Balancing** is the process of distributing incoming network traffic across multiple servers (EC2 instances) to ensure:

* High availability
* Fault tolerance
* Scalability
* Better performance

In AWS, this service is called **Elastic Load Balancing**.

Instead of sending traffic to **one EC2 instance**, traffic is distributed across **multiple EC2 instances**.

---

### Example

Without Load Balancer

```
User Requests
      |
      v
   EC2 Instance
```

Problem

* Instance overload
* Application crash
* Single point of failure

---

With Load Balancer

```
Users
  |
  v
Load Balancer
 |     |     |
EC2   EC2   EC2
```

Benefits

* Even traffic distribution
* High availability
* Fault tolerance
* Automatic failover

---

### Real-World Example

Example: E-commerce Website

During **festival sale**, millions of users visit the website.

Without Load Balancer

* Server crash
* Website down

With Load Balancer

* Traffic distributed across multiple servers
* Website remains available

---

## 14.2 What is Elastic Load Balancer (ELB)

**Elastic Load Balancing** automatically distributes incoming traffic across multiple targets such as:

* EC2 instances
* Containers
* IP addresses
* Lambda functions

---

### Key Features

1. Automatic traffic distribution
2. Health checks
3. Fault tolerance
4. SSL termination
5. High availability
6. Integration with Auto Scaling

---

### High Availability

Load Balancers run across **multiple Availability Zones**.

Example

```
Availability Zone A
   EC2 Instance

Availability Zone B
   EC2 Instance

Availability Zone C
   EC2 Instance
```

Load Balancer routes traffic to **healthy instances only**.

---

## 14.3 Types of AWS Load Balancers

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2AGb7hi5pqKmYYxEIUCJylHw.gif)

![Image](https://d2908q01vomqb2.cloudfront.net/fc074d501302eb2b93e2554793fcaf50b3bf7291/2020/04/06/NLB_Blog1-1-897x630.jpg)

![Image](https://d2908q01vomqb2.cloudfront.net/5b384ce32d8cdef02bc3a139d4cac0a22bb029e8/2020/11/12/GWLB-Architecture-p1.2-original.jpg)

![Image](https://d2908q01vomqb2.cloudfront.net/5b384ce32d8cdef02bc3a139d4cac0a22bb029e8/2020/11/10/GWLB-Architecture-p5-original.jpg)

AWS provides **four types of Load Balancers**.

| Load Balancer             | Layer     | Use Case             |
| ------------------------- | --------- | -------------------- |
| Application Load Balancer | Layer 7   | HTTP / HTTPS traffic |
| Network Load Balancer     | Layer 4   | TCP / UDP traffic    |
| Gateway Load Balancer     | Layer 3   | Security appliances  |
| Classic Load Balancer     | Layer 4/7 | Legacy               |

---

### 1 Application Load Balancer (ALB)

**Application Load Balancer**

Used for:

* Web applications
* HTTP / HTTPS traffic
* Microservices architecture

Features

* Path-based routing
* Host-based routing
* WebSocket support
* Integration with containers

Example

```
example.com/api  -> EC2 Group A
example.com/app  -> EC2 Group B
```

---

### 2 Network Load Balancer (NLB)

**Network Load Balancer**

Works at **Transport Layer (Layer 4)**.

Features

* Ultra high performance
* Millions of requests per second
* Low latency
* Static IP support

Used for

* Gaming servers
* Real-time applications
* Financial systems

---

### 3 Gateway Load Balancer

**Gateway Load Balancer**

Used for **security appliances** such as:

* Firewalls
* Intrusion detection systems
* Deep packet inspection

---

### 4 Classic Load Balancer

**Classic Load Balancer**

Older load balancer.

Supports

* EC2 Classic
* Basic HTTP and TCP load balancing

⚠️ Not recommended for new applications.

---

# 14.4 What is a Target Group

![Image](https://d2908q01vomqb2.cloudfront.net/da4b9237bacccdf19c0760cab7aec4a8359010b0/2019/10/06/illustration-2-779x630.png)

![Image](https://d2908q01vomqb2.cloudfront.net/da4b9237bacccdf19c0760cab7aec4a8359010b0/2019/10/06/illustration-2.png)

![Image](https://d2908q01vomqb2.cloudfront.net/5b384ce32d8cdef02bc3a139d4cac0a22bb029e8/2023/04/10/figure_2-1024x688.png)

![Image](https://media.licdn.com/dms/image/v2/D4E12AQFHHP68W00qrA/article-cover_image-shrink_600_2000/article-cover_image-shrink_600_2000/0/1657369068559?e=2147483647\&t=6tAPLggMrMj1-_2C7lFBDKScI9Acjdnm7_Tpe6n0bK4\&v=beta)

A **Target Group** is a collection of resources where the Load Balancer sends traffic.

Targets can be:

* EC2 instances
* IP addresses
* Lambda functions
* Containers

---

### Architecture

```
Internet
   |
   v
Load Balancer
   |
Target Group
 |     |     |
EC2   EC2   EC2
```

The Load Balancer forwards traffic to **targets inside the target group**.

---

### Target Types

| Target Type | Description          |
| ----------- | -------------------- |
| Instance    | EC2 instances        |
| IP          | Private IP addresses |
| Lambda      | Lambda functions     |

---

### Why Target Groups are Important

* Traffic routing
* Health checking
* Instance grouping
* Scaling support

---

# 14.5 Health Checks

Load Balancer continuously checks whether instances are **healthy or unhealthy**.

If an instance fails the health check:

* Load balancer stops sending traffic to that instance.

---

### Health Check Example

```
Health Check URL

http://instance-ip/health
```

Response

```
200 OK
```

Instance becomes **Healthy**.

---

### Health Check Parameters

| Parameter           | Description          |
| ------------------- | -------------------- |
| Protocol            | HTTP / HTTPS / TCP   |
| Path                | URL path             |
| Interval            | Time between checks  |
| Timeout             | Health check timeout |
| Healthy threshold   | Success count        |
| Unhealthy threshold | Failure count        |

---

# 14.6 Load Balancer Components

| Component    | Description                      |
| ------------ | -------------------------------- |
| Listener     | Checks incoming traffic          |
| Rule         | Determines where to send traffic |
| Target Group | Group of servers                 |
| Health Check | Checks server health             |

---

### Listener Example

```
Protocol: HTTP
Port: 80
```

Rule Example

```
IF path = /api
Forward to Target Group A
```

---

# 14.7 Steps to Create Load Balancer (ALB)

### Step 1

Open **Amazon EC2 Console

```
EC2 Dashboard
→ Load Balancers
→ Create Load Balancer
```

---

### Step 2

Select

```
Application Load Balancer
```

---

### Step 3

Configure Load Balancer

Name:

```
my-alb
```

Scheme

```
Internet Facing
```

IP Type

```
IPv4
```

---

### Step 4

Select Network

Choose

* VPC
* Availability Zones
* Subnets

Example

```
VPC: default
AZ1: subnet-a
AZ2: subnet-b
```

---

### Step 5

Security Group

Allow

```
HTTP (80)
HTTPS (443)
```

---

### Step 6

Create Target Group

Target Type

```
Instance
```

Protocol

```
HTTP
```

Port

```
80
```

---

### Step 7

Register Targets

Select EC2 instances.

Example

```
Web-server-1
Web-server-2
```

---

### Step 8

Review and Create

Click

```
Create Load Balancer
```

AWS creates:

* Load Balancer
* Target Group
* Listener

---

# 14.8 Load Balancer Algorithms

Load balancers distribute traffic using algorithms.

### Round Robin

Traffic sent sequentially.

```
User1 → EC2-1
User2 → EC2-2
User3 → EC2-3
```

---

### Least Outstanding Requests

Traffic sent to instance with **least active connections**.

---

### Flow Hash

Used in **Network Load Balancer**.

Based on

* Source IP
* Destination IP
* Port

---

# 14.9 Cross-Zone Load Balancing

Normally

```
AZ-A → instances in AZ-A
AZ-B → instances in AZ-B
```

With **Cross-Zone Load Balancing**

Traffic distributed across **all instances in all AZs**.

---

# 14.10 Sticky Sessions (Session Affinity)

Sticky session ensures the same user connects to the **same EC2 instance**.

Example

```
User → EC2-1
Next request → EC2-1
```

Implemented using **cookies**.

---

# 15. AWS Auto Scaling

---

## 15.1 Introduction to Auto Scaling

![Image](https://docs.aws.amazon.com/images/autoscaling/ec2/userguide/images/elb-tutorial-architecture-diagram.png)

![Image](https://docs.aws.amazon.com/images/autoscaling/ec2/userguide/images/asg-basic-arch.png)

![Image](https://miro.medium.com/1%2Ak9LK1pVd9lxD5OuLvNIA3g.png)

![Image](https://docs.aws.amazon.com/images/autoscaling/ec2/userguide/images/sample-3-tier-architecture-with-azs-diagram.png)

### What is Auto Scaling?

**Amazon EC2 Auto Scaling** automatically **adds or removes EC2 instances** based on application demand.

It helps maintain:

* High availability
* Fault tolerance
* Performance
* Cost optimization

---

### Example Scenario

Website traffic changes during the day.

Morning

```text
Users → 100
Instances → 2
```

Evening (high traffic)

```text
Users → 10,000
Instances → 10
```

Night (low traffic)

```text
Users → 50
Instances → 1
```

Auto Scaling automatically adjusts the number of EC2 instances.

---

### Without Auto Scaling

Problems:

* Server overload
* Website crashes
* Manual scaling required

---

### With Auto Scaling

Benefits:

* Automatic scaling
* High availability
* Cost savings
* Better performance

---

# 15.2 Components of Auto Scaling

Main components of Auto Scaling.

| Component          | Description                 |
| ------------------ | --------------------------- |
| Launch Template    | Configuration for instances |
| Auto Scaling Group | Group of EC2 instances      |
| Scaling Policies   | Rules for scaling           |
| CloudWatch Alarms  | Monitor metrics             |

---

## 15.3 Launch Template

A **Launch Template** defines the configuration used to launch EC2 instances.

Used by Auto Scaling to create new instances.

Created in **Amazon EC2**.

---

### Launch Template Configuration

Includes:

* AMI ID
* Instance type
* Key pair
* Security group
* Storage
* User data script
* Network configuration

---

### Example

```text
AMI: Amazon Linux 2
Instance Type: t2.micro
Security Group: web-sg
Key Pair: my-key
```

---

# 15.4 Auto Scaling Group (ASG)

![Image](https://docs.aws.amazon.com/images/autoscaling/ec2/userguide/images/elb-tutorial-architecture-diagram.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2AZ-DC516_NPhaBhs3o0VXVg.png)

![Image](https://docs.aws.amazon.com/images/autoscaling/ec2/userguide/images/sample-3-tier-architecture-with-azs-diagram.png)

![Image](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2023/05/12/03-odcr-backed-architecture.png)

An **Auto Scaling Group** manages a collection of EC2 instances.

Features:

* Maintains minimum number of instances
* Automatically replaces unhealthy instances
* Distributes instances across Availability Zones

---

### Key Parameters

| Parameter        | Description                 |
| ---------------- | --------------------------- |
| Desired Capacity | Number of running instances |
| Minimum Capacity | Minimum instances           |
| Maximum Capacity | Maximum instances           |

---

### Example

```text
Minimum = 2
Desired = 3
Maximum = 10
```

System behavior

* Always keep **minimum 2 instances**
* Normally run **3 instances**
* Can scale up to **10 instances**

---

# 15.5 Scaling Types

There are three main scaling types.

---

## 1. Dynamic Scaling

Instances scale automatically based on metrics.

Example:

CPU utilization > 70%

```text
Launch new EC2 instance
```

CPU utilization < 20%

```text
Terminate instance
```

Metrics monitored using **Amazon CloudWatch**.

---

## 2. Scheduled Scaling

Scaling based on **time schedule**.

Example

```text
Scale Out at 9 AM
Scale In at 10 PM
```

Useful for predictable traffic patterns.

Example:

Office hours traffic increase.

---

## 3. Predictive Scaling

AWS predicts traffic based on **historical data**.

Automatically prepares instances before traffic increases.

---

# 15.6 Scaling Policies

Scaling policies define **when and how scaling happens**.

Types:

| Policy          | Description              |
| --------------- | ------------------------ |
| Target Tracking | Maintain specific metric |
| Step Scaling    | Scale in steps           |
| Simple Scaling  | Basic scaling rule       |

---

### Target Tracking Example

Goal:

```text
Maintain CPU utilization at 50%
```

If CPU increases:

```text
Add instances
```

If CPU decreases:

```text
Remove instances
```

---

### Step Scaling Example

CPU usage thresholds.

| CPU Usage | Action          |
| --------- | --------------- |
| 60%       | Add 1 instance  |
| 75%       | Add 2 instances |
| 90%       | Add 3 instances |

---

# 15.7 Health Checks

Auto Scaling continuously checks instance health.

Health checks come from:

* **Amazon EC2**
* **Elastic Load Balancing**

If instance fails health check:

```text
Instance terminated
New instance launched
```

---

# 15.8 Scaling Process

Example architecture.

```text
Users
   |
Load Balancer
   |
Auto Scaling Group
 |    |    |
EC2  EC2  EC2
```

Traffic increases.

```text
CPU → 80%
```

CloudWatch alarm triggered.

Auto Scaling launches **new EC2 instances**.

---

# 15.9 Steps to Create Auto Scaling Group

---

### Step 1

Open **Amazon EC2 Console

```text
EC2 Dashboard
→ Auto Scaling Groups
→ Create Auto Scaling Group
```

---

### Step 2

Create Launch Template.

Provide:

* AMI
* Instance type
* Security group
* Key pair

---

### Step 3

Create Auto Scaling Group.

Enter:

```text
Name: web-asg
Launch Template: web-template
```

---

### Step 4

Select Network

Choose:

* VPC
* Subnets
* Availability Zones

Example

```text
AZ-1 subnet
AZ-2 subnet
```

---

### Step 5

Attach Load Balancer.

Select Target Group created earlier.

Example

```text
Target Group: web-tg
```

---

### Step 6

Configure Scaling.

Example:

```text
Min: 2
Desired: 3
Max: 10
```

---

### Step 7

Add Scaling Policy.

Example:

```text
Target CPU utilization = 50%
```

---

### Step 8

Review and Create.

AWS launches instances automatically.

---

# 15.10 Lifecycle Hooks

Lifecycle hooks allow custom actions when instances start or terminate.

Example actions:

* Install software
* Configure application
* Backup data

States include:

```text
Pending
InService
Terminating
```

---

# 15.11 Instance Termination Policies

When scaling in, AWS decides which instance to terminate.

Policies include:

* Oldest instance
* Newest instance
* Closest to billing hour

---

# 15.12 Auto Scaling Monitoring

Monitoring done with:

**Amazon CloudWatch**

Metrics:

| Metric           | Description        |
| ---------------- | ------------------ |
| CPUUtilization   | Instance CPU usage |
| NetworkIn        | Incoming traffic   |
| NetworkOut       | Outgoing traffic   |
| HealthyHostCount | Healthy instances  |

---

# 15.13 Auto Scaling Benefits

1. High availability
2. Automatic scaling
3. Cost optimization
4. Fault tolerance
5. Better performance

---

# 15.14 Real Production Architecture

```text
Users
  |
Route53
  |
Application Load Balancer
  |
Auto Scaling Group
 |     |     |
EC2   EC2   EC2
```

Components used:

* **Amazon Route 53**
* **Application Load Balancer**
* **Amazon EC2 Auto Scaling**
* **Amazon EC2**

---
