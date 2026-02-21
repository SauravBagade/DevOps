#  Linux Documentation 1-10
---
# 1. Linux Introduction Basic

## 1.1 What is Linux

Linux is an **open-source operating system kernel** created by **Linus Torvalds** in 1991.
An operating system (OS) acts as an interface between **hardware** and **users/applications**.

Linux by itself is only a **kernel**.
When combined with tools, libraries, shell, and utilities, it becomes a **Linux Operating System** (Linux distribution).

**Key Points:**

* Multi-user
* Multi-tasking
* Secure
* Stable
* Highly customizable

**Examples of Linux OS:**

* Ubuntu
* RHEL
* CentOS
* Amazon Linux

---

## 1.2 Why Linux is Used

Linux is widely used because it is:

* **Free & Open Source**
* **Highly secure**
* **Stable (runs for years without reboot)**
* **Lightweight**
* **Automation friendly**
* **Perfect for servers & cloud**

**Where Linux dominates:**

* Servers (90%+)
* Cloud platforms (AWS, Azure, GCP)
* DevOps & CI/CD
* Containers (Docker, Kubernetes)
* Supercomputers
* Android OS

---

## 1.3 Linux vs Unix

| Feature       | Linux                  | Unix               |
| ------------- | ---------------------- | ------------------ |
| Source        | Open Source            | Mostly Proprietary |
| Cost          | Free                   | Paid               |
| Development   | Community driven       | Vendor driven      |
| Usage         | Servers, Cloud, DevOps | Enterprise systems |
| Customization | High                   | Limited            |

Examples of Unix:

* AIX
* Solaris
* HP-UX

---

## 1.4 Linux vs Windows

| Feature       | Linux       | Windows    |
| ------------- | ----------- | ---------- |
| Cost          | Free        | Paid       |
| Security      | Very strong | Moderate   |
| CLI           | Powerful    | Limited    |
| Automation    | Excellent   | Limited    |
| Server usage  | Very high   | Lower      |
| Customization | Full        | Restricted |

**DevOps uses Linux because:**

* Everything is scriptable
* Native cloud support
* Containers are Linux-based

---

## 1.5 Open Source Concept

**Open Source** means:

* Source code is publicly available
* Anyone can modify, distribute, improve it

Benefits:

* Transparency
* Security (anyone can audit code)
* Community support
* No vendor lock-in

Linux is developed by **thousands of contributors worldwide**.

---

## 1.6 GPL License (GNU General Public License)

Linux uses **GPL (General Public License)**.

GPL ensures:

* You can use the software freely
* You can modify it
* You can redistribute it
* Modified code must remain open source

**GPL protects freedom, not price.**

---

## 1.7 Linux Use Cases

### Server

* Web servers (Apache, Nginx)
* Database servers (MySQL, PostgreSQL)
* Application servers

### Cloud

* AWS EC2
* Azure VM
* Google Compute Engine

### DevOps

* CI/CD pipelines
* Infrastructure as Code
* Automation scripting

### Embedded Systems

* Routers
* Smart TVs
* IoT devices
* Android phones

---

# 2. Linux History & Evolution

---

## 2.1 History of Unix

Unix is the **foundation of Linux**.

**Timeline:**

* **1969** – Unix developed at **Bell Labs**
* Created by **Ken Thompson** and **Dennis Ritchie**
* Written in **C language** (portable, revolutionary)

**Why Unix was important:**

* Multi-user system
* Multi-tasking
* Simple design philosophy
* Powerful command-line tools

Unix introduced core concepts still used in Linux:

* Everything is a file
* Pipes and redirection
* Permissions and ownership
* Process management

**Unix Philosophy:**

> “Do one thing and do it well.”

---

## 2.2 Linus Torvalds

* **1991** – Linus Torvalds, a Finnish student, created the **Linux kernel**
* Inspired by **MINIX** (a teaching OS)
* Initial goal: personal learning project

**Important facts:**

* First Linux version: **0.01**
* Announced on Usenet
* Released as open source under **GPL**

Linux quickly grew because:

* Community contributions
* Open development
* Internet collaboration

Linus still **maintains the Linux kernel** today.

---

## 2.3 Linux Kernel Evolution

The Linux kernel evolved from a hobby project into a **global infrastructure backbone**.

**Key milestones:**

| Year  | Version   | Highlights                |
| ----- | --------- | ------------------------- |
| 1991  | 0.01      | Initial release           |
| 1994  | 1.0       | Stable kernel             |
| 1996  | 2.0       | SMP support               |
| 2003  | 2.6       | Performance & scalability |
| 2011  | 3.x       | Mobile & embedded growth  |
| 2015  | 4.x       | Cloud & containers        |
| 2019+ | 5.x / 6.x | Modern hardware, security |

**Modern Kernel Capabilities:**

* Containers (cgroups, namespaces)
* Cloud workloads
* Security (SELinux, AppArmor)
* High-performance networking

---

## 2.4 Community & Distributions

Linux is **community-driven**, not company-owned.

**Key contributors:**

* Individual developers
* Companies (Red Hat, Google, IBM, Intel, Amazon)

**Linux Distribution =**

> Linux Kernel + User tools + Package manager + Libraries

Different needs → different distributions.

**Why multiple distributions exist:**

* Servers vs desktops
* Stability vs bleeding-edge
* Enterprise vs personal use

---

## 2.5 GNU Project (Very Important)

* Started by **Richard Stallman (1983)**
* Goal: create a **free Unix-like OS**
* Provided essential tools:

  * gcc
  * glibc
  * bash
  * coreutils

Linux kernel + GNU tools = **GNU/Linux**

---

## 2.6 Linux Growth in Industry

Linux dominates:

* 🌐 **Web servers**
* ☁ **Cloud platforms**
* 📦 **Containers**
* 🤖 **Android OS**
* 🧠 **AI & ML workloads**

**Top companies using Linux:**

* Google
* Amazon
* Meta
* Netflix
* Tesla

---

## 2.7 Why Linux Won (Reality)

Linux succeeded because:

* Free and open
* Stable and secure
* Rapid innovation
* No vendor lock-in
* Perfect for automation

Windows failed in servers due to:

* Licensing cost
* Closed ecosystem
* Poor automation (historically)

---

## 2.8 Linux Today

Linux is:

* Backbone of the internet
* Default OS for DevOps
* Mandatory skill for Cloud Engineers

**DevOps Reality:**

> If you don’t know Linux deeply, DevOps is impossible.

---

# 3. Linux Architecture

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

## 3.11 Why Architecture Matters 

You need architecture knowledge to:

* Debug crashes
* Tune performance
* Understand containers
* Handle kernel issues
* Pass interviews

**Containers are kernel features**, not magic.

---

## 4. Linux Distributions

---

## 4.1 Debian Family

Debian-based systems focus on **stability and reliability**.

### Debian

* One of the **oldest Linux distributions**
* Extremely stable
* Slow release cycle
* Preferred for servers

**Package manager:**

```bash
apt
apt-get
```

### Ubuntu

* Based on Debian
* User-friendly
* Fast updates
* Strong community support

Used in:

* Cloud (AWS, Azure, GCP)
* DevOps
* Desktop

Check OS:

```bash
cat /etc/os-release
```

---

## 4.2 RedHat Family

Enterprise-focused distributions.

### RHEL (Red Hat Enterprise Linux)

* Paid
* Enterprise support
* Certified software
* Long-term stability

Used in:

* Banks
* Data centers
* Enterprises

### CentOS (Discontinued classic)

* Free clone of RHEL
* Stable
* Widely used earlier

### Rocky Linux & AlmaLinux

* Replacements for CentOS
* 1:1 compatible with RHEL
* Free & enterprise-ready

**Package manager:**

```bash
yum
dnf
rpm
```

---

## 4.3 SUSE Family

* Enterprise Linux
* Strong in Europe
* Used in SAP environments

Examples:

* SUSE Linux Enterprise (SLES)
* openSUSE

---

## 4.4 Arch Linux

* Rolling release
* Bleeding-edge
* Minimal base install
* For advanced users

Used by:

* Developers
* Linux enthusiasts

Not recommended for servers.

---

## 4.5 Amazon Linux

* AWS-optimized Linux
* Free on AWS EC2
* Security patches included
* Tight AWS integration

Used in:

* Cloud production workloads

Check version:

```bash
cat /etc/system-release
```

---

## 4.6 Alpine Linux

* Extremely lightweight
* Uses musl libc
* Very small image size

Used in:

* Docker containers
* Kubernetes
* Microservices

Check size:

```bash
docker images
```

---

## 4.7 Choosing the Right Distro (Reality)

| Use Case           | Recommended Distro    |
| ------------------ | --------------------- |
| Beginners          | Ubuntu                |
| DevOps             | Ubuntu / Amazon Linux |
| Enterprise         | RHEL / Rocky / Alma   |
| Containers         | Alpine                |
| Desktop            | Ubuntu / Fedora       |
| Learning Internals | Arch                  |

**DevOps Reality:**

> Learn **Ubuntu + RHEL-based**. That covers 90% of jobs.

---

## 4.8 Common Distro Commands

Check distro:

```bash
cat /etc/os-release
```

Check kernel:

```bash
uname -r
```

Package update:

```bash
apt update
dnf update
```
---

# 5. Linux File System Hierarchy (FHS)

---

## 5.1 Root Directory (`/`)

`/` is the **top-level directory**.
All other directories exist **under root**.

You cannot boot Linux without `/`.

Check root:

```bash
ls /
```

---

## 5.2 `/bin` – Essential User Binaries

Contains **basic commands** required for system operation.

Examples:

* ls
* cp
* mv
* rm
* cat
* bash

Used when:

* System is in rescue mode
* Single-user mode

Check:

```bash
ls /bin
```

---

## 5.3 `/boot` – Boot Loader Files

Contains:

* Kernel images
* initramfs
* GRUB files

System **will not boot** if `/boot` is corrupted.

Check:

```bash
ls /boot
```

---

## 5.4 `/dev` – Device Files

Contains **device representations**.

Examples:

* /dev/sda
* /dev/null
* /dev/tty
* /dev/random

Devices are managed by **udev**.

List devices:

```bash
ls /dev
```

---

## 5.5 `/etc` – Configuration Files

Contains **system-wide configuration**.

Examples:

* /etc/passwd
* /etc/shadow
* /etc/hosts
* /etc/ssh/sshd_config

**Rule:**

> No binaries in /etc, only config.

Check:

```bash
ls /etc
```

---

## 5.6 `/home` – User Home Directories

Each user gets:

```bash
/home/username
```

Contains:

* Documents
* Downloads
* User configs (.bashrc)

Example:

```bash
ls /home
```

---

## 5.7 `/lib` and `/lib64` – Essential Libraries

Contains:

* Shared libraries needed by /bin and /sbin

Without these:

* Commands will fail

Check:

```bash
ls /lib
ls /lib64
```

---

## 5.8 `/media` – Removable Media

Used for:

* USB drives
* CDs
* External disks

Auto-mounted by system.

Example:

```bash
ls /media
```

---

## 5.9 `/mnt` – Temporary Mounts

Used by admins for **manual mounts**.

Example:

```bash
mount /dev/sdb1 /mnt
```

---

## 5.10 `/opt` – Optional Software

Used for:

* Third-party applications
* Custom software

Examples:

* /opt/oracle
* /opt/tomcat

Check:

```bash
ls /opt
```

---

## 5.11 `/proc` – Process Information (Virtual FS)

Not real files — generated by kernel.

Contains:

* Process info
* Kernel parameters

Examples:

```bash
cat /proc/cpuinfo
cat /proc/meminfo
```

---

## 5.12 `/root` – Root User Home

Home directory of **root user**.

Not same as `/`.

Check:

```bash
ls /root
```

---

## 5.13 `/run` – Runtime Data

Stores:

* PID files
* Socket files
* Runtime state

Cleared on reboot.

Check:

```bash
ls /run
```

---

## 5.14 `/sbin` – System Binaries

Contains:

* Administrative commands

Examples:

* reboot
* fsck
* ip
* mount

Check:

```bash
ls /sbin
```

---

## 5.15 `/srv` – Service Data

Used by:

* Web servers
* FTP servers

Example:

```bash
/srv/www
```

---

## 5.16 `/sys` – Kernel Interface

Used to:

* Interact with kernel
* Tune hardware

Example:

```bash
ls /sys
```

---

## 5.17 `/tmp` – Temporary Files

* World-writable
* Cleared on reboot

Example:

```bash
touch /tmp/testfile
```

---

## 5.18 `/usr` – User Programs & Data

Contains:

* Applications
* Libraries
* Documentation

Subdirs:

* /usr/bin
* /usr/lib
* /usr/share

Check:

```bash
ls /usr
```

---

## 5.19 `/var` – Variable Data

Contains:

* Logs
* Spool files
* Cache

Important subdirs:

* /var/log
* /var/tmp
* /var/spool

Check logs:

```bash
ls /var/log
```

---

## 5.20 Filesystem Hierarchy Summary

| Directory | Purpose              |
| --------- | -------------------- |
| /         | Root                 |
| /bin      | Essential commands   |
| /etc      | Config files         |
| /home     | User data            |
| /var      | Logs & variable data |
| /proc     | Kernel info          |
| /tmp      | Temporary files      |

---

## 5.21 DevOps Reality (Very Important)

* Logs → `/var/log`
* Config → `/etc`
* Binaries → `/bin` / `/usr/bin`
* Kernel info → `/proc`, `/sys`
* Containers rely heavily on FHS

---
# 6 Terminal & Shell

---

## 6.1 Terminal vs Console

Console:
Physical monitor + keyboard directly attached to machine.
Used in data centers during recovery mode.

Terminal:
Software interface to access system shell.
Examples:

* SSH session
* GNOME Terminal
* PuTTY
* VSCode Remote Terminal

DevOps Reality:
99% of server work happens over terminal (SSH), not console.

---

## 6.2 What is a Shell?

Shell = Command Interpreter
It translates human commands → Kernel system calls

Flow:
User → Shell → Kernel → Hardware

Kernel never talks directly to users.
Shell is the bridge.

---

## 6.3 Types of Shells

| Shell    | Use Case            |
| -------- | ------------------- |
| sh       | Old POSIX scripts   |
| bash     | Default Linux shell |
| zsh      | Power users         |
| fish     | Beginner friendly   |
| csh/tcsh | Legacy systems      |

Check shell:

```
echo $SHELL
```

Check all shells:

```
cat /etc/shells
```

---

## 6.4 Shell Configuration Files

User Level:
~/.bashrc → interactive shell settings
~/.bash_profile → login shell
~/.profile → POSIX compatible

System Level:
/etc/profile
/etc/bashrc
/etc/profile.d/*.sh

Reload config without logout:

```
source ~/.bashrc
```

---

## 6.5 Login vs Non‑Login Shell

Login shell:
SSH login
Console login
su - user

Non-login shell:
Opening terminal inside GUI
Running scripts

Why important?
Environment variables may not load in scripts.

---

## 6.6 Interactive vs Non‑interactive

Interactive:
User typing commands manually

Non-interactive:
Script execution
Cron jobs
CI/CD pipelines

---

## 6.7 Default Shell

Check current shell:

```
echo $SHELL
```

Change shell:

```
chsh -s /bin/bash username
```

---

## 6.8 Shell Prompt (PS1)

Default prompt shows:
user@host:directory$

Customize:

```
PS1="[\u@\h \W]$ "
```

Useful production prompt:
Show hostname to avoid running command on wrong server.

---

## 6.9 Command Structure

General format:
command [options] [arguments]

Example:

```
ls -la /var/log
```

---

## 6.10 Command Execution Order

When you run a command Linux checks in order:

1. Alias
2. Shell built‑in
3. PATH directories

Check command source:

```
type ls
which ls
```

---

## 6.11 Alias & Unalias

Temporary:

```
alias k='kubectl'
```

Permanent:
Add in ~/.bashrc

Remove:

```
unalias k
```

---

## 6.12 History & Shortcuts

Command history:

```
history
!45
!!
```

Shortcuts:
Ctrl + r → search history
Ctrl + a → start
Ctrl + e → end
Ctrl + u → delete line
Ctrl + l → clear screen

---

## 6.13 Job Control

Run background job:

```
sleep 200 &
```

Pause process:
Ctrl + Z

List jobs:

```
jobs
```

Foreground:

```
fg %1
```

Background:

```
bg %1
```

---

## 6.14 Shell Built‑ins

Built into shell (faster than binaries)
Examples:
cd, echo, export, read, exit

Check:

```
type cd
```

---

## 6.15 Environment Awareness

View variables:

```
env
printenv
```

Create variable:

```
export APP=production
```

Used heavily in:
Docker
Kubernetes
CI/CD

---

# 7 Help & Documentation

---

## 7.1 man — Manual Pages

The primary documentation system in Linux.
Every serious troubleshooting starts with man pages.

Basic usage:

```
man ls
man systemctl
```

Man sections:

| Section | Meaning             |
| ------- | ------------------- |
| 1       | User commands       |
| 2       | System calls        |
| 3       | Library functions   |
| 4       | Devices             |
| 5       | Configuration files |
| 6       | Games               |
| 7       | Misc                |
| 8       | Admin commands      |

Example:

```
man 5 passwd
man 8 mount
```

Navigation:

```
Arrow keys → scroll
/word → search
n → next result
Shift+g → end
q → quit
```

---

## 7.2 --help (Quick Help)

Fast option summary.
Useful during scripting.

```
ls --help
cp --help
kubectl --help
```

Best for remembering flags quickly.

---

## 7.3 info — GNU Detailed Docs

More detailed than man pages.
Hierarchical navigation system.

```
info ls
info coreutils 'cp invocation'
```

Navigation:
Enter → open topic
u → up
n → next
q → quit

---

## 7.4 where documentation lives

Installed package documentation path:

```
/usr/share/doc/
```

Examples:

```
ls /usr/share/doc/nginx
ls /usr/share/doc/bash
```

Contains:
README
Examples
Changelog
Config samples

---

## 7.5 apropos & whatis — Command Discovery

Search command by description:

```
apropos password
apropos network
```

Short description:

```
whatis ls
```

Update database (admin):

```
sudo mandb
```

---

## 7.6 help — Shell Built‑ins Help

Used for shell built‑in commands (cd, echo, export).

```
help cd
help export
```

Why important?
man cd will not work because cd is shell built‑in.

---

## 7.7 tldr — Practical Examples (Common in DevOps)

Modern helper tool with real examples.
(Not always preinstalled)

```
tldr tar
tldr docker
```

---

# 8 File & Directory Management

---

## 8.1 Navigation Commands

Print working directory:

```
pwd
```

List files:

```
ls
ls -l
ls -la
ls -lh
ls -ltr
```

Change directory:

```
cd /var/log
cd ..
cd ~
cd -
```

Tips:

* cd - switches to previous directory
* ls -ltr useful for latest logs

---

## 8.2 Creating & Deleting Files and Directories

Create empty file:

```
touch file.txt
```

Create directory:

```
mkdir project
mkdir -p app/src/config
```

Remove empty directory:

```
rmdir dir
```

Remove file:

```
rm file.txt
```

Remove directory recursively:

```
rm -r folder
rm -rf folder
```

⚠ Production Safety:
Never run rm -rf / or rm -rf * in root directories.

Interactive delete:

```
rm -i file
```

---

## 8.3 Copy, Move & Rename

Copy file:

```
cp file1 file2
```

Copy directory:

```
cp -r dir1 dir2
```

Preserve permissions:

```
cp -a source dest
```

Move or rename:

```
mv old new
mv file /tmp/
```

---

## 8.4 File Information & Structure

Show file type:

```
file filename
```

Detailed metadata:

```
stat filename
```

Directory tree view:

```
tree
```

Disk usage by directory:

```
du -sh *
```

---

## 8.5 Find & Search Binaries

Find executable location:

```
which python
```

Find binary + man + source:

```
whereis nginx
```

Difference:
which → PATH lookup
whereis → system database search

---

## 8.6 find Command (Advanced Searching)

Search file by name:

```
find /var -name "*.log"
```

Search case insensitive:

```
find / -iname nginx.conf
```

Search by size:

```
find / -size +100M
```

Search by time:

```
find /var/log -mtime -1
```

Execute command on results:

```
find . -name "*.log" -delete
find . -name "*.txt" -exec rm {} \;
```

---

## Real Production Scenarios

Find large files:

```
find / -size +1G
```

Find logs generated today:

```
find /var/log -mtime 0
```

Delete old backups:

```
find /backup -mtime +7 -delete
```

---

# 9 File Viewing & Editing 

---

## 9.1 Viewing Files

### cat — display full file

```
cat file.txt
cat -n file.txt
```

Avoid using for large files (memory heavy)

### less — recommended viewer (industry standard)

```
less file.log
```

Navigation:
/word → search
n → next
Shift+g → end
g → top
q → quit

### more — older pager

```
more file.txt
```

### head — first lines

```
head file
head -n 50 file
```

### tail — last lines

```
tail file
```

Follow logs (VERY IMPORTANT):

```
tail -f /var/log/syslog
tail -f app.log
```

### watch — run command repeatedly

```
watch -n 2 df -h
watch -n 1 kubectl get pods
```

---

### Log Reading Strategy (Production)

1. tail -f running logs
2. less for investigation
3. grep filtering

Example:

```
tail -f app.log | grep ERROR
```

---

## 9.2 Editing Files

### nano (Beginner Friendly)

```
nano file.txt
```

Controls shown at bottom (Ctrl+O save, Ctrl+X exit)

---

### vi / vim (Industry Standard Editor)

Modes:

| Mode    | Purpose    |
| ------- | ---------- |
| Normal  | Navigation |
| Insert  | Editing    |
| Command | Save/Quit  |

Enter insert:

```
i
```

Save & quit:

```
Esc :wq
```

Quit without saving:

```
Esc :q!
```

---

### Navigation (Important for Interviews)

```
gg → start
G → end
:number → go to line
0 → line start
$ → line end
```

---

### Editing Shortcuts

```
x → delete char
dd → delete line
yy → copy line
p → paste
u → undo
Ctrl+r → redo
```

---

### Search & Replace

Search:

```
/word
```

Replace all:

```
:%s/old/new/g
```

---

### Multi-file Editing (Advanced)

```
vim file1 file2
:n next file
:prev previous
```

---

# 10 Input / Output Redirection & Pipes

This is one of the MOST IMPORTANT Linux topics.
Used everywhere: log analysis, automation, DevOps pipelines, CI/CD, monitoring.

Linux programs communicate using streams:
STDIN  (0) → input
STDOUT (1) → normal output
STDERR (2) → error output

---

## 10.1 Output Redirection

Overwrite file:

```
ls > files.txt
```

Append to file:

```
echo hello >> files.txt
```

Prevent overwrite (safe mode):

```
set -o noclobber
```

---

### Redirect Errors

Only errors:

```
command 2> error.log
```

Output + errors together:

```
command > all.log 2>&1
```

Discard output:

```
command > /dev/null 2>&1
```

---

### Input Redirection

Provide input from file:

```
wc -l < file.txt
```

Here document (multi‑line input):

```
cat <<EOF
hello
world
EOF
```

---

## 10.2 Pipes (|)

Pipe passes output of one command as input to another.

```
ps aux | grep nginx
cat access.log | grep 500 | wc -l
```

Golden Rule:
Small programs + pipes = powerful automation

---

### Multiple Pipes (Data Processing Chain)

```
df -h | grep /dev | sort -k5 -n
```

Log analysis example:

```
grep ERROR app.log | cut -d' ' -f4 | sort | uniq -c | sort -nr
```

---

## 10.3 tee Command

Write to file AND screen simultaneously.

```
echo hello | tee file.txt
echo world | tee -a file.txt
```

Useful in CI/CD logs and debugging scripts.

---

### Named Pipes (FIFO) — Advanced

Create communication channel between processes:

```
mkfifo mypipe
```

Terminal 1:

```
cat mypipe
```

Terminal 2:

```
echo hello > mypipe
```

---

### Real Production Scenarios

Check service errors live:

```
journalctl -u nginx -f | grep error
```

Top memory processes:

```
ps aux --sort=-%mem | head
```

Count failed logins:

```
grep "Failed password" /var/log/auth.log | wc -l
```

---
