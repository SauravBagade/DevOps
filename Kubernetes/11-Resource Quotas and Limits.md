# Resource Quotas and Limits 
There are **3 different levels** — many people confuse them:

| Level          | Applies To                      | Purpose                            |
| -------------- | ------------------------------- | ---------------------------------- |
| Container      | `resources.requests` & `limits` | Control individual container usage |
| Pod/Deployment | Same but inside template        | Controls all replicas              |
| Namespace      | `ResourceQuota` & `LimitRange`  | Controls team/project usage        |

---

# 1️⃣ Requests vs Limits (Most Important Concept)

| Field   | Meaning                                           |
| ------- | ------------------------------------------------- |
| request | Guaranteed minimum resource (scheduler uses this) |
| limit   | Maximum allowed resource (kernel enforces this)   |

👉 Kubernetes scheduler places Pod on node based on **requests only**
👉 But container cannot exceed **limits**

---

### Example Understanding

| CPU            | What Happens                     |
| -------------- | -------------------------------- |
| request = 200m | Node reserves 0.2 CPU            |
| limit = 500m   | Container can burst till 0.5 CPU |
| uses 800m      | ❌ throttled (slow)               |

| Memory          | What Happens              |
| --------------- | ------------------------- |
| request = 256Mi | Guaranteed RAM            |
| limit = 512Mi   | Max allowed               |
| uses 700Mi      | 💀 Pod Killed (OOMKilled) |

---

# 2️⃣ Add Resources in POD

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec:
  containers:
  - name: nginx
    image: nginx
    resources:
      requests:
        memory: "256Mi"
        cpu: "200m"
      limits:
        memory: "512Mi"
        cpu: "500m"
```

Apply:

```bash
kubectl apply -f pod.yml
kubectl describe pod nginx-pod
```

---

# 3️⃣ Add Resources in Deployment (REAL USE CASE)

💡 In real DevOps — always configure in **Deployment**, not Pod

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deploy
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
        resources:
          requests:
            cpu: "200m"
            memory: "256Mi"
          limits:
            cpu: "500m"
            memory: "512Mi"
```

Check usage:

```bash
kubectl top pod
kubectl describe pod <pod-name>
```

---

# 4️⃣ Namespace ResourceQuota (Team Control)

👉 Prevent one team from using entire cluster

```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: team-quota
  namespace: dev
spec:
  hard:
    pods: "10"
    requests.cpu: "2"
    requests.memory: 2Gi
    limits.cpu: "4"
    limits.memory: 4Gi
```

Apply:

```bash
kubectl create ns dev
kubectl apply -f quota.yml
kubectl describe quota -n dev
```

---

# 5️⃣ LimitRange (Default Limits Auto Apply)

If developer forgets limits → cluster rejects pod
So we set default automatically.

```yaml
apiVersion: v1
kind: LimitRange
metadata:
  name: default-limit
  namespace: dev
spec:
  limits:
  - default:
      cpu: "500m"
      memory: "512Mi"
    defaultRequest:
      cpu: "200m"
      memory: "256Mi"
    type: Container
```

---

# 🔥 What Happens in Real Cluster

| Situation         | Result             |
| ----------------- | ------------------ |
| No request        | Scheduler confused |
| No limit          | Pod can crash node |
| High request      | Pod Pending        |
| High memory usage | OOMKilled          |
| High CPU usage    | Throttled          |

---

# 🧠 Interview One-Line Answer

**Requests = scheduling guarantee**
**Limits = runtime restriction**

---

# 📊 Full Flow

Developer → Deployment → Container Limits → Namespace Quota → Node Capacity

---
