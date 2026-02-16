# 🧭 Kubernetes Namespace — Complete Guide

## 📘 Overview

A **Namespace** in Kubernetes is a way to divide cluster resources between multiple users or projects.
It provides **logical isolation** — allowing teams to manage resources independently within a shared cluster.

Namespaces act like **virtual clusters** within the same physical Kubernetes cluster.

---

## 🎯 Why Use Namespaces?

| Purpose                 | Description                                               |
| ----------------------- | --------------------------------------------------------- |
| **Isolation**           | Separate environments like dev, test, and prod            |
| **Resource Management** | Apply CPU/memory limits using ResourceQuota               |
| **Access Control**      | Assign permissions with Role and RoleBinding              |
| **Name Uniqueness**     | Same resource names can exist in different namespaces     |
| **Multi-tenancy**       | Safely share one cluster among multiple teams or projects |

---

## 🎗️ Default Namespaces

When you install Kubernetes, these namespaces are created automatically:

| Namespace         | Purpose                                                    |
| ----------------- | ---------------------------------------------------------- |
| `default`         | Used for resources without an explicit namespace           |
| `kube-system`     | System components like scheduler, controller-manager, etc. |
| `kube-public`     | Publicly readable resources (e.g., cluster info)           |
| `kube-node-lease` | Tracks node heartbeat information                          |

---

## 🧬 Namespace Scope

| Type                         | Examples                                         |
| ---------------------------- | ------------------------------------------------ |
| **Namespaced resources**     | Pods, Deployments, Services, ConfigMaps, Secrets |
| **Cluster-scoped resources** | Nodes, PersistentVolumes, ClusterRoles, CRDs     |

---

## ⚙️ Common Commands

### 🔹 List all namespaces

```bash
kubectl get namespaces
# or
kubectl get ns
```

### 🔹 Create a namespace

**Option 1: Using kubectl**

```bash
kubectl create namespace dev
```

**Option 2: Using YAML**

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: dev
```

Apply it:

```bash
kubectl apply -f namespace.yaml
```

### 🔹 Get resources inside a namespace

```bash
kubectl get pods -n dev
kubectl get all -n dev
```

### 🔹 Delete a namespace

```bash
kubectl delete namespace dev
```

> ⚠️ This deletes all resources inside the namespace.

---

## 🧠 Example: Multiple Environments

You can manage multiple environments in one cluster:

| Environment | Namespace | Example Resource |
| ----------- | --------- | ---------------- |
| Development | `dev`     | `dev-app`        |
| Testing     | `test`    | `test-app`       |
| Production  | `prod`    | `prod-app`       |

Example:

```bash
kubectl create deployment app --image=nginx -n dev
kubectl create deployment app --image=nginx -n prod
```

Both deployments are named `app`, but isolated in their respective namespaces.

---

## 🧽 Resource Quota Example

```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: dev-quota
  namespace: dev
spec:
  hard:
    pods: "10"
    requests.cpu: "2"
    requests.memory: 2Gi
    limits.cpu: "4"
    limits.memory: 4Gi
```

Apply it:

```bash
kubectl apply -f quota.yaml
```

This ensures the `dev` namespace cannot exceed defined resource limits.

---

## 🔐 RBAC Example (Namespace-level Access)

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: dev
  name: dev-role
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "list", "watch"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: dev-binding
  namespace: dev
subjects:
- kind: User
  name: dev-user
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: dev-role
  apiGroup: rbac.authorization.k8s.io
```

➡️ This gives `dev-user` permission to view pods only in the `dev` namespace.

---

## 🌍 View Resources Across All Namespaces

```bash
kubectl get pods --all-namespaces
# or
kubectl get all -A
```

---

## ⚠️ Limitations

* No nested namespaces.
* Some resources (like Nodes, PVs) are cluster-scoped.
* Not a replacement for full multi-cluster isolation.

---

## 🧾 Summary

| Concept                | Description                                                                            |
| ---------------------- | -------------------------------------------------------------------------------------- |
| **Purpose**            | Logical grouping and isolation of resources                                            |
| **Default Namespaces** | default, kube-system, kube-public, kube-node-lease                                     |
| **Scope**              | Namespaced or Cluster-scoped                                                           |
| **Key Features**       | Isolation, Access control, Resource quota, Multi-tenancy                               |
| **Commands**           | `kubectl get ns`, `kubectl create ns`, `kubectl delete ns`, `kubectl get pods -n <ns>` |

---

## 🚀 Quick Practical Flow

```bash
# Create namespace
kubectl create ns dev

# Deploy app in dev namespace
kubectl run nginx --image=nginx -n dev

# Get pods from dev namespace
kubectl get pods -n dev

# Switch context to dev namespace
kubectl config set-context --current --namespace=dev

# Delete namespace
kubectl delete ns dev
```

---

## 🖼️ Visual Overview

```
+-------------------------------------------------------+
|                   Kubernetes Cluster                  |
|-------------------------------------------------------|
| Namespace: dev     | Namespace: test   | Namespace: prod |
| ------------------ | ----------------- | ---------------- |
| Pods, Services     | Pods, Services    | Pods, Services   |
| ConfigMaps, Secrets| ConfigMaps, Secrets| ConfigMaps, Secrets|
+-------------------------------------------------------+
```

---

✅ **In short:**
Namespaces help organize, isolate, and manage workloads within a shared Kubernetes cluster —
essential for **multi-environment setups**, **RBAC**, and **resource quotas**.
