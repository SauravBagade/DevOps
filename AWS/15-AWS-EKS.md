---
AWS-EKS
---
---
# 1. Introduction to Amazon EKS
---

![Image](https://d2908q01vomqb2.cloudfront.net/fc074d501302eb2b93e2554793fcaf50b3bf7291/2020/12/14/EKS-arhitecture-overview-1024x782.png)

![Image](https://miro.medium.com/1%2A22us38QKC10bPCzDHsmXcg.jpeg)

![Image](https://d2908q01vomqb2.cloudfront.net/fe2ef495a1152561572949784c16bf23abb28057/2020/04/10/eks_architecture.png)

![Image](https://docs.aws.amazon.com/images/eks/latest/best-practices/images/reliability/eks-data-plane-connectivity.jpeg)

## 1.1 What is Amazon EKS?

**Amazon EKS (Elastic Kubernetes Service)** is a **managed Kubernetes service** provided by Amazon Web Services that makes it easy to run **Kubernetes clusters** on AWS without managing the control plane.

In simple words:

👉 **EKS = Kubernetes managed by AWS**

AWS manages important components like:

* Kubernetes **Control Plane**
* **API Server**
* **etcd database**
* **Cluster availability**
* **Security updates**

You only manage:

* Worker nodes
* Applications
* Containers

---

## 1.2 What is Kubernetes?

Kubernetes is an **open-source container orchestration platform** used to:

* Deploy containers
* Manage containers
* Scale applications
* Automate deployments

It is mainly used to run **Docker containers in production**.

Example:

```
Docker → Container
Kubernetes → Manage containers
AWS EKS → Managed Kubernetes
```

---

## 1.3 Why Amazon EKS is Used

Companies use **Amazon EKS** because it simplifies Kubernetes management.

Main reasons:

* Fully managed Kubernetes
* High availability
* Automatic updates
* Easy scaling
* Deep AWS integration

Example integrations:

* Amazon ECR – container images
* Amazon EC2 – worker nodes
* Amazon CloudWatch – monitoring
* Amazon VPC – networking

---

## 1.4 Benefits of Amazon EKS

### 1️⃣ Managed Control Plane

AWS manages Kubernetes control plane automatically.

### 2️⃣ High Availability

Control plane runs across **multiple Availability Zones**.

### 3️⃣ Scalability

Applications automatically scale using Kubernetes.

### 4️⃣ Security

Integration with:

* AWS Identity and Access Management (IAM)
* Kubernetes RBAC

### 5️⃣ Easy Integration

Works easily with many AWS services.

---

## 1.5 Basic EKS Workflow

Simple workflow:

```
Developer
   │
   │ Push Code
   ▼
Docker Image
   │
   ▼
Amazon ECR (Container Registry)
   │
   ▼
Amazon EKS Cluster
   │
   ▼
Pods Running Application
   │
   ▼
Load Balancer → Users
```

---

## 1.6 Example Use Case

Example company architecture:

* Application runs in **Docker containers**
* Containers stored in **ECR**
* Application deployed in **EKS cluster**
* Traffic handled by **Load Balancer**

Result:

✔ Scalable
✔ Highly available
✔ Easy to manage

---

## 1.7 Key Components of EKS

Important parts:

| Component     | Description                      |
| ------------- | -------------------------------- |
| EKS Cluster   | Kubernetes cluster               |
| Control Plane | Managed by AWS                   |
| Worker Nodes  | EC2 instances running containers |
| Pods          | Smallest unit in Kubernetes      |
| Services      | Expose applications              |

---

## 1.8 Simple Real Example

Example:

A **shopping website** uses:

* EKS cluster
* 10 pods running application
* Auto scaling during sale time

If traffic increases:

```
10 pods → 50 pods automatically
```

This is **auto scaling with Kubernetes**.

---
---
# 2. Kubernetes Basics for Amazon EKS
---
![Image](https://cdn.shopaccino.com/igmguru/images/kubernetes-architecture-components-3528183568043978.jpg)

![Image](https://miro.medium.com/1%2A-zkqfnQqG99F09dPDLJF5w.png)

![Image](https://kubernetes.io/images/docs/components-of-kubernetes.svg)

![Image](https://miro.medium.com/1%2AQWJijlj7kwd0hIYk8Wsnow.png)

Before learning Amazon Elastic Kubernetes Service, it is important to understand the basics of Kubernetes because **EKS is simply Kubernetes managed by AWS**.

---

# 2.1 What is Kubernetes?

**Kubernetes (K8s)** is an **open-source container orchestration platform** used to:

* Deploy containerized applications
* Manage containers automatically
* Scale applications
* Handle failures

Originally developed by **Google**.

### Simple Meaning

```
Docker → Creates containers
Kubernetes → Manages containers
Amazon EKS → Managed Kubernetes by AWS
```

---

# 2.2 Kubernetes Cluster

A **Kubernetes Cluster** is a group of machines that run containerized applications.

Two main parts:

1️⃣ **Control Plane (Master Node)**
2️⃣ **Worker Nodes**

```
Kubernetes Cluster
│
├── Control Plane
│
└── Worker Nodes
      ├── Pod
      ├── Pod
      └── Pod
```

---

# 2.3 Control Plane (Master Node)

The **Control Plane** manages the entire Kubernetes cluster.

Main components:

| Component          | Function                   |
| ------------------ | -------------------------- |
| API Server         | Entry point for Kubernetes |
| Scheduler          | Assigns pods to nodes      |
| Controller Manager | Maintains desired state    |
| etcd               | Stores cluster data        |

In **EKS**, AWS manages the **control plane automatically**.

---

# 2.4 Worker Nodes

Worker nodes are machines that **run applications**.

In AWS EKS, worker nodes are usually:

* Amazon Elastic Compute Cloud instances.

Each worker node contains:

* kubelet
* kube-proxy
* container runtime

Example:

```
Worker Node
   │
   ├── Pod
   ├── Pod
   └── Pod
```

---

# 2.5 Pods

A **Pod** is the **smallest unit in Kubernetes**.

A pod contains:

* One container
  or
* Multiple containers

Example:

```
Pod
 ├── Application Container
 └── Sidecar Container
```

Example use:

* Web application
* API service
* Database container

---

# 2.6 Deployments

A **Deployment** manages pods.

It ensures:

* Correct number of pods
* Automatic updates
* Rollbacks

Example:

```
Deployment
   │
   ├── Pod
   ├── Pod
   └── Pod
```

If a pod crashes:

```
Kubernetes automatically creates a new pod
```

---

# 2.7 Services

A **Service** exposes pods to the network.

Because pods are temporary and their IP changes.

Service provides:

* Stable IP
* Load balancing

Types of services:

| Type         | Use                      |
| ------------ | ------------------------ |
| ClusterIP    | Internal communication   |
| NodePort     | External access via node |
| LoadBalancer | Cloud load balancer      |

---

# 2.8 Namespaces

A **Namespace** divides a cluster into logical environments.

Example:

```
Cluster
 ├── Namespace: Dev
 ├── Namespace: Testing
 └── Namespace: Production
```

Benefits:

* Resource isolation
* Environment separation
* Better management

---

# 2.9 Kubernetes Basic Workflow

Example workflow:

```
Developer
   │
   ▼
Create Docker Image
   │
   ▼
Push Image to Registry
   │
   ▼
Create Kubernetes Deployment
   │
   ▼
Pods Created
   │
   ▼
Service Exposes Application
```

---

# 2.10 Simple Real Example

Example **E-commerce website**

Application components:

```
Frontend → React App
Backend → Node.js API
Database → MySQL
```

In Kubernetes:

```
Frontend Deployment → 3 Pods
Backend Deployment → 3 Pods
Database Pod → 1 Pod
```

Kubernetes automatically:

* Scales pods
* Restarts failed pods
* Balances traffic

---
---
# 3. Amazon EKS Architecture
---
![Image](https://docs.aws.amazon.com/images/eks/latest/best-practices/images/reliability/eks-data-plane-connectivity.jpeg)

![Image](https://docs.aws.amazon.com/images/eks/latest/best-practices/images/networking/subnet_image.png)

![Image](https://d2908q01vomqb2.cloudfront.net/fe2ef495a1152561572949784c16bf23abb28057/2020/04/10/eks_architecture.png)

![Image](https://docs.aws.amazon.com/images/eks/latest/best-practices/images/networking/cn-image-3.png)

The architecture of Amazon Elastic Kubernetes Service shows how Kubernetes components run on AWS infrastructure provided by Amazon Web Services.

In EKS architecture, the cluster is divided into two main parts:

```
EKS Cluster
│
├── Control Plane (Managed by AWS)
│
└── Worker Nodes (Managed by User)
```

---

# 3.1 EKS Control Plane

The **Control Plane** manages the Kubernetes cluster.

In EKS, AWS automatically manages the control plane.

It runs across **multiple Availability Zones** for high availability.

### Control Plane Components

| Component             | Description             |
| --------------------- | ----------------------- |
| Kubernetes API Server | Entry point for cluster |
| etcd                  | Stores cluster data     |
| Scheduler             | Assigns pods to nodes   |
| Controller Manager    | Maintains cluster state |

Important point:

✔ Users **do not manage control plane servers** in EKS.

---

# 3.2 Worker Nodes

Worker nodes are servers where **containers run**.

In EKS, worker nodes are usually:

* Amazon Elastic Compute Cloud instances.

Worker nodes run:

* Pods
* Containers
* Applications

Each worker node contains:

```
Worker Node
│
├── kubelet
├── kube-proxy
└── Container Runtime
```

---

# 3.3 Pods

Pods are the **smallest deployable unit in Kubernetes**.

A pod contains one or more containers.

Example:

```
Pod
├── Container (Application)
└── Container (Logging sidecar)
```

Pods run inside **worker nodes**.

---

# 3.4 Node Groups

EKS organizes worker nodes into **Node Groups**.

Types of node groups:

### 1️⃣ Managed Node Groups

AWS automatically manages:

* Node updates
* Auto scaling
* Instance management

### 2️⃣ Self-Managed Nodes

User manually manages EC2 instances.

### 3️⃣ Fargate

Serverless compute using AWS Fargate.

No servers to manage.

---

# 3.5 VPC Networking

EKS clusters run inside an AWS **Virtual Private Cloud**.

Networking components:

* Amazon Virtual Private Cloud
* Public Subnets
* Private Subnets
* Security Groups

Example architecture:

```
VPC
│
├── Public Subnet
│   └── Load Balancer
│
└── Private Subnet
    └── Worker Nodes
```

Pods communicate using **AWS networking**.

---

# 3.6 Elastic Network Interface (ENI)

EKS uses **ENI (Elastic Network Interface)** to assign IP addresses to pods.

This allows:

✔ Direct VPC networking
✔ High network performance

---

# 3.7 Load Balancer Integration

Applications running in EKS are exposed using AWS load balancers.

Common types:

* Application Load Balancer
* Network Load Balancer

Traffic flow example:

```
User
 │
 ▼
Load Balancer
 │
 ▼
Kubernetes Service
 │
 ▼
Pods
```

---

# 3.8 Container Images

Applications in EKS use container images stored in a registry.

Common registry:

* Amazon Elastic Container Registry

Example workflow:

```
Developer
 │
 ▼
Build Docker Image
 │
 ▼
Push to ECR
 │
 ▼
Deploy to EKS
```

---

# 3.9 Simple EKS Architecture Flow

Example architecture:

```
User
 │
 ▼
Route 53
 │
 ▼
Load Balancer
 │
 ▼
EKS Cluster
 │
 ├── Pod (Frontend)
 ├── Pod (Backend)
 └── Pod (API)
 │
 ▼
Database (RDS)
```

---

# 3.10 High Availability in EKS

EKS provides high availability using:

* Multi Availability Zones
* Auto scaling node groups
* Managed control plane

Result:

✔ Highly available applications
✔ Fault tolerant infrastructure

---
---
# 4. Amazon EKS Components
---
![Image](https://miro.medium.com/0%2ALeA6rbKnXsZWsZoy.jpeg)

![Image](https://miro.medium.com/0%2AD_CvUWPkJ-TxwFRi.png)

![Image](https://kubernetes.io/images/docs/kubernetes-cluster-architecture.svg)

![Image](https://miro.medium.com/0%2AV4FrQX-bATauEzU_.png)

In Amazon Elastic Kubernetes Service, multiple components work together to run containerized applications on infrastructure provided by Amazon Web Services.

Understanding these components is important for **DevOps engineers and Kubernetes users**.

---

# 4.1 EKS Cluster

An **EKS Cluster** is the main environment where Kubernetes applications run.

It includes:

* Control Plane
* Worker Nodes
* Networking
* Storage

Simple structure:

```text
EKS Cluster
│
├── Control Plane
│
└── Worker Nodes
      ├── Pod
      ├── Pod
      └── Pod
```

The cluster manages the **deployment, scaling, and operation of containers**.

---

# 4.2 Control Plane

The **Control Plane** is responsible for managing the entire Kubernetes cluster.

In EKS, AWS manages the control plane automatically.

Main responsibilities:

* Scheduling containers
* Managing cluster state
* Handling API requests

---

# 4.3 Kubernetes API Server

The **API Server** is the **main entry point of Kubernetes**.

All communication with the cluster goes through the API server.

Examples:

* kubectl commands
* Deployment creation
* Scaling pods

Example command:

```bash
kubectl get pods
```

This command communicates with the **API server**.

---

# 4.4 etcd

**etcd** is a distributed key-value database used by Kubernetes.

It stores:

* Cluster configuration
* Node information
* Pod status
* Secrets and configurations

Important point:

In EKS, **AWS manages etcd automatically**.

---

# 4.5 Scheduler

The **Kubernetes Scheduler** decides **which worker node should run a pod**.

Example:

If a pod is created:

```text
Pod Created → Scheduler selects best worker node
```

Scheduler decisions depend on:

* CPU availability
* Memory resources
* Node conditions

---

# 4.6 Controller Manager

The **Controller Manager** ensures that the cluster maintains the desired state.

Example:

If a deployment requires **3 pods**, and one pod fails:

```text
Required Pods = 3
Running Pods = 2
Controller → Create new pod
```

---

# 4.7 Worker Nodes

Worker nodes are machines where **containers run**.

In EKS, worker nodes usually use:

* Amazon Elastic Compute Cloud instances.

Worker nodes host:

* Pods
* Containers
* Applications

---

# 4.8 kubelet

**kubelet** is an agent running on each worker node.

Responsibilities:

* Communicates with API server
* Starts and stops containers
* Ensures pods are running correctly

Example workflow:

```text
API Server → kubelet → Run container
```

---

# 4.9 kube-proxy

**kube-proxy** manages networking for pods.

Responsibilities:

* Service networking
* Load balancing inside the cluster
* Routing traffic to pods

Example:

```text
Service → kube-proxy → Pod
```

---

# 4.10 Container Runtime

The **Container Runtime** runs containers inside pods.

Common runtime:

* containerd

Earlier Kubernetes used **Docker**, but now containerd is commonly used.

---

# 4.11 Pods

A **Pod** is the smallest unit in Kubernetes.

A pod contains:

* One container
  or
* Multiple containers

Example:

```text
Pod
 ├── Web Application Container
 └── Logging Container
```

Pods run on **worker nodes**.

---

# 4.12 Services

A **Service** exposes pods and provides a stable network endpoint.

Types:

| Service Type | Description                  |
| ------------ | ---------------------------- |
| ClusterIP    | Internal communication       |
| NodePort     | External access through node |
| LoadBalancer | Cloud load balancer          |

---

# 4.13 Node Groups

In EKS, worker nodes are organized into **Node Groups**.

Types:

1️⃣ Managed Node Groups
2️⃣ Self-Managed Nodes
3️⃣ AWS Fargate

Node groups help manage:

* Scaling
* Updates
* Instance types

---

# 4.14 Simple Component Flow

Example flow:

```text
Developer
   │
   ▼
kubectl command
   │
   ▼
API Server
   │
   ▼
Scheduler
   │
   ▼
Worker Node
   │
   ▼
Pod running container
```

---
---
# 5. EKS Cluster Creation Methods
---
![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2AM4O2Uye2UVQvvOAXXeBnpg.gif)

![Image](https://d2908q01vomqb2.cloudfront.net/fe2ef495a1152561572949784c16bf23abb28057/2020/04/10/eks_architecture-1120x630.png)

![Image](https://docs.codacy.com/v13.0/chart/infrastructure/images/codacy-chart-eks-quickstart.jpg)

![Image](https://scalardb.scalar-labs.com/assets/images/EKS_ScalarDB_Cluster_Indirect_Mode.drawio-7836b07adea502a0b8eb6fe04ec82444.png)

An Amazon Elastic Kubernetes Service cluster can be created using different tools provided by Amazon Web Services.
Each method is used for different purposes such as **manual setup, automation, or infrastructure as code**.

---

# 5.1 AWS Management Console

The easiest way to create an EKS cluster is using the **AWS web console**.

Steps overview:

1. Login to AWS Console
2. Go to **EKS Service**
3. Click **Create Cluster**
4. Configure cluster settings
5. Create Node Group

### Best for

* Beginners
* Learning EKS
* Testing environments

Example workflow:

```text
AWS Console
   │
   ▼
Create EKS Cluster
   │
   ▼
Create Node Group
   │
   ▼
Deploy Application
```

---

# 5.2 AWS CLI

The **AWS Command Line Interface** allows creating EKS clusters from the command line.

Tool:

* AWS Command Line Interface

Example command:

```bash
aws eks create-cluster \
--name my-cluster \
--role-arn arn:aws:iam::123456789:role/EKSRole \
--resources-vpc-config subnetIds=subnet-abc,subnet-def
```

### Best for

* Automation scripts
* DevOps workflows
* CI/CD pipelines

---

# 5.3 eksctl

**eksctl** is the most popular tool for creating EKS clusters.

It is a CLI tool specifically designed for EKS.

Tool:

* eksctl

Example command:

```bash
eksctl create cluster --name my-cluster --region ap-south-1
```

This command automatically creates:

* VPC
* Subnets
* EKS Cluster
* Node Group

### Best for

* Fast cluster setup
* DevOps engineers
* Learning Kubernetes on AWS

---

# 5.4 Terraform

**Terraform** is used to create EKS clusters using **Infrastructure as Code (IaC)**.

Tool:

* Terraform

Example workflow:

```text
Terraform Code
   │
   ▼
terraform init
   │
   ▼
terraform plan
   │
   ▼
terraform apply
   │
   ▼
EKS Cluster Created
```

### Best for

* Production environments
* Infrastructure automation
* DevOps pipelines

Since you are learning DevOps and Terraform, **Terraform + EKS is commonly used in companies**.

---

# 5.5 CloudFormation

Another infrastructure automation tool from AWS is:

* AWS CloudFormation

Cluster is created using **YAML or JSON templates**.

Example flow:

```text
CloudFormation Template
   │
   ▼
Create Stack
   │
   ▼
EKS Cluster
```

### Best for

* AWS-native automation
* Infrastructure templates

---

# 5.6 Comparison of EKS Creation Methods

| Method         | Difficulty      | Use Case                  |
| -------------- | --------------- | ------------------------- |
| AWS Console    | Easy            | Learning / Testing        |
| AWS CLI        | Medium          | Automation                |
| eksctl         | Easy            | Quick cluster setup       |
| Terraform      | Medium/Advanced | Production infrastructure |
| CloudFormation | Advanced        | AWS template automation   |

---

# 5.7 Most Common Method in Real Companies

Most DevOps teams use:

```text
Terraform + EKS
```

or

```text
eksctl + CI/CD pipeline
```

Because they support **automation and repeatable infrastructure**.

---
---
# 6. Creating an Amazon EKS Cluster (Step-by-Step Practical Guide)
---
![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2AM4O2Uye2UVQvvOAXXeBnpg.gif)

![Image](https://docs.aws.amazon.com/images/eks/latest/best-practices/images/networking/cni_image-3.png)

![Image](https://d2908q01vomqb2.cloudfront.net/fe2ef495a1152561572949784c16bf23abb28057/2023/12/20/Pod-Identity-Worklow.jpg)

![Image](https://d2908q01vomqb2.cloudfront.net/fe2ef495a1152561572949784c16bf23abb28057/2023/12/21/IAM-Role-chaining.png)

This section explains how to create an **EKS cluster step-by-step** using Amazon Elastic Kubernetes Service on Amazon Web Services.

Typical workflow:

```text
IAM Role → EKS Cluster → Node Group → Configure kubectl → Deploy Application
```

---

# 6.1 Prerequisites

Before creating an EKS cluster, install the following tools.

### Required Tools

| Tool                       | Purpose                    |
| -------------------------- | -------------------------- |
| AWS Command Line Interface | Manage AWS services        |
| kubectl                    | Manage Kubernetes cluster  |
| eksctl                     | Create EKS clusters easily |

Check installation:

```bash
aws --version
kubectl version --client
eksctl version
```

---

# 6.2 Configure AWS CLI

Configure AWS credentials.

```bash
aws configure
```

Enter:

```text
AWS Access Key
AWS Secret Key
Region (example: ap-south-1)
Output format: json
```

Example region near India:

```
ap-south-1 (Mumbai)
```

---

# 6.3 Create EKS Cluster using eksctl

The easiest way to create a cluster is using **eksctl**.

Command:

```bash
eksctl create cluster \
--name my-cluster \
--region ap-south-1
```

This command automatically creates:

* VPC
* Subnets
* EKS Cluster
* Managed Node Group
* Security Groups

Cluster creation takes about **10–15 minutes**.

---

# 6.4 Verify EKS Cluster

List clusters:

```bash
aws eks list-clusters
```

Expected output:

```text
clusters:
- my-cluster
```

---

# 6.5 Configure kubectl for EKS

Connect kubectl to the cluster.

```bash
aws eks update-kubeconfig \
--region ap-south-1 \
--name my-cluster
```

Now kubectl can access the cluster.

---

# 6.6 Check Worker Nodes

Verify nodes in the cluster.

```bash
kubectl get nodes
```

Example output:

```text
NAME                 STATUS   ROLES    AGE
ip-192-168-1-10     Ready    worker   5m
ip-192-168-1-20     Ready    worker   5m
```

---

# 6.7 Deploy a Sample Application

Deploy **NGINX container**.

```bash
kubectl create deployment nginx \
--image=nginx
```

Check pods:

```bash
kubectl get pods
```

Example output:

```text
nginx-7c79c4bf97-abcde   Running
```

---

# 6.8 Expose Application

Expose the application using a service.

```bash
kubectl expose deployment nginx \
--type=LoadBalancer \
--port=80
```

Check service:

```bash
kubectl get svc
```

Example output:

```text
NAME         TYPE           EXTERNAL-IP
nginx        LoadBalancer   a1b2c3d4.elb.amazonaws.com
```

Open the **External IP** in a browser to access the application.

---

# 6.9 Check Running Resources

Useful commands:

Check pods:

```bash
kubectl get pods
```

Check services:

```bash
kubectl get svc
```

Check deployments:

```bash
kubectl get deployments
```

---

# 6.10 Delete the EKS Cluster

To avoid AWS costs, delete the cluster.

```bash
eksctl delete cluster --name my-cluster
```

This removes:

* EKS Cluster
* Node groups
* VPC resources

---

# 6.11 Complete Workflow

```text
Developer
   │
   ▼
Create EKS Cluster
   │
   ▼
Configure kubectl
   │
   ▼
Deploy Application
   │
   ▼
Create Service
   │
   ▼
Application Accessible via Load Balancer
```

---
---
# 7. Amazon EKS Networking
---
![Image](https://docs.aws.amazon.com/images/eks/latest/best-practices/images/networking/cn-image-3.png)

![Image](https://docs.aws.amazon.com/images/eks/latest/best-practices/images/networking/cni_image-3.png)

![Image](https://d2908q01vomqb2.cloudfront.net/fe2ef495a1152561572949784c16bf23abb28057/2020/04/10/eks_architecture.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2A3gmiOlweWrAV5VE6ySRtHg.png)

Networking is one of the most important parts of Amazon Elastic Kubernetes Service.
In EKS, networking is built on top of the AWS network infrastructure provided by Amazon Virtual Private Cloud.

This allows **pods, nodes, and services** to communicate securely inside the cluster.

---

# 7.1 VPC Integration

Every EKS cluster runs inside an **AWS VPC**.

A **Virtual Private Cloud (VPC)** is an isolated network in AWS.

Components used in EKS networking:

* VPC
* Subnets
* Route Tables
* Internet Gateway
* Security Groups

Example architecture:

```text
VPC
│
├── Public Subnet
│     └── Load Balancer
│
└── Private Subnet
      └── Worker Nodes
           └── Pods
```

Best practice:

✔ Load balancer in **public subnet**
✔ Worker nodes in **private subnet**

---

# 7.2 Subnets

Subnets divide a VPC network into smaller networks.

Two main types used in EKS:

| Subnet         | Purpose                   |
| -------------- | ------------------------- |
| Public Subnet  | Internet-facing resources |
| Private Subnet | Worker nodes and pods     |

Example:

```text
VPC
│
├── Public Subnet
│   └── Application Load Balancer
│
└── Private Subnet
    └── EKS Worker Nodes
```

---

# 7.3 Pod Networking

Pods in EKS receive **their own IP addresses** from the VPC.

Important point:

✔ Each pod gets a **real VPC IP address**

Example:

```text
Worker Node
│
├── Pod → 10.0.1.10
├── Pod → 10.0.1.11
└── Pod → 10.0.1.12
```

This allows:

* Direct pod-to-pod communication
* High network performance

---

# 7.4 AWS VPC CNI Plugin

EKS uses a special networking plugin:

**AWS VPC CNI (Container Network Interface)**.

This plugin allows Kubernetes pods to use **VPC networking directly**.

Functions:

* Assign IP addresses to pods
* Manage ENI attachments
* Handle pod networking

---

# 7.5 Elastic Network Interface (ENI)

An **ENI (Elastic Network Interface)** is a virtual network interface attached to EC2 instances.

In EKS:

* Worker nodes receive ENIs
* Pods get IP addresses from ENI

Example:

```text
Worker Node
│
├── ENI
│    ├── Pod IP
│    ├── Pod IP
│    └── Pod IP
```

This enables **high-speed networking inside the cluster**.

---

# 7.6 Service Networking

A **Kubernetes Service** allows communication with pods.

Service provides:

* Stable IP address
* Load balancing

Example flow:

```text
User
 │
 ▼
Load Balancer
 │
 ▼
Kubernetes Service
 │
 ▼
Pods
```

---

# 7.7 Internet Access in EKS

There are two main ways pods access the internet.

### 1️⃣ Internet Gateway

Used for resources in **public subnets**.

Example:

```text
Internet
   │
   ▼
Internet Gateway
   │
   ▼
Public Subnet
```

---

### 2️⃣ NAT Gateway

Used for **private subnet resources** to access the internet.

Example:

```text
Private Subnet
      │
      ▼
NAT Gateway
      │
      ▼
Internet
```

This allows pods to:

* Pull container images
* Access external APIs

---

# 7.8 Security Groups

Security groups act as **virtual firewalls**.

They control:

* Incoming traffic
* Outgoing traffic

Example rules:

| Type           | Example  |
| -------------- | -------- |
| HTTP           | Port 80  |
| HTTPS          | Port 443 |
| Kubernetes API | Port 443 |

Security groups protect:

* Worker nodes
* Load balancers

---

# 7.9 Networking Flow Example

Example request flow:

```text
User
 │
 ▼
Route53
 │
 ▼
Application Load Balancer
 │
 ▼
Kubernetes Service
 │
 ▼
Pods
 │
 ▼
Database
```

---

# 7.10 Key Benefits of EKS Networking

✔ Direct VPC networking
✔ High performance
✔ Secure communication
✔ Easy integration with AWS services

---
---
# 8. Amazon EKS Node Groups
---
![Image](https://d2908q01vomqb2.cloudfront.net/fe2ef495a1152561572949784c16bf23abb28057/2019/11/16/eks-api-evolution-1260x610.png)

![Image](https://d2908q01vomqb2.cloudfront.net/fe2ef495a1152561572949784c16bf23abb28057/2022/11/09/ipfs-1.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2AM4O2Uye2UVQvvOAXXeBnpg.gif)

![Image](https://kodekloud.com/kk-media/image/upload/v1752862754/notes-assets/images/AWS-EKS-EKS-Node-Groups/node-group-api-server-architecture.jpg)

In Amazon Elastic Kubernetes Service, **Node Groups** are used to manage worker nodes that run containers.
Worker nodes are usually **EC2 instances** provided by Amazon Elastic Compute Cloud.

Node groups help manage:

* Worker nodes
* Auto scaling
* Instance updates
* Kubernetes workloads

---

# 8.1 What is a Node Group?

A **Node Group** is a collection of worker nodes within an EKS cluster.

Each node group contains multiple EC2 instances that run pods.

Example:

```text
Node Group
│
├── Worker Node (EC2)
│      ├── Pod
│      └── Pod
│
├── Worker Node (EC2)
│      ├── Pod
│      └── Pod
│
└── Worker Node (EC2)
       ├── Pod
       └── Pod
```

Node groups allow **easy scaling and management of nodes**.

---

# 8.2 Types of Node Groups in EKS

There are **three types of node groups** in EKS.

| Type                | Description                       |
| ------------------- | --------------------------------- |
| Managed Node Groups | Managed automatically by AWS      |
| Self-Managed Nodes  | Fully managed by the user         |
| Fargate             | Serverless compute for containers |

---

# 8.3 Managed Node Groups

Managed Node Groups are the **most commonly used option**.

AWS automatically manages:

* Node provisioning
* Node updates
* Auto scaling
* Instance health

Example:

```text
EKS Cluster
│
└── Managed Node Group
      ├── EC2 Instance
      ├── EC2 Instance
      └── EC2 Instance
```

Benefits:

✔ Easy to manage
✔ Automatic updates
✔ Integrated auto scaling

---

# 8.4 Self-Managed Nodes

Self-managed nodes give **full control over worker nodes**.

Users manage:

* EC2 instances
* Updates
* Scaling
* AMI selection

Example:

```text
User manages
│
├── EC2 Launch Templates
├── Auto Scaling Groups
└── Node updates
```

Used when:

* Custom configurations are required
* Advanced networking is needed

---

# 8.5 AWS Fargate

Another option is **serverless compute** using AWS Fargate.

With Fargate:

* No servers to manage
* No EC2 instances
* AWS runs containers automatically

Example architecture:

```text
EKS Cluster
│
└── Fargate
      ├── Pod
      ├── Pod
      └── Pod
```

Best for:

✔ Small workloads
✔ Microservices
✔ Serverless architecture

---

# 8.6 Node Auto Scaling

Node groups support **Auto Scaling**.

This automatically increases or decreases the number of nodes.

Example:

```text
Low traffic → 2 nodes
High traffic → 10 nodes
```

Auto scaling works with:

* Kubernetes Cluster Autoscaler
* AWS Auto Scaling Groups

---

# 8.7 Node Instance Types

Node groups can use different **EC2 instance types**.

Example:

| Instance Type | Use Case           |
| ------------- | ------------------ |
| t3.medium     | Small workloads    |
| m5.large      | General workloads  |
| c5.large      | CPU intensive apps |

Choosing the right instance type improves **performance and cost efficiency**.

---

# 8.8 Node Group Configuration Example

Example node group settings:

```text
Cluster Name : my-eks-cluster
Node Type : t3.medium
Min Nodes : 2
Max Nodes : 6
Desired Nodes : 3
```

This means:

* Minimum nodes = 2
* Maximum nodes = 6
* Initially running nodes = 3

---

# 8.9 Node Group Scaling Example

Traffic increases:

```text
Before Scaling
3 Nodes
```

After scaling:

```text
Cluster Autoscaler
      │
      ▼
Add More Nodes
      │
      ▼
8 Nodes
```

Pods are distributed across nodes automatically.

---

# 8.10 Best Practices for Node Groups

Best practices used in production:

✔ Use **Managed Node Groups**
✔ Run nodes in **private subnets**
✔ Enable **Auto Scaling**
✔ Use **multiple availability zones**
✔ Monitor nodes using **CloudWatch**

---
---
# 9. Amazon EKS Security
---
![Image](https://d2908q01vomqb2.cloudfront.net/fe2ef495a1152561572949784c16bf23abb28057/2020/06/07/K8sOperator.png)

![Image](https://miro.medium.com/1%2AeFfKhBin6cL39BSg1zfDFA.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2AP8Vm38Y4kZVyABM18SAlBg.png)

![Image](https://cdn.prod.website-files.com/681e366f54a6e3ce87159ca4/68b6f813a339ea0eea27c815_687d7b62a5379c24ed1f018d_kubernetes.jpeg)

Security is a critical part of running workloads on Amazon Elastic Kubernetes Service.
EKS security combines **AWS security services** with **Kubernetes security mechanisms** to protect clusters, nodes, and applications.

---

# 9.1 Security Layers in EKS

EKS security works in multiple layers.

```text
AWS Infrastructure Security
        │
        ▼
IAM Authentication
        │
        ▼
Kubernetes RBAC Authorization
        │
        ▼
Network Security
        │
        ▼
Pod and Application Security
```

Each layer helps protect the cluster from unauthorized access.

---

# 9.2 IAM Authentication

Access to the EKS cluster is controlled using
AWS Identity and Access Management.

IAM is used for:

* Authenticating users
* Granting AWS permissions
* Managing access to EKS clusters

Example IAM users:

```text
DevOps Engineer
Developer
Admin
```

These users access the cluster using **AWS credentials**.

---

# 9.3 Kubernetes RBAC (Role-Based Access Control)

RBAC controls **what users can do inside the Kubernetes cluster**.

Example permissions:

| Role      | Permissions         |
| --------- | ------------------- |
| Admin     | Full cluster access |
| Developer | Deploy applications |
| Viewer    | Read-only access    |

Example RBAC structure:

```text
User
 │
 ▼
Role
 │
 ▼
RoleBinding
 │
 ▼
Cluster Permissions
```

RBAC ensures **only authorized users can manage resources**.

---

# 9.4 IAM Roles for Service Accounts (IRSA)

A very important security feature in EKS is **IRSA**.

IRSA allows **Kubernetes pods to access AWS services securely**.

Example:

```text
Pod
 │
 ▼
Service Account
 │
 ▼
IAM Role
 │
 ▼
AWS Service (S3, DynamoDB)
```

Benefits:

✔ Secure access to AWS services
✔ No need to store AWS credentials in pods
✔ Fine-grained permissions

---

# 9.5 Security Groups

Security groups act as **virtual firewalls** in AWS.

They control **network traffic to and from resources**.

Security groups protect:

* Worker nodes
* Load balancers
* Control plane communication

Example rules:

| Port | Purpose        |
| ---- | -------------- |
| 443  | Kubernetes API |
| 80   | HTTP traffic   |
| 22   | SSH access     |

---

# 9.6 Network Policies

Network policies control **pod-to-pod communication**.

Example:

```text
Frontend Pod
      │
      ▼
Backend Pod
      │
      ▼
Database Pod
```

Network policies can:

* Allow traffic
* Block traffic
* Restrict communication

This improves **internal cluster security**.

---

# 9.7 Secrets Management

Sensitive data should not be stored in plain text.

Kubernetes uses **Secrets** to store confidential data such as:

* Database passwords
* API keys
* Tokens

Secrets can also integrate with:

* AWS Secrets Manager
* AWS Key Management Service

This ensures **secure credential management**.

---

# 9.8 EKS Control Plane Security

In EKS, AWS automatically secures the **Kubernetes control plane**.

Security features include:

✔ Managed etcd encryption
✔ Automatic patching
✔ Multi-AZ high availability
✔ Secure API server access

This reduces the operational burden on DevOps teams.

---

# 9.9 Best Practices for EKS Security

Recommended practices:

✔ Use **IAM roles instead of access keys**
✔ Enable **RBAC policies**
✔ Use **private subnets for nodes**
✔ Encrypt secrets using **KMS**
✔ Restrict API server access

These practices help secure **production Kubernetes clusters**.

---

# 9.10 Example Secure EKS Architecture

Example security flow:

```text
User
 │
 ▼
IAM Authentication
 │
 ▼
Kubernetes RBAC
 │
 ▼
EKS Cluster
 │
 ├── Pod (Frontend)
 ├── Pod (Backend)
 └── Pod (Database)
 │
 ▼
AWS Services (S3, RDS)
```

Security policies control access at every stage.

---
---
# 10. Deploying Applications on Amazon EKS
---
![Image](https://docs.aws.amazon.com/images/architecture-diagrams/latest/modernize-applications-with-microservices-using-amazon-eks/images/modernize-applications-with-microservices-using-amazon-eks.png)

![Image](https://www-uploads.scaleway.com/Capture_d_ecran_2023_03_10_a_16_00_49_2459982941.webp)

![Image](https://miro.medium.com/0%2AP2r_uiNorJC6sdIU.png)

![Image](https://d2908q01vomqb2.cloudfront.net/fe2ef495a1152561572949784c16bf23abb28057/2023/12/20/Pod-Identity-Worklow.jpg)

After creating a cluster in Amazon Elastic Kubernetes Service, the next step is to **deploy containerized applications** using Kubernetes.

Applications in EKS run inside **Pods**, which are managed using **Deployments and Services**.

---

# 10.1 Application Deployment Workflow

Typical deployment process:

```text
Developer
   │
   ▼
Build Docker Image
   │
   ▼
Push Image to Container Registry
   │
   ▼
Create Kubernetes Deployment
   │
   ▼
Pods Created
   │
   ▼
Expose Service
   │
   ▼
Application Accessible to Users
```

Most companies store container images in
Amazon Elastic Container Registry.

---

# 10.2 Kubernetes Deployment

A **Deployment** is used to manage pods and applications.

Deployment ensures:

* Correct number of pods
* Automatic scaling
* Rolling updates
* Self-healing

Example deployment YAML:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 80
```

Apply deployment:

```bash
kubectl apply -f deployment.yaml
```

Check running pods:

```bash
kubectl get pods
```

---

# 10.3 Pods

Pods are the **smallest deployable unit in Kubernetes**.

Example structure:

```text
Pod
 └── Container (Application)
```

Example:

```text
Deployment → 3 Pods
```

If a pod crashes:

```text
Kubernetes automatically creates a new pod
```

---

# 10.4 Kubernetes Service

Pods are temporary and their IP addresses change.

A **Service** provides a **stable network endpoint** for accessing pods.

Example service YAML:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
  - port: 80
    targetPort: 80
  type: LoadBalancer
```

Create service:

```bash
kubectl apply -f service.yaml
```

---

# 10.5 Service Types

Kubernetes supports multiple service types.

| Service Type | Description                    |
| ------------ | ------------------------------ |
| ClusterIP    | Internal cluster communication |
| NodePort     | Exposes service on node port   |
| LoadBalancer | Creates AWS load balancer      |

In EKS production environments, **LoadBalancer type** is commonly used.

It integrates with AWS load balancers like:

* Application Load Balancer
* Network Load Balancer

---

# 10.6 Exposing Applications to the Internet

Example traffic flow:

```text
User
 │
 ▼
Load Balancer
 │
 ▼
Kubernetes Service
 │
 ▼
Pods
 │
 ▼
Application
```

The LoadBalancer service automatically creates an **AWS ELB**.

Check service:

```bash
kubectl get svc
```

Example output:

```text
NAME           TYPE           EXTERNAL-IP
nginx-service  LoadBalancer   abc123.elb.amazonaws.com
```

Open the **External IP** in a browser.

---

# 10.7 Scaling Applications

Applications can be scaled easily.

Example scaling command:

```bash
kubectl scale deployment nginx-deployment --replicas=5
```

Before scaling:

```text
3 Pods
```

After scaling:

```text
5 Pods
```

Kubernetes distributes traffic automatically.

---

# 10.8 Updating Applications

Deployment supports **rolling updates**.

Example:

```bash
kubectl set image deployment/nginx-deployment nginx=nginx:latest
```

Benefits:

* Zero downtime updates
* Gradual rollout
* Easy rollback

---

# 10.9 Checking Application Resources

Useful commands:

Check pods:

```bash
kubectl get pods
```

Check deployments:

```bash
kubectl get deployments
```

Check services:

```bash
kubectl get svc
```

Describe resources:

```bash
kubectl describe pod <pod-name>
```

---

# 10.10 Real Production Example

Example **microservices architecture**:

```text
EKS Cluster
│
├── Frontend Deployment
│     └── React Pods
│
├── Backend Deployment
│     └── API Pods
│
└── Database
      └── Amazon RDS
```

Traffic flow:

```text
User
 │
 ▼
Route53
 │
 ▼
Application Load Balancer
 │
 ▼
Kubernetes Services
 │
 ▼
Pods
```

---
---
# 11. Amazon EKS Storage
---
![Image](https://d2908q01vomqb2.cloudfront.net/e1822db470e60d090affd0956d743cb0e7cdf113/2022/10/28/3.Persistent-Volume-and-Persistent-Volume-Claim.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/0%2AoCS44eYGLA2ce2rY.png)

![Image](https://miro.medium.com/1%2AhYuhPT326a55b4Vf7LkJJQ.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2APyGq82fNPZFMxbzAH5Btuw.png)

In Amazon Elastic Kubernetes Service, storage is used to store **persistent data** for applications running inside pods.

Normally, pods are **temporary**, so when a pod is deleted the data inside it is lost.
To solve this problem, Kubernetes provides **persistent storage mechanisms**.

---

# 11.1 Why Storage is Needed in EKS

Many applications need to store data permanently.

Examples:

* Databases
* Logs
* File uploads
* Application data

Example:

```text
Pod deleted → Data lost
```

Solution:

```text
Persistent Storage → Data remains safe
```

---

# 11.2 Persistent Volume (PV)

A **Persistent Volume (PV)** is a storage resource in the Kubernetes cluster.

It represents actual storage from AWS services.

Example storage providers:

* Amazon Elastic Block Store
* Amazon Elastic File System
* Amazon FSx

Example architecture:

```text
AWS Storage
     │
     ▼
Persistent Volume (PV)
     │
     ▼
Pod
```

PV is **cluster-level storage**.

---

# 11.3 Persistent Volume Claim (PVC)

A **Persistent Volume Claim (PVC)** is a request for storage made by a pod.

Example:

```text
Pod
 │
 ▼
Persistent Volume Claim
 │
 ▼
Persistent Volume
 │
 ▼
AWS Storage
```

PVC specifies:

* Storage size
* Access mode
* Storage class

Example PVC YAML:

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: app-storage
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 5Gi
```

Apply configuration:

```bash
kubectl apply -f pvc.yaml
```

---

# 11.4 Storage Classes

A **Storage Class** defines how storage is dynamically created.

Example storage classes:

* EBS storage class
* EFS storage class

Example architecture:

```text
Pod
 │
 ▼
PVC
 │
 ▼
Storage Class
 │
 ▼
AWS Storage
```

This allows **automatic storage provisioning**.

---

# 11.5 Amazon EBS Storage

Amazon Elastic Block Store provides **block storage** for Kubernetes pods.

Characteristics:

* High performance
* Single node access
* Ideal for databases

Example architecture:

```text
Pod
 │
 ▼
Persistent Volume
 │
 ▼
Amazon EBS Volume
```

Best for:

* Databases
* Stateful applications

---

# 11.6 Amazon EFS Storage

Amazon Elastic File System provides **shared file storage**.

Characteristics:

* Multiple pods can access it simultaneously
* Highly scalable
* Network-based storage

Example:

```text
Pod 1
   │
Pod 2
   │
Pod 3
   │
 ▼
Amazon EFS
```

Best for:

* Shared file storage
* Microservices

---

# 11.7 Amazon FSx Storage

Amazon FSx provides **high-performance file systems**.

Used for:

* High performance workloads
* Machine learning
* Large datasets

---

# 11.8 Storage Access Modes

Kubernetes storage supports different access modes.

| Access Mode   | Description               |
| ------------- | ------------------------- |
| ReadWriteOnce | Single node read/write    |
| ReadOnlyMany  | Multiple nodes read only  |
| ReadWriteMany | Multiple nodes read/write |

Example:

```text
ReadWriteOnce → Database storage
ReadWriteMany → Shared file system
```

---

# 11.9 Example Storage Workflow

Example architecture:

```text
Application Pod
      │
      ▼
Persistent Volume Claim
      │
      ▼
Persistent Volume
      │
      ▼
Amazon EBS
```

Even if the pod is deleted:

```text
Pod Deleted → Data still stored in EBS
```

---

# 11.10 Best Practices for EKS Storage

Best practices used in production:

✔ Use **EBS for databases**
✔ Use **EFS for shared storage**
✔ Use **Storage Classes for dynamic provisioning**
✔ Monitor storage usage
✔ Encrypt storage using AWS KMS

---
---
# 12. Amazon EKS Load Balancing
---
![Image](https://d2908q01vomqb2.cloudfront.net/ca3512f4dfa95a03169c5a670a4c91a19b3077b4/2018/11/20/image1-1.png)

![Image](https://d2908q01vomqb2.cloudfront.net/fe2ef495a1152561572949784c16bf23abb28057/2020/08/01/NLB-NGINX-Architecture.png)

![Image](https://docs.aws.amazon.com/images/eks/latest/userguide/images/lbc-overview.png)

![Image](https://d2908q01vomqb2.cloudfront.net/fe2ef495a1152561572949784c16bf23abb28057/2024/01/04/Solution-overview.jpg)

Load balancing in Amazon Elastic Kubernetes Service distributes incoming traffic across multiple pods to ensure **high availability, scalability, and reliability**.

EKS integrates directly with AWS load balancing services provided by Amazon Web Services.

---

# 12.1 Why Load Balancing is Needed

Applications running in Kubernetes usually have **multiple pods**.

Example:

```text
Frontend Deployment
│
├── Pod 1
├── Pod 2
└── Pod 3
```

If users send requests:

```text
User Traffic
     │
     ▼
Load Balancer
     │
     ├── Pod 1
     ├── Pod 2
     └── Pod 3
```

Benefits:

✔ Distributes traffic
✔ Prevents server overload
✔ Improves availability

---

# 12.2 Load Balancer Types in EKS

EKS supports multiple AWS load balancers.

| Load Balancer             | Use Case                     |
| ------------------------- | ---------------------------- |
| Application Load Balancer | HTTP/HTTPS web applications  |
| Network Load Balancer     | High-performance TCP traffic |

These load balancers automatically route traffic to Kubernetes services.

---

# 12.3 Kubernetes Service LoadBalancer

Kubernetes can automatically create an AWS load balancer.

Example service YAML:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: web-service
spec:
  selector:
    app: web
  type: LoadBalancer
  ports:
  - port: 80
    targetPort: 80
```

Apply service:

```bash
kubectl apply -f service.yaml
```

Check service:

```bash
kubectl get svc
```

Example output:

```text
NAME         TYPE           EXTERNAL-IP
web-service  LoadBalancer   abc123.elb.amazonaws.com
```

---

# 12.4 Kubernetes Ingress

Ingress is used to manage **HTTP and HTTPS routing**.

Instead of creating multiple load balancers, one load balancer can route traffic to multiple services.

Example architecture:

```text
User
 │
 ▼
Application Load Balancer
 │
 ├── /api → Backend Service
 ├── /web → Frontend Service
 └── /admin → Admin Service
```

Ingress reduces cost because **one load balancer can handle many services**.

---

# 12.5 AWS Load Balancer Controller

EKS uses a controller to manage load balancers automatically.

Tool:

* AWS Load Balancer Controller

Responsibilities:

* Creates ALB automatically
* Configures routing rules
* Manages Kubernetes ingress resources

Example workflow:

```text
Ingress Resource
      │
      ▼
AWS Load Balancer Controller
      │
      ▼
Application Load Balancer
      │
      ▼
Pods
```

---

# 12.6 Application Load Balancer (ALB)

ALB works at **Layer 7 (HTTP/HTTPS)**.

Features:

* Path-based routing
* Host-based routing
* SSL termination
* Web application support

Example routing:

```text
example.com/api → Backend Pods
example.com/web → Frontend Pods
```

---

# 12.7 Network Load Balancer (NLB)

NLB works at **Layer 4 (TCP/UDP)**.

Features:

* Extremely high performance
* Low latency
* Handles millions of requests

Used for:

* Gaming applications
* Real-time applications
* Financial systems

---

# 12.8 Example Traffic Flow in EKS

Example production architecture:

```text
User
 │
 ▼
Route 53
 │
 ▼
Application Load Balancer
 │
 ▼
Ingress
 │
 ▼
Kubernetes Service
 │
 ▼
Pods
```

---

# 12.9 Benefits of EKS Load Balancing

✔ Automatic traffic distribution
✔ High availability
✔ Integration with AWS networking
✔ Supports microservices architectures

---

# 12.10 Best Practices

Production recommendations:

✔ Use **ALB for web applications**
✔ Use **Ingress for multiple services**
✔ Run nodes in **private subnets**
✔ Enable **HTTPS encryption**
✔ Monitor traffic using **CloudWatch**

---
---
# 13. Monitoring and Logging in Amazon EKS
---
![Image](https://d1.awsstatic.com/onedam/marketing-channels/website/aws/en_US/solution-case-studies/approved/images/5b5e4e8a08f513b339e3fb2346471f2d-monitoring-amazon-eks-workloads-with-managed-prometheus-grafana-2982x1824.661869920697df04e7937494555b8d77edb51031.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2A0vXfW4gPKFcwC2alH2qMyA.gif)

![Image](https://d2908q01vomqb2.cloudfront.net/fe2ef495a1152561572949784c16bf23abb28057/2021/01/22/image-88.png)

![Image](https://d2908q01vomqb2.cloudfront.net/ca3512f4dfa95a03169c5a670a4c91a19b3077b4/2019/07/09/e2e-log-analysis-app-1024x608.png)

Monitoring and logging are important for managing applications running on Amazon Elastic Kubernetes Service.
They help DevOps teams track **performance, errors, resource usage, and system health**.

Monitoring tools collect **metrics**, while logging tools collect **application and system logs**.

---

# 13.1 Why Monitoring is Important

Monitoring helps in:

* Detecting system failures
* Tracking application performance
* Analyzing resource usage
* Troubleshooting issues

Example monitoring information:

```text
CPU Usage
Memory Usage
Network Traffic
Pod Health
Application Errors
```

---

# 13.2 Amazon CloudWatch for EKS

The most common monitoring tool used with EKS is
Amazon CloudWatch.

CloudWatch provides:

* Metrics monitoring
* Log collection
* Alarms and alerts
* Dashboard visualization

Example monitoring flow:

```text
EKS Cluster
   │
   ▼
CloudWatch Agent
   │
   ▼
CloudWatch Metrics & Logs
   │
   ▼
Monitoring Dashboard
```

CloudWatch can monitor:

* Nodes
* Pods
* Containers
* Applications

---

# 13.3 Prometheus Monitoring

Prometheus is a popular **open-source monitoring tool for Kubernetes**.

It collects metrics from:

* Kubernetes nodes
* Pods
* Containers
* Applications

Example architecture:

```text
Pods / Nodes
     │
     ▼
Prometheus
     │
     ▼
Metrics Storage
```

Prometheus stores metrics and allows querying using **PromQL**.

---

# 13.4 Grafana Dashboards

Grafana is used to visualize monitoring data.

Grafana creates dashboards showing:

* CPU usage
* Memory usage
* Network traffic
* Pod status

Example architecture:

```text
Prometheus
     │
     ▼
Grafana Dashboard
     │
     ▼
DevOps Engineers
```

Grafana dashboards make it easy to **analyze system performance visually**.

---

# 13.5 Logging in EKS

Logging records system events and application messages.

Logs help identify:

* Errors
* Application crashes
* Security events

Types of logs:

| Log Type           | Description          |
| ------------------ | -------------------- |
| Application Logs   | Application output   |
| Container Logs     | Logs from containers |
| Node Logs          | Worker node logs     |
| Control Plane Logs | Kubernetes API logs  |

---

# 13.6 Log Collection with Fluentd

A common log collection tool in Kubernetes is
Fluentd.

Fluentd collects logs from containers and sends them to monitoring systems.

Example logging flow:

```text
Containers
     │
     ▼
Fluentd
     │
     ▼
CloudWatch Logs
```

This allows centralized log management.

---

# 13.7 EKS Control Plane Logs

EKS can send **control plane logs** to CloudWatch.

These logs include:

* API server logs
* Scheduler logs
* Controller manager logs
* Authentication logs

Benefits:

✔ Better troubleshooting
✔ Security monitoring
✔ Audit tracking

---

# 13.8 Example Monitoring Architecture

Example production monitoring setup:

```text
EKS Cluster
│
├── Nodes
├── Pods
└── Containers
     │
     ▼
Prometheus
     │
     ▼
Grafana Dashboard
     │
     ▼
CloudWatch Logs
```

This setup provides **complete observability**.

---

# 13.9 Alerts and Notifications

Monitoring tools can send alerts when problems occur.

Example alerts:

* High CPU usage
* Pod crash
* Node failure

Alerts can be sent via:

* Email
* Slack
* SMS

CloudWatch alarms help automate alerting.

---

# 13.10 Best Practices for Monitoring

Recommended monitoring practices:

✔ Monitor **CPU and memory usage**
✔ Collect **application logs**
✔ Enable **CloudWatch metrics**
✔ Use **Prometheus + Grafana dashboards**
✔ Configure **alerts for failures**

These practices help maintain **stable and reliable EKS environments**.

---
---
# 14. Auto Scaling in Amazon EKS
---
![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2A0wJBUCAWTLAe62PHmhoLOQ.gif)

![Image](https://docs.aws.amazon.com/images/eks/latest/best-practices/images/autoscaling/cas_architecture.png)

![Image](https://cdn.prod.website-files.com/681e366f54a6e3ce87159ca4/6877c72c005c1d4c13b30b8e_kubernetes_scaler_diagram.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2ALgM4NNphVcyDesY_lo8OkA.png)

Auto scaling in Amazon Elastic Kubernetes Service automatically adjusts **pods and worker nodes** based on application demand.
It ensures that applications handle increased traffic while optimizing resource usage.

Auto scaling helps achieve:

* High availability
* Better performance
* Cost optimization

---

# 14.1 Types of Auto Scaling in EKS

Kubernetes supports three main types of auto scaling.

| Auto Scaling Type               | Purpose               |
| ------------------------------- | --------------------- |
| Horizontal Pod Autoscaler (HPA) | Scales pods           |
| Vertical Pod Autoscaler (VPA)   | Adjusts pod resources |
| Cluster Autoscaler              | Scales worker nodes   |

---

# 14.2 Horizontal Pod Autoscaler (HPA)

The **Horizontal Pod Autoscaler** automatically increases or decreases the number of pods based on metrics like:

* CPU usage
* Memory usage
* Custom metrics

Example:

```text
Low Traffic → 2 Pods
High Traffic → 10 Pods
```

Architecture example:

```text
User Traffic
     │
     ▼
Application
     │
     ▼
HPA Controller
     │
     ▼
Pods Scaled Automatically
```

Example command:

```bash
kubectl autoscale deployment nginx \
--cpu-percent=50 \
--min=2 \
--max=10
```

This means:

* Minimum pods = 2
* Maximum pods = 10
* Scale when CPU > 50%

---

# 14.3 Vertical Pod Autoscaler (VPA)

The **Vertical Pod Autoscaler** adjusts **CPU and memory resources** for pods.

Example:

```text
Pod CPU request = 200m
Pod CPU usage = 500m
```

VPA automatically increases resource allocation.

Architecture:

```text
Pod
 │
 ▼
VPA Controller
 │
 ▼
Adjust CPU and Memory
```

VPA is useful when:

* Applications require changing resource limits
* Workloads have unpredictable resource usage

---

# 14.4 Cluster Autoscaler

The **Cluster Autoscaler** automatically scales **worker nodes** in the EKS cluster.

Example scenario:

```text
Pods Pending
 │
 ▼
Cluster Autoscaler
 │
 ▼
Add New Worker Nodes
```

If traffic decreases:

```text
Unused Nodes
 │
 ▼
Cluster Autoscaler
 │
 ▼
Remove Nodes
```

This works with **Auto Scaling Groups of Amazon Elastic Compute Cloud instances**.

---

# 14.5 Example Auto Scaling Workflow

Example scaling process:

```text
User Traffic Increase
        │
        ▼
CPU Usage Increases
        │
        ▼
Horizontal Pod Autoscaler
        │
        ▼
More Pods Created
        │
        ▼
Cluster Autoscaler Adds Nodes
```

This ensures applications remain responsive during heavy traffic.

---

# 14.6 Real Production Example

Example **e-commerce website** during a sale:

```text
Normal Traffic
Pods = 3
Nodes = 2
```

During sale:

```text
High Traffic
Pods = 20
Nodes = 8
```

Auto scaling ensures **no downtime during high demand**.

---

# 14.7 Metrics Server

Auto scaling requires metrics collected from the cluster.

Kubernetes uses:

* **Metrics Server**

It collects metrics such as:

* CPU usage
* Memory usage

Architecture:

```text
Pods / Nodes
     │
     ▼
Metrics Server
     │
     ▼
HPA Controller
```

---

# 14.8 Benefits of Auto Scaling

✔ Automatic resource adjustment
✔ Improved application performance
✔ Cost savings
✔ High availability

---

# 14.9 Best Practices

Recommended practices:

✔ Enable **Horizontal Pod Autoscaler** for applications
✔ Configure **Cluster Autoscaler for nodes**
✔ Set proper CPU and memory requests
✔ Monitor scaling using **CloudWatch or Prometheus**

---

# 14.10 Example Scaling Architecture

```text
Users
 │
 ▼
Load Balancer
 │
 ▼
EKS Cluster
 │
 ├── HPA → Scale Pods
 │
 └── Cluster Autoscaler → Scale Nodes
```

This architecture supports **high traffic and production workloads**.

---
---
# 15. Amazon EKS High Availability
---
![Image](https://d2908q01vomqb2.cloudfront.net/887309d048beef83ad3eabf2a79a64a389ab1c9f/2022/03/21/DBBLOG-1908-image001.png)

![Image](https://d2908q01vomqb2.cloudfront.net/fe2ef495a1152561572949784c16bf23abb28057/2023/08/22/Multi-region-traffic.png)

![Image](https://d2908q01vomqb2.cloudfront.net/fe2ef495a1152561572949784c16bf23abb28057/2022/04/15/ONTAP-1.jpg)

![Image](https://d2908q01vomqb2.cloudfront.net/fe2ef495a1152561572949784c16bf23abb28057/2023/07/18/AZ-Isolated-EKS-Topology.jpg)

High Availability (HA) in Amazon Elastic Kubernetes Service ensures that applications remain **available even if failures occur** in servers, nodes, or entire availability zones.

HA is critical for **production environments** where downtime must be minimized.

---

# 15.1 What is High Availability?

High Availability means the system continues to operate even when components fail.

Example failure scenarios:

* Node failure
* Pod crash
* Availability Zone outage

Solution:

```text
Multiple nodes + multiple zones + load balancing
```

This ensures applications stay online.

---

# 15.2 Multi–Availability Zone Architecture

EKS clusters are designed to run across **multiple Availability Zones** within an AWS region.

Example:

```text
Region
│
├── Availability Zone A
│     └── Worker Nodes
│
├── Availability Zone B
│     └── Worker Nodes
│
└── Availability Zone C
      └── Worker Nodes
```

If one zone fails:

```text
Traffic automatically routed to other zones
```

This ensures **continuous availability**.

---

# 15.3 Highly Available Control Plane

In EKS, the **Kubernetes control plane** is automatically managed by Amazon Web Services.

AWS provides:

* Multiple API servers
* Distributed etcd database
* Automatic failover

Benefits:

✔ No manual management
✔ Automatic recovery
✔ Multi-AZ control plane

---

# 15.4 Node Redundancy

Worker nodes should run across **multiple Availability Zones**.

Example:

```text
EKS Cluster
│
├── AZ-A
│     ├── Node 1
│     └── Node 2
│
├── AZ-B
│     ├── Node 3
│     └── Node 4
│
└── AZ-C
      ├── Node 5
      └── Node 6
```

If a node fails:

```text
Kubernetes schedules pods on other nodes
```

---

# 15.5 Pod Replication

Applications should run multiple pods using **Deployments**.

Example:

```text
Frontend Deployment
│
├── Pod 1
├── Pod 2
└── Pod 3
```

If one pod fails:

```text
Kubernetes automatically creates a new pod
```

This provides **application-level redundancy**.

---

# 15.6 Load Balancer for High Availability

Load balancers distribute traffic across pods and nodes.

Common AWS load balancers:

* Application Load Balancer
* Network Load Balancer

Traffic flow:

```text
Users
 │
 ▼
Load Balancer
 │
 ▼
Multiple Pods
```

This prevents a single pod from being overloaded.

---

# 15.7 Auto Scaling for Availability

Auto scaling ensures enough resources are available.

Two main scaling types:

| Scaling Type              | Purpose     |
| ------------------------- | ----------- |
| Horizontal Pod Autoscaler | Scale pods  |
| Cluster Autoscaler        | Scale nodes |

Example:

```text
High Traffic
Pods: 3 → 15
Nodes: 2 → 6
```

Applications remain responsive during traffic spikes.

---

# 15.8 Example Production Architecture

Example high availability architecture:

```text
Users
 │
 ▼
Route 53
 │
 ▼
Application Load Balancer
 │
 ▼
EKS Cluster
 │
 ├── AZ-A → Pods
 ├── AZ-B → Pods
 └── AZ-C → Pods
 │
 ▼
Database (Multi-AZ)
```

This architecture ensures **fault tolerance and high reliability**.

---

# 15.9 Benefits of High Availability

✔ No single point of failure
✔ Continuous service availability
✔ Automatic recovery
✔ Better user experience

---

# 15.10 Best Practices for High Availability

Recommended practices:

✔ Run nodes in **multiple Availability Zones**
✔ Use **multiple pod replicas**
✔ Enable **auto scaling**
✔ Use **load balancers for traffic distribution**
✔ Monitor cluster health using **CloudWatch**

---
---
# 16. Amazon EKS Cost Optimization
---
![Image](https://d2908q01vomqb2.cloudfront.net/1b6453892473a467d07372d45eb05abc2031647a/2020/06/02/EKS-worker-node-architecture.jpg)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2AC-mgO3xIagmEeJgn4_1yFQ.png)

![Image](https://cdn.prod.website-files.com/655bc1860a87f22da98dd83c/6824ac3b62ae4d83337b8817_karpenter-overview.png)

![Image](https://d2908q01vomqb2.cloudfront.net/fe2ef495a1152561572949784c16bf23abb28057/2019/11/15/caseylee1.png)

Running workloads on Amazon Elastic Kubernetes Service can become expensive if resources are not managed properly.
Cost optimization focuses on **reducing infrastructure costs while maintaining performance and availability**.

DevOps engineers must optimize **compute, storage, and networking costs** in EKS clusters running on Amazon Web Services.

---

# 16.1 Why Cost Optimization is Important

Without optimization, clusters may run unnecessary resources.

Example:

```text
10 nodes running but only 3 nodes needed
```

Result:

* Wasted compute resources
* Higher AWS bills

Optimized environment:

```text
Use only required nodes and pods
```

---

# 16.2 Use Auto Scaling

Auto scaling automatically adjusts cluster resources.

Example:

```text
Low Traffic → 2 Nodes
High Traffic → 8 Nodes
```

Types used in EKS:

| Scaling Type              | Purpose             |
| ------------------------- | ------------------- |
| Horizontal Pod Autoscaler | Scales pods         |
| Cluster Autoscaler        | Scales worker nodes |

Auto scaling prevents **unused infrastructure costs**.

---

# 16.3 Use Spot Instances

One of the best ways to reduce cost is using **Spot Instances** from
Amazon Elastic Compute Cloud.

Spot Instances can be **up to 70–90% cheaper** than on-demand instances.

Example node group:

```text
Node Group
│
├── On-Demand Instances
└── Spot Instances
```

Best workloads for spot:

* Batch processing
* CI/CD pipelines
* Non-critical workloads

---

# 16.4 Right-Sizing Instances

Choosing the correct instance type is important.

Example:

| Instance Type | Usage                   |
| ------------- | ----------------------- |
| t3.medium     | Small workloads         |
| m5.large      | General workloads       |
| c5.large      | CPU intensive workloads |

Using oversized instances increases cost unnecessarily.

---

# 16.5 Use AWS Fargate for Small Workloads

Serverless compute using
AWS Fargate can reduce infrastructure management.

Benefits:

* No EC2 nodes to manage
* Pay only for used resources

Best for:

* Small microservices
* Event-driven workloads

---

# 16.6 Optimize Pod Resource Requests

Pods should define proper CPU and memory requests.

Example:

```yaml
resources:
  requests:
    cpu: "200m"
    memory: "256Mi"
```

If resources are too large:

```text
Pod reserves large resources → Node waste
```

Proper resource configuration improves **cluster efficiency**.

---

# 16.7 Use Efficient Storage

Storage costs also affect EKS clusters.

Common storage services:

* Amazon Elastic Block Store
* Amazon Elastic File System

Cost optimization tips:

* Delete unused volumes
* Use appropriate storage type
* Monitor storage usage

---

# 16.8 Use Multiple Node Groups

Using different node groups improves cost efficiency.

Example architecture:

```text
EKS Cluster
│
├── Node Group 1 → On-demand nodes
│
└── Node Group 2 → Spot nodes
```

Critical workloads run on **on-demand nodes**, while non-critical workloads run on **spot nodes**.

---

# 16.9 Monitor Costs

Cost monitoring tools help track cluster expenses.

Useful AWS services:

* AWS Cost Explorer
* Amazon CloudWatch

These tools help identify:

* Expensive resources
* Unused infrastructure

---

# 16.10 Best Practices for EKS Cost Optimization

✔ Use **auto scaling** for pods and nodes
✔ Run workloads on **spot instances when possible**
✔ Choose **correct instance types**
✔ Delete unused resources
✔ Monitor costs regularly

These strategies help maintain **efficient and cost-effective EKS clusters**.

---
---
# 17. Amazon EKS Integration with AWS Services
---
![Image](https://d2908q01vomqb2.cloudfront.net/fe2ef495a1152561572949784c16bf23abb28057/2024/04/12/412.jpg)

![Image](https://docs.aws.amazon.com/images/architecture-diagrams/latest/modernize-applications-with-microservices-using-amazon-eks/images/modernize-applications-with-microservices-using-amazon-eks.png)

![Image](https://d2908q01vomqb2.cloudfront.net/fe2ef495a1152561572949784c16bf23abb28057/2020/08/01/NLB-NGINX-Architecture.png)

![Image](https://media.licdn.com/dms/image/v2/D4E22AQHD727xEAtCGA/feedshare-shrink_800/B4EZqHkq2LIIAk-/0/1763211128838?e=2147483647\&t=AGCFAOIKs2G8xoydVwfBSFUze5QHeREEIfPqtLvmSj4\&v=beta)

Amazon Elastic Kubernetes Service integrates with many services from Amazon Web Services to build **scalable, secure, and production-ready cloud architectures**.

These integrations allow Kubernetes applications to use AWS infrastructure services like **storage, security, monitoring, and networking**.

---

# 17.1 Amazon ECR Integration

Amazon Elastic Container Registry is used to store **Docker container images**.

Workflow:

```text
Developer
   │
   ▼
Build Docker Image
   │
   ▼
Push Image to Amazon ECR
   │
   ▼
Deploy Image in EKS
```

Benefits:

✔ Secure container image storage
✔ Fully integrated with EKS
✔ Scalable container registry

---

# 17.2 IAM Integration

EKS integrates with
AWS Identity and Access Management for authentication and authorization.

IAM controls:

* Access to EKS clusters
* Permissions for users and services
* API access

Example:

```text
User
 │
 ▼
IAM Authentication
 │
 ▼
EKS Cluster Access
```

IAM ensures **secure cluster access management**.

---

# 17.3 CloudWatch Integration

Monitoring and logging in EKS can be handled using
Amazon CloudWatch.

CloudWatch collects:

* Container logs
* Pod metrics
* Node metrics
* Application logs

Example architecture:

```text
EKS Cluster
   │
   ▼
CloudWatch Agent
   │
   ▼
CloudWatch Logs and Metrics
```

This helps monitor **cluster health and performance**.

---

# 17.4 Load Balancer Integration

EKS integrates with AWS load balancers for external traffic.

Supported load balancers:

* Application Load Balancer
* Network Load Balancer

Traffic flow example:

```text
Users
 │
 ▼
Load Balancer
 │
 ▼
Kubernetes Service
 │
 ▼
Pods
```

Load balancers ensure **high availability and traffic distribution**.

---

# 17.5 Storage Integration

EKS supports multiple AWS storage services.

Common storage options:

| Storage Service            | Purpose                       |
| -------------------------- | ----------------------------- |
| Amazon Elastic Block Store | Block storage for pods        |
| Amazon Elastic File System | Shared file storage           |
| Amazon FSx                 | High performance file systems |

These services provide **persistent storage for Kubernetes workloads**.

---

# 17.6 Secrets Manager Integration

Sensitive data like passwords and API keys can be stored securely using
AWS Secrets Manager.

Example workflow:

```text
Application Pod
     │
     ▼
Service Account
     │
     ▼
Secrets Manager
     │
     ▼
Retrieve Secret
```

Benefits:

✔ Secure secret storage
✔ Automatic secret rotation
✔ Reduced credential exposure

---

# 17.7 CI/CD Integration

EKS integrates with CI/CD tools for automated deployments.

Common tools:

* Jenkins
* GitHub Actions
* GitLab

Example CI/CD pipeline:

```text
Developer
 │
 ▼
Git Repository
 │
 ▼
CI/CD Pipeline
 │
 ▼
Build Docker Image
 │
 ▼
Push Image to ECR
 │
 ▼
Deploy to EKS
```

This enables **continuous deployment of applications**.

---

# 17.8 Database Integration

Applications in EKS often use managed databases.

Common AWS database services:

* Amazon RDS
* Amazon DynamoDB

Example architecture:

```text
EKS Pods
 │
 ▼
Application API
 │
 ▼
Database (RDS / DynamoDB)
```

This separates **application logic from data storage**.

---

# 17.9 Example Real-World Architecture

Example production architecture:

```text
Users
 │
 ▼
Route 53
 │
 ▼
Application Load Balancer
 │
 ▼
EKS Cluster
 │
 ├── Pods
 ├── Services
 └── Deployments
 │
 ▼
RDS Database
 │
 ▼
CloudWatch Monitoring
```

This architecture uses multiple AWS services integrated with EKS.

---

# 17.10 Benefits of AWS Integration with EKS

✔ Seamless service integration
✔ High scalability
✔ Strong security model
✔ Simplified infrastructure management

---
---
# 18. CI/CD with Amazon EKS
---
![Image](https://d2908q01vomqb2.cloudfront.net/7719a1c782a1ba91c031a682a0a2f8658209adbf/2021/03/09/diagram.png)

![Image](https://miro.medium.com/1%2AU7Ab7y9FCa512RibpUT3ow.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A2000/1%2ACH2R5552IjZCTqhgaBpXHw.jpeg)

![Image](https://apim.docs.wso2.com/en/4.1.0/assets/img/deploy/mi-cicd-k8s.png)

CI/CD (Continuous Integration and Continuous Deployment) automates the process of **building, testing, and deploying applications** to Amazon Elastic Kubernetes Service.

Using CI/CD pipelines helps DevOps teams deploy applications **faster, more reliably, and with less manual work**.

---

# 18.1 What is CI/CD?

CI/CD stands for:

| Term                        | Meaning                           |
| --------------------------- | --------------------------------- |
| Continuous Integration (CI) | Automatically build and test code |
| Continuous Deployment (CD)  | Automatically deploy applications |

Simple workflow:

```text
Developer → Git Repository → Build → Test → Deploy → EKS
```

---

# 18.2 CI/CD Pipeline Architecture

Typical pipeline for EKS:

```text
Developer
 │
 ▼
Git Repository
 │
 ▼
CI Tool (Build & Test)
 │
 ▼
Docker Image Build
 │
 ▼
Push Image to ECR
 │
 ▼
Deploy to EKS
```

This automates the **complete application delivery process**.

---

# 18.3 Source Code Repository

Applications are stored in a version control system such as:

* Git
* GitHub
* GitLab

Example workflow:

```text
Developer pushes code → Git repository
```

This triggers the CI/CD pipeline.

---

# 18.4 Build Stage (CI)

During the CI stage:

1. Code is pulled from the repository
2. Application is built
3. Automated tests are executed

Common CI tools:

* Jenkins
* GitHub Actions
* GitLab CI/CD

Example pipeline:

```text
Git Commit
   │
   ▼
CI Pipeline
   │
   ▼
Run Tests
```

---

# 18.5 Build Docker Image

After successful testing, a container image is created using:

* Docker

Example command:

```bash
docker build -t my-app .
```

The image contains:

* Application code
* Dependencies
* Runtime environment

---

# 18.6 Push Image to Container Registry

After building the image, it is pushed to:

* Amazon Elastic Container Registry

Example workflow:

```text
Docker Image
   │
   ▼
Push to ECR
```

EKS will later pull this image for deployment.

---

# 18.7 Deploy to EKS

Deployment happens using Kubernetes manifests.

Example command:

```bash
kubectl apply -f deployment.yaml
```

Example deployment flow:

```text
ECR Image
   │
   ▼
Kubernetes Deployment
   │
   ▼
Pods Created in EKS
```

Applications become available to users after deployment.

---

# 18.8 GitOps Deployment

Modern DevOps teams use **GitOps tools** such as:

* Argo CD

GitOps workflow:

```text
Git Repository
   │
   ▼
Argo CD
   │
   ▼
Synchronize Kubernetes manifests
   │
   ▼
Deploy to EKS
```

Benefits:

✔ Automatic deployments
✔ Version-controlled infrastructure
✔ Easy rollbacks

---

# 18.9 Example Real DevOps Pipeline

Example production pipeline:

```text
Developer
 │
 ▼
GitHub
 │
 ▼
GitHub Actions Pipeline
 │
 ▼
Build Docker Image
 │
 ▼
Push Image to ECR
 │
 ▼
Deploy to EKS
 │
 ▼
Application Running
```

This pipeline supports **continuous delivery of microservices**.

---

# 18.10 Benefits of CI/CD with EKS

✔ Faster deployments
✔ Automated testing
✔ Reduced manual errors
✔ Consistent application releases

CI/CD pipelines are essential for **modern DevOps workflows**.

---
---
# 19. Real-World Amazon EKS Production Architecture
---
![Image](https://d2908q01vomqb2.cloudfront.net/fc074d501302eb2b93e2554793fcaf50b3bf7291/2025/04/02/ARCHBLOG-1141-arch-diagr-1024x669.png)

![Image](https://miro.medium.com/1%2AGnfRjWW--Y_IQeYEktUbPQ.png)

![Image](https://miro.medium.com/1%2ATyniYK6zt-6j6IuLf8xVXQ.png)

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2A_XeArtkIOVZ5k4H4eV49gQ.png)

A real production system using Amazon Elastic Kubernetes Service integrates multiple services from Amazon Web Services to deliver **scalable, secure, and highly available applications**.

Large companies commonly deploy **microservices architectures** using EKS.

---

# 19.1 High-Level Production Architecture

Typical architecture flow:

```text
Users
 │
 ▼
Route53 (DNS)
 │
 ▼
CloudFront (CDN)
 │
 ▼
Application Load Balancer
 │
 ▼
EKS Cluster
 │
 ├── Frontend Pods
 ├── Backend Pods
 └── API Pods
 │
 ▼
Database (RDS / DynamoDB)
```

This architecture supports **high traffic, scalability, and fault tolerance**.

---

# 19.2 User Request Flow

Example request flow in production:

```text
User Request
 │
 ▼
DNS Resolution
 │
 ▼
CDN Cache
 │
 ▼
Load Balancer
 │
 ▼
EKS Services
 │
 ▼
Pods
 │
 ▼
Database
```

Each component helps improve **performance and reliability**.

---

# 19.3 DNS Layer

DNS routing is handled by
Amazon Route 53.

Responsibilities:

* Domain name resolution
* Traffic routing
* Health checks

Example:

```text
example.com → Load Balancer
```

---

# 19.4 Content Delivery Layer

Static content is delivered using
Amazon CloudFront.

Benefits:

✔ Faster content delivery
✔ Global caching
✔ Reduced latency

Example content:

* Images
* Videos
* Static files

---

# 19.5 Load Balancer Layer

Traffic enters the cluster through:

* Application Load Balancer

Responsibilities:

* Distribute traffic
* Route requests to services
* Provide SSL termination

Example routing:

```text
/api → Backend Service
/web → Frontend Service
```

---

# 19.6 EKS Cluster Layer

Inside the EKS cluster:

```text
EKS Cluster
│
├── Namespace: frontend
│      └── React Pods
│
├── Namespace: backend
│      └── API Pods
│
└── Namespace: services
       └── Microservices Pods
```

Kubernetes manages:

* Pod scaling
* Pod scheduling
* Application deployment

---

# 19.7 Storage and Database Layer

Applications store data in managed AWS databases.

Common choices:

* Amazon RDS – relational databases
* Amazon DynamoDB – NoSQL databases

Example architecture:

```text
Application Pods
      │
      ▼
Database
```

Separating application and database improves **scalability and reliability**.

---

# 19.8 Container Image Storage

Container images are stored in:

* Amazon Elastic Container Registry

Example workflow:

```text
Developer
 │
 ▼
Build Docker Image
 │
 ▼
Push Image to ECR
 │
 ▼
Deploy to EKS
```

---

# 19.9 Monitoring and Logging

Production systems require monitoring.

Common tools:

* Amazon CloudWatch
* Prometheus
* Grafana

These tools monitor:

* CPU usage
* Memory usage
* Pod health
* Application logs

---

# 19.10 CI/CD Pipeline Integration

Production systems use automated pipelines.

Example pipeline:

```text
Developer
 │
 ▼
Git Repository
 │
 ▼
CI/CD Pipeline
 │
 ▼
Build Docker Image
 │
 ▼
Push to ECR
 │
 ▼
Deploy to EKS
```

This allows **continuous deployment of applications**.

---

# 19.11 Security Layer

Production environments include strong security.

Security tools include:

* AWS Identity and Access Management
* AWS Secrets Manager
* Kubernetes RBAC

Security ensures **controlled access to cluster resources**.

---

# 19.12 Example Enterprise Architecture

Example enterprise production setup:

```text
Users
 │
 ▼
Route53
 │
 ▼
CloudFront
 │
 ▼
Application Load Balancer
 │
 ▼
EKS Cluster
 │
 ├── Frontend Pods
 ├── Backend Pods
 └── API Pods
 │
 ▼
RDS Database
 │
 ▼
CloudWatch Monitoring
```

This architecture supports **large-scale applications used by millions of users**.

---
---
# 20. EKS vs Other Kubernetes Platforms
---
![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2A1fYlrnT0jR2Dw2gpCMLD6A.png)

![Image](https://media.licdn.com/dms/image/v2/D4D12AQEnVwj7N4sBhw/article-inline_image-shrink_1000_1488/article-inline_image-shrink_1000_1488/0/1698916377736?e=2147483647\&t=A3p9ZOowFwXz-oh1UhUBbGkF1aSwk7zOsMo-RdfWsag\&v=beta)

![Image](https://media2.dev.to/dynamic/image/width%3D1600%2Cheight%3D900%2Cfit%3Dcover%2Cgravity%3Dauto%2Cformat%3Dauto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fqolu2wml5wlic7xp0l6c.png)

![Image](https://hasura.io/blog/content/images/2019/03/gkevsaksvseks.png)

Managed Kubernetes platforms allow organizations to run Kubernetes clusters without managing the control plane infrastructure.

The three major cloud providers offer managed Kubernetes services:

* Amazon Elastic Kubernetes Service
* Google Kubernetes Engine
* Azure Kubernetes Service

These services provide similar functionality but differ in **features, integrations, and ecosystem**.

---

# 20.1 What is Managed Kubernetes?

Managed Kubernetes means the cloud provider manages important components like:

* Kubernetes control plane
* API server
* etcd database
* Cluster updates

Users only manage:

* Applications
* Pods
* Containers

Example:

```text
Cloud Provider → Manages Kubernetes infrastructure
User → Deploys applications
```

---

# 20.2 Amazon EKS Overview

Amazon Elastic Kubernetes Service is the Kubernetes service provided by **Amazon Web Services**.

Key features:

* Fully managed control plane
* Deep integration with AWS services
* High availability across multiple AZs
* Strong security with IAM integration

Best for:

* Organizations already using AWS
* Large production workloads

---

# 20.3 Google Kubernetes Engine (GKE)

Google Kubernetes Engine is the Kubernetes platform from **Google Cloud**.

Google originally created Kubernetes, so GKE has strong Kubernetes integration.

Key features:

* Advanced Kubernetes features
* Automatic upgrades
* Built-in monitoring tools

Best for:

* Kubernetes-focused workloads
* Cloud-native applications

---

# 20.4 Azure Kubernetes Service (AKS)

Azure Kubernetes Service is the managed Kubernetes platform from **Microsoft Azure**.

Key features:

* Integration with Azure services
* Active Directory authentication
* Simplified cluster management

Best for:

* Enterprises using Microsoft ecosystem

---

# 20.5 Feature Comparison

| Feature               | EKS        | GKE          | AKS             |
| --------------------- | ---------- | ------------ | --------------- |
| Cloud Provider        | AWS        | Google Cloud | Microsoft Azure |
| Kubernetes Management | Managed    | Managed      | Managed         |
| Security Integration  | IAM        | Google IAM   | Azure AD        |
| Monitoring            | CloudWatch | Stackdriver  | Azure Monitor   |
| Networking            | AWS VPC    | Google VPC   | Azure VNet      |

---

# 20.6 Ease of Use Comparison

| Platform | Ease of Setup    |
| -------- | ---------------- |
| GKE      | Easiest          |
| AKS      | Moderate         |
| EKS      | Slightly complex |

EKS requires more networking setup but provides **strong AWS ecosystem integration**.

---

# 20.7 Ecosystem Integration

Each platform integrates best with its own cloud services.

Example integrations:

| Platform | Integrated Services                     |
| -------- | --------------------------------------- |
| EKS      | ECR, CloudWatch, IAM                    |
| GKE      | Artifact Registry, Cloud Monitoring     |
| AKS      | Azure Container Registry, Azure Monitor |

---

# 20.8 Performance and Scalability

All platforms support:

* Auto scaling
* High availability
* Multi-zone clusters

However:

* GKE often provides **faster Kubernetes updates**
* EKS provides **better AWS service integration**
* AKS integrates well with **Microsoft enterprise tools**

---

# 20.9 Real-World Usage

Example company scenarios:

```text
AWS-based company → EKS
Google Cloud company → GKE
Microsoft enterprise → AKS
```

Many enterprises choose a platform based on their **existing cloud infrastructure**.

---

# 20.10 Summary Comparison

| Platform | Best For                          |
| -------- | --------------------------------- |
| EKS      | AWS-based architectures           |
| GKE      | Kubernetes-focused development    |
| AKS      | Microsoft enterprise environments |

All three services support **enterprise-grade Kubernetes deployments**.

---
---
# 21. Amazon EKS Best Practices
---
![Image](https://docs.aws.amazon.com/images/eks/latest/best-practices/images/networking/subnet_image.png)

![Image](https://docs.aws.amazon.com/images/eks/latest/best-practices/images/networking/subnet_eks-shared-subnets.png)

![Image](https://miro.medium.com/1%2AfhlgakTlSthE_HEdUHxSfQ.jpeg)

![Image](https://media.licdn.com/dms/image/v2/D5612AQHU9HkiztWVVw/article-cover_image-shrink_720_1280/article-cover_image-shrink_720_1280/0/1728044420341?e=2147483647\&t=uLbWJ-LoBSg5y_MstYG12NdUP5e9hu4uCYMlwuQm8pA\&v=beta)

Running workloads on Amazon Elastic Kubernetes Service in production requires following certain best practices to ensure **security, scalability, reliability, and cost efficiency**.

These best practices are commonly used by DevOps teams working with infrastructure on Amazon Web Services.

---

# 21.1 Use Multiple Availability Zones

Deploy worker nodes across **multiple Availability Zones**.

Example architecture:

```text
EKS Cluster
│
├── AZ-A → Worker Nodes
├── AZ-B → Worker Nodes
└── AZ-C → Worker Nodes
```

Benefits:

✔ High availability
✔ Fault tolerance
✔ Better load distribution

---

# 21.2 Use Managed Node Groups

Use **Managed Node Groups** instead of self-managed nodes.

Advantages:

* Automatic updates
* Node health monitoring
* Easy scaling

Managed nodes reduce operational complexity.

---

# 21.3 Use Private Subnets for Worker Nodes

Worker nodes should run inside **private subnets**.

Example network architecture:

```text
VPC
│
├── Public Subnet
│     └── Load Balancer
│
└── Private Subnet
      └── Worker Nodes
```

Benefits:

✔ Improved security
✔ Protection from direct internet access

---

# 21.4 Enable Auto Scaling

Use auto scaling for both **pods and nodes**.

Types of scaling:

| Scaling Type              | Purpose     |
| ------------------------- | ----------- |
| Horizontal Pod Autoscaler | Scale pods  |
| Cluster Autoscaler        | Scale nodes |

Example:

```text
Traffic Increase → Pods and Nodes scale automatically
```

---

# 21.5 Use Resource Requests and Limits

Define CPU and memory limits for pods.

Example YAML configuration:

```yaml
resources:
  requests:
    cpu: "200m"
    memory: "256Mi"
  limits:
    cpu: "500m"
    memory: "512Mi"
```

Benefits:

✔ Prevents resource overuse
✔ Improves cluster efficiency

---

# 21.6 Secure Access with IAM and RBAC

Use security controls like:

* AWS Identity and Access Management
* Kubernetes RBAC

Example:

```text
User → IAM Authentication → RBAC Authorization → EKS Cluster
```

This ensures **secure access management**.

---

# 21.7 Store Secrets Securely

Sensitive data should be stored securely using:

* AWS Secrets Manager
* AWS Key Management Service

Avoid storing credentials directly in application code.

---

# 21.8 Monitor Cluster Health

Use monitoring tools to track cluster performance.

Common monitoring services:

* Amazon CloudWatch
* Prometheus
* Grafana

Monitor:

* CPU usage
* Memory usage
* Pod status
* Node health

---

# 21.9 Use CI/CD for Deployments

Automate application deployments using CI/CD pipelines.

Popular tools:

* Jenkins
* GitHub Actions
* Argo CD

Example workflow:

```text
Developer → Git → CI/CD Pipeline → Build → Deploy to EKS
```

---

# 21.10 Regularly Update Clusters

Keep Kubernetes clusters updated to maintain security and stability.

Updates include:

* Kubernetes version upgrades
* Node updates
* Security patches

AWS provides managed upgrades for EKS clusters.

---

# 21.11 Backup and Disaster Recovery

Always implement backup strategies.

Important resources to backup:

* Kubernetes manifests
* Persistent volumes
* Database snapshots

This ensures recovery during failures.

---

# 21.12 Production Architecture Example

Example recommended production setup:

```text
Users
 │
 ▼
Route53
 │
 ▼
Application Load Balancer
 │
 ▼
EKS Cluster
 │
 ├── Pods
 ├── Services
 └── Deployments
 │
 ▼
Database
 │
 ▼
Monitoring Tools
```

This architecture supports **scalable and secure applications**.

---
---
# 22. Amazon EKS Troubleshooting
---
![Image](https://static.learnkube.com/28f6010f7a66c0986e9353611c34a67b.png)

![Image](https://miro.medium.com/1%2A32qJGDfk-6Ifl68PG8fwYQ.png)

![Image](https://cdn.prod.website-files.com/681e366f54a6e3ce87159ca4/68757f9e61edb27b795c9588_What-is-Crashloopbackoff-02.png)

![Image](https://static.learnkube.com/7bcf2c9e9dce01269c436a16b77b276f.png)

Troubleshooting is an important skill when managing clusters in Amazon Elastic Kubernetes Service.
Problems may occur due to **pod failures, networking issues, container errors, or node problems**.

DevOps engineers use Kubernetes commands and monitoring tools to **identify and fix issues quickly**.

---

# 22.1 Common EKS Problems

Some common issues in EKS clusters include:

| Problem             | Description               |
| ------------------- | ------------------------- |
| Pod not starting    | Container startup failure |
| Image pull error    | Container image not found |
| Node not ready      | Worker node issue         |
| Networking issue    | Pods cannot communicate   |
| High resource usage | CPU or memory overload    |

Understanding these issues helps **resolve cluster problems faster**.

---

# 22.2 Checking Cluster Resources

First step in troubleshooting is checking cluster resources.

Useful command:

```bash
kubectl get all
```

Example output:

```text
Pods
Services
Deployments
ReplicaSets
```

This shows the **current state of the cluster**.

---

# 22.3 Checking Pod Status

To check pod status:

```bash
kubectl get pods
```

Example output:

```text
NAME            STATUS
nginx-pod       Running
api-pod         CrashLoopBackOff
```

Common pod statuses:

| Status           | Meaning                       |
| ---------------- | ----------------------------- |
| Running          | Pod working normally          |
| Pending          | Pod waiting for resources     |
| CrashLoopBackOff | Container crashing repeatedly |
| ImagePullBackOff | Image cannot be downloaded    |

---

# 22.4 Viewing Pod Logs

Logs help identify application errors.

Command:

```bash
kubectl logs <pod-name>
```

Example:

```bash
kubectl logs nginx-pod
```

Logs may show:

* Application errors
* Configuration problems
* Runtime issues

---

# 22.5 Describing Pod Details

To see detailed information about a pod:

```bash
kubectl describe pod <pod-name>
```

Example output includes:

* Events
* Container status
* Error messages

Example:

```text
Failed to pull image
Back-off restarting container
```

---

# 22.6 Troubleshooting Image Pull Errors

Common error:

```text
ImagePullBackOff
```

Possible reasons:

* Incorrect image name
* Image not available in registry
* Authentication failure

Solution:

* Verify image name
* Check container registry access
* Ensure image exists in Amazon Elastic Container Registry

---

# 22.7 Troubleshooting Node Issues

Check node status:

```bash
kubectl get nodes
```

Example output:

```text
NAME           STATUS
node-1         Ready
node-2         NotReady
```

If node shows **NotReady**, possible causes include:

* Resource exhaustion
* Network issues
* Node failure

---

# 22.8 Checking Events

Cluster events provide useful troubleshooting information.

Command:

```bash
kubectl get events
```

Example events:

```text
Pod scheduled
Image pulled
Container started
```

Events help identify **recent cluster activities and errors**.

---

# 22.9 Monitoring with CloudWatch

Cluster logs and metrics can also be viewed using:

* Amazon CloudWatch

CloudWatch helps monitor:

* Node health
* Container logs
* Cluster metrics

This provides **centralized monitoring for EKS clusters**.

---

# 22.10 Example Troubleshooting Workflow

Typical debugging process:

```text
Application Not Working
        │
        ▼
Check Pods
        │
        ▼
View Logs
        │
        ▼
Check Events
        │
        ▼
Identify Issue
        │
        ▼
Fix Configuration
```

Following a structured workflow helps quickly identify the root cause.

---

# 22.11 Useful Troubleshooting Commands

Common Kubernetes debugging commands:

| Command              | Purpose             |
| -------------------- | ------------------- |
| kubectl get pods     | View pod status     |
| kubectl logs         | View container logs |
| kubectl describe pod | Detailed pod info   |
| kubectl get nodes    | Check node status   |
| kubectl get events   | View cluster events |

These commands are frequently used by **DevOps engineers in production environments**.

---

# 22.12 Best Practices for Troubleshooting

✔ Monitor cluster health regularly
✔ Enable logging and monitoring tools
✔ Check logs and events first
✔ Use debugging commands systematically

Proper troubleshooting ensures **stable and reliable Kubernetes clusters**.

---
---
# 23. Amazon EKS Interview Questions (50 DevOps Q&A)
---
![Image](https://miro.medium.com/1%2A34NrXxLL9CiSCQvtw94QnQ.png)

![Image](https://d1.awsstatic.com/onedam/marketing-channels/website/aws/en_US/solutions/approved/images/architecture-diagrams/a-cell-based-architecture-for-amazon-eks-main-architecture.2e4dc1e14cb73e5bbe8fe1708f14744efa87b41a.png)

![Image](https://miro.medium.com/1%2AiplZoNrpqB-qS95ZxYPAwQ.png)

![Image](https://cdn.shopaccino.com/igmguru/images/kubernetes-architecture-components-3528183568043978.jpg)

Below are **important interview questions and answers** related to Amazon Elastic Kubernetes Service and Kubernetes.
These questions are commonly asked in **DevOps and cloud interviews**.

---

# 23.1 Basic EKS Interview Questions

### 1. What is Amazon EKS?

Amazon EKS is a **managed Kubernetes service** provided by Amazon Web Services that allows users to run Kubernetes clusters without managing the control plane.

---

### 2. What is Kubernetes?

Kubernetes is an **open-source container orchestration platform** used to deploy, manage, and scale containerized applications.

---

### 3. What are the main components of EKS?

Main components include:

* Control Plane
* Worker Nodes
* Pods
* Services
* Deployments

---

### 4. What is a Kubernetes Pod?

A Pod is the **smallest deployable unit in Kubernetes** that contains one or more containers.

---

### 5. What is a Node in EKS?

A Node is a **worker machine (usually EC2 instance)** where pods run.

---

### 6. What is a Node Group?

A Node Group is a collection of worker nodes managed together in an EKS cluster.

---

### 7. What is the EKS Control Plane?

The Control Plane manages Kubernetes cluster operations like:

* Scheduling pods
* Maintaining cluster state
* API communication

---

### 8. What is etcd in Kubernetes?

etcd is a **distributed key-value database** used to store cluster configuration and state.

---

### 9. What is kubelet?

kubelet is an agent running on worker nodes that communicates with the Kubernetes API server and manages containers.

---

### 10. What is kube-proxy?

kube-proxy manages networking and routing between Kubernetes services and pods.

---

# 23.2 Intermediate EKS Interview Questions

### 11. What is a Deployment?

A Deployment manages pods and ensures the correct number of replicas are running.

---

### 12. What is a Service in Kubernetes?

A Service provides a **stable network endpoint** for accessing pods.

---

### 13. What are the types of Kubernetes Services?

Types include:

* ClusterIP
* NodePort
* LoadBalancer

---

### 14. What is Ingress?

Ingress manages **HTTP/HTTPS routing to services** inside the Kubernetes cluster.

---

### 15. What is Horizontal Pod Autoscaler?

Horizontal Pod Autoscaler automatically scales pods based on metrics like CPU usage.

---

### 16. What is Cluster Autoscaler?

Cluster Autoscaler automatically adds or removes worker nodes based on pod resource requirements.

---

### 17. What is a Persistent Volume (PV)?

A Persistent Volume is a storage resource in Kubernetes used for persistent data storage.

---

### 18. What is a Persistent Volume Claim (PVC)?

PVC is a request for storage by a pod.

---

### 19. What container registry is commonly used with EKS?

Amazon Elastic Container Registry is commonly used to store container images.

---

### 20. What is IRSA in EKS?

IRSA (IAM Roles for Service Accounts) allows Kubernetes pods to securely access AWS services using IAM roles.

---

# 23.3 Advanced EKS Interview Questions

### 21. How does networking work in EKS?

EKS uses **VPC networking**, where pods receive IP addresses from the VPC using the AWS VPC CNI plugin.

---

### 22. What is AWS VPC CNI?

AWS VPC CNI is a networking plugin that allows pods to use VPC IP addresses.

---

### 23. What is the difference between EKS and ECS?

| Feature                 | EKS           | ECS          |
| ----------------------- | ------------- | ------------ |
| Container orchestration | Kubernetes    | AWS native   |
| Complexity              | Higher        | Simpler      |
| Flexibility             | More flexible | AWS specific |

---

### 24. What are Managed Node Groups?

Managed Node Groups are worker nodes automatically managed by AWS.

---

### 25. What is AWS Fargate in EKS?

AWS Fargate allows running containers without managing servers.

---

### 26. How do you deploy applications to EKS?

Applications are deployed using Kubernetes manifests with commands like:

```bash
kubectl apply -f deployment.yaml
```

---

### 27. How do you expose applications externally in EKS?

Applications can be exposed using:

* LoadBalancer service
* Ingress controller

---

### 28. What monitoring tools are used with EKS?

Common tools:

* Amazon CloudWatch
* Prometheus
* Grafana

---

### 29. What security mechanisms exist in EKS?

Security mechanisms include:

* IAM authentication
* Kubernetes RBAC
* Network policies
* Secrets management

---

### 30. What is the role of kubectl?

kubectl is a CLI tool used to manage Kubernetes clusters.

---

# 23.4 Scenario-Based Interview Questions

### 31. How do you scale applications in EKS?

Using Horizontal Pod Autoscaler and Cluster Autoscaler.

---

### 32. How do you troubleshoot a failing pod?

Steps include:

* Check pod status
* View logs
* Describe pod
* Check events

---

### 33. What happens if a node fails?

Kubernetes automatically reschedules pods to another healthy node.

---

### 34. How do you perform rolling updates?

Use Deployment updates with rolling strategy.

---

### 35. How do you rollback a deployment?

Command:

```bash
kubectl rollout undo deployment <deployment-name>
```

---

### 36. How do you manage secrets securely?

Use Kubernetes secrets or integrate with
AWS Secrets Manager.

---

### 37. How do you secure communication between pods?

Using network policies and service mesh solutions.

---

### 38. How do you optimize EKS costs?

* Use Spot Instances
* Enable auto scaling
* Right-size instances

---

### 39. What is a namespace in Kubernetes?

Namespace divides the cluster into logical environments like dev, test, and production.

---

### 40. What is a DaemonSet?

DaemonSet ensures a pod runs on every worker node.

---

# 23.5 Expert-Level Questions

### 41. What is GitOps in Kubernetes?

GitOps uses Git as the source of truth for cluster configurations.

---

### 42. What tool is used for GitOps deployments?

Argo CD is commonly used.

---

### 43. How do you secure container images?

Use trusted registries and image scanning tools.

---

### 44. How do you manage Kubernetes configuration?

Using ConfigMaps and environment variables.

---

### 45. What is a StatefulSet?

StatefulSet manages stateful applications like databases.

---

### 46. How do you monitor pod performance?

Using Prometheus metrics and Grafana dashboards.

---

### 47. What is Helm?

Helm is a package manager for Kubernetes.

---

### 48. How do you implement high availability in EKS?

Use:

* Multi-AZ nodes
* Load balancers
* Multiple pod replicas

---

### 49. How do you backup Kubernetes clusters?

Backup:

* Kubernetes manifests
* Persistent volumes
* Database snapshots

---

### 50. What are common EKS best practices?

* Use private subnets for nodes
* Enable auto scaling
* Monitor clusters
* Secure access with IAM

---
