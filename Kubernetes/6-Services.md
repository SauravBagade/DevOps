# 🌐 Kubernetes Services — Complete Guide

A **Service** in Kubernetes provides stable networking and discovery for a dynamic set of Pods. Since Pods are ephemeral (their IP changes when recreated), Services act as a permanent entry point.

---

## 🎯 Why Services Exist

Pods:

* Get recreated anytime
* IP keeps changing
* Cannot be reliably accessed directly

Service provides:

* Stable DNS name
* Stable virtual IP (ClusterIP)
* Load balancing
* Internal & external exposure

---

## 🧠 How Traffic Flows

Client → Service → kube-proxy → Pod (selected via labels)

Service does NOT talk to containers directly — it routes to matching Pods using **label selectors**.

---

## 🧩 Basic Example — NGINX Service

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
  namespace: nginx
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
      nodePort: 30080
```

Apply:

```bash
kubectl apply -f service.yml
kubectl get svc -n nginx
```

Access:

```
http://<Node-IP>:30080
```

---

# 🔵 Service Types (Very Important)

## 1️⃣ ClusterIP (Default — Internal Only)

Used for communication between applications inside the cluster.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-clusterip
  namespace: nginx
spec:
  type: ClusterIP
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
```

Access from inside cluster:

```bash
curl http://nginx-clusterip.nginx.svc.cluster.local
```

---

## 2️⃣ NodePort (Lab / Local / Practice)

Opens a port on every worker node.

Port range: **30000–32767**

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-nodeport
  namespace: nginx
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30080
```

Access:

```
http://<Node-IP>:30080
```

---

## 3️⃣ LoadBalancer (Production — Cloud)

Creates a cloud load balancer (AWS ELB / Azure LB / GCP LB).

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-loadbalancer
  namespace: nginx
spec:
  type: LoadBalancer
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
```

Check external IP:

```bash
kubectl get svc -n nginx
```

Open:

```
http://EXTERNAL-IP
```

---

## 4️⃣ Headless Service (Stateful Applications)

No load balancing — returns individual Pod IPs.

Used for:

* Databases
* Kafka
* StatefulSet
* Clusters needing direct node communication

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-headless
  namespace: nginx
spec:
  clusterIP: None
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
```

Check DNS records:

```bash
nslookup nginx-headless.nginx.svc.cluster.local
```

---

# 🧪 Port Forwarding (Temporary Access)

```bash
kubectl port-forward svc/nginx-service -n nginx 8080:80 --address=0.0.0.0
```

Open:

```
http://localhost:8080
```

---

# 🔧 Useful Commands

## Namespace

```bash
kubectl create namespace nginx
kubectl get ns
```

## Service Management

```bash
kubectl apply -f service.yml
kubectl get svc -n nginx
kubectl describe svc nginx-service -n nginx
kubectl delete svc nginx-service -n nginx
```

## Debugging

```bash
kubectl get endpoints -n nginx
kubectl get pods -o wide -n nginx
kubectl logs <pod>
kubectl exec -it <pod> -- sh
```

---

# 🧠 Key Concepts (Interview Focus)

| Concept    | Meaning                   |
| ---------- | ------------------------- |
| port       | Service port              |
| targetPort | Container port            |
| nodePort   | External node port        |
| selector   | Connects service to pods  |
| ClusterIP  | Virtual IP inside cluster |
| Endpoints  | Actual Pod IPs            |

---

# ⚠️ Common Mistakes

1. Labels not matching selector
2. Pod not listening on targetPort
3. Security group blocking NodePort
4. Forgetting namespace
5. LoadBalancer pending (cloud controller missing)

---

# 🧠 Quick Memory Trick

| Type         | Usage      | Internet   |
| ------------ | ---------- | ---------- |
| ClusterIP    | Pod ↔ Pod  | ❌          |
| NodePort     | Testing    | ⚠️         |
| LoadBalancer | Production | ✅          |
| Headless     | Database   | Direct Pod |

---

✅ **In short:**

* Service = stable networking layer
* Selects Pods using labels
* Provides load balancing
* Exposes apps internally or externally
