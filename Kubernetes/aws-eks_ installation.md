# 📘 **PRACTICAL DOCUMENTATION — EKS Cluster + NodeGroup + EC2 Tools + kubectl + Test (Complete)**

---

## **SECTION-0 — Overview**

This lab covers:

✔ Launch EC2 for Kubernetes tools
✔ Install AWS CLI + kubectl + helm + git + authenticator
✔ Create EKS Cluster (Manual / Auto-mode OFF)
✔ Create IAM Roles
✔ Create NodeGroup for Worker Nodes
✔ Connect EC2 → EKS (kubeconfig)
✔ Deploy Nginx Pod
✔ Expose via NodePort
✔ Access in Browser
✔ Validate

---

# **SECTION-1 — Launch EC2 for Kubernetes Tools**

### **Step-1: Launch EC2 Instance**

| Field    | Value                                        |
| -------- | -------------------------------------------- |
| AMI      | Ubuntu 22.04                                 |
| Type     | t2.medium                                    |
| Storage  | 20GB                                         |
| Key Pair | Yes                                          |
| SG       | Allow SSH + HTTP (Lab can allow All Traffic) |

Connect via SSH:

```bash
ssh -i key.pem ubuntu@<public-ip>
```

---

# **SECTION-2 — Install AWS Tools on EC2**

Switch to root:

```bash
sudo -i
```

Update:

```bash
apt update -y
```

---

## **Install AWS CLI**

```bash
apt install unzip -y
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
aws --version
```

Configure:

```bash
aws configure
```

Enter:

```
AWS Access Key ID
AWS Secret Access Key
Region = ap-south-1  (or us-east-1)
Output = json
```

---

## **Install kubectl (Official)**

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"
echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
kubectl version --client
```

---

## **Install Git**

```bash
apt install git -y
git --version
```

---

## **Install aws-iam-authenticator (sometimes needed)**

```bash
curl -o aws-iam-authenticator \
https://amazon-eks.s3.us-west-2.amazonaws.com/latest/2023-03-17/bin/linux/amd64/aws-iam-authenticator

chmod +x aws-iam-authenticator
mv aws-iam-authenticator /usr/local/bin/
aws-iam-authenticator version
```

---

## **Install Helm (Recommended)**

```bash
curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash
helm version
```

---

## **Enable kubectl Autocomplete**

```bash
apt install bash-completion -y
echo "source <(kubectl completion bash)" >> ~/.bashrc
echo "alias k=kubectl" >> ~/.bashrc
echo "complete -F __start_kubectl k" >> ~/.bashrc
source ~/.bashrc
```

---

# **SECTION-3 — Create EKS Cluster (Manual Mode)**

AWS Console → **EKS → Add Cluster**

### **Cluster Mode:**

```
Auto Mode → OFF
Manual Mode → ON
```

### **Create IAM Role (Cluster Role)**

IAM → Create Role → Service = EKS

Attach Policies:

✔ AmazonEKSClusterPolicy
✔ AmazonEKSServicePolicy

Role Name:

```
eks-cluster-role
```

### **Cluster Configuration**

| Field   | Value            |
| ------- | ---------------- |
| Name    | cluster          |
| Version | v1.33            |
| Role    | eks-cluster-role |

### **Networking Setup**

| Setting         | Value                    |
| --------------- | ------------------------ |
| VPC             | default                  |
| Subnets         | default public + private |
| SG              | default                  |
| Endpoint Access | Public & Private         |

> Public = kubectl allowed
> Private = secure internal traffic

Enable Logs (Optional):
✔ API ✔ Scheduler ✔ Controller-Manager

Click:

```
Create Cluster
```

Wait 10–15 mins for Active.

---

# **SECTION-4 — Create Worker Nodes (NodeGroup)**

### **Create IAM Role (Node Role)**

IAM → Create Role → Service = EC2

Attach Policies:

✔ AmazonEKSWorkerNodePolicy
✔ AmazonEKS_CNI_Policy
✔ AmazonEC2ContainerRegistryReadOnly

Role Name:

```
eks-node-role
```

### **Create NodeGroup**

EKS → cluster → Compute → Add Node Group

| Field    | Value               |
| -------- | ------------------- |
| Name     | nodegroup           |
| Role     | eks-node-role       |
| Instance | t3.medium           |
| Desired  | 2                   |
| Min      | 1                   |
| Max      | 4                   |
| Subnets  | Private recommended |

Click:

```
Create Node Group
```

AWS launches 2 Worker Nodes.

---

# **SECTION-5 — Connect EC2 to EKS (kubectl)**

Update kubeconfig:

```bash
aws eks update-kubeconfig --name cluster --region ap-south-1
```

Verify:

```bash
kubectl cluster-info
```

Check Nodes:

```bash
kubectl get nodes
```

Expected:

```
2 nodes Ready
```

---

# **SECTION-6 — Deploy Test Application**

Deploy nginx:

```bash
kubectl run mypod --image=nginx --port=80
```

Expose via NodePort:

```bash
kubectl expose pod mypod --type=nodeport --port=80
```

Check svc:

```bash
kubectl get svc
```

Example:

```
mypod NodePort 80:31845/TCP
```

Access in browser:

```
http://<NodePublicIP>:<NodePort>
```

Example:

```
http://3.109.24.88:31845
```

Output:
✔ **Welcome to nginx!**

---

# **SECTION-7 — Security Group Notes**

If NodePort not accessible:

→ Edit NodeGroup SG
Allow:

```
All Traffic → 0.0.0.0/0 (Lab only)
```

Prod hardening later:

```
Ports 22, 80, 443 only
```

---

# **SECTION-8 — Cleanup (Optional)**

```bash
kubectl delete svc mypod
kubectl delete pod mypod
```

---
