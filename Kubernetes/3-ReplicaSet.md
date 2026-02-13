# 🚀 Kubernetes ReplicaSet — Complete Guide

---

## 📘 Overview

**ReplicaSet** ensures that a specified number of identical Pods are always running.

> If a Pod crashes → ReplicaSet automatically creates a new Pod
> If extra Pods exist → ReplicaSet deletes extra Pods

ReplicaSet does only one job:
👉 **Maintain desired Pod count**

It does NOT support:

* Rollout history ❌
* Rollback ❌
* Proper updates ❌

---

## 🎯 Why Use ReplicaSet?

| Feature            | Description                           |
| ------------------ | ------------------------------------- |
| High availability  | Always keeps required pods running    |
| Self healing       | Recreates deleted or failed pods      |
| Load distribution  | Multiple pods serve traffic           |
| Base of Deployment | Deployment internally uses ReplicaSet |

---

# 🛠️ Step-by-Step Practical

---

## 🔹 Step 1 — Create Namespace

```bash
kubectl create namespace nginx
kubectl get ns
```

---

## 🔹 Step 2 — Create ReplicaSet YAML

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: nginx-replica
  namespace: nginx

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
        image: nginx:latest
        ports:
        - containerPort: 80
```

---

## 🔹 Step 3 — Apply ReplicaSet

```bash
kubectl apply -f replicaset.yaml
```

---

## 🔹 Step 4 — Verify

```bash
kubectl get rs -n nginx
kubectl get pods -n nginx
kubectl describe rs nginx-replica -n nginx
```

---

## 🔹 Step 5 — Labels

```bash
kubectl get pods --show-labels -n nginx
```

---

## 🔹 Step 6 — Self Healing Test

```bash
kubectl delete pod <pod-name> -n nginx
kubectl get pods -n nginx
```

---

## 🔹 Step 7 — Scaling

```bash
kubectl scale rs nginx-replica --replicas=5 -n nginx
kubectl scale rs nginx-replica --replicas=2 -n nginx
```

---

## 🔹 Step 8 — Edit Live

```bash
kubectl edit rs nginx-replica -n nginx
```

---

## 🔹 Step 9 — Exec Into Pod

```bash
kubectl exec -it <pod-name> -n nginx -- bash
curl localhost
```

---

## 🔹 Step 10 — Logs

```bash
kubectl logs <pod-name> -n nginx
kubectl logs -f <pod-name> -n nginx
```

---

## 🔹 Step 11 — Update Image (Limitation Demo)

```bash
kubectl set image rs/nginx-replica nginx=nginx:1.27 -n nginx
kubectl delete pod -l app=nginx -n nginx
```

---

## 🔹 Step 12 — Delete

```bash
kubectl delete rs nginx-replica -n nginx
kubectl delete namespace nginx
```

---

# 🧠 Deployment vs ReplicaSet

| Feature          | ReplicaSet | Deployment |
| ---------------- | ---------- | ---------- |
| Maintain pods    | ✅          | ✅          |
| Scaling          | ✅          | ✅          |
| Rolling update   | ❌          | ✅          |
| Rollback         | ❌          | ✅          |
| Production ready | ❌          | ✅          |

---

# 🔌 Expose Service

```bash
kubectl expose rs nginx-replica --port=80 --target-port=80 --name=nginx-svc -n nginx
kubectl expose rs nginx-replica --type=NodePort --port=80 --target-port=80 --name=nginx-node -n nginx
kubectl get svc -o wide -n nginx
```

---

# 📄 Output Formats

```bash
kubectl get rs nginx-replica -n nginx -o yaml
kubectl get rs nginx-replica -n nginx -o json
kubectl get pods -n nginx -o wide
```

---

# 📦 Get All Resources

```bash
kubectl get all -n nginx
kubectl get pods -n nginx
kubectl get rs -n nginx
kubectl get svc -n nginx
kubectl get pods --show-labels -n nginx
```

---

# 🧠 Debug Commands

```bash
kubectl get events -n nginx
kubectl top pod -n nginx
kubectl get pods -n nginx -w
```
