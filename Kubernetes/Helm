# 🚀 Kubernetes **HELM — Complete Guide**

---

## 📘 What is Helm?

**Helm = Package Manager for Kubernetes (like apt, yum, npm for k8s)**

Instead of writing 10–50 YAML files manually, Helm bundles them into a reusable **Chart** and deploys with one command.

👉 Deploy application
👉 Configure environments (dev/prod)
👉 Upgrade versions
👉 Rollback safely

Helm uses **templates + values** to dynamically generate Kubernetes manifests. ([Wikipedia][1])

---

## ❗ Problem Without Helm

| Without Helm  | With Helm          |
| ------------- | ------------------ |
| 20 YAML files | 1 chart            |
| Manual edit   | values.yaml config |
| Hard upgrade  | helm upgrade       |
| No history    | versioned releases |
| Risky deploy  | rollback           |

---

## 🧠 Core Helm Concepts

| Concept    | Meaning                             |
| ---------- | ----------------------------------- |
| Chart      | Application package (k8s templates) |
| Release    | Running instance of chart           |
| Repository | Chart store (like Docker Hub)       |
| Values     | Configuration inputs                |
| Template   | Dynamic YAML generator              |
| Revision   | Each upgrade version                |

Installing a chart creates a **release instance** in cluster. ([Edge Delta][2])

---

# 🏗️ Helm Architecture

Helm 3 works **client → Kubernetes API** (no server/Tiller)

```
Developer
   ↓
helm CLI
   ↓
Kubernetes API
   ↓
Cluster Resources
```

Simple + secure architecture. ([Edge Delta][2])

---

# 📂 Helm Chart Structure

```
mychart/
 ├── Chart.yaml
 ├── values.yaml
 ├── templates/
 │     ├── deployment.yaml
 │     ├── service.yaml
 │     └── ingress.yaml
 ├── charts/
 └── README.md
```

* `Chart.yaml` → metadata
* `values.yaml` → default config
* `templates/` → dynamic manifests ([Helm][3])

---

# 🛠️ Install Helm

## Linux

```bash
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
helm version
```

## Verify cluster

```bash
kubectl get nodes
```

---

# 📦 Helm Repositories

### Add repo

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
```

### Update repo

```bash
helm repo update
```

### Search charts

```bash
helm search repo nginx
```

([Medium][4])

---

# 🚀 Deploy Application (Install)

```bash
helm install my-nginx bitnami/nginx
```

### Install in namespace

```bash
helm install my-nginx bitnami/nginx -n web --create-namespace
```

---

# ⚙️ Configuration using values.yaml

Instead of editing YAML files:

### values.yaml

```yaml
service:
  type: NodePort
  port: 80

replicaCount: 3
```

### Apply config

```bash
helm install myapp ./mychart -f values.yaml
```

You can override via CLI:

```bash
helm install myapp ./mychart --set replicaCount=5
```

([Helm][5])

---

# 🔄 Upgrade Application

```bash
helm upgrade myapp ./mychart -f values.yaml
```

### Safe Production Upgrade

```bash
helm upgrade myapp ./mychart --atomic
```

Automatic rollback if fails. ([OneUptime][6])

---

# ⏪ Rollback (Most Important Feature)

Check history:

```bash
helm history myapp
```

Rollback:

```bash
helm rollback myapp 2
```

Rollback previous:

```bash
helm rollback myapp 0
```

([Helm][7])

---

# 📊 Manage Releases

| Command              | Purpose         |
| -------------------- | --------------- |
| helm list            | Show releases   |
| helm status myapp    | Release status  |
| helm history myapp   | Version history |
| helm uninstall myapp | Delete app      |

---

# 🧩 Create Your Own Chart

```bash
helm create mychart
cd mychart
```

### Install locally

```bash
helm install testapp .
```

---

# 🧠 Templating Example

### deployment.yaml

```yaml
replicas: {{ .Values.replicaCount }}
```

### values.yaml

```yaml
replicaCount: 2
```

Helm replaces values dynamically.

---

# 🌍 Environment Based Deployments

## Dev

```bash
helm install app ./chart -f values-dev.yaml
```

## Prod

```bash
helm install app ./chart -f values-prod.yaml
```

---

# 🧪 Debugging

```bash
helm template ./chart
helm lint ./chart
helm get all myapp
```

---

# 🔐 Best Practices

✔ Use separate values per env
✔ Always use --atomic in prod
✔ Store charts in repo
✔ Never hardcode secrets
✔ Use helm upgrade, not delete/install

Helm charts are reusable across environments via repositories. ([Codefresh][8])

---

# 🏭 CI/CD Workflow (Real DevOps)

```
Git Push
   ↓
CI Build Docker Image
   ↓
Update values.yaml
   ↓
helm upgrade --install
   ↓
Auto rollout
```

---

# 🏁 Final Understanding

Helm manages **Application Lifecycle**

| Stage     | Helm Command |
| --------- | ------------ |
| Deploy    | install      |
| Configure | values       |
| Update    | upgrade      |
| Monitor   | status       |
| Recover   | rollback     |
| Remove    | uninstall    |

---
