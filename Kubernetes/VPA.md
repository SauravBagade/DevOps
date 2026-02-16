# 🚀 Kubernetes Vertical Pod Autoscaler (VPA) — Complete Guide

---

# 1️⃣ Overview

**Vertical Pod Autoscaler (VPA)** automatically adjusts CPU and Memory requests & limits of a Pod based on its real usage.

Instead of increasing the number of Pods (HPA), VPA increases or decreases resources inside the same Pod.

> Pod hungry → increase CPU/RAM
> Pod idle → decrease CPU/RAM

Kubernetes automatically gives the right‑sized resources to applications.

---

# 2️⃣ Purpose of VPA

## Right‑Sizing Resources

Developers usually guess values:

```yaml
resources:
  requests:
    cpu: "100m"
    memory: "128Mi"
```

| Situation | Problem               |
| --------- | --------------------- |
| Too Low   | Pod crash / OOMKilled |
| Too High  | Cloud cost waste      |

VPA fixes this automatically.

---

## Prevent OOMKilled

If memory insufficient → container restarts
VPA learns usage pattern and increases memory before crash.

---

## Cost Optimization

Unused CPU/RAM wastes node capacity.

VPA reduces unused resources → saves infrastructure cost.

---

## No Manual Monitoring

No need for:

* kubectl top pod
* manual metrics analysis
* trial & error tuning

---

# 3️⃣ How VPA Works

1. Metrics Server collects usage
2. VPA analyzes historical data
3. Calculates recommended CPU & Memory
4. Restarts Pod with new values

---

# 4️⃣ Components

| Component            | Function                           |
| -------------------- | ---------------------------------- |
| Recommender          | Calculates best resources          |
| Updater              | Evicts pod to resize               |
| Admission Controller | Applies values during pod creation |

---

# 5️⃣ VPA vs HPA

| Feature     | VPA           | HPA            |
| ----------- | ------------- | -------------- |
| Scaling     | Pod Size      | Pod Count      |
| Changes     | CPU/RAM       | Replicas       |
| Pod Restart | Yes           | No             |
| Best For    | Stateful Apps | Stateless Apps |

---

# 6️⃣ When to Use

✔ Databases (MySQL, MongoDB)
✔ Java / Spring Boot apps
✔ Long running services
✔ Memory heavy workloads

## Avoid Using

✖ With HPA on CPU metric
✖ Ultra zero‑downtime apps
✖ Highly burst traffic apps

---

# 7️⃣ Prerequisites

VPA requires **Metrics Server**

Check:

```bash
kubectl top nodes
kubectl top pods
```

If not installed:

```bash
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```

---

# 8️⃣ Install VPA

```bash
git clone https://github.com/kubernetes/autoscaler.git
cd autoscaler/vertical-pod-autoscaler/
./hack/vpa-up.sh
```

Verify:

```bash
kubectl get pods -n kube-system
```

Expected:

```
vpa-admission-controller
vpa-recommender
vpa-updater
```

---

# 9️⃣ Demo Application Deployment

## app-deploy.yml

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-vpa
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx-vpa
  template:
    metadata:
      labels:
        app: nginx-vpa
    spec:
      containers:
      - name: nginx
        image: nginx
        resources:
          requests:
            cpu: "50m"
            memory: "50Mi"
          limits:
            cpu: "100m"
            memory: "100Mi"
```

Apply:

```bash
kubectl apply -f app-deploy.yml
```

---

# 🌐 Expose Service (service.yml)

Create ClusterIP service so load‑generator can access the app

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-vpa
spec:
  selector:
    app: nginx-vpa
  ports:
  - port: 80
    targetPort: 80
  type: ClusterIP
```

Apply:

```bash
kubectl apply -f service.yml
kubectl get svc
```

Now inside cluster you can access using:

```
http://nginx-vpa
```

---

# 🔟 Create VPA Object

## vpa.yml

```yaml
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
  name: nginx-vpa
spec:
  targetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: nginx-vpa
  updatePolicy:
    updateMode: Auto
  resourcePolicy:
    containerPolicies:
    - containerName: nginx
      minAllowed:
        cpu: 20m
        memory: 20Mi
      maxAllowed:
        cpu: 500m
        memory: 500Mi
```

Apply:

```bash
kubectl apply -f vpa.yml
```

---

# 1️⃣1️⃣ Check Recommendation

Wait ~2 minutes

```bash
kubectl describe vpa nginx-vpa
```

Example:

```
Target: cpu: 62m memory: 78Mi
```

---

# 1️⃣2️⃣ Generate Load

```bash
kubectl run -i --tty load-generator --rm --image=busybox -- /bin/sh
```

Inside container:

```sh
while true; do wget -q -O- http://nginx-vpa; done
```

Watch scaling:

```bash
kubectl get pods -w
```

VPA recreates pod with new resources.

Verify:

```bash
kubectl describe pod <pod-name>
```

---

# 1️⃣3️⃣ Update Modes

| Mode     | Behavior                      |
| -------- | ----------------------------- |
| Off      | Recommendation only           |
| Initial  | Apply only at first creation  |
| Auto     | Restart & apply automatically |
| Recreate | Always recreate pod           |

---

# 1️⃣4️⃣ Production Best Practice

Use together safely:

* HPA → scale traffic
* VPA → adjust resource size

Do NOT use same metric (CPU) together.

---

# 1️⃣5️⃣ Cleanup

```bash
kubectl delete -f vpa.yml
kubectl delete -f app-deploy.yml
./hack/vpa-down.sh
```

---

# 🧠 Final Flow Understanding

```
Metrics Server → VPA Analyze → Recommend → Restart Pod → Apply Resources
```

---

## One Line Definition

**VPA ensures every pod gets perfect CPU & RAM automatically based on usage.**
