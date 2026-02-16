# 🔐 Kubernetes RBAC — Namespace Level (Role + RoleBinding + ServiceAccount)

---

## 📘 Overview

Kubernetes RBAC (Role‑Based Access Control) controls **who can access what resources** inside the cluster.

Instead of giving full admin access, RBAC follows **Least Privilege Principle** → user/app gets only required permissions.

Example:

* Developer → deploy app only in dev namespace
* Tester → read logs only
* Monitoring → read metrics only

---

## 🎯 Purpose

RBAC is used to:

* Protect production resources
* Prevent accidental deletion
* Separate team access (Dev / QA / Ops)
* Secure service accounts used by pods
* Control API access in Kubernetes

Without RBAC → anyone can delete cluster 😱
With RBAC → controlled & auditable access 🔒

---

## 🧱 Components Explained

| Component          | What it does                     |
| ------------------ | -------------------------------- |
| **ServiceAccount** | Identity used by Pod             |
| **Role**           | Defines permissions in namespace |
| **RoleBinding**    | Connects Role to identity        |

### Flow

```
Pod → ServiceAccount → Role → RoleBinding → Access Granted
```

---

# 🧪 LAB — Namespace Level Permission

Namespace: `apache`
Permission: Read pods only inside apache namespace

---

## 1️⃣ Create Namespace

```bash
kubectl create namespace apache
kubectl get ns
kubectl describe namespace apache
```

---

## 2️⃣ Create ServiceAccount (Identity)

### sa.yml

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: apache-user
  namespace: apache
```

Apply

```bash
kubectl apply -f sa.yml
```

Verify

```bash
kubectl get serviceaccount -n apache
kubectl get sa -n apache
kubectl describe sa apache-user -n apache
kubectl get sa apache-user -n apache -o yaml
```

---

## 3️⃣ Create Role (Permission)

### role.yml

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: pod-reader
  namespace: apache
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get","list","watch"]
```

Apply

```bash
kubectl apply -f role.yml
```

Verify

```bash
kubectl get role -n apache
kubectl describe role pod-reader -n apache
kubectl get role pod-reader -n apache -o yaml
```

---

## 4️⃣ Create RoleBinding (Attach Permission)

### rolebinding.yml

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: pod-reader-binding
  namespace: apache
subjects:
- kind: ServiceAccount
  name: apache-user
  namespace: apache
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```

Apply

```bash
kubectl apply -f rolebinding.yml
```

Verify

```bash
kubectl get rolebinding -n apache
kubectl describe rolebinding pod-reader-binding -n apache
kubectl get rolebinding pod-reader-binding -n apache -o yaml
```

---

## 5️⃣ Create Test Pod

### pod.yml

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: rbac-apache-test
  namespace: apache
spec:
  serviceAccountName: apache-user
  containers:
  - name: busybox
    image: busybox
    command: ["sleep","3600"]
```

Apply

```bash
kubectl apply -f pod.yml
kubectl get pods -n apache
kubectl describe pod rbac-apache-test -n apache
```

---

## 6️⃣ Test Access

Enter Pod

```bash
kubectl exec -it rbac-apache-test -n apache -- sh
```

Allowed

```sh
kubectl get pods -n apache
kubectl get pods
```

Denied

```sh
kubectl get pods -n kube-system
kubectl get nodes
kubectl delete pod rbac-apache-test -n apache
```

Exit

```sh
exit
```

---

## 7️⃣ Verify Using can‑i

```bash
kubectl auth can-i list pods --as system:serviceaccount:apache:apache-user -n apache
kubectl auth can-i delete pods --as system:serviceaccount:apache:apache-user -n apache
kubectl auth can-i get nodes --as system:serviceaccount:apache:apache-user
```

---

## 🔍 Debug Commands

```bash
kubectl get all -n apache
kubectl get serviceaccount -n apache
kubectl get role -n apache
kubectl get rolebinding -n apache
kubectl describe sa apache-user -n apache
kubectl describe role pod-reader -n apache
kubectl describe rolebinding pod-reader-binding -n apache
```

---

## 🧹 Cleanup

```bash
kubectl delete pod rbac-apache-test -n apache
kubectl delete rolebinding pod-reader-binding -n apache
kubectl delete role pod-reader -n apache
kubectl delete sa apache-user -n apache
kubectl delete namespace apache
```

---

## ✅ Final Result

Namespace level RBAC working successfully
User can only read pods in apache namespace
Secure and production safe configuration

---

# 🌍 Cluster Level RBAC (ClusterRole + ClusterRoleBinding)

## 📘 Overview

Cluster level RBAC gives permission across **ALL namespaces** in the cluster.

Used for:

* Monitoring tools (Prometheus)
* CI/CD (Jenkins, ArgoCD)
* Operators & controllers
* Read cluster resources

---

## 🧱 Components

| Component          | Purpose                    |
| ------------------ | -------------------------- |
| ServiceAccount     | Identity used by Pod       |
| ClusterRole        | Cluster-wide permissions   |
| ClusterRoleBinding | Attach permission globally |

Flow:

```
Pod → ServiceAccount → ClusterRole → ClusterRoleBinding → Cluster Access
```

---

## 1️⃣ Create Namespace

```bash
kubectl create namespace dev
kubectl get ns
```

---

## 2️⃣ Create ServiceAccount

```bash
kubectl create serviceaccount cluster-user -n dev
kubectl get sa -n dev
kubectl describe sa cluster-user -n dev
```

---

## 3️⃣ Create ClusterRole

### clusterrole.yml

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: pod-reader-cluster
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get","list","watch"]
```

Apply

```bash
kubectl apply -f clusterrole.yml
kubectl get clusterrole
kubectl describe clusterrole pod-reader-cluster
```

---

## 4️⃣ Create ClusterRoleBinding

### clusterrolebinding.yml

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: pod-reader-global
subjects:
- kind: ServiceAccount
  name: cluster-user
  namespace: dev
roleRef:
  kind: ClusterRole
  name: pod-reader-cluster
  apiGroup: rbac.authorization.k8s.io
```

Apply

```bash
kubectl apply -f clusterrolebinding.yml
kubectl get clusterrolebinding
kubectl describe clusterrolebinding pod-reader-global
```

---

## 5️⃣ Test Permission

```bash
kubectl auth can-i list pods --as system:serviceaccount:dev:cluster-user -A
kubectl auth can-i delete pods --as system:serviceaccount:dev:cluster-user -A
```

---

## 🔍 Debug Commands

```bash
kubectl get clusterrole
kubectl get clusterrolebinding
kubectl describe clusterrole pod-reader-cluster
kubectl describe clusterrolebinding pod-reader-global
```

---

## 🧹 Cleanup

```bash
kubectl delete clusterrolebinding pod-reader-global
kubectl delete clusterrole pod-reader-cluster
kubectl delete sa cluster-user -n dev
kubectl delete namespace dev
```

---

## 🎯 Key Difference

| Role          | ClusterRole        |
| ------------- | ------------------ |
| One namespace | All namespaces     |
| RoleBinding   | ClusterRoleBinding |
| Safer         | Powerful           |
