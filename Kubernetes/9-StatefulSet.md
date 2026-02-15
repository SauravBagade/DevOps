# 🧠 Kubernetes StatefulSet Notes

## 📘 Overview

**StatefulSets** are used to manage stateful applications in Kubernetes, such as **databases (MySQL, MongoDB, PostgreSQL)**. Unlike Deployments, each pod in a StatefulSet has a **unique, stable identity** and maintains its **state even after restarts**.

---

## ⚙️ Key Concepts

* **Ordered & Numbered Pods** – Pods are created sequentially (`pod-0`, `pod-1`, `pod-2`...).
* **Persistent State** – When a pod dies, its data is preserved and attached to the new pod with the same identity.
* **Volume Usage** – StatefulSets require persistent volumes to store data.
* **Stable Network ID** – Each pod gets a predictable DNS name.
* **Commonly used for:**

  * Databases: MySQL, MongoDB, PostgreSQL
  * Message Queues: Kafka, RabbitMQ

---

## Namesapace mysql

```yaml
kubectl create ns mysql
```
---
## 🧩 Example: MySQL StatefulSet

```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: mysql-statefulset
  namespace: mysql
spec:
  serviceName: mysql-service
  replicas: 3
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
    spec:
      containers:
        - name: mysql
          image: mysql:8.0
          ports:
            - containerPort: 3306
          env:
            - name: MYSQL_ROOT_PASSWORD
              value: root        #password
            - name: MYSQL_DATABASE
              value: devops    #database
          volumeMounts:
            - name: mysql-data
              mountPath: /var/lib/mysql  
  volumeClaimTemplates:
    - metadata:
        name: mysql-data
      spec:
        accessModes: ["ReadWriteOnce"]
        resources:
          requests:
            storage: 1Gi
```

---

## 🧱 Headless Service

A **Headless Service** is used with StatefulSets to provide stable network identities for pods.

* **`clusterIP: None`** → No cluster-wide IP; instead, each pod gets its own DNS record.
* Used for **internal communication** between pods.

### Example:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: mysql-service
  namespace: mysql
spec:
  clusterIP: None
  selector:
    app: mysql
  ports:
    - name: mysql
      protocol: TCP
      port: 3306
      targetPort: 3306
```

---

## 🚀 Deployment Steps

1. Apply the StatefulSet and Service files:

   ```bash
   kubectl apply -f statefulset.yml
   kubectl apply -f service.yml
   ```
2. Verify Pods and Services:

   ```bash
   kubectl get pods -n mysql
   kubectl get svc -n mysql
   ```
3. Access the MySQL pod:

   ```bash
   kubectl exec -it pod/mysql-statefulset-0 -n mysql -- bash
   mysql -u root -p
   # password: root
   ```
4. Verify database:

   ```sql
   SHOW DATABASES;
   ```
5. Delete any pod (e.g., `mysql-statefulset-0`) and see it recreated automatically with the same identity.

---

## 🔍 Health Checks (Probes) in StatefulSets

Stateful applications require **careful health management** because restarting a database pod unnecessarily can cause data inconsistency.

### 1️⃣ Liveness Probe

* Checks if the container is **stuck or dead**
* If it fails → **Pod is restarted**
* Should be used **very carefully** for databases

```yaml
livenessProbe:
  tcpSocket:
    port: 3306
  initialDelaySeconds: 60
  periodSeconds: 10
```

---

### 2️⃣ Readiness Probe

* Checks if the pod is **ready to receive traffic**
* If it fails → Pod is **removed from Service endpoints**
* **Most important probe for StatefulSets**

```yaml
readinessProbe:
  exec:
    command:
      - sh
      - -c
      - mysqladmin ping -uroot -proot
  initialDelaySeconds: 30
  periodSeconds: 10
```

---

### 3️⃣ Startup Probe (Highly Recommended)

* Used for **slow-starting applications** (databases)
* Prevents liveness probe from killing the pod during startup

```yaml
startupProbe:
  exec:
    command:
      - sh
      - -c
      - mysqladmin ping -uroot -proot
  failureThreshold: 30
  periodSeconds: 10
```

---

## 🔁 StatefulSet Update Strategies

StatefulSets **do NOT update all pods at once** like Deployments.

### RollingUpdate (Default)

* Pods are updated **one by one**
* Update order (highest ordinal first):

  ```
  pod-2 → pod-1 → pod-0
  ```
* Next pod updates only after the previous one becomes **Ready**

```yaml
updateStrategy:
  type: RollingUpdate
```

---

### OnDelete

* Pods are updated **only when manually deleted**
* Useful for **production databases**

```yaml
updateStrategy:
  type: OnDelete
```

---

## 📈 Scaling Behavior in StatefulSets

### Scaling Up

* Pods are created **sequentially**
* Example:

  ```
  pod-0 → pod-1 → pod-2
  ```

### Scaling Down

* Pods are deleted in **reverse order**
* Example:

  ```
  pod-2 → pod-1 → pod-0
  ```

> ⚠️ PVCs are **NOT deleted automatically** when scaling down.

---

## 📦 Storage Behavior (Very Important)

* Each pod gets **its own PersistentVolumeClaim (PVC)**
* PVC naming format:

  ```
  <volume-name>-<statefulset-name>-<ordinal>
  ```

  Example:

  ```
  mysql-data-mysql-statefulset-0
  ```

### PVC Lifecycle Behavior

| Action              | Data Retained       |
| ------------------- | ------------------- |
| Pod deleted         | ✅ Yes               |
| Pod recreated       | ✅ Same PVC attached |
| StatefulSet deleted | ❌ PVCs remain       |
| Namespace deleted   | ❌ PVCs remain       |

---

## 🧭 Pod Management Policy

Controls **how pods are created or deleted**.

### OrderedReady (Default)

* Pods are created **one by one**
* Next pod waits until the previous pod becomes **Ready**

```yaml
podManagementPolicy: OrderedReady
```

---

### Parallel

* Pods are created or deleted **simultaneously**
* Useful when strict ordering is not required

```yaml
podManagementPolicy: Parallel
```

---

## 🌐 DNS Format for StatefulSet Pods

Each pod gets a **stable DNS name**:

```
<pod-name>.<service-name>.<namespace>.svc.cluster.local
```

Example:

```
mysql-statefulset-0.mysql-service.mysql.svc.cluster.local
```

Used for:

* Database replication
* Leader–Follower architecture
* Cluster discovery

---

## 🧠 StatefulSet vs Deployment (Interview Comparison)

| Feature      | StatefulSet | Deployment     |
| ------------ | ----------- | -------------- |
| Pod Identity | Stable      | Random         |
| Pod Names    | Fixed       | Random         |
| Storage      | Persistent  | Ephemeral      |
| Scaling      | Ordered     | Parallel       |
| Use Case     | Databases   | Stateless apps |

---

## ✅ Best Practices for StatefulSets

* Always configure **Readiness Probes**
* Prefer **Startup Probes** for databases
* Avoid aggressive **Liveness Probes**
* Use **OnDelete** strategy for production DBs
* Always use **Headless Services**
* Backup PVC data regularly
* Test scaling and failover scenarios

---

## ❓ Common Interview Questions

* Why StatefulSet instead of Deployment?
* Why is a Headless Service mandatory?
* What happens to PVC when a pod is deleted?
* Difference between OrderedReady and Parallel?
* Can StatefulSet work without PVC?
* How rolling updates work in StatefulSets?
