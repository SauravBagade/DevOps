# 🚀 Kubernetes DaemonSet — Complete Guide

---

## 📘 Overview

**DaemonSet** ensures that exactly one Pod runs on every selected Node.

> New node added → Pod automatically created
> Node removed → Pod deleted

Used for node‑level services.

Examples:

* Log collectors (Fluentd)
* Monitoring agents (Node Exporter)
* Security agents
* CNI networking pods

---

## 🎯 Why Use DaemonSet?

| Feature           | Description                   |
| ----------------- | ----------------------------- |
| One pod per node  | Automatically runs everywhere |
| Auto node join    | New node gets pod             |
| Node level apps   | Monitoring / logging          |
| No scaling needed | Node count = Pod count        |

---

# 🛠️ Step‑by‑Step Practical

---

## 🔹 Step 1 — Namespace

```bash
kubectl create namespace nginx
kubectl get ns
```

---

## 🔹 Step 2 — DaemonSet YAML

```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: nginx-daemon
  namespace: nginx
spec:
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
kubectl apply -f daemonset.yaml
```

---

## 🔹 Step 4 — Verify

```bash
kubectl get ds -n nginx
kubectl get pods -o wide -n nginx
kubectl describe ds nginx-daemon -n nginx
```

---

## 🔹 Step 5 — Node Level Behavior

Add new node → pod auto created

Check node count:

```bash
kubectl get nodes
kubectl get pods -o wide -n nginx
```

---

## 🔹 Step 6 — Delete Pod (Self Healing)

```bash
kubectl delete pod <pod-name> -n nginx
kubectl get pods -n nginx
```

---

## 🔹 Step 7 — Rolling Update (Image Change)

```bash
kubectl set image ds/nginx-daemon nginx=nginx:1.27 -n nginx
kubectl rollout status ds/nginx-daemon -n nginx
```

---

## 🔹 Step 8 — Rollout History

```bash
kubectl rollout history ds/nginx-daemon -n nginx
kubectl rollout history ds/nginx-daemon --revision=2 -n nginx
```

---

## 🔹 Step 9 — Rollback

```bash
kubectl rollout undo ds/nginx-daemon -n nginx
kubectl rollout undo ds/nginx-daemon --to-revision=1 -n nginx
```

---

## 🔹 Step 10 — Update Strategy

Rolling update config example:

```yaml
updateStrategy:
  type: RollingUpdate
  rollingUpdate:
    maxUnavailable: 1
```

OnDelete strategy:

```yaml
updateStrategy:
  type: OnDelete
```

Apply change:

```bash
kubectl apply -f daemonset.yaml
```

---

## 🔹 Step 11 — Node Selector

Label node:

```bash
kubectl label nodes <node-name> type=worker
```

DaemonSet config:

```yaml
nodeSelector:
  type: worker
```

---

## 🔹 Step 12 — Taints & Tolerations

Taint node:

```bash
kubectl taint nodes <node-name> dedicated=monitor:NoSchedule
```

Add toleration in YAML:

```yaml
tolerations:
- key: "dedicated"
  operator: "Equal"
  value: "monitor"
  effect: "NoSchedule"
```

---

## 🔹 Step 13 — Exec Into Pod

```bash
kubectl exec -it <pod-name> -n nginx -- bash
curl localhost
```

---

## 🔹 Step 14 — Logs

```bash
kubectl logs <pod-name> -n nginx
kubectl logs -f <pod-name> -n nginx
```

---

## 🔹 Step 15 — Expose Service (Optional)

```bash
kubectl expose ds nginx-daemon --port=80 --target-port=80 --name=nginx-svc -n nginx
kubectl expose ds nginx-daemon --type=NodePort --port=80 --target-port=80 --name=nginx-node -n nginx
kubectl get svc -o wide -n nginx
```

---

## 🔹 Step 16 — Output Formats

```bash
kubectl get ds nginx-daemon -n nginx -o yaml
kubectl get ds nginx-daemon -n nginx -o json
kubectl get pods -o wide -n nginx
```

---

## 🔹 Step 17 — Labels & Annotations

```bash
kubectl label ds nginx-daemon env=prod -n nginx
kubectl annotate ds nginx-daemon owner=devops -n nginx
```

---

## 🔹 Step 18 — Patch Update

```bash
kubectl patch ds nginx-daemon -p '{"spec":{"template":{"spec":{"containers":[{"name":"nginx","image":"nginx:1.27"}]}}}}' -n nginx
```

---

## 🔹 Step 19 — Delete

```bash
kubectl delete ds nginx-daemon -n nginx
kubectl delete namespace nginx
```

---

# 📦 Get All Resources

```bash
kubectl get all -n nginx
kubectl get ds -n nginx
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
