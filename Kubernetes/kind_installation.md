# Kind Installation (Ubuntu)

Recommended specs:

| Cluster Size     | EC2 Recommended   |
| ---------------- | ----------------- |
| 1 node (default) | t3.medium / 2 GB+ |
| 3 nodes          | t3.large / 4 GB+  |
| 5 nodes          | t3.xlarge / 8 GB+ |

## 1. Create Working Directory

```bash
mkdir kind
cd kind
```
---

## **2. Install Docker**

Update packages:

```bash
sudo apt update -y
sudo apt install -y docker.io
```

Enable & start Docker:

```bash
sudo systemctl enable --now docker
```

Allow current user to run docker:

```bash
sudo usermod -aG docker $USER
```

Logout & login once.

Verify:

```bash
docker --version
docker run hello-world
```

---

## **3. Install KIND**

Check CPU architecture:

```bash
uname -m
```

### For x86_64:

```bash
curl -Lo kind https://kind.sigs.k8s.io/dl/v0.29.0/kind-linux-amd64
```

### For ARM64:

```bash
curl -Lo kind https://kind.sigs.k8s.io/dl/v0.29.0/kind-linux-arm64
```

Make executable:

```bash
chmod +x kind
sudo mv kind /usr/local/bin/
```

Verify:

```bash
kind --version
```

---

## **4. Install kubectl**

Get latest stable version:

```bash
VERSION=$(curl -Ls https://dl.k8s.io/release/stable.txt)
```

Download binary:

### For x86_64:

```bash
curl -Lo kubectl https://dl.k8s.io/release/${VERSION}/bin/linux/amd64/kubectl
```

### For ARM64:

```bash
curl -Lo kubectl https://dl.k8s.io/release/${VERSION}/bin/linux/arm64/kubectl
```

Make executable:

```bash
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
```

Verify:

```bash
kubectl version --client --output=yaml
```

---

## **5. Verify All Tools Installed**

```bash
docker --version
kind --version
kubectl version --client
```

---

## **6. Create KIND Multi-Node Cluster**

Create config file:

```yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane
    image: kindest/node:v1.30.4
  - role: worker
    image: kindest/node:v1.30.4
  - role: worker
    image: kindest/node:v1.30.4
```

Save the file as: `kind-config.yaml`

Create cluster:

```bash
kind create cluster --config kind-config.yaml --name kind
```

Verify nodes:

```bash
kubectl get nodes
kubectl get pods -A
kubectl cluster-info
```

---

## **7. Deploy Kubernetes Dashboard**

Apply dashboard manifest:

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml
```

Check deployment:

```bash
kubectl -n kubernetes-dashboard get pods
```

---

## **8. Create Admin User for Dashboard**

Create file: `dashboard-admin-user.yml`

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: admin-user
  namespace: kubernetes-dashboard
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: admin-user
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- kind: ServiceAccount
  name: admin-user
  namespace: kubernetes-dashboard
```

Apply:

```bash
kubectl apply -f dashboard-admin-user.yml
```

---

## **9. Generate Dashboard Login Token**

```bash
kubectl -n kubernetes-dashboard create token admin-user
```

Copy the token shown — used for login.

---

## **10. Access Dashboard**

Start proxy:

```bash
kubectl proxy
```
or  currnt ip not localhost
``
kubectl proxy --port=8001 --address=0.0.0.0 -accept-hosts='.*'
``
local machine any terminal like git terminal login instance ssh

```
ssh -i saurav.pem -L 8001:localhost:8001 ubuntu@52.55.100.87
```

Open browser:

```
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/
```

Select **Token** login → paste token.

---

## **11. Delete Cluster (Optional)**

```bash
kind delete cluster --name kind
```

---
