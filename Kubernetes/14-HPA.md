# 🚀 Kubernetes HPA (Horizontal Pod Autoscaler) — Complete Guide

---

## 📘 Overview

**Horizontal Pod Autoscaler (HPA)** automatically increases or decreases the number of Pods in a Deployment / ReplicaSet / StatefulSet based on load.

Instead of manually scaling:

```bash
kubectl scale deployment nginx --replicas=10
```

Kubernetes automatically decides:

Traffic ↑ → Pods ↑
Traffic ↓ → Pods ↓

HPA continuously checks metrics from Metrics Server / Prometheus / Custom Metrics API and adjusts replicas.

---

## 🎯 Purpose of HPA

Applications never have constant traffic.

| Time    | Users  |
| ------- | ------ |
| Night   | 50     |
| Morning | 500    |
| Sale    | 10,000 |

Fixed replicas cause:

• Too many pods → Cost waste
• Too few pods → App crash

HPA solves this automatically.

| Situation     | Action      |
| ------------- | ----------- |
| CPU high      | Add Pods    |
| CPU low       | Remove Pods |
| Traffic spike | Scale Out   |
| Traffic drop  | Scale In    |

---

## 🧠 How HPA Works

```
User Traffic → CPU Increase
      ↓
Metrics Server collects metrics
      ↓
HPA checks every 15 sec
      ↓
Scale up or down
```

Works only on controllers (not pods):

* Deployment
* ReplicaSet
* StatefulSet

---

## ⚙️ Requirements follow doc 13-Metrix-server doc.md

### Install Metrics Server

```bash
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
kubectl top nodes
kubectl top pods
```

### Resource Requests Required of deployment.yml file

```yaml
resources:
  requests:
    cpu: 100m
  limits:
    cpu: 200m
```

---

## 📊 Scaling Formula

```
desiredReplicas = currentReplicas × ( currentMetric / targetMetric )
```

---

## 🧩 Architecture

```
HPA Controller → Metrics Server → Kubelet → Pods
```

---

# 🛠️ Practical Setup

## 1️⃣ Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: cpu-demo
spec:
  replicas: 1
  selector:
    matchLabels:
      app: cpu-demo
  template:
    metadata:
      labels:
        app: cpu-demo
    spec:
      containers:
      - name: cpu-demo
        image: nginx
        resources:
          requests:
            cpu: 100m
          limits:
            cpu: 200m
        ports:
        - containerPort: 80
```

```bash
kubectl apply -f deploy.yml
```

---

## 2️⃣ Service

```yaml
apiVersion: v1
kind: Service
metadata:
  name: cpu-demo-svc
spec:
  selector:
    app: cpu-demo
  ports:
  - port: 80
    targetPort: 80
  type: NodePort
```

```bash
kubectl apply -f service.yml
```

---

## 3️⃣ HPA YAML

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: cpu-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: cpu-demo
  minReplicas: 1
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 50
```

```bash
kubectl apply -f hpa.yml
kubectl get hpa
```

---

## 🧪 Generate Load

```bash
kubectl run -it load-generator --rm --image=busybox -- /bin/sh
while true; do wget -q -O- http://cpu-demo-svc; done
```

Watch scaling:

```bash
kubectl get hpa -w
kubectl get pods -w
```

---

# 📟 HPA Commands

## Basic

```bash
kubectl get hpa
kubectl describe hpa <name>
kubectl delete hpa <name>
kubectl edit hpa <name>
```

## Create Without YAML

```bash
kubectl autoscale deployment cpu-demo --cpu-percent=50 --min=1 --max=10
```

## Monitoring

```bash
kubectl top pods
kubectl top nodes
kubectl get hpa -w
```

## Debug

```bash
kubectl get events
kubectl describe pod <pod>
kubectl logs -n kube-system <metrics-server-pod>
kubectl get apiservice v1beta1.metrics.k8s.io -o yaml
kubectl get --raw "/apis/metrics.k8s.io/v1beta1/pods"
```

---

# 🧯 Troubleshooting Requirements follow doc 13-Metrix-server doc.md

## <unknown> CPU

Metrics server not working

Fix:

```bash
kubectl edit deployment metrics-server -n kube-system
```

Add:

```
--kubelet-insecure-tls
--kubelet-preferred-address-types=InternalIP
```

Restart:

```bash
kubectl rollout restart deployment metrics-server -n kube-system
```

---

## Not Scaling

Missing CPU request in deployment.

---

## Always 1 Pod

No load on application.

---

## kubectl top not working

Metrics API unavailable → reinstall metrics server.

---

## Slow Scaling

Normal behavior (stabilization window).

---

## App Still Slow

HPA scales pods, not database/cache/network.

---
