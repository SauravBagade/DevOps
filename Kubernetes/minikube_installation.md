# Minikube Installation (Ubuntu)

## 1. Create Working Directory

```bash
mkdir minikube
cd minikube
```

## 2. Update System & Install Requirements

```bash
sudo apt update
sudo apt install -y curl wget apt-transport-https
```

## 3. Install Docker (Container Runtime)

```bash
sudo apt install -y docker.io
sudo systemctl enable --now docker
sudo usermod -aG docker $USER && newgrp docker
```

## 4. Install Minikube Binary

```bash
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
chmod +x minikube
sudo mv minikube /usr/local/bin/
```

## 5. Install Kubectl Client

```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
```

## 6. Start Minikube

Recommended with Docker driver:

```bash
minikube start --driver=docker --vm=true
```

If resources are low:

```bash
minikube start --driver=docker --memory=2048 --cpus=2 --force
```

## 7. Verify Status

```bash
minikube status
minikube profile list
```

## 8. Kubernetes Validation

```bash
docker ps
kubectl get nodes
kubectl get pods -A
```

## Notes

* Docker driver avoids VirtualBox dependencies.
* Use `kubectl` for cluster interaction.
* Use `minikube delete` to reset cluster.
