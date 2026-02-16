# Kubernetes Ingress — NGINX & Apache Routing

---
*Install the Kubernetes Ingress Controller based on the cluster environment (Kind, Minikube, kubeadm, or EKS).

## Overview

This lab demonstrates Layer‑7 routing in Kubernetes using the NGINX Ingress Controller. Two applications (NGINX and Apache) are exposed through a single entry point.

```
/nginx   → nginx pod
/apache  → apache pod
```

---

## Why Ingress?

Without Ingress:

* Each app requires its own NodePort
* Many open ports
* No SSL or domain routing

With Ingress:

* Single public port
* Path based routing
* Production architecture (used in EKS/AKS/GKE)

---

## Step 1 — Install Ingress Controller only kind cluster

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml
```

Verify:

```bash
kubectl get ns
kubectl get pods -n ingress-nginx
kubectl get svc -n ingress-nginx
kubectl get all -n ingress-nginx
kubectl get ingressclass
```

Wait until controller pod is Running.

---

## Step 2 — Namespace

```bash
kubectl create ns production
```
---

create folder 

```bash
mkdir nginx-ingress
cd nginx-ingress
```
---

## Step 3 — Deploy Applications

### nginx-deployment.yml

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  namespace: production
  labels:
    app: nginx
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
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

### apache-deployment.yml

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: apache2-deployment
  namespace: production
  labels:
    app: apache2
spec:
  replicas: 1
  selector:
    matchLabels:
      app: apache2
  template:
    metadata:
      labels:
        app: apache2
    spec:
      containers:
      - name: apache2
        image: httpd:latest
        ports:
        - containerPort: 80
```

Apply:

```bash
kubectl apply -f nginx-deployment.yml
kubectl apply -f apache-deployment.yml
```

---

## Step 4 — Services

### nginx-service.yml

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
  namespace: production
spec:
  selector:
    app: nginx
  ports:
  - port: 80
    targetPort: 80
    nodePort: 30080
  type: NodePort
```

### apache-service.yml

```yaml
apiVersion: v1
kind: Service
metadata:
  name: apache2-service
  namespace: production
spec:
  selector:
    app: apache2
  ports:
  - port: 80
    targetPort: 80
    nodePort: 30081
  type: NodePort
```

Apply:

```bash
kubectl apply -f nginx-service.yml
kubectl apply -f apache-service.yml
kubectl get all -n production
```

Check endpoints (important):

```bash
kubectl get endpoints -n production
```

---

## Step 5 — Ingress Router

### ingress.yml

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: web-traffic-router
  namespace: production
  # Annotation needed to tell the Nginx Ingress Controller how to handle the path matching
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  # The Ingress Controller will use the LoadBalancer/NodePort it provides
  ingressClassName: nginx # Use the name of your specific Ingress Controller
  rules:
  # A host is not mandatory, but if you don't use one, all traffic will match this rule.
  # If you have a domain, use: host: "example.com"
  - http:
      paths:
      # Rule 1: Route traffic from /apache to the apache2-service
      - path: /apache
        # The pathType Exact means only /apache will match.
        # Prefix means /apache, /apache/foo, /apache/bar all match.
        pathType: Prefix 
        backend:
          service:
            name: apache2-service # Name of your Apache Service
            port:
              number: 80 # The target port on the Service
      # Rule 2: Route traffic from /nginx to the nginx-service
      - path: /nginx
        pathType: Prefix
        backend:
          service:
            name: nginx-service # Name of your Nginx Service
            port:
              number: 80 # The target port on the Service
```

Apply:

```bash
kubectl apply -f ingress.yml
kubectl get ingress -n production
```

---

## Step 6 — Expose to Internet (EC2)

```bash
kubectl port-forward service/ingress-nginx-controller -n ingress-nginx 8080:80 --address=0.0.0.0
```
or
```bash
kubectl port-forward service/ingress-nginx-controller -n ingress-nginx 80:80 --address=0.0.0.0
```
Access:

```
http://EC2-PUBLIC-IP:8080/nginx
http://EC2-PUBLIC-IP:8080/apache
```

---

## Testing

```bash
curl http://localhost:8080/nginx
curl http://localhost:8080/apache
```

---

## Debugging Commands

### Resource Check

```bash
kubectl get pods -A
kubectl get svc -A
kubectl get ingress -A
kubectl describe ingress web-traffic-router -n production
```

### Endpoints (Most Important)

```bash
kubectl get endpoints -n production
```

If empty → service selector mismatch.

### Pod Debug

```bash
kubectl describe pod -n production
kubectl exec -it <pod-name> -n production -- sh
```

---

## Logs

### Ingress Controller Logs

```bash
kubectl logs -n ingress-nginx deploy/ingress-nginx-controller
kubectl logs -f -n ingress-nginx deploy/ingress-nginx-controller
```

### Application Logs

```bash
kubectl logs -n production deploy/nginx-deployment
kubectl logs -n production deploy/apache2-deployment
```

---

## Common Errors

| Error                   | Reason                    |
| ----------------------- | ------------------------- |
| 404 Not Found           | Wrong path                |
| 503 Service Unavailable | Service selector mismatch |
| No endpoints            | Label mismatch            |
| Connection refused      | Port-forward not running  |
| Ingress ignored         | Wrong namespace           |

---

## Cleanup

```bash
kubectl delete namespace production
```
