# 🚀 Kubernetes Deployment — Complete Guide

---

## 📘 Overview

**Deployment** manages ReplicaSets and Pods and provides safe updates.

> Pod crash → recreated
> Update image → rolling update
> Problem → rollback

Deployment Responsibilities:

* Maintain desired pods
* Rolling updates
* Rollback support
* Version history

---

## 🎯 Why Use Deployment?

| Feature          | Description                |
| ---------------- | -------------------------- |
| Self healing     | Recreates failed pods      |
| Scaling          | Increase / decrease pods   |
| Rolling update   | Zero downtime release      |
| Rollback         | Return to previous version |
| Production ready | Yes                        |

---

# 🛠️ Step-by-Step Practical

---

## 🔹 Step 1 — Namespace

```bash
kubectl create namespace nginx
kubectl get ns
```

---

## 🔹 Step 2 — Deployment YAML

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deploy
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

## 🔹 Step 3 — Apply

```bash
kubectl apply -f deployment.yaml
```

---

## 🔹 Step 4 — Verify

```bash
kubectl get deploy -n nginx
kubectl get rs -n nginx
kubectl get pods -n nginx
kubectl describe deploy nginx-deploy -n nginx
```

---

## 🔹 Step 5 — Scaling

```bash
kubectl scale deploy nginx-deploy --replicas=5 -n nginx
kubectl scale deploy nginx-deploy --replicas=2 -n nginx
```

---

## 🔹 Step 6 — Rolling Update (Image Change)

```bash
kubectl set image deploy/nginx-deploy nginx=nginx:1.27 -n nginx
kubectl rollout status deploy/nginx-deploy -n nginx
```

---

## 🔹 Step 7 — Rollout History

```bash
kubectl rollout history deploy/nginx-deploy -n nginx
```

Specific revision:

```bash
kubectl rollout history deploy/nginx-deploy --revision=2 -n nginx
```

---

## 🔹 Step 8 — Rollback

```bash
kubectl rollout undo deploy/nginx-deploy -n nginx
```

Rollback to specific version:

```bash
kubectl rollout undo deploy/nginx-deploy --to-revision=1 -n nginx
```

---

## 🔹 Step 9 — Pause & Resume

```bash
kubectl rollout pause deploy/nginx-deploy -n nginx
kubectl rollout resume deploy/nginx-deploy -n nginx
```

---

## 🔹 Step 10 — Exec Into Pod

```bash
kubectl exec -it <pod-name> -n nginx -- bash
curl localhost
```

---

## 🔹 Step 11 — Logs

```bash
kubectl logs <pod-name> -n nginx
kubectl logs -f <pod-name> -n nginx
```

---

## 🔹 Step 12 — Expose Service

```bash
kubectl expose deploy nginx-deploy --port=80 --target-port=80 --name=nginx-svc -n nginx
kubectl expose deploy nginx-deploy --type=NodePort --port=80 --target-port=80 --name=nginx-node -n nginx
kubectl get svc -o wide -n nginx
```

---

## 🔹 Step 13 — Output Formats

```bash
kubectl get deploy nginx-deploy -n nginx -o yaml
kubectl get deploy nginx-deploy -n nginx -o json
kubectl get pods -o wide -n nginx
```

---

## 🔹 Step 14 — Labels & Annotations

```bash
kubectl label deploy nginx-deploy env=prod -n nginx
kubectl annotate deploy nginx-deploy owner=devops -n nginx
```

---

## 🔹 Step 15 — Patch Update

```bash
kubectl patch deploy nginx-deploy -p '{"spec":{"replicas":4}}' -n nginx
```

---

## 🔹 Step 16 — Env Variable Update

```bash
kubectl set env deploy/nginx-deploy APP=prod -n nginx
```

---

## 🔹 Step 17 — Resources

```bash
kubectl set resources deploy nginx-deploy -c nginx --limits=cpu=500m,memory=512Mi -n nginx
```

---

## 🔹 Step 18 — Delete

```bash
kubectl delete deploy nginx-deploy -n nginx
kubectl delete namespace nginx
```

---

# 📦 Get All Resources

```bash
kubectl get all -n nginx
kubectl get deploy -n nginx
kubectl get rs -n nginx
kubectl get pods -n nginx
kubectl get svc -n nginx
```

---

# 🧠 Debug Commands

```bash
kubectl get events -n nginx
kubectl top pod -n nginx
kubectl get pods -w -n nginx
```
