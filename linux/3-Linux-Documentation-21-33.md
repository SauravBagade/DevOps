# 21 Environment Variables 

---

## 21.1 Local vs Global Variables

### Local Variable

Available only in current shell session

```bash
NAME=Saurav
echo $NAME
```

Not available to child processes

```bash
bash
echo $NAME   # empty
```

---

### Global Variable (Environment Variable)

Exported to child processes

```bash
export NAME=Saurav
bash
echo $NAME   # works
```

---

## 21.2 env

Displays environment variables

```bash
env
```

Run program with temporary variable

```bash
PORT=8080 env | grep PORT
```

---

## 21.3 printenv

Better for scripting

```bash
printenv PATH
```

Difference:

| Command  | Purpose                |
| -------- | ---------------------- |
| env      | show all variables     |
| printenv | show specific variable |

---

## 21.4 export

Convert local → environment variable

```bash
APP=nginx
export APP
```

One line:

```bash
export APP=nginx
```

---

## 21.5 echo $VAR

```bash
echo $HOME
echo $USER
echo $PATH
```

---

## 21.6 set

Shows shell variables + functions

```bash
set | less
```

---

## 21.7 unset

Remove variable

```bash
unset APP
```

---

## 21.8 PATH Variable (VERY IMPORTANT)

Tells shell where to find executables

View PATH

```bash
echo $PATH
```

Add temporary path

```bash
export PATH=$PATH:/opt/scripts
```

---

## 21.9 .bashrc

Loaded for interactive non‑login shell

Common usage:

* aliases
* prompt
* environment variables

Reload:

```bash
source ~/.bashrc
```

---

## 21.10 .profile

Login shell configuration (POSIX compatible)

Used by:

* SSH login
* TTY login

---

## 21.11 .bash_profile

Bash specific login configuration
Priority order:

1. .bash_profile
2. .bash_login
3. .profile

---

## 21.12 .bash_login

Rarely used fallback login file

---

## 21.13 /etc/environment

System wide variables (no shell syntax)

Example:

```
JAVA_HOME=/usr/lib/jvm/java-17
```

---

## 21.14 /etc/profile

Global login shell configuration

---

## 21.15 /etc/profile.d/*.sh

Best production practice
Create app specific config

```bash
sudo nano /etc/profile.d/java.sh
export JAVA_HOME=/opt/java
```

---

## 21.16 Command-level variables

Temporary variable only for one command

```bash
PORT=3000 node app.js
DEBUG=true npm start
```

---

## 21.17 SHELL Variable

Current shell info

```bash
echo $SHELL
ps -p $$
```

---

# Variable Scope Summary

| Scope            | Lifetime      | File             |
| ---------------- | ------------- | ---------------- |
| Local            | current shell | none             |
| Exported         | child process | export           |
| User permanent   | user login    | ~/.bashrc        |
| System permanent | all users     | /etc/environment |

---

# Production DevOps Usage

## Java / Docker / Kubernetes

```bash
export JAVA_HOME=/usr/lib/jvm/java-17
export KUBECONFIG=/etc/kubernetes/admin.conf
export DOCKER_HOST=tcp://127.0.0.1:2375
```

## Secrets (never hardcode in scripts)

Use environment variables instead

---

# 22 Scheduling & Automation (cron, at, system jobs)

## 22.1 cron (Concept)

cron = time‑based job scheduler in Linux
Used for automation: backups, log cleanup, monitoring, patching

Daemon:

```
crond / cron
```

Time Format (VERY IMPORTANT)

```
* * * * * command
| | | | |
| | | | └── Day of week (0‑7 Sun)
| | | └──── Month (1‑12)
| | └────── Day of month (1‑31)
| └──────── Hour (0‑23)
└────────── Minute (0‑59)
```

Examples:

```
* * * * *        every minute
*/5 * * * *      every 5 minutes
0 * * * *        every hour
0 2 * * *        daily 2 AM
0 2 * * 0        weekly Sunday 2 AM
0 2 1 * *        monthly 1st day
```

---

## 22.2 crontab

User cron table

View:

```
crontab -l
```

Edit:

```
crontab -e
```

Remove:

```
crontab -r
```

Different user:

```
sudo crontab -u nginx -e
```

---

## 22.3 at (One‑time jobs)

Run command once in future

Start service:

```
systemctl enable --now atd
```

Schedule job:

```
at 10:30
at now + 5 minutes
at now + 1 hour
at 2am tomorrow
```

Then type command → Ctrl+D

---

## 22.4 atq

List scheduled at jobs

```
atq
```

---

## 22.5 atrm

Remove job

```
atrm 3
```

---

## 22.6 batch

Run when system load is low

```
batch
```

---

## 22.7 watch

Repeatedly run command (monitoring)

```
watch -n 2 free -m
watch df -h
```

---

## 22.8 /etc/crontab (System Cron)

System‑wide scheduled tasks
Format includes USER field

```
* * * * * user command
```

Example:

```
0 3 * * * root /usr/local/bin/backup.sh
```

---

## 22.9 /etc/cron.hourly

Run scripts every hour

## 22.10 /etc/cron.daily

Daily jobs (logrotate etc)

## 22.11 /etc/cron.weekly

Weekly jobs

## 22.12 /etc/cron.monthly

Monthly jobs

---

## 22.13 /etc/cron.allow

Users allowed to run cron

## 22.14 /etc/cron.deny

Users denied cron access

---

## 22.15 /etc/at.allow

Users allowed at command

## 22.16 /etc/at.deny

Users denied at command

---

## 22.17 cron service (systemctl)

```
systemctl status cron
systemctl restart cron
systemctl enable cron
```

(RHEL: crond)

---

## 22.18 cron logs (Troubleshooting)

Ubuntu/Debian:

```
/var/log/syslog
```

RHEL:

```
/var/log/cron
```

Check:

```
grep CRON /var/log/syslog
```

---

# Production Best Practices

## Always use full paths

BAD:

```
backup.sh
```

GOOD:

```
/usr/local/bin/backup.sh
```

## Redirect output

```
0 2 * * * /backup.sh >> /var/log/backup.log 2>&1
```

## Avoid interactive commands

cron has no TTY

## Use environment variables

```
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

---

# DevOps Real Use Cases

* DB backup nightly
* Clear docker logs
* Rotate application logs
* Health check monitoring
* SSL renewal (certbot)
* Kubernetes cleanup jobs

---

# 23 System Monitoring (CPU, Memory, Disk, Network, Load, Performance)

---
## 23.1 CPU Monitoring

### top (real‑time processes)

```
top
```

Keys:

* P → CPU sort
* M → Memory sort
* k → kill process
* 1 → per‑core CPU

Fields:

| Field | Meaning          |
| ----- | ---------------- |
| us    | user CPU         |
| sy    | system CPU       |
| id    | idle             |
| wa    | IO wait          |
| st    | steal (VM issue) |

---

### htop (better top)

```
htop
```

Color bars show usage clearly
(F3 search, F9 kill)

---

### mpstat (per‑CPU stats)

```
mpstat -P ALL 1
```

Detect CPU imbalance

---

## 23.2 Memory Monitoring

### free

```
free -h
```

Important:

* available = real usable RAM
* buff/cache = reclaimable memory

### vmstat

```
vmstat 1
```

Important columns:
| r | runnable processes |
| si/so | swap in/out |
| wa | IO wait |

Swap usage high → RAM shortage

---

## 23.3 Disk Monitoring

### df (filesystem usage)

```
df -h
```

### du (directory usage)

```
du -sh *
```

### iostat (disk IO)

```
iostat -xz 1
```

Key metrics:
| util | disk busy % |
| await | latency |
| svctm | service time |

High await → storage slow

---

## 23.4 Process Monitoring

### ps

```
ps aux
ps -ef --forest
```

### pstree

```
pstree -p
```

Parent‑child relation debugging

---

## 23.5 Network Monitoring

### ss (modern netstat)

```
ss -tulnp
```

### netstat (legacy)

```
netstat -tulnp
```

### iftop (live bandwidth)

```
iftop
```

### nload

```
nload
```

---

## 23.6 System Load & Uptime

```
uptime
```

Load average:

| Value | Meaning        |
| ----- | -------------- |
| 1m    | immediate load |
| 5m    | short term     |
| 15m   | long term      |

Rule:
Load > CPU cores → system overloaded

---

## 23.7 Performance Statistics

### sar (historical metrics)

```
sar -u 1 5
sar -r
sar -d
```

Enable on Ubuntu:

```
sudo apt install sysstat
```

### dstat (combined view)

```
dstat -cdnm
```

---

# /proc Monitoring (Advanced)

```
cat /proc/cpuinfo
cat /proc/meminfo
cat /proc/loadavg
```

---

# Production Troubleshooting Flow

High CPU → top → mpstat → ps
High Memory → free → vmstat → top
Disk Full → df → du
Slow App → iostat → wa%
Network Issue → ss → iftop

---

# DevOps Use Cases

* Detect container resource limits
* Kubernetes node debugging
* Identify noisy neighbor VM
* Investigate slow DB queries

---

# 24 Logging & Journals (rsyslog, journald, logrotate, troubleshooting)

---
## 24.1 Log Files Concept

Linux stores system & application events as logs for auditing and troubleshooting.

Types:

* System logs
* Authentication logs
* Application logs
* Kernel logs

---

## 24.2 /var/log Directory

Main log directory

```
ls -lah /var/log
```

Common files:

| File              | Purpose                 |
| ----------------- | ----------------------- |
| syslog / messages | general system logs     |
| auth.log / secure | login attempts          |
| kern.log          | kernel events           |
| dmesg             | boot messages           |
| boot.log          | boot services           |
| dpkg.log          | package install history |
| apt/history.log   | apt operations          |

---

## 24.3 Common Log Files

Authentication:

```
/var/log/auth.log
```

Failed SSH login:

```
grep Failed /var/log/auth.log
```

Boot logs:

```
dmesg | less
```

---

## 24.4 rsyslog (Traditional logging)

Service collects logs from system and apps

Config:

```
/etc/rsyslog.conf
/etc/rsyslog.d/*.conf
```

Restart:

```
systemctl restart rsyslog
```

---

## 24.5 journalctl (systemd logs)

Central binary logging system

View logs:

```
journalctl
```

Boot logs:

```
journalctl -b
```

Service logs:

```
journalctl -u nginx
```

Live logs:

```
journalctl -f
```

Time filter:

```
journalctl --since "10 min ago"
```

---

## 24.6 journald

Binary log storage system
Location:

```
/run/log/journal  (temporary)
/var/log/journal  (persistent)
```

Enable persistent logs:

```
mkdir -p /var/log/journal
systemctl restart systemd-journald
```

---

## 24.7 Log Levels

| Level   | Meaning              |
| ------- | -------------------- |
| emerg   | system unusable      |
| alert   | immediate action     |
| crit    | critical             |
| err     | error                |
| warning | warning              |
| notice  | normal but important |
| info    | informational        |
| debug   | debug details        |

---

## 24.8 logger Command

Write custom log entry

```
logger "Backup completed"
```

---

## 24.9 Log Rotation

Prevents disk full due to logs

---

## 24.10 logrotate

Rotate, compress, delete old logs

Manual run:

```
logrotate -f /etc/logrotate.conf
```

---

## 24.11 /etc/logrotate.conf

Global rotation config

---

## 24.12 /etc/logrotate.d/

Per‑application rotation configs

Example nginx:

```
/var/log/nginx/*.log {
    daily
    rotate 14
    compress
    missingok
    notifempty
}
```

---

## 24.13 Persistent Journals

Keeps logs after reboot
Required in production debugging

---

# Production Troubleshooting

Service failed:

```
journalctl -u nginx -xe
```

SSH attack detection:

```
grep "Failed password" /var/log/auth.log
```

Disk full due to logs:

```
du -sh /var/log/*
```

---

# DevOps Use Cases

* Debug failed deployment
* Detect brute force login
* Audit system activity
* Kubernetes node troubleshooting

---

# 25 Services & systemd (units, targets, timers, production usage)
l
---
## 25.1 systemd Architecture

systemd = init system (PID 1) that manages boot, services, sockets, mounts and timers.

Boot Flow:
BIOS/UEFI → Bootloader (GRUB) → Kernel → systemd → Targets → Services

Check PID 1:

```
ps -p 1 -o comm=
```

---

## 25.2 systemctl (Main command)

```
systemctl list-units
systemctl list-unit-files
systemctl daemon-reload
```

---

## 25.3 Service Files (Unit Files)

Location priority:

| Path                    | Purpose                   |
| ----------------------- | ------------------------- |
| /etc/systemd/system     | custom (highest priority) |
| /run/systemd/system     | runtime                   |
| /usr/lib/systemd/system | packages                  |

---

## 25.4 Unit File Types

| Type    | Extension |
| ------- | --------- |
| Service | .service  |
| Target  | .target   |
| Socket  | .socket   |
| Mount   | .mount    |
| Timer   | .timer    |
| Path    | .path     |

---

## 25.5 Service File Structure

Example:

```
[Unit]
Description=My App
After=network.target

[Service]
ExecStart=/usr/bin/python3 /opt/app/app.py
Restart=always
User=ubuntu

[Install]
WantedBy=multi-user.target
```

Reload config:

```
systemctl daemon-reload
```

---

## 25.6 Start / Stop / Restart

```
systemctl start nginx
systemctl stop nginx
systemctl restart nginx
systemctl reload nginx
```

---

## 25.7 Enable / Disable (Boot startup)

```
systemctl enable nginx
systemctl disable nginx
systemctl is-enabled nginx
```

---

## 25.8 Status & Listing

```
systemctl status nginx
systemctl list-units --type=service --state=running
```

Logs directly:

```
journalctl -u nginx
```

---

## 25.9 Reload & Reexec

```
systemctl daemon-reload   # reread unit files
systemctl daemon-reexec   # restart systemd process safely
```

---

## 25.10 Targets (Runlevels replacement)

| Old Runlevel | systemd Target    |
| ------------ | ----------------- |
| 0            | poweroff.target   |
| 1            | rescue.target     |
| 3            | multi-user.target |
| 5            | graphical.target  |
| 6            | reboot.target     |

Switch:

```
systemctl isolate multi-user.target
```

Default target:

```
systemctl get-default
systemctl set-default multi-user.target
```

---

## 25.11 systemd Timers (Cron alternative)

Timer file:

```
[Timer]
OnCalendar=*-*-* 02:00:00
Persistent=true
```

Service + timer:

```
systemctl enable backup.timer
systemctl start backup.timer
systemctl list-timers
```

Advantages over cron:

* dependency aware
* missed job recovery
* logs in journal

---

# Production Best Practices

* Never edit files in /usr/lib/systemd/system
* Use /etc/systemd/system override files
* Always daemon-reload after change
* Use Restart=always for apps
* Use After=network-online.target for network apps

---

# DevOps Use Cases

* Run Node/Java apps as services
* Auto restart crashed containers
* Replace cron with timers
* Control DB startup order

---

# 26 SSH & Remote Access (Keys, Config, Security, Tunneling, rsync)

---
## 26.1 SSH Basics

Secure Shell allows remote login & command execution over encrypted channel (TCP 22 by default)

Connect:

```
ssh user@server_ip
ssh user@host -p 2222
```

First login stores fingerprint in:

```
~/.ssh/known_hosts
```

---

## 26.2 Password Authentication

Server side config:

```
/etc/ssh/sshd_config
PasswordAuthentication yes
```

Restart service:

```
systemctl restart ssh
```

---

## 26.3 Key Authentication (Recommended)

Generate key pair:

```
ssh-keygen -t ed25519 -C "mykey"
```

Files:

| File           | Purpose              |
| -------------- | -------------------- |
| id_ed25519     | private key (secret) |
| id_ed25519.pub | public key           |

Copy to server:

```
ssh-copy-id user@server_ip
```

Manual:

```
cat id_ed25519.pub >> ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
chmod 700 ~/.ssh
```

Login:

```
ssh user@server_ip
```

---

## 26.4 SSH Commands

Execute remote command:

```
ssh user@host "uptime"
```

Interactive shell:

```
ssh -t user@host bash
```

Verbose debug:

```
ssh -vvv user@host
```

---

## 26.5 SSH Server

Service name:

| Distro        | Service |
| ------------- | ------- |
| Ubuntu/Debian | ssh     |
| RHEL/CentOS   | sshd    |

Check:

```
systemctl status ssh
```

---

## 26.6 SSH Configuration

Main config:

```
/etc/ssh/sshd_config
```

Important settings:

```
Port 22
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
MaxAuthTries 3
AllowUsers devops
```

Reload safely:

```
sshd -t
systemctl reload ssh
```

---

## 26.7 Key Management

Agent:

```
eval "$(ssh-agent)"
ssh-add ~/.ssh/id_ed25519
```

Multiple hosts config:

```
~/.ssh/config
Host prod
  HostName 10.0.0.5
  User ubuntu
  IdentityFile ~/.ssh/prod.pem
```

Connect:

```
ssh prod
```

---

## 26.8 Security Hardening

Best practices:

* Disable root login
* Disable password auth
* Change port
* Use fail2ban
* Limit users
* Use firewall allow only office IP

Example:

```
PermitRootLogin no
PasswordAuthentication no
AllowUsers ubuntu devops
```

---

## 26.9 Port Forwarding & Tunneling

Local forward (access remote DB locally):

```
ssh -L 3306:localhost:3306 user@server
```

Remote forward:

```
ssh -R 8080:localhost:80 user@server
```

Dynamic proxy (SOCKS VPN):

```
ssh -D 1080 user@server
```

---

## 26.10 Debugging

Connection issues:

```
ssh -vvv user@server
journalctl -u ssh
```

Permission denied (publickey):

* wrong permissions
* wrong user
* wrong key

Required permissions:

```
700 ~/.ssh
600 authorized_keys
```

---

## 26.11 rsync over SSH

Secure file sync:

```
rsync -avz file user@server:/backup/
rsync -avz user@server:/data ./data
```

Auto backup:

```
rsync -az --delete /var/www user@backup:/data/www
```

---

# Production DevOps Use Cases

* CI/CD deployment
* Remote troubleshooting
* Database tunnels
* Secure backups
* Kubernetes node access

---

# 27 Linux Security (Firewall, SELinux, AppArmor, Fail2ban)

---
## 27.1 Linux Security Model

Layers of security:

1. User & Permissions (rwx, sudo)
2. Authentication (PAM, SSH)
3. Network firewall
4. Mandatory Access Control (SELinux/AppArmor)
5. Intrusion prevention (Fail2ban)
6. Auditing & logs

Principle: **Least Privilege**

---

## 27.2 Firewall Concepts

Controls inbound/outbound traffic using rules.
Key ideas:

* Allow vs deny
* Stateful inspection
* Default policy (deny recommended)

---

## 27.3 ufw (Ubuntu firewall)

Easy wrapper over iptables

Enable:

```
sudo ufw enable
```

Status:

```
ufw status verbose
```

Allow SSH:

```
ufw allow 22
```

Allow port:

```
ufw allow 80/tcp
```

Deny IP:

```
ufw deny from 1.2.3.4
```

Delete rule:

```
ufw delete allow 80
```

---

## 27.4 firewalld (RHEL based)

Zone based firewall

Check:

```
firewall-cmd --state
```

List zones:

```
firewall-cmd --get-active-zones
```

Allow service:

```
firewall-cmd --permanent --add-service=http
firewall-cmd --reload
```

Allow port:

```
firewall-cmd --permanent --add-port=8080/tcp
```

---

## 27.5 SELinux (Mandatory Access Control)

Adds policy rules beyond file permissions.
Modes:

| Mode       | Meaning           |
| ---------- | ----------------- |
| Enforcing  | blocks violations |
| Permissive | logs only         |
| Disabled   | off               |

Check mode:

```
getenforce
```

Temporary permissive:

```
setenforce 0
```

Contexts:

```
ls -Z /var/www/html
```

Restore default context:

```
restorecon -Rv /var/www
```

---

## 27.6 AppArmor (Ubuntu MAC alternative)

Profile based protection

Status:

```
aa-status
```

Complain mode:

```
aa-complain /usr/sbin/nginx
```

Enforce mode:

```
aa-enforce /usr/sbin/nginx
```

---

## 27.7 Fail2ban (Intrusion prevention)

Blocks brute‑force attackers via firewall rules

Install:

```
sudo apt install fail2ban
```

Config copy:

```
cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
```

Enable SSH protection:

```
[sshd]
enabled = true
maxretry = 3
bantime = 1h
```

Status:

```
fail2ban-client status sshd
```

---

# Production Hardening Checklist

* Disable root SSH login
* Key authentication only
* Firewall allow required ports only
* Enable fail2ban
* Keep updates patched
* Separate service users
* Monitor auth logs

---

# DevOps Use Cases

* Protect public servers
* Secure Kubernetes nodes
* Prevent brute force attacks
* Compliance hardening (CIS)

---

# 28 Boot Troubleshooting & Recovery (GRUB, rescue, emergency, password reset)

---
## 28.1 Single User Mode (Maintenance)

Minimal environment with root access (no network by default)

From GRUB:

* Press `e` on kernel
* Append: `single` or `systemd.unit=rescue.target`
* Boot with Ctrl+X

Use cases:

* Fix configs
* Repair filesystem
* Reset password

---

## 28.2 Rescue Mode

Loads basic services + root shell

```
systemctl isolate rescue.target
```

Mount root RW:

```
mount -o remount,rw /
```

---

## 28.3 Emergency Mode

Lowest level (almost no services)

```
systemctl isolate emergency.target
```

Used when filesystem corrupted

---

## 28.4 GRUB Commands

List disks:

```
ls
```

Set root:

```
set root=(hd0,1)
linux /vmlinuz root=/dev/sda1 rw
initrd /initrd.img
boot
```

---

## 28.5 Reset Root Password

1. Edit kernel line add:

```
rd.break
```

2. Boot
3. Remount:

```
mount -o remount,rw /sysroot
chroot /sysroot
passwd root
```

4. SELinux relabel:

```
touch /.autorelabel
```

5. Reboot

---

## 28.6 fsck in Recovery

Check filesystem errors

```
fsck -fy /dev/sda1
```

Never run on mounted RW filesystem

---

## 28.7 Initramfs Rebuild

Broken boot modules fix

```
draccut -f        # RHELdraccut -f        # RHEL\update-initramfs -u   # Ubuntu
```

---

## 28.8 Boot Logs

```
dmesg | less
journalctl -b
journalctl -xb
```

---

# Production Troubleshooting Flow

Boot stops → check journalctl -xb
Kernel panic → initramfs rebuild
Filesystem error → fsck
Forgot password → rd.break
Service fails → rescue mode

---

# DevOps Use Cases

* Recover cloud VM
* Fix failed fstab mount
* Repair corrupted disk
* Recover locked root account

--- 

# 29 Kernel Management (modules, parameters, sysctl, troubleshooting)

---
## 29.1 Kernel Version

Show running kernel:

```
uname -r
uname -a
```

Installed kernels (Debian/Ubuntu):

```
dpkg --list | grep linux-image
```

(RHEL):

```
rpm -qa | grep kernel
```

---

## 29.2 Kernel Modules (Concept)

Modules = drivers loaded dynamically (no reboot required)
Examples: filesystem, network, virtualization, storage

List loaded modules:

```
lsmod
```

Module dependency tree:

```
lsmod | less
```

---

## 29.3 modprobe (Load module)

Load module:

```
sudo modprobe br_netfilter
```

Remove module:

```
sudo modprobe -r br_netfilter
```

Load at boot:

```
/etc/modules-load.d/k8s.conf
br_netfilter
```

---

## 29.4 modinfo (Module info)

```
modinfo br_netfilter
```

Shows version, author, parameters, dependencies

---

## 29.5 rmmod (Remove module)

Force remove:

```
sudo rmmod module_name
```

Fails if module in use

---

## 29.6 sysctl (Kernel runtime parameters)

View all:

```
sysctl -a | less
```

View specific:

```
sysctl net.ipv4.ip_forward
```

Temporary change:

```
sysctl -w net.ipv4.ip_forward=1
```

---

## 29.7 /proc/sys (Direct interface)

Equivalent to sysctl:

```
cat /proc/sys/net/ipv4/ip_forward
echo 1 > /proc/sys/net/ipv4/ip_forward
```

(Not persistent)

---

## 29.8 Persistent Kernel Parameters

Edit:

```
/etc/sysctl.conf
/etc/sysctl.d/*.conf
```

Example:

```
net.ipv4.ip_forward = 1
vm.swappiness = 10
fs.file-max = 1000000
```

Apply:

```
sysctl -p
```

---

## 29.9 Boot Kernel Parameters (GRUB)

Edit:

```
/etc/default/grub
```

Add parameters:

```
GRUB_CMDLINE_LINUX="quiet splash cgroup_enable=memory swapaccount=1"
```

Apply:

```
update-grub        # Debian/Ubuntu
grub2-mkconfig -o /boot/grub2/grub.cfg   # RHEL
```

Common parameters:

* nomodeset (GPU issues)
* systemd.unified_cgroup_hierarchy=0
* selinux=0 (troubleshooting only)

---

# Production DevOps Usage

* Kubernetes requires br_netfilter + ip_forward
* High traffic tuning via tcp parameters
* Increase file descriptors for DB servers
* Disable swap for containers

---

# Troubleshooting Examples

Networking not forwarding:

```
sysctl net.ipv4.ip_forward
```

Pods cannot communicate:

```
modprobe br_netfilter
sysctl net.bridge.bridge-nf-call-iptables=1
```

Too many open files:

```
sysctl fs.file-max
```

---

# 30 Advanced Permissions & ACL (POSIX ACL, Default ACL, Capabilities)

---
## 30.1 ACL Concept

ACL = Access Control List → allows fine‑grained permissions beyond rwx for owner/group/others.
Useful when multiple users need different permissions on same file.

Check filesystem support:

```
tune2fs -l /dev/sda1 | grep "Default mount options"
```

Mount with ACL if required:

```
mount -o remount,acl /
```

---

## 30.2 getfacl (View ACL)

```
getfacl file.txt
```

Output fields:

| Field     | Meaning           |
| --------- | ----------------- |
| user::    | owner permissions |
| user:john | specific user     |
| group::   | group permissions |
| mask      | maximum allowed   |
| other     | others            |

---

## 30.3 setfacl (Set ACL)

Give read access to user:

```
setfacl -m u:john:r file.txt
```

Give rw access to group:

```
setfacl -m g:dev:rw file.txt
```

Remove ACL:

```
setfacl -x u:john file.txt
```

Remove all ACLs:

```
setfacl -b file.txt
```

---

## 30.4 Default ACL (Directory inheritance)

New files inherit permissions

```
setfacl -d -m u:john:rw project/
```

Important for shared team directories

---

## 30.5 Capabilities (Root privilege splitting)

Traditional Linux:
root = all power
Capabilities → give only specific privileges

Example allow ping without root:

```
setcap cap_net_raw+p /bin/ping
```

---

## 30.6 getcap

```
getcap /bin/ping
```

---

## 30.7 setcap

Give port binding under 1024 without root:

```
setcap cap_net_bind_service=+ep /usr/bin/node
```

Remove capability:

```
setcap -r /usr/bin/node
```

---

# Permission Priority Order

1. Owner
2. ACL user
3. Group
4. ACL group
5. Others
6. Mask restriction

---

# Production DevOps Use Cases

* Shared deployment directories
* Web servers writing logs
* Containers binding privileged ports
* Secure application privilege reduction

---

# Troubleshooting

User cannot access file but permission looks correct:

```
getfacl file
```

(mask blocking access)

App needs root for port 80:

```
setcap cap_net_bind_service=+ep binary
```

---

# 31 Backup & Restore (tar, rsync, snapshots, strategies)

---
## 31.1 Backup Concepts

Goals:

* Protect data from deletion/corruption
* Recover system quickly

Types:

| Type         | Meaning                   |
| ------------ | ------------------------- |
| Full         | entire data               |
| Incremental  | changes since last backup |
| Differential | changes since last full   |

3‑2‑1 Rule:
3 copies • 2 media • 1 offsite

---

## 31.2 tar Backups

Create archive:

```
tar -cvf backup.tar /etc
```

Compressed:

```
tar -czvf backup.tar.gz /etc
tar -cjvf backup.tar.bz2 /etc
tar -cJvf backup.tar.xz /etc
```

Extract:

```
tar -xvf backup.tar
tar -xzvf backup.tar.gz
```

List contents:

```
tar -tvf backup.tar
```

Exclude paths:

```
tar --exclude=/proc --exclude=/tmp -czvf system.tar.gz /
```

---

## 31.3 rsync Backups (Preferred)

Fast incremental sync

Local:

```
rsync -avh /data /backup/
```

Remote:

```
rsync -avz /data user@server:/backup/
```

Mirror (delete removed files):

```
rsync -av --delete /data /backup/
```

Dry run:

```
rsync -av --dry-run /data /backup/
```

---

## 31.4 cron Backups

Automate nightly backup:

```
0 2 * * * /usr/bin/rsync -az /var/www /backup/www >> /var/log/backup.log 2>&1
```

---

## 31.5 Snapshot Concept

Instant point‑in‑time copy (LVM/ZFS/Btrfs/Cloud)
Benefits:

* Very fast
* Consistent DB backups
* Easy rollback

LVM example:

```
lvcreate -L1G -s -n snap /dev/vg/data
```

---

## 31.6 /etc Backup (Critical)

Contains configuration

```
tar -czvf etc-backup-$(date +%F).tar.gz /etc
```

---

## 31.7 Restore Strategies

Single file:

```
tar -xvf backup.tar etc/nginx/nginx.conf
```

Full restore:

```
rsync -av /backup/ /
```

Disaster recovery order:

1. OS reinstall
2. Packages
3. Config (/etc)
4. Data (/var/lib, /home)
5. Services start

---

# Production Best Practices

* Test restore regularly
* Store offsite (S3/object storage)
* Encrypt backups
* Separate DB + file backups
* Monitor backup logs

---

# DevOps Use Cases

* Server migration
* Kubernetes persistent volume backup
* Database nightly backup
* Pre‑deployment snapshot

---

# 32 Linux Performance Tuning (CPU, Memory, IO, Limits, tuned)

---
## 32.1 CPU Tuning

Check usage:

```
top
mpstat -P ALL 1
```

Nice priority:

```
nice -n 10 process
renice -n -5 -p 1234
```

Lower nice = higher priority

CPU affinity:

```
taskset -c 0,1 ./app
```

---

## 32.2 I/O Tuning

Check IO:

```
iostat -xz 1
```

Change scheduler (temporary):

```
echo mq-deadline > /sys/block/sda/queue/scheduler
```

Read ahead:

```
blockdev --setra 4096 /dev/sda
```

---

## 32.3 vm.swappiness

Controls swap usage

View:

```
sysctl vm.swappiness
```

Recommended:

* DB servers → 1–10
* general → 60

Set temporary:

```
sysctl -w vm.swappiness=10
```

Persistent:

```
/etc/sysctl.d/99-tuning.conf
vm.swappiness=10
```

---

## 32.4 fs.file-max (open files limit)

```
sysctl fs.file-max
sysctl -w fs.file-max=1000000
```

---

## 32.5 ulimit (per-user limits)

Check:

```
ulimit -a
```

Temporary:

```
ulimit -n 65535
```

Persistent:

```
/etc/security/limits.conf
* soft nofile 65535
* hard nofile 65535
```

---

## 32.6 nice / renice (priority tuning)

Use for heavy background jobs

```
nice -n 19 backup.sh
```

---

## 32.7 tuned (auto optimization)

Install:

```
sudo apt install tuned
```

Profiles:

```
tuned-adm list
tuned-adm profile throughput-performance
```

---

# Production Scenarios

High load → check CPU steal
DB slow → reduce swappiness
Too many connections → increase file-max + ulimit
Slow disk → change scheduler

---

# DevOps Use Cases

* Kubernetes nodes optimization
* High traffic web servers
* Database performance tuning

---

# 33 Linux Troubleshooting (Real‑World Scenarios & Debugging Flow)

---
# Golden Rule

Never guess → Always verify using logs + metrics

Troubleshooting Order:

1. What changed?
2. Check logs
3. Check resources
4. Check network
5. Check configuration

---

## 33.1 Disk Full Issue

Symptoms:

* Cannot write file
* Services fail
* apt/yum errors

Check:

```
df -h
du -sh /* 2>/dev/null | sort -h
```

Common causes:

* logs filling /var/log
* docker images
* core dumps

Fix:

```
journalctl --vacuum-time=7d
docker system prune -a
rm old logs
```

---

## 33.2 High CPU Issue

Check process:

```
top
ps aux --sort=-%cpu | head
```

Per CPU:

```
mpstat -P ALL 1
```

Common causes:

* infinite loop
* heavy queries
* crypto mining malware

Fix:

```
kill -9 PID
renice +10 PID
```

---

## 33.3 High Memory Issue

Check memory:

```
free -h
vmstat 1
```

Find process:

```
ps aux --sort=-%mem | head
```

OOM killer logs:

```
dmesg | grep -i kill
```

---

## 33.4 Zombie Process

Check:

```
ps aux | grep Z
```

Fix: restart parent process

```
pstree -p
kill parentPID
```

---

## 33.5 Network Not Working

Check interface:

```
ip a
ip route
```

Connectivity:

```
ping 8.8.8.8
ping google.com
```

DNS issue if IP works but domain fails

```
cat /etc/resolv.conf
```

Ports:

```
ss -tulnp
```

---

## 33.6 SSH Login Failed

Verbose:

```
ssh -vvv user@host
```

Server logs:

```
journalctl -u ssh
cat /var/log/auth.log
```

Common causes:

* wrong permissions
* firewall blocked
* wrong key

---

## 33.7 Service Not Starting

Check status:

```
systemctl status nginx
journalctl -u nginx -xe
```

Common causes:

* port in use
* config error
* permission denied

Port check:

```
ss -tulnp | grep 80
```

---

## 33.8 Boot Failure

Check logs:

```
journalctl -xb
```

Filesystem:

```
fsck -fy /dev/sda1
```

Fix fstab issue:
comment bad mount in /etc/fstab

---

# Quick Diagnosis Table

| Symptom      | First Command     |
| ------------ | ----------------- |
| Server slow  | top               |
| Cannot login | journalctl -u ssh |
| Disk full    | df -h             |
| App down     | systemctl status  |
| Network down | ip a              |
| Reboot loop  | journalctl -xb    |

---

# Production Mindset

Logs > assumptions
Reproduce issue
Fix root cause not symptom
Document incident (postmortem)

---
