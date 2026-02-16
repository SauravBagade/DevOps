# 🚫 Kubernetes Taints and Tolerations – Complete Guide

---

## 1️⃣ What are Taints and Tolerations?

**Taints and Tolerations** are Kubernetes scheduling features used to **control which pods can run on which nodes**.

* **Taint** → Applied on a **node** (repels pods)
* **Toleration** → Applied on a **pod** (allows pod to be scheduled on tainted node)

📌 Rule:

> *Pods do NOT get scheduled on tainted nodes unless they tolerate the taint.*

---

## 2️⃣ Why Taints and Tolerations are Needed (Real-World Reason)

In production clusters:

* Some nodes are **special-purpose** (GPU, DB, infra)
* Some nodes are **dedicated** to specific teams
* Control plane nodes should not run application pods

### Without Taints ❌

* Any pod can run on any node
* Critical nodes may get overloaded
* Poor workload isolation

### With Taints & Tolerations ✅

* Strong workload isolation
* Better security & stability
* Dedicated nodes for specific workloads

---

## 3️⃣ Basic Terminology

| Term       | Meaning                             |
| ---------- | ----------------------------------- |
| Taint      | A key-value-effect set on a node    |
| Toleration | Permission on pod to tolerate taint |
| Scheduler  | Checks taints before scheduling     |

---

## 4️⃣ Taint Structure

A taint has **3 parts**:

```
<key>=<value>:<effect>
```

### Example

```
dedicated=database:NoSchedule
```

---

## 5️⃣ Taint Effects (VERY IMPORTANT)

### 1️⃣ NoSchedule

* New pods **will not be scheduled**
* Existing pods remain running

### 2️⃣ PreferNoSchedule

* Scheduler **tries to avoid** the node
* Not a hard restriction

### 3️⃣ NoExecute

* New pods not scheduled
* Existing pods **are evicted** (unless tolerated)

---

## 6️⃣ Adding a Taint to a Node

```bash
kubectl taint nodes node-1 dedicated=database:NoSchedule
```

✔ Node now repels pods without toleration

---

## 7️⃣ Removing a Taint

```bash
kubectl taint nodes node-1 dedicated=database:NoSchedule-
```

---

## 8️⃣ Viewing Node Taints

```bash
kubectl describe node node-1
```

Look under **Taints:** section

---

## 9️⃣ What is a Toleration?

A **toleration** allows a pod to be scheduled on a node with matching taint.

📌 Tolerations **do not force** scheduling – they only **allow** it.

---

## 🔟 Basic Toleration Example

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: db-pod
spec:
  tolerations:
  - key: "dedicated"
    operator: "Equal"
    value: "database"
    effect: "NoSchedule"
  containers:
  - name: mysql
    image: mysql
```

✔ Pod can run on node tainted with `dedicated=database:NoSchedule`

---

## 1️⃣1️⃣ Toleration Operators

| Operator | Meaning                       |
| -------- | ----------------------------- |
| Equal    | Key & value must match        |
| Exists   | Key must exist, value ignored |

### Exists Example

```yaml
- key: "dedicated"
  operator: "Exists"
  effect: "NoSchedule"
```

---

## 1️⃣2️⃣ TolerationSeconds (NoExecute Only)

Used with **NoExecute** taint

```yaml
- key: "dedicated"
  operator: "Equal"
  value: "database"
  effect: "NoExecute"
  tolerationSeconds: 60
```

✔ Pod stays for 60 seconds before eviction

---

## 1️⃣3️⃣ Default Kubernetes Taints

### Control Plane Node Taint

```
node-role.kubernetes.io/control-plane:NoSchedule
```

✔ Prevents app pods from running on control plane

---

## 1️⃣4️⃣ Taints vs NodeSelector vs NodeAffinity

| Feature    | Taints & Tolerations | NodeSelector | NodeAffinity        |
| ---------- | -------------------- | ------------ | ------------------- |
| Applied on | Node + Pod           | Pod          | Pod                 |
| Purpose    | Repel pods           | Attract pods | Advanced attraction |
| Strength   | Strong               | Simple       | Flexible            |

📌 Best practice:

* **Taints** → Keep pods out
* **Affinity** → Pull pods in

---

## 1️⃣5️⃣ Real-World Use Cases

### 🧠 Case 1: Dedicated DB Nodes

* Taint DB nodes
* Only DB pods tolerate

### 🧠 Case 2: GPU Nodes

```
nvidia.com/gpu=true:NoSchedule
```

### 🧠 Case 3: Team Isolation

```
team=dev:NoSchedule
team=qa:NoSchedule
```

---

## 1️⃣6️⃣ Taints + Tolerations + ResourceQuota (Production)

* ResourceQuota → Limits total usage
* Taints → Isolate nodes
* Tolerations → Allow specific pods

✔ Strong multi-tenant isolation

---

## 1️⃣7️⃣ What Happens If No Toleration Exists?

❌ Pod stays in **Pending** state

```bash
kubectl describe pod <pod-name>
```

Shows:

```
0/3 nodes are available: taint not tolerated
```

---

## 1️⃣8️⃣ Common Interview Questions

### Q1. Do tolerations guarantee scheduling?

❌ No

### Q2. Can a pod tolerate multiple taints?

✅ Yes

### Q3. Can one toleration match multiple taints?

❌ No

### Q4. Difference between NoSchedule & NoExecute?

* NoSchedule → no new pods
* NoExecute → evict existing pods

---

## 1️⃣9️⃣ Production Best Practices

✅ Use taints for critical nodes
✅ Avoid overusing PreferNoSchedule
✅ Combine with NodeAffinity
✅ Label + taint nodes clearly
✅ Document node purposes

---

## 2️⃣0️⃣ Common Mistakes

❌ Using tolerations without taints
❌ Forgetting NoExecute eviction
❌ Using taints instead of quotas

---

## 2️⃣1️⃣ Summary

✔ Taints repel pods from nodes
✔ Tolerations allow pods on tainted nodes
✔ Used for node isolation
✔ Critical for production clusters
✔ Very common interview topic

---
