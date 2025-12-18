# Linux Documentation – Index Page (ONLY NUMBERING FIXED)
---
## 1. Linux Introduction Basic

1.1 What is Linux
1.2 Why Linux is Used
1.3 Linux vs Unix
1.4 Linux vs Windows
1.5 Open Source Concept
1.6 GPL License
1.7 Linux Use Cases (Server, Cloud, DevOps, Embedded)

---

## 2. Linux History & Evolution

2.1 History of Unix
2.2 Linus Torvalds
2.3 Linux Kernel Evolution
2.4 Community & Distributions

---

## 3. Linux Architecture

3.1 Hardware Layer
3.2 Kernel
3.3 Shell
3.4 System Libraries
3.5 User Space
3.6 Applications
3.7 Kernel Space vs User Space

---

## 4. Linux Distributions

4.1 Debian Family

* Ubuntu
* Debian

4.2 RedHat Family

* RHEL
* CentOS
* Rocky Linux
* AlmaLinux

4.3 SUSE Family
4.4 Arch Linux
4.5 Amazon Linux
4.6 Alpine Linux
4.7 Choosing Right Distro

---

## 5. Linux File System Hierarchy (FHS)

/
├── bin
├── boot
├── dev
├── etc
├── home
├── lib
├── media
├── mnt
├── opt
├── proc
├── root
├── run
├── sbin
├── srv
├── sys
├── tmp
├── usr
└── var

---

## 6. Terminal & Shell

6.1 Terminal vs Console
6.2 Shell Definition
6.3 Types of Shells

* bash
* sh
* zsh
* fish
* csh

6.4 Shell Configuration Files

* .bashrc
* .bash_profile
* .profile

6.5 Login vs Non-login Shell
6.6 Interactive vs Non-interactive Shell
6.7 Default Shell

* echo $SHELL
* chsh
* /etc/shells

6.8 Shell Prompt (PS1)
6.9 Command Structure
6.10 Command Execution Order
6.11 Alias & Unalias
6.12 History & Shortcuts
6.13 Job Control
6.14 Shell Built-ins
6.15 Environment Awareness

---

## 7. Help & Documentation

7.1 `man`
7.2 `--help`
7.3 `info`
7.4 `/usr/share/doc`

---

## 8. File & Directory Management — Index

### 8.1 Navigation

* `pwd`
* `ls`
* `cd`

### 8.2 Creating & Deleting

* `touch`
* `mkdir`
* `rmdir`
* `rm`

### 8.3 Copy, Move & Rename

* `cp`
* `mv`

### 8.4 File Information & Structure

* `tree`
* `stat`
* `file`

### 8.5 Find & Search

* `which`
* `whereis`


## 9. File Viewing & Editing — Index

### 9.1 File Viewing

* `cat`
* `less`
* `more`
* `head`
* `tail`
* `watch`

### 9.2 File Editing

* `nano`
* `vi`
* `vim`

---

## 10. Input / Output Redirection & Pipes — Index

### 10.1 Redirection

* `>`
* `>>`
* `<`

### 10.2 Pipes

* `|`

### 10.3 `tee` Command

* `tee`

---

## 11. File Permissions & Ownership

11.1 Permission Model
11.2 Read / Write / Execute
11.3 Numeric Permissions
11.4 Symbolic Permissions
11.5 `chmod`
11.6 `chown`
11.7 `chgrp`
11.8 `umask`
11.9 SUID
11.10 SGID
11.11 Sticky Bit

---

## 12. Links

12.1 Hard Links
12.2 Soft Links (Symbolic)
12.3 `ln`

---

## 13. User & Group Management

13.1 User Concept
13.2 Group Concept
13.3 `useradd`
13.4 `adduser`
13.5 `usermod`
13.6 `userdel`
13.7 `groupadd`
13.8 `groupdel`
13.9 `groupmod`
13.10 `passwd`
13.11 `/etc/passwd`
13.12 `/etc/shadow`
13.13 `/etc/group`
13.14 Switch User: su, sudo

---

## 14. Package Management

14.1 Package Concepts
14.2 `apt`
14.3 `apt-get`
14.4 `yum`
14.5 `dnf`
14.6 `rpm`
14.7 Repositories
14.8 GPG Keys

---

## 15. Process Management

15.1 Process Lifecycle
15.2 PID
15.3 `ps`
15.4 `top`
15.5 `htop`
15.6 `atop`
15.7 `kill`
15.8 `killall`
15.9 `pkill`
15.10 `nice`
15.11 `renice`
15.12 jobs ,nohup &
15.13 `bg` / `fg`
15.14 `pstree`

---

## 16. Disk & Storage Management

16.1 Disk Concepts
16.2 `lsblk`
16.3 `df`
16.4 `du`
16.5 Partitions
16.6 `fdisk` -l
16.7 `parted`
16.8 File Systems

* ext4
* xfs
* btrfs

16.9 Mounting
16.10 `mount`
16.11 `umount`
16.12 `/etc/fstab`

---

## 17. Networking Basics

17.1 IP Address
17.2 Subnet
17.3 Gateway
17.4 DNS
17.5 Ports
17.6 TCP vs UDP

---

## 18. Networking

18.1 Check IP & Network Interfaces

* ip a
* ifconfig
* ip link

18.2 Routing

* ip route
* route

18.3 Connectivity & Data Transfer

* ping
* traceroute
* curl
* wget

18.4 DNS & Name Resolution

* nslookup
* dig
* /etc/hosts
* /etc/resolv.conf

18.5 Ports, Sockets & Services

* netstat
* ss
* lsof -i

18.6 Remote Access & File Transfer

* ssh
* scp
* sftp
* telnet
* nc

18.7 Network Interface Management

* nmcli
* nmtui
* ifup
* ifdown

18.8 Network Security & Troubleshooting

* iptables
* firewalld
* ufw
* tcpdump
* nmap
* arp
* arping
* ip neigh

18.9 Network Monitoring

* iftop
* nload
* bmon

18.10 Host & Identity

* hostname
* hostnamectl

18.11 IPv6

* ip -6 a
* ip -6 route

---

## 19. Compression & Archiving

19.1 `tar`
19.2 `gzip`
19.3 `gunzip`
19.4 `bzip2`, `xz`
19.5 `zip`
19.6 `unzip`

---

## 20. Searching & Text Processing

20.1 `grep`
20.2 `egrep`
20.3 `fgrep`
20.4 `find`
20.5 `locate`
20.6 `awk`
20.7 `sed`
20.8 `cut`
20.9 `paste`
20.10 `sort`
20.11 `uniq`
20.12 `wc`
20.13 `tr`

---

## 21. Environment Variables

21.1 Local vs Global Variables
21.2 `env`
21.3 `printenv`
21.4 `export`
21.5 `echo $VAR`
21.6 `set`
21.7 `unset`
21.8 PATH variable
21.9 .bashrc
21.10 .profile
21.11 .bash_profile
21.12 .bash_login
21.13 /etc/environment
21.14 /etc/profile
21.15 /etc/profile.d/*.sh
21.16 Command-level variables
21.17 SHELL variable

---

## 22. Scheduling & Automation

22.1 cron
22.2 crontab
22.3 at
22.4 atq
22.5 atrm
22.6 batch
22.7 watch
22.8 /etc/crontab
22.9 /etc/cron.hourly
22.10 /etc/cron.daily
22.11 /etc/cron.weekly
22.12 /etc/cron.monthly
22.13 /etc/cron.allow
22.14 /etc/cron.deny
22.15 /etc/at.allow
22.16 /etc/at.deny
22.17 cron service (systemctl)
22.18 cron logs

---

## 23. System Monitoring

23.1 CPU Monitoring
23.2 Memory Monitoring
23.3 Disk Monitoring
23.4 Process Monitoring
23.5 Network Monitoring
23.6 System Load & Uptime
23.7 Performance Statistics

---

## 24. Logging & Journals

24.1 Log Files
24.2 /var/log
24.3 Common Log Files
24.4 rsyslog
24.5 journalctl
24.6 journald
24.7 Log Levels
24.8 logger
24.9 Log Rotation
24.10 logrotate
24.11 /etc/logrotate.conf
24.12 /etc/logrotate.d/
24.13 Persistent Journals

---

## 25. Services & systemd

25.1 systemd Architecture
25.2 systemctl
25.3 Service Files
25.4 Unit File Types
25.5 Unit File Locations
25.6 Start / Stop / Restart
25.7 Enable / Disable
25.8 Status & Listing
25.9 Reload & Reexec
25.10 Targets
25.11 systemd Timers

---

## 26. SSH & Remote Access

26.1 SSH Basics
26.2 Password Authentication
26.3 Key Authentication
26.4 SSH Commands
26.5 SSH Server
26.6 SSH Configuration
26.7 Key Management
26.8 Security Hardening
26.9 Port Forwarding & Tunneling
26.10 Debugging
26.11 rsync over SSH

---

## 27. Linux Security

27.1 Linux Security Model
27.2 Firewall Concepts
27.3 ufw
27.4 firewalld
27.5 SELinux
27.6 AppArmor
27.7 Fail2ban

---

## 28. Boot Troubleshooting & Recovery

28.1 Single User Mode
28.2 Rescue Mode
28.3 Emergency Mode
28.4 GRUB Commands
28.5 Reset Root Password
28.6 fsck in Recovery
28.7 Initramfs Rebuild
28.8 Boot Logs

---

## 29. Kernel Management

29.1 Kernel Version
29.2 uname -a
29.3 lsmod
29.4 modprobe
29.5 modinfo
29.6 rmmod
29.7 sysctl
29.8 /proc/sys
29.9 Kernel Parameters

---

## 30. Advanced Permissions & ACL

30.1 ACL Concept
30.2 getfacl
30.3 setfacl
30.4 Default ACL
30.5 Capabilities
30.6 getcap
30.7 setcap

---

## 31. Backup & Restore

31.1 tar backups
31.2 rsync backups
31.3 cron backups
31.4 snapshot concept
31.5 /etc backup
31.6 restore strategies

---

## 32. Linux Performance Tuning

32.1 CPU tuning
32.2 I/O tuning
32.3 vm.swappiness
32.4 fs.file-max
32.5 ulimit
32.6 nice / renice
32.7 tuned

---

## 33. Linux Troubleshooting

33.1 Disk Full Issue
33.2 High CPU Issue
33.3 High Memory Issue
33.4 Zombie Process
33.5 Network Not Working
33.6 SSH Login Failed
33.7 Service Not Starting
33.8 Boot Failure

---
