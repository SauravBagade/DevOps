# 🧭 Kubernetes Pod — Complete Guide

## 📘 Overview

A **Pod** is the **smallest deployable unit** in Kubernetes.
It represents a **single instance of a running process** in your cluster.

A pod can contain **one or more containers** that share the same network namespace, storage volumes, and lifecycle.
Usually, a single pod = one container, but sometimes multiple tightly coupled containers (like sidecars) run together.

---

## 🎯 Why Use Pods?

| Feature                  | Description                                                      |
| ------------------------ | ---------------------------------------------------------------- |
| **Encapsulation**        | Pods encapsulate one or more containers that share resources     |
| **Networking**           | Containers inside a pod share the same IP address and port space |
| **Storage**              | Pods can share storage volumes among containers                  |
| **Scaling**              | Deployments and ReplicaSets scale pods, not containers directly  |
| **Lifecycle Management** | Kubernetes schedules, restarts, and manages pods automatically   |

---

## 🌐 Pod Structure (YAML Example)

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  namespace: nginx
  labels:
    app: nginx
spec:
  containers:
    - name: nginx
      image: nginx:latest
      ports:
        - containerPort: 80
```

Apply it:

```bash
kubectl apply -f nginx-pod.yaml
```

---

## 🔹 Common Pod Commands

### ✅ Get all pods

```bash
kubectl get pods
kubectl get pods -n nginx
```

### ✅ Create a pod

```bash
kubectl run nginx-pod --image=nginx --port=80 -n nginx
```

### ✅ Delete a pod

```bash
kubectl delete pod nginx-pod -n nginx
```

### ✅ Get detailed info about a pod

```bash
kubectl describe pod nginx-pod -n nginx
```

This shows container states, events, IP, node name, and more.

---

## ⚙️ Interact with Pods

### 🔹 Go inside a running pod (open shell)

```bash
kubectl exec -it nginx-pod -n nginx -- bash
```

Once inside:

```bash
curl 127.0.0.1
```

This verifies that the Nginx container is running and serving traffic.

### 🔹 Run a single command inside a pod

```bash
kubectl exec nginx-pod -n nginx -- ls /usr/share/nginx/html
```

### 🔹 Copy files from/to a pod

```bash
# Copy file from pod to local
kubectl cp nginx/nginx-pod:/usr/share/nginx/html/index.html ./index.html

# Copy file from local to pod
kubectl cp ./test.html nginx/nginx-pod:/usr/share/nginx/html/test.html
```

---

## 🔹 Check Pod Logs

### View logs of a running pod

```bash
kubectl logs nginx-pod -n nginx
```

### View logs for a specific container (if multiple containers in a pod)

```bash
kubectl logs nginx-pod -c nginx -n nginx
```

### Stream logs (like tail -f)

```bash
kubectl logs -f nginx-pod -n nginx
```

### View logs of previous failed container

```bash
kubectl logs -p nginx-pod -n nginx
```

---

## 🛠️ Pod Lifecycle Phases

| Phase         | Description                                                             |
| ------------- | ----------------------------------------------------------------------- |
| **Pending**   | Pod accepted but not yet running (waiting for scheduling/pulling image) |
| **Running**   | All containers are running or starting up                               |
| **Succeeded** | All containers completed successfully                                   |
| **Failed**    | At least one container terminated with failure                          |
| **Unknown**   | State cannot be determined (network or node issues)                     |

---

## 🔹 Describe Pod Status

```bash
kubectl get pods -n nginx -o wide
```

This shows:

* Pod IP
* Node name
* Status (Running / Pending / CrashLoopBackOff / Completed)

To get detailed info:

```bash
kubectl describe pod nginx-pod -n nginx
```

Look for:

* **Events** section for scheduling or crash errors
* **State** for container health
* **Image pull messages**

---

## 🔹 Restarting and Debugging Pods

### Delete and recreate the pod

```bash
kubectl delete pod nginx-pod -n nginx
kubectl run nginx-pod --image=nginx -n nginx
```

### Port forward a pod to access locally

```bash
kubectl port-forward pod/nginx-pod 8080:80 -n nginx
```

Now visit [http://localhost:8080](http://localhost:8080) to see the Nginx welcome page.

---

## 🌐 Multi-Container Pod Example

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: sidecar-pod
  namespace: dev
spec:
  containers:
    - name: main-app
      image: nginx
      ports:
        - containerPort: 80
    - name: log-agent
      image: busybox
      command: ["sh", "-c", "tail -f /var/log/nginx/access.log"]
```

This example shows a **sidecar container** pattern — `log-agent` collects logs while `main-app` runs Nginx.

---

## 📈 Monitoring Pod Resource Usage

```bash
kubectl top pod nginx-pod -n nginx
```

Displays CPU and memory usage (requires `metrics-server`).

---

## 🧾 Summary

| Concept              | Description                                                                        |
| -------------------- | ---------------------------------------------------------------------------------- |
| **Definition**       | Smallest deployable unit containing one or more containers                         |
| **Common Commands**  | `kubectl get pods`, `kubectl describe pod`, `kubectl logs`, `kubectl exec`         |
| **Networking**       | All containers share same IP, hostname, and ports                                  |
| **Lifecycle Phases** | Pending, Running, Succeeded, Failed, Unknown                                       |
| **Debugging**        | Use `kubectl logs`, `kubectl describe`, `kubectl exec`, and `kubectl port-forward` |

---

## 🖼️ Visual Overview

```
+---------------------------------------------+
|                 Kubernetes Node             |
|---------------------------------------------|
| Pod: nginx-pod                             |
| +-----------------------------------------+ |
| | Container: nginx                        | |
| |  - Port: 80                             | |
| |  - Shared Volume (if any)               | |
| +-----------------------------------------+ |
|                                             |
| Pod: sidecar-pod                           |
| +-----------------------------------------+ |
| | Container: main-app (nginx)             | |
| | Container: log-agent (busybox)          | |
| +-----------------------------------------+ |
+---------------------------------------------+
```

---

✅ **In short:**
A **Pod** is the building block of Kubernetes workloads. It encapsulates one or more containers, their shared network, and storage, enabling efficient deployment, scaling
