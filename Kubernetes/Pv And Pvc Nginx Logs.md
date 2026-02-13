# Persistent Volume (PV) and Persistent Volume Claim (PVC) in Kubernetes

This guide explains **Persistent Volumes (PV)**, **Persistent Volume Claims (PVC)**, and how to **store Nginx logs** using PV and PVC in a Deployment.

---

## **1. What is a Persistent Volume (PV)?**

A **Persistent Volume (PV)** is a piece of storage in the cluster that has been provisioned by an administrator or dynamically provisioned using a **StorageClass**. PVs are independent of any Pod lifecycle.

### **Key Points:**

* PV is **cluster-level storage** resource.
* It provides storage to Pods using PVC.
* It supports various backend storage types (EBS, NFS, hostPath, etc.).

### **PV YAML Example:**

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: nginx-pv
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  storageClassName: standard
  hostPath:
    path: /mnt/data/nginx-logs
```

**Explanation:**

* `capacity`: Defines storage size (1Gi).
* `accessModes`: Controls how the volume can be mounted.

  * `ReadWriteOnce` → Mounted by a single node.
  * `ReadOnlyMany` → Read-only by many nodes.
  * `ReadWriteMany` → Read-write by many nodes.
* `persistentVolumeReclaimPolicy`: Defines what happens after PVC deletion (`Retain`, `Recycle`, or `Delete`).
* `hostPath`: Stores data on the host node (used for testing).

---

## **2. What is a Persistent Volume Claim (PVC)?**

A **Persistent Volume Claim (PVC)** is a request for storage by a user. It is similar to a Pod requesting compute resources.

### **PVC YAML Example:**

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: nginx-pvc
  namespace: default
spec:
  storageClassName: standard
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```

**Explanation:**

* The PVC requests 1Gi of storage from a PV with matching `storageClassName`.
* Once bound, the PVC will remain attached until it’s manually released or deleted.

---

## **3. Nginx Deployment with PV and PVC for Logs**

This Deployment mounts a PVC to store Nginx logs persistently.

### **Deployment YAML:**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  namespace: default
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      volumes:
      - name: log-storage
        persistentVolumeClaim:
          claimName: nginx-pvc # Reference the PVC
      containers:
      - name: nginx
        image: nginx:latest
        ports:
         - containerPort: 80
        volumeMounts:
        - name: log-storage
          mountPath: /var/log/nginx # Mount the PV/PVC to Nginx log directory
```

---

## **4. Apply All Manifests**

```bash
kubectl apply -f pv.yaml
kubectl apply -f pvc.yaml
kubectl apply -f nginx-deployment.yaml
```

---

## **5. Verify Setup**

```bash
# Check PV and PVC status
kubectl get pv
kubectl get pvc

# Check Deployment and Pod
kubectl get deployments
kubectl get pods
```

---

## **6. Access and Generate Logs**

Forward port and access Nginx page to generate logs.

```bash
kubectl port-forward service/nginx-deployment 8080:80 --address 0.0.0.0
```

Open in browser:

```
http://<EC2_PUBLIC_IP>:8080
```

---

## **7. Check Nginx Logs from PV**

### **Go inside the Pod:**

```bash
kubectl exec -it <nginx-pod-name> -- bash
cd /var/log/nginx
cat access.log
```

### **Or directly from Node:**

```bash
sudo cat /mnt/data/nginx-logs/access.log
```

---

## **8. Useful Commands**

```bash
# Describe PV and PVC
kubectl describe pv nginx-pv
kubectl describe pvc nginx-pvc

# Delete Resources
kubectl delete deployment nginx-deployment
kubectl delete pvc nginx-pvc
kubectl delete pv nginx-pv
```

---

## **9. Summary**

| Component                       | Purpose                                              |
| ------------------------------- | ---------------------------------------------------- |
| **PersistentVolume (PV)**       | Actual physical/disk storage provisioned in cluster  |
| **PersistentVolumeClaim (PVC)** | Request for storage by Pod/Deployment                |
| **Deployment**                  | Mounts PVC to container and writes logs persistently |

---

### ✅ **Result:**

* Nginx container logs (`access.log`, `error.log`) are stored persistently at `/mnt/data/nginx-logs` ev

# Kubernetes PersistentVolume (PV) and PersistentVolumeClaim (PVC)

This document explains PersistentVolume (PV) and PersistentVolumeClaim (PVC) concepts in Kubernetes with an interview-focused and real-world perspective. It is formatted for clean rendering in editors and GitHub.

---

## Important PV Fields (Interview)

| Field                         | Meaning                              |
| ----------------------------- | ------------------------------------ |
| capacity.storage              | Size of the storage                  |
| accessModes                   | How the volume can be mounted        |
| storageClassName              | StorageClass associated with the PV  |
| persistentVolumeReclaimPolicy | Action taken when PVC is deleted     |
| volumeMode                    | Filesystem or Block storage          |
| nodeAffinity                  | Restricts which nodes can use the PV |

---

## PV Access Modes (Very Important)

| Access Mode             | Meaning                          | Example          |
| ----------------------- | -------------------------------- | ---------------- |
| ReadWriteOnce (RWO)     | Mounted read-write by one node   | AWS EBS          |
| ReadOnlyMany (ROX)      | Mounted read-only by many nodes  | Shared content   |
| ReadWriteMany (RWX)     | Mounted read-write by many nodes | NFS, EFS         |
| ReadWriteOncePod (RWOP) | Mounted by only one Pod          | Newer Kubernetes |

---

## PV Reclaim Policies

What happens when a PersistentVolumeClaim is deleted?

| Policy  | Behavior                                  |
| ------- | ----------------------------------------- |
| Retain  | Data remains; manual cleanup required     |
| Delete  | Storage deleted automatically             |
| Recycle | Deprecated; cleans data and reuses volume |

---

## What is PersistentVolumeClaim (PVC)

### Definition

A PersistentVolumeClaim (PVC) is a request for storage made by a user or application.

Example requirement:

"I need 10GB of storage with ReadWriteMany access."

---

## What PVC Does

* Requests storage
* Finds a matching PersistentVolume
* Binds to the PersistentVolume
* Acts as a storage abstraction for Pods

Note:
Pods never reference PersistentVolumes directly. Pods always use PVCs.

---

## Static vs Dynamic Provisioning

### Static Provisioning

* Cluster administrator manually creates PersistentVolumes
* User creates PersistentVolumeClaims
* PVC binds to an existing PV

Commonly used in:

* Minikube
* On-prem Kubernetes clusters

---

### Dynamic Provisioning (Production)

* User creates a PVC
* Storage is created automatically
* No manual PV creation is required

Dynamic provisioning uses StorageClass.

---

## PV Lifecycle States

| State     | Meaning                           |
| --------- | --------------------------------- |
| Available | PV is ready to be claimed         |
| Bound     | PV is bound to a PVC              |
| Released  | PVC deleted; PV not yet reclaimed |
| Failed    | Error occurred                    |

---

## Common Mistakes

* PVC stuck in Pending state due to no matching PV or incorrect StorageClass
* Using ReadWriteMany access mode with AWS EBS
* Data loss due to Delete reclaim policy
* Using hostPath volumes in production environments

---

## Kubernetes Storage vs Docker Volumes

| Docker               | Kubernetes            |
| -------------------- | --------------------- |
| Volume               | PersistentVolume      |
| Bind mount           | hostPath              |
| Manual configuration | Declarative YAML      |
| Node-level storage   | Cluster-level storage |

---

## Interview One-Line Summary

PersistentVolume (PV) represents actual storage.
PersistentVolumeClaim (PVC) is a request for storage.
Pods mount PVCs, not PVs.

---

## Notes

* PVs are cluster-scoped resources
* PVCs are namespace-scoped resources
* Storage abstraction improves portability and scalability

