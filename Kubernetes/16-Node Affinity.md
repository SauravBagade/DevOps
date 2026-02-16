# 📘 Kubernetes Node Affinity 

This guide is written so you can **study, practice, revise, and teach** Node Affinity properly.

---

# 1️⃣ What is Node Affinity?

**Node Affinity = Control where a Pod runs (on which node)**

Kubernetes scheduler normally:

> Pod → Any available node

With Node Affinity:

> Pod → Only specific nodes (based on labels)

---

## Real Meaning

You are giving Kubernetes a rule:

> “Run this workload only on machines suitable for it”

Examples:

* Database → SSD node
* AI app → GPU node
* Production → Secure node
* Dev → Cheap node
* App near DB → Same zone

---

# 2️⃣ How Kubernetes Decides Placement

Scheduler checks in order:

1. Taints & Tolerations
2. Node Selector
3. **Node Affinity**
4. Resources (CPU/RAM)
5. Scoring (best node)

So Node Affinity = **Placement rule**

---

# 3️⃣ Node Labels (Very Important Concept)

Affinity works using labels.

Node has metadata:

```
key=value
```

Examples:

```
env=production
disk=ssd
gpu=true
zone=ap-south-1a
```

---

## View Node Labels

```bash
kubectl get nodes --show-labels
```

---

## Add Label

```bash
kubectl label nodes worker1 env=production
kubectl label nodes worker1 disk=ssd
kubectl label nodes worker2 env=dev
```

---

## Remove Label

```bash
kubectl label nodes worker1 env-
```

---

# 4️⃣ Types of Node Affinity

| Type                                            | Meaning   | Behaviour    |
| ----------------------------------------------- | --------- | ------------ |
| requiredDuringSchedulingIgnoredDuringExecution  | Hard Rule | MUST match   |
| preferredDuringSchedulingIgnoredDuringExecution | Soft Rule | Try to match |

---

# 5️⃣ Hard Rule (Required Affinity)

If node not match → Pod Pending

## YAML

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-ssd
spec:
  containers:
  - name: nginx
    image: nginx
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: disk
            operator: In
            values:
            - ssd
```

Apply:

```bash
kubectl apply -f pod.yml
```

Check:

```bash
kubectl get pod -o wide
kubectl describe pod nginx-ssd
```

If no node:

```
0/3 nodes available: node(s) didn't match Pod's node affinity
```

---

# 6️⃣ Soft Rule (Preferred Affinity)

Pod runs anywhere but prefers matching node.

```yaml
affinity:
  nodeAffinity:
    preferredDuringSchedulingIgnoredDuringExecution:
    - weight: 100
      preference:
        matchExpressions:
        - key: disk
          operator: In
          values:
          - ssd
```

---

# 7️⃣ Operators (Interview Important)

| Operator     | Meaning              |
| ------------ | -------------------- |
| In           | Value must match     |
| NotIn        | Value must NOT match |
| Exists       | Key present          |
| DoesNotExist | Key absent           |
| Gt           | Greater than         |
| Lt           | Less than            |

Example:

```yaml
- key: cpu
  operator: Gt
  values: ["4"]
```

---

# 8️⃣ Multiple Conditions

## AND Condition

All must match

```yaml
matchExpressions:
- key: env
  operator: In
  values: ["production"]
- key: disk
  operator: In
  values: ["ssd"]
```

---

## OR Condition

Any one match

```yaml
nodeSelectorTerms:
- matchExpressions:
  - key: env
    operator: In
    values: ["production"]
- matchExpressions:
  - key: gpu
    operator: In
    values: ["true"]
```

---

# 9️⃣ Node Selector vs Node Affinity

| Feature     | nodeSelector | nodeAffinity |
| ----------- | ------------ | ------------ |
| Complexity  | Simple       | Advanced     |
| Operators   | Only =       | Many         |
| Soft Rule   | ❌            | ✅            |
| AND/OR      | ❌            | ✅            |
| Recommended | Old          | Modern       |

Example nodeSelector:

```yaml
nodeSelector:
  env: production
```

---

# 🔟 Real Production Example (Dev & Prod Separation)

## Label Nodes

```bash
kubectl label nodes worker1 env=production
kubectl label nodes worker2 env=production
kubectl label nodes worker3 env=dev
```

---

## Production Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: prod-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: prod
  template:
    metadata:
      labels:
        app: prod
    spec:
      containers:
      - name: nginx
        image: nginx
      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
            - matchExpressions:
              - key: env
                operator: In
                values:
                - production
```

---

# 11️⃣ Zone Based Scheduling (Cloud)

Check zones:

```bash
kubectl get nodes -L topology.kubernetes.io/zone
```

Run app in zone:

```yaml
- key: topology.kubernetes.io/zone
  operator: In
  values:
  - ap-south-1a
```

---

# 12️⃣ Troubleshooting

## Pod Pending

```bash
kubectl describe pod <pod>
```

Common error:

```
didn't match Pod's node affinity
```

## Check labels

```bash
kubectl get nodes --show-labels
```

---

# 13️⃣ Important Commands Cheat Sheet

```bash
kubectl get nodes
kubectl get nodes --show-labels
kubectl label nodes node1 env=production
kubectl label nodes node1 env-
kubectl apply -f file.yml
kubectl delete -f file.yml
kubectl get pods -o wide
kubectl describe pod <pod>
```

---

# 14️⃣ Best Practices (Production)

✔ Use naming standard

```
env=prod
tier=db
type=gpu
zone=ap-south-1a
```

✔ Combine with:

* Taints & Tolerations
* Pod Anti-Affinity
* Topology Spread Constraints

---

# 🧠 Interview Revision (Quick)

**Q: What happens if required affinity not match?**
Pod Pending

**Q: Does it reschedule running pods?**
No (IgnoredDuringExecution)

**Q: Difference preferred vs required?**
Soft vs Hard rule

**Q: Purpose?**
Control workload placement

---

# 🏁 Final Summary

Node Affinity helps in:

* Performance optimization
* Environment isolation
* Hardware specific workloads
* Cost control
* High availability

> Right Pod → Right Node

---
