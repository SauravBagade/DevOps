# ⚙️ Kubernetes Jobs & CronJobs — Ultimate Complete Guide

---
## 📘 Overview

**Kubernetes Jobs & CronJobs** belong to the **Batch API** — used for tasks that should **finish**, not run forever.

| Resource    | Purpose                           | Example                        |
| ----------- | --------------------------------- | ------------------------------ |
| **Job**     | Run a task once until success     | DB migration, data import      |
| **CronJob** | Run a task repeatedly on schedule | Nightly backup, cleanup script |

> 👉 Deployments = long-running apps
> 👉 Jobs = finish work and exit
> 👉 CronJobs = automate Jobs

---

## 🧱 What is a Job?

A **Job** creates one or more Pods and keeps retrying them **until the task succeeds**.

Behavior:

* Pod fails → Kubernetes restarts new Pod
* Pod succeeds → Job marked **Completed**
* After completion → stops permanently

📌 Real use cases:

* Database schema migration
* Batch processing (ETL)
* Image/video processing
* One-time scripts
* Sending bulk emails

---

## ⚙️ Important Job Fields

| Field                     | Meaning                              |
| ------------------------- | ------------------------------------ |
| `completions`             | How many successful Pods required    |
| `parallelism`             | How many Pods run at same time       |
| `backoffLimit`            | Retry attempts before marking Failed |
| `activeDeadlineSeconds`   | Maximum execution time               |
| `ttlSecondsAfterFinished` | Auto delete after completion         |
| `restartPolicy`           | Must be `Never` or `OnFailure`       |
| `suspend`                 | Pause Job execution                  |
| `template`                | Pod specification                    |

📍 Example meaning:

```
completions: 5
parallelism: 2
```

→ Run 2 pods at a time until 5 succeed

---

## ⏰ What is a CronJob?

A **CronJob** automatically creates a **Job on a schedule** (Linux cron format).

It does NOT run pods directly
➡️ CronJob → creates Job → Job creates Pod

📌 Real use cases:

* Daily database backup
* Cache cleanup every hour
* Log rotation
* Report generation
* Sync data between systems

---

## ⚙️ Important CronJob Fields

| Field                        | Meaning                                |
| ---------------------------- | -------------------------------------- |
| `schedule`                   | Cron timing (`* * * * *`)              |
| `jobTemplate`                | Job specification                      |
| `concurrencyPolicy`          | Allow / Forbid / Replace parallel runs |
| `startingDeadlineSeconds`    | Skip if missed schedule too late       |
| `successfulJobsHistoryLimit` | Keep last successful jobs              |
| `failedJobsHistoryLimit`     | Keep last failed jobs                  |
| `suspend`                    | Pause schedule                         |
| `timeZone`                   | Set timezone (K8s 1.27+)               |

📍 Example:

```
schedule: "0 2 * * *"
```

→ Runs daily at 2 AM

---

## 🧠 Quick Understanding

| Resource | Think Like           |
| -------- | -------------------- |
| Pod      | Worker               |
| Job      | One assignment       |
| CronJob  | Repeating assignment |

---

**Golden Line (Remember):**

> Job guarantees completion
> CronJob guarantees schedule

### 🔹 Job

Runs a task **until it finishes successfully**.

> Pod fails → retry
> Pod succeeds → stop forever

Used for:

* DB migration
* Backup scripts
* ETL processing
* Batch jobs
* Data import/export
* One-time automation

---

### 🔹 CronJob

Runs a **Job on schedule (cron syntax)**

> Example: backup every night at 2 AM

---

## 🎯 Job vs CronJob

| Feature                     | Job | CronJob |
| --------------------------- | --- | ------- |
| One-time task               | ✅   | ❌       |
| Scheduled                   | ❌   | ✅       |
| Retry support               | ✅   | ✅       |
| Parallel execution          | ✅   | ✅       |
| Production batch processing | ✅   | ✅       |

---

# 🧱 PART 1 — JOB PRACTICAL

---

## Step 1 — Namespace

```bash
kubectl create namespace batch
kubectl get ns
kubectl config set-context --current --namespace=batch
```

---

## Step 2 — Create Job YAML

```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: demo-job
  labels:
    app: batch
spec:
  completions: 1
  parallelism: 1
  backoffLimit: 4
  activeDeadlineSeconds: 120
  ttlSecondsAfterFinished: 100
  template:
    metadata:
      labels:
        job: demo
    spec:
      restartPolicy: Never
      containers:
      - name: job
        image: busybox
        command: ["sh","-c","echo Hello Kubernetes && sleep 5"]
```

Apply:

```bash
kubectl apply -f job.yaml
```

---

## Step 3 — Verify

```bash
kubectl get jobs
kubectl get pods
kubectl get pods -o wide
kubectl describe job demo-job
kubectl get all
```

Watch live:

```bash
kubectl get pods -w
```

---

## Step 4 — Logs

```bash
kubectl logs <pod-name>
kubectl logs -f <pod-name>
kubectl logs -l job-name=demo-job
```

---

## Step 5 — Parallel Jobs

```yaml
completions: 5
parallelism: 2
```

Meaning:

* Need 5 successful pods
* Run 2 at same time

---

## Step 6 — Retry Control

```yaml
backoffLimit: 3
```

If failed 3 times → Job FAILED

Check failures:

```bash
kubectl describe job demo-job | grep Failed
```

---

## Step 7 — Timeout

```yaml
activeDeadlineSeconds: 60
```

If running > 60 sec → KILLED

---

## Step 8 — Auto Cleanup

```yaml
ttlSecondsAfterFinished: 30
```

Auto delete completed pod + job

---

## Step 9 — Suspend / Resume Job

```bash
kubectl patch job demo-job -p '{"spec":{"suspend":true}}'
kubectl patch job demo-job -p '{"spec":{"suspend":false}}'
```

---

## Step 10 — Change Image (Recreate Required)

Jobs immutable → must delete & recreate

```bash
kubectl delete job demo-job
kubectl apply -f job.yaml
```

---

## Step 11 — Export YAML

```bash
kubectl get job demo-job -o yaml > job-export.yaml
kubectl get job demo-job -o json
```

---

## Step 12 — Label Filtering

```bash
kubectl get pods -l job-name=demo-job
kubectl delete pods -l job-name=demo-job
```

---

## Step 13 — Manual Trigger New Run

```bash
kubectl create job manual-job --from=job/demo-job
```

---

## Step 14 — Delete

```bash
kubectl delete job demo-job
```

---

# ⏰ PART 2 — CRONJOB PRACTICAL

---

## Step 1 — CronJob YAML

```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: demo-cron
spec:
  schedule: "*/1 * * * *"
  timeZone: "Asia/Kolkata"
  concurrencyPolicy: Forbid
  successfulJobsHistoryLimit: 3
  failedJobsHistoryLimit: 1
  jobTemplate:
    spec:
      template:
        spec:
          restartPolicy: Never
          containers:
          - name: cron
            image: busybox
            command: ["sh","-c","date; echo running cron"]
```

Apply:

```bash
kubectl apply -f cronjob.yaml
```

---

## Step 2 — Verify

```bash
kubectl get cronjobs
kubectl get jobs
kubectl get pods
kubectl describe cronjob demo-cron
```

Watch execution:

```bash
kubectl get jobs -w
```

---

## Step 3 — Suspend & Resume

```bash
kubectl patch cronjob demo-cron -p '{"spec":{"suspend":true}}'
kubectl patch cronjob demo-cron -p '{"spec":{"suspend":false}}'
```

---

## Step 4 — Run Immediately

```bash
kubectl create job manual-run --from=cronjob/demo-cron
```

---

## Step 5 — Change Schedule

```bash
kubectl edit cronjob demo-cron
```

or

```bash
kubectl patch cronjob demo-cron -p '{"spec":{"schedule":"*/5 * * * *"}}'
```

---

## Step 6 — Concurrency Policy

| Value   | Behavior             |
| ------- | -------------------- |
| Allow   | Run multiple jobs    |
| Forbid  | Skip if running      |
| Replace | Kill old & start new |

---

## Step 7 — Missed Job Deadline

```yaml
startingDeadlineSeconds: 30
```

If missed > 30 sec → skip run

---

## Step 8 — History Cleanup

```yaml
successfulJobsHistoryLimit: 2
failedJobsHistoryLimit: 1
```

---

## Step 9 — Logs

```bash
kubectl logs <cronjob-pod>
kubectl logs -l job-name=<job-created-by-cron>
```

---

## Step 10 — Delete

```bash
kubectl delete cronjob demo-cron
kubectl delete namespace batch
```

---

# 📦 Get All Resources

```bash
kubectl get all
kubectl get jobs
kubectl get cronjobs
kubectl get pods
kubectl get events
```

---

# 🧠 Debug Commands (Very Important in Interview)

```bash
kubectl describe job demo-job
kubectl describe cronjob demo-cron
kubectl get events --sort-by=.metadata.creationTimestamp
kubectl logs -l job-name=demo-job
kubectl get pods -w
kubectl get pods -o wide
```

---

# 🧾 Cron Syntax (Remember for Interview)

```
* * * * *
| | | | |
| | | | └ Day of week (0-7)
| | | └── Month
| | └──── Day
| └────── Hour
└──────── Minute
```

Examples:

```
*/5 * * * *  → every 5 min
0 * * * *    → every hour
0 0 * * *    → daily midnight
0 2 * * *    → 2 AM daily
0 3 * * 0    → Sunday 3 AM
```

---

# 🏁 Final Summary

| Resource          | Purpose              |
| ----------------- | -------------------- |
| Job               | Run task once        |
| Parallel Job      | Batch processing     |
| CronJob           | Scheduled automation |
| TTL               | Auto cleanup         |
| BackoffLimit      | Retry control        |
| ConcurrencyPolicy | Overlap control      |
| ActiveDeadline    | Timeout              |
| HistoryLimit      | Cleanup old runs     |

---

✅ **Golden Interview Line**

> Deployment runs forever
> Job runs until completion
> CronJob runs on schedule

---

If you want next → I’ll make **Production real examples (DB backup to S3, log cleanup, report generator)** — that’s what interviewers actually ask.
