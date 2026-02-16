# 📊 Kubernetes Metrics Server — Complete Guide

---

## 📘 Overview

**Metrics Server** is a cluster-wide aggregator of resource usage data in Kubernetes.

It collects CPU & Memory usage from:

* Nodes
* Pods

And provides data to:

* `kubectl top`
* Horizontal Pod Autoscaler (HPA)
* Vertical Pod Autoscaler (VPA)
* Kubernetes Dashboard

> ⚠️ Without Metrics Server → HPA & `kubectl top` WILL NOT WORK

---

## 🧠 How It Works

Flow:

Kubelet → Metrics Server → Kubernetes API → HPA / kubectl top

1. Kubelet exposes `/metrics/resource`
2. Metrics Server scrapes data
3. Stores in memory (not persistent DB)
4. Exposes via `metrics.k8s.io` API

---

## 🚀 Install Metrics Server (kubeadm / bare metal / local cluster)

### Step 1 — Apply Official Manifest

```bash
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```

---

### Step 2 — Fix TLS Issue (VERY IMPORTANT FOR LAB / LOCAL CLUSTER)

Edit deployment:

```bash
kubectl -n kube-system edit deployment metrics-server
```

Add this inside container args:

```yaml
- --kubelet-insecure-tls
- --kubelet-preferred-address-types=InternalIP,ExternalIP,Hostname
```

Save & exit

---

### Restart Metrics Server (after edit)

```bash
kubectl rollout restart deployment metrics-server -n kube-system
kubectl wait --for=condition=available deployment/metrics-server -n kube-system --timeout=120s
```

### Step 3 — Verify Pods

```bash
kubectl get pods -n kube-system | grep metrics
```

Expected:

```
metrics-server-xxxxx Running
```

---

### Step 4 — Test Metrics API

```bash
kubectl get apiservice v1beta1.metrics.k8s.io
```

STATUS should be:

```
True
```

---

## 📈 Using Metrics Server

---

### Node Usage

```bash
kubectl top nodes
```

Output:

```
NAME       CPU(cores)   CPU%   MEMORY(bytes)   MEMORY%
master     250m         12%    1200Mi          45%
worker1    120m         6%     700Mi           32%
```

---

### Pod Usage

```bash
kubectl top pods -A
```

Or specific namespace:

```bash
kubectl top pods -n default
```

---

## 📦 Which Kubernetes installs Metrics Server by default?

| Kubernetes Type    | Metrics Server Included? | Notes                            |
| ------------------ | ------------------------ | -------------------------------- |
| kubeadm            | ❌ No                     | Must install manually            |
| Bare Metal         | ❌ No                     | Always manual install            |
| Minikube           | ✅ Yes                    | Enabled via addon                |
| kind               | ❌ No                     | Install manually                 |
| Docker Desktop K8s | ✅ Yes                    | Pre-installed                    |
| MicroK8s           | ✅ Yes                    | `microk8s enable metrics-server` |
| AWS EKS            | ❌ No                     | Install using manifest           |
| Azure AKS          | ✅ Yes                    | Available by default             |
| Google GKE         | ✅ Yes                    | Managed by Google                |

---

🔥 Horizontal Pod Autoscaler (HPA)

Metrics Server is REQUIRED for HPA.

---

### Create HPA

```bash
kubectl autoscale deployment nginx-deployment \
  --cpu-percent=50 \
  --min=1 \
  --max=10
```

Check:

```bash
kubectl get hpa
```

Detailed view:

```bash
kubectl describe hpa nginx-deployment
```

---

## 🛠 Important Commands

### View Metrics API

```bash
kubectl get --raw "/apis/metrics.k8s.io/v1beta1/nodes" | jq
```

```bash
kubectl get --raw "/apis/metrics.k8s.io/v1beta1/pods" | jq
```

---

### Restart Metrics Server

```bash
kubectl rollout restart deployment metrics-server -n kube-system
```

---

### Logs

```bash
kubectl logs -n kube-system deployment/metrics-server
```

---

### Delete Metrics Server

```bash
kubectl delete -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```

---

## ❌ Common Errors & Fixes

---

### Error: Metrics API not available

```
error: Metrics API not available
```

Fix:

Add flag:

```
--kubelet-insecure-tls
```

---

### Error: x509 certificate signed by unknown authority

Cause: self-signed kubelet certificate

Fix: same as above

---

### Error: no metrics returned

Wait 30–60 seconds after install

Metrics Server needs time to scrape nodes.

---

### Error: HPA shows unknown

Check:

```bash
kubectl get apiservice v1beta1.metrics.k8s.io
```

Must be **True**

---

## 🧩 Where Metrics Server is Used in Production

| Component          | Usage                   |
| ------------------ | ----------------------- |
| HPA                | Auto scaling pods       |
| Cluster monitoring | Resource visibility     |
| Dashboard          | Live usage graphs       |
| Cost optimization  | Detect overprovisioning |

---

## 🆚 Metrics Server vs Prometheus

| Feature          | Metrics Server | Prometheus     |
| ---------------- | -------------- | -------------- |
| Purpose          | Autoscaling    | Monitoring     |
| Storage          | Memory only    | Time-series DB |
| History          | ❌ No           | ✅ Yes          |
| Alerting         | ❌              | ✅              |
| Lightweight      | ✅              | ❌              |
| Required for HPA | ✅              | ❌              |

> Metrics Server ≠ Monitoring tool
> It is ONLY a resource usage provider

---

## 🏁 Final Result

After installation you can:

✔ View node usage
✔ View pod usage
✔ Enable HPA autoscaling
✔ Detect resource bottlenecks

---

## 📚 Key Takeaway

**Metrics Server is the brain behind Kubernetes autoscaling.**

No Metrics Server → No HPA → No auto scaling
