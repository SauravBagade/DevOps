# 🚀 **Kubeadm Installation Guide **

This guide explains how to install and configure a Kubernetes cluster using **kubeadm** on Ubuntu.

---

## 📌 Prerequisites

* Create 2 instance first control-plan , second worker-node
* Ubuntu 20.04 / 22.04 / 24.04 (recommended)
* sudo privileges
* Internet access
* Instance type: **t2.medium or higher**
* Minimum requirements:

  * 2 CPU
  * 4 GB RAM

---

# ☁️ AWS Setup (Security Group Configuration)

### Required Ports

| Port        | Protocol | Purpose               |
| ----------- | -------- | --------------------- |
| 22          | TCP      | SSH Access            |
| 6443        | TCP      | Kubernetes API Server |
| 2379-2380   | TCP      | etcd                  |
| 10250       | TCP      | Kubelet               |
| 30000-32767 | TCP      | NodePort Services     |

---

## Step 1 – Create Security Group

1. Go to **AWS Console → EC2 Dashboard**
2. Open **Security Groups**
3. Click **Create Security Group**

Example:

* **Name**: Kubernetes-Cluster-SG
* **Description**: Kubernetes cluster communication
* **VPC**: Default (or your own)

---

### Add Inbound Rules

* SSH (22) → Anywhere (or your IP)
* Custom TCP (6443) → Anywhere
* Custom TCP (30000-32767) → Anywhere
* Custom TCP (10250) → Anywhere

Save the Security Group.

---

## Step 2 – Attach Security Group

While launching EC2 instances:

* Choose **Kubernetes-Cluster-SG** as security group for both Master and Worker nodes.

---

# 🔧 Perform on BOTH Master & Worker Nodes

---

## 1. Disable Swap (MANDATORY)

```bash
sudo swapoff -a
sudo sed -i '/ swap / s/^/#/' /etc/fstab
```

---

## 2. Load Required Kernel Modules

```bash
cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
overlay
br_netfilter
EOF

sudo modprobe overlay
sudo modprobe br_netfilter
```

---

## 3. Configure Sysctl Networking

```bash
cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-iptables  = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward                 = 1
EOF

sudo sysctl --system
```

Verify:

```bash
lsmod | grep br_netfilter
lsmod | grep overlay
```

---

# 🐳 Install Container Runtime (containerd)

---

### Install Dependencies

```bash
sudo apt-get update
sudo apt-get install -y ca-certificates curl gnupg lsb-release
```

---

### Add Docker Repository

```bash
sudo install -m 0755 -d /etc/apt/keyrings

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo tee /etc/apt/keyrings/docker.asc > /dev/null

sudo chmod a+r /etc/apt/keyrings/docker.asc

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] \
  https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

---

### Install Containerd

```bash
sudo apt-get update
sudo apt-get install -y containerd.io
```

---

### Configure containerd

```bash
sudo mkdir -p /etc/containerd

containerd config default | sudo tee /etc/containerd/config.toml
```

Enable Systemd Cgroup:

```bash
sudo sed -i 's/SystemdCgroup = false/SystemdCgroup = true/' /etc/containerd/config.toml
```

Update pause image (latest):

```bash
sudo sed -i 's|sandbox_image = "registry.k8s.io/pause:.*"|sandbox_image = "registry.k8s.io/pause:3.9"|' /etc/containerd/config.toml
```

Restart containerd:

```bash
sudo systemctl restart containerd
sudo systemctl enable containerd
sudo systemctl status containerd
```

---

# ☸ Install Kubernetes Components (Latest Repo)

---

### Add Kubernetes Repository

```bash
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl gpg
```

```bash
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.30/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
```

```bash
echo "deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] \
https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /" | sudo tee /etc/apt/sources.list.d/kubernetes.list
```

---

### Install kubeadm, kubelet, kubectl

```bash
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```

---

# 👑 STEPS ONLY ON MASTER NODE

---

## 1. Initialize Kubernetes Cluster

```bash
sudo kubeadm init --pod-network-cidr=192.168.0.0/16
```

---

## 2. Configure kubectl Access

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

---

## 3. Install Network Plugin (Calico)

```bash
kubectl apply -f https://raw.githubusercontent.com/projectcalico/calico/v3.27.0/manifests/calico.yaml
```

---

## 4. Generate Join Command

```bash
kubeadm token create --print-join-command
```

Example Output:

```
kubeadm join 172.31.10.100:6443 --token abcdef.1234567890 \
--discovery-token-ca-cert-hash sha256:xxxxxxxx
```

👉 COPY THIS COMMAND – you will need it on worker nodes.

---

# 🖥️ ON WORKER NODES

---

## 1. Reset (If Previously Used)

```bash
sudo kubeadm reset -f
```

---

## 2. Join Worker to Cluster

Paste the join command from master and add:

* `sudo` at beginning
* `--v=5` at end

Example:

```bash
sudo kubeadm join 172.31.10.100:6443 \
--token abcdef.1234567890 \
--discovery-token-ca-cert-hash sha256:xxxxxx \
--cri-socket unix:///run/containerd/containerd.sock --v=5
```

---

# ✅ VERIFY CLUSTER

Run on MASTER node:

```bash
kubectl get nodes
```

You should see:

```
NAME       STATUS   ROLES           AGE
master     Ready    control-plane   5m
worker1    Ready    <none>          2m
worker2    Ready    <none>          2m
```

---
