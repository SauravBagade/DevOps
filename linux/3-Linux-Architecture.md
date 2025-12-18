# Linux Documentation – Detailed Guide

---

## 3. Linux Architecture

Linux architecture explains **how Linux works internally** — from hardware to applications.
This is **very important for DevOps, troubleshooting, performance, and interviews**.

---

## 3.1 Hardware Layer

This is the **lowest layer**.

Includes:

* CPU
* RAM
* Disk (HDD / SSD / NVMe)
* Network Interface (NIC)
* I/O devices

Linux does **not** access hardware directly from applications.
All hardware access is controlled by the **kernel**.

**Why this matters:**

* Prevents crashes
* Improves security
* Enables multi-user systems

---

## 3.2 Kernel

The **kernel** is the **core of Linux**.

**Main responsibilities:**

* Process management
* Memory management
* Device drivers
* File system management
* Network stack
* Security & permissions

### Types of Kernel

Linux uses a **Monolithic Kernel**:

* Core services run in kernel space
* Modular (drivers can be loaded/unloaded)

### Kernel Commands

Check kernel version:

```bash
uname -r
```

Full kernel info:

```bash
uname -a
```

Kernel modules:

```bash
lsmod
modprobe module_name
modinfo module_name
```

---

## 3.3 Shell

The **shell** is the **command interpreter**.

Role:

* Takes user commands
* Sends them to kernel
* Displays output

Shell ≠ Kernel

Common shells:

* bash (default)
* sh
* zsh
* fish

Check current shell:

```bash
echo $SHELL
```

---

## 3.4 System Libraries

System libraries provide **standard functions** for applications.

Examples:

* glibc
* libc

Libraries:

* Act as bridge between apps and kernel
* Prevent direct kernel calls

**Without libraries, apps cannot run.**

Check library usage:

```bash
ldd /bin/ls
```

---

## 3.5 User Space

User space is where **applications and users operate**.

Includes:

* Shell
* Applications
* Utilities
* Daemons

Rules:

* User space **cannot directly access hardware**
* Must request kernel via system calls

---

## 3.6 Applications

Applications run in **user space**.

Examples:

* Web servers (nginx, apache)
* Databases (mysql, postgres)
* CLI tools (ls, cp, grep)
* Editors (vim, nano)

Application → Library → Kernel → Hardware

---

## 3.7 Kernel Space vs User Space

| Feature   | Kernel Space         | User Space       |
| --------- | -------------------- | ---------------- |
| Access    | Full hardware access | No direct access |
| Stability | Critical             | Isolated         |
| Crashes   | System crash         | App crash only   |
| Mode      | Privileged           | Unprivileged     |

### Diagram (Conceptual)

```
User
 ↓
Applications
 ↓
Shell
 ↓
System Libraries
 ↓
Kernel
 ↓
Hardware
```

---

## 3.8 System Calls

System calls allow **user programs to request kernel services**.

Examples:

* read()
* write()
* fork()
* exec()

View system calls:

```bash
strace ls
```

---

## 3.9 Device Drivers

Device drivers allow Linux to talk to hardware.

Types:

* Block devices (disk)
* Character devices (keyboard)
* Network devices

Drivers run in **kernel space**.

List devices:

```bash
ls /dev
```

---

## 3.10 Process & Memory Flow

### Process Flow

* Program → Process
* Kernel assigns PID
* Scheduler manages CPU

### Memory Flow

* Virtual memory
* Paging & swapping
* Protection per process

Check memory:

```bash
free -h
vmstat
```

---

## 3.11 Why Architecture Matters (DevOps Reality)

You need architecture knowledge to:

* Debug crashes
* Tune performance
* Understand containers
* Handle kernel issues
* Pass interviews

**Containers are kernel features**, not magic.

---
