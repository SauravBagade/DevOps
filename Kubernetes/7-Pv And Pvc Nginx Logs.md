# Kubernetes PersistentVolume (PV) & PersistentVolumeClaim (PVC) — Complete Guide

* THIS CODE WAS WORK ON SINGLE WORKER NODE GOOD WORK ON AWS EBS 
This document explains Kubernetes storage concepts and demonstrates how to store **Nginx logs persistently** using PV and PVC. Designed for learning + interviews + real‑world usage.

---

# 1. What is a PersistentVolume (PV)?

A **PersistentVolume (PV)** is cluster storage provisioned by an administrator or dynamically via a StorageClass. It exists independently of Pods.

## Key Points

* Cluster‑level resource
* Represents real disk / network storage
* Used by Pods through PVC only
* Survives Pod deletion

---

## PV Example (hostPath — lab/testing only)

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

---

## Important PV Fields (Interview)

| Field                         | Meaning                     |
| ----------------------------- | --------------------------- |
| capacity.storage              | Disk size                   |
| accessModes                   | Mount permissions           |
| storageClassName              | Storage class binding       |
| persistentVolumeReclaimPolicy | Behavior after PVC deletion |
| volumeMode                    | Filesystem / Block          |
| nodeAffinity                  | Restrict node usage         |

---

## Access Modes (VERY IMPORTANT)

| Mode                    | Meaning               | Example        |
| ----------------------- | --------------------- | -------------- |
| ReadWriteOnce (RWO)     | One node read/write   | AWS EBS        |
| ReadOnlyMany (ROX)      | Many nodes read only  | Shared content |
| ReadWriteMany (RWX)     | Many nodes read/write | NFS / EFS      |
| ReadWriteOncePod (RWOP) | Single pod only       | New Kubernetes |

---

## Reclaim Policies

| Policy  | Result                        |
| ------- | ----------------------------- |
| Retain  | Data kept (manual cleanup)    |
| Delete  | Storage removed automatically |
| Recycle | Deprecated                    |

---

# 2. What is a PersistentVolumeClaim (PVC)?

A **PVC** is a storage request made by a user/application.

Pods never use PV directly → they always use PVC.

---

## PVC Example

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

---

## PVC Responsibilities

* Requests storage
* Finds matching PV
* Binds to PV
* Provides abstraction to Pods

---

# 3. Static vs Dynamic Provisioning

## Static (Manual)

* Admin creates PV
* User creates PVC
* PVC binds to existing PV

Used in: Minikube, local clusters

## Dynamic (Production)

* User creates PVC
* Storage auto‑created via StorageClass

Used in: AWS, GCP, Azure

---

# 4. PV Lifecycle States

| State     | Meaning         |
| --------- | --------------- |
| Available | Ready to claim  |
| Bound     | Attached to PVC |
| Released  | PVC deleted     |
| Failed    | Error           |

---

# 5. Nginx Deployment with Persistent Logs

## Deployment YAML

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
          claimName: nginx-pvc
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
        volumeMounts:
        - name: log-storage
          mountPath: /var/log/nginx
```

---

# 6. Service YAML

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
  namespace: default
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80 #node port
      targetPort: 80 #pod  port
  type: ClusterIP
```

---

# 7. Apply Resources

```bash
kubectl apply -f pv.yaml
kubectl apply -f pvc.yaml
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

---

# 8. Verify

```bash
kubectl get pv
kubectl get pvc
kubectl get pods
kubectl get svc
```

---

# 9. Generate Logs

```bash
kubectl port-forward svc/nginx-service 8080:80
```

Open browser:

[http://localhost:8080](http://localhost:8080)

---

# 10. Check Logs

## Inside Pod

```bash
kubectl exec -it <pod-name> -- bash
cd /var/log/nginx
cat access.log
```

## From Node (hostPath only)

```bash
sudo cat /mnt/data/nginx-logs/access.log
```

---

# 11. Common Mistakes

* PVC stuck Pending → no matching PV
* Using RWX with EBS
* Using hostPath in production
* Data loss with Delete policy

---

# 12. Docker vs Kubernetes Storage

| Docker       | Kubernetes       |
| ------------ | ---------------- |
| Volume       | PersistentVolume |
| Bind mount   | hostPath         |
| Manual       | Declarative      |
| Node storage | Cluster storage  |

---

# Interview One‑Line Answer

PersistentVolume = Actual storage
PersistentVolumeClaim = Request for storage
Pod mounts PVC, not PV
