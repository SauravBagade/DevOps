# 🩺 Kubernetes Probes — Complete Guide

**Probes** tell Kubernetes the health of a container.
Kubelet continuously checks containers and decides:

| Probe               | Purpose                          | Action                             |
| ------------------- | -------------------------------- | ---------------------------------- |
| **Liveness Probe**  | Is app alive?                    | Restart container if failed        |
| **Readiness Probe** | Is app ready to receive traffic? | Remove from Service endpoints      |
| **Startup Probe**   | Has app finished starting?       | Prevent premature liveness failure |

---

## 🧠 Why Probes Are Important (Production)

Without probes:

> App crashed → Pod still running → Users get 500 errors

With probes:

> App unhealthy → Removed from LB → Restart → Auto recovery

---

# 1️⃣ Liveness Probe

### 👉 Detects deadlock / crash / stuck process

If failed → **container restarts**

---

## Example — HTTP Check

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: liveness-http
spec:
  containers:
  - name: nginx
    image: nginx
    livenessProbe:
      httpGet:
        path: /
        port: 80
      initialDelaySeconds: 5
      periodSeconds: 10
      timeoutSeconds: 2
      failureThreshold: 3
```

### How it works

After 5 sec → Every 10 sec check `/`
Fail 3 times → Restart container

---

## Example — Command Check

```yaml
livenessProbe:
  exec:
    command:
    - cat
    - /tmp/healthy
```

File missing → restart

---

## Example — TCP Check

```yaml
livenessProbe:
  tcpSocket:
    port: 80
```

Port closed → restart

---

# 2️⃣ Readiness Probe

### 👉 Controls traffic routing (Service / Ingress)

If failed → **Pod not killed**
Only removed from Load Balancer

---

```yaml
readinessProbe:
  httpGet:
    path: /
    port: 80
  initialDelaySeconds: 3
  periodSeconds: 5
```

### Real Example

App starting DB connection…

| Time              | Status                 |
| ----------------- | ---------------------- |
| Container running | ❌ Not Ready            |
| DB Connected      | ✅ Ready                |
| DB Down           | ❌ Removed from traffic |

---

# 3️⃣ Startup Probe

### 👉 For slow starting apps (Java, SpringBoot, ML models)

Prevents liveness killing app during startup.

---

```yaml
startupProbe:
  httpGet:
    path: /
    port: 80
  failureThreshold: 30
  periodSeconds: 10
```

**Meaning:**
K8s waits = 30 × 10 = **300 sec startup time allowed**

After success → liveness starts

---

# ⚙️ Probe Parameters (Very Important)

| Field                 | Meaning                    |
| --------------------- | -------------------------- |
| `initialDelaySeconds` | Wait before first check    |
| `periodSeconds`       | Interval between checks    |
| `timeoutSeconds`      | Probe response timeout     |
| `failureThreshold`    | Fail count before action   |
| `successThreshold`    | Success count before ready |

---

# 🏗️ Full Production Example

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: probe-demo
spec:
  replicas: 2
  selector:
    matchLabels:
      app: probe
  template:
    metadata:
      labels:
        app: probe
    spec:
      containers:
      - name: web
        image: nginx
        ports:
        - containerPort: 80

        livenessProbe:
          httpGet:
            path: /
            port: 80
          initialDelaySeconds: 5
          periodSeconds: 5

        readinessProbe:
          httpGet:
            path: /
            port: 80
          initialDelaySeconds: 3
          periodSeconds: 3

        startupProbe:
          httpGet:
            path: /
            port: 80
          failureThreshold: 30
          periodSeconds: 5

```
# service.yml

```yml
apiVersion: v1
kind: Service
metadata:
  name: probe-svc
spec:
  selector:
    app: probe
  ports:
  - port: 80
    targetPort: 80
  type: NodePort
```

kubectl apply -f deployment.yml
kubectl apply -f service.yml


---

# 🧪 Testing Probes (Interview Favorite)

```bash
kubectl get pods -w
kubectl describe pod <pod-name>
```

👉 Shows probe failures

```bash
kubectl get events
```

```bash
kubectl logs <pod-name>
```

```bash
kubectl exec -it <pod-name> -- bash
kubectl port-forward probe-svc/nginx-pod 8080:80


```
---

# 🔥 Real Production Behaviour

| Situation       | Result                   |
| --------------- | ------------------------ |
| App crash       | Liveness restart         |
| DB down         | Readiness remove traffic |
| Slow start      | Startup protects         |
| High CPU freeze | Restart                  |
| Memory leak     | Restart automatically    |

---

# 🎯 Easy Memory Trick

> **Startup = Birth**
> **Readiness = Ready to serve**
> **Liveness = Alive or dead**

---
svc.yml crate ,and kubectl port-forward pod/nginx-pod 8080:80
