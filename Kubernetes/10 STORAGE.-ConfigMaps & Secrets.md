#  ConfigMaps & Secrets (Kubernetes ConfigFile Concept)

# 📘 Overview 

**ConfigMaps and Secrets** allow applications to run without hard-coding configuration inside Docker images.

| Resource  | Used For             | Example           |
| --------- | -------------------- | ----------------- |
| ConfigMap | Non-sensitive config | DB_HOST, PORT     |
| Secret    | Sensitive data       | Passwords, Tokens |

### Why Important?

👉 Makes containers reusable
👉 Change config without rebuilding image
👉 Secure password management
👉 Required in production (12-factor app principle)

---

# 🧩 1️⃣ ConfigMap

## 📄 Purpose

Store configuration data and inject into pods.

Examples:

* DB host
* port
* environment mode
* API URL

---

## 🔧 Create ConfigMap (YAML Method)

### `app-configmap.yml`

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
  namespace: project-db
data:
  DB_HOST: mysql-service
  DB_PORT: "3306"
  DB_NAME: mydb
```

Apply:

```bash
kubectl apply -f app-configmap.yml
kubectl get configmap -n project-db
```

---

## 🧠 How Pod Uses ConfigMap

Injected as environment variables:

```yaml
envFrom:
- configMapRef:
    name: app-config
```

Inside container:

```bash
printenv | grep DB
```

---

# 🔐 2️⃣ Secret

## 📄 Purpose

Store sensitive data securely (passwords, tokens, certificates)

Kubernetes stores secret values in **Base64 encoded format**

> Important: Base64 is NOT encryption — only encoding

---

## ✏️ Create Secret using Base64 (Learning Method)

### Convert values

```bash
echo -n root123 | base64
echo -n mydb | base64
echo -n devuser | base64
echo -n devpass | base64
```

Example Output:

```
cm9vdDEyMw==
bXlkYg==
ZGV2dXNlcg==
ZGV2cGFzcw==
```

---

## 🔧 Secret YAML

### `mysql-secret.yml`

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: mysql-secret
  namespace: project-db
type: Opaque
data:
  MYSQL_ROOT_PASSWORD: cm9vdDEyMw==
  MYSQL_DATABASE: bXlkYg==
  MYSQL_USER: ZGV2dXNlcg==
  MYSQL_PASSWORD: ZGV2cGFzcw==
```

Apply:

```bash
kubectl apply -f mysql-secret.yml
kubectl get secret -n project-db
```

---

## 🧠 How Pod Uses Secret

```yaml
envFrom:
- secretRef:
    name: mysql-secret
```

Check inside container:

```bash
kubectl exec -it <pod> -n project-db -- printenv | grep MYSQL
```

---

# 🗄️ MySQL StatefulSet (Database Deployment)

> Database always uses **StatefulSet** (not Deployment)

Reason:

* Stable Pod name
* Persistent storage
* Ordered start
* Required for DB replication

---

## 📦 PVC (Storage)

### `mysql-pvc.yml`

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mysql-pvc
  namespace: project-db
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```

Apply:

```bash
kubectl apply -f mysql-pvc.yml
```

---

## 🗃️ MySQL StatefulSet

### `mysql-statefulset.yml`

```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: mysql
  namespace: project-db
spec:
  serviceName: mysql-service
  replicas: 1
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
        image: mysql:8
        ports:
        - containerPort: 3306

        envFrom:
        - secretRef:
            name: mysql-secret

        volumeMounts:
        - name: mysql-storage
          mountPath: /var/lib/mysql

  volumeClaimTemplates:
  - metadata:
      name: mysql-storage
    spec:
      accessModes: ["ReadWriteOnce"]
      resources:
        requests:
          storage: 1Gi
```

Apply:

```bash
kubectl apply -f mysql-statefulset.yml
```

---

## 🌐 MySQL Headless Service

### `mysql-service.yml`

```yaml
apiVersion: v1
kind: Service
metadata:
  name: mysql-service
  namespace: project-db
spec:
  clusterIP: None
  selector:
    app: mysql
  ports:
  - port: 3306
    targetPort: 3306
```

Apply:

```bash
kubectl apply -f mysql-service.yml
```

---

# 🔌 Inject MySQL into Application

## `app-statefulset-with-db.yml`

```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: webapp
  namespace: project-db
spec:
  serviceName: webapp-service
  replicas: 2
  selector:
    matchLabels:
      app: webapp

  template:
    metadata:
      labels:
        app: webapp

    spec:
      containers:
      - name: webapp
        image: nginx

        envFrom:
        - configMapRef:
            name: app-config
        - secretRef:
            name: mysql-secret
```

Apply:

```bash
kubectl apply -f app-statefulset-with-db.yml
kubectl rollout restart statefulset webapp -n project-db
```

---

# 🔍 Verification

```bash
kubectl exec -it webapp-0 -n project-db -- printenv | grep DB
kubectl exec -it webapp-0 -n project-db -- printenv | grep MYSQL
```

---

# 🧠 Interview Theory (Very Important)

| Concept                 | Reason                            |
| ----------------------- | --------------------------------- |
| Why ConfigMap?          | Separate config from image        |
| Why Secret?             | Secure sensitive data             |
| Why StatefulSet for DB? | Stable identity & storage         |
| Why Headless Service?   | Direct pod DNS for database       |
| Why envFrom?            | Inject multiple variables at once |

---
