# Linux Documentation – Index Page

## 1. Basics
1.1 What is Linux?  
1.2 Linux Distributions (Ubuntu, CentOS, RHEL, Amazon Linux, etc.)  
1.3 Linux Directory Structure (`/`, `/home`, `/var`, `/etc`, `/tmp`, `/opt`, `/usr`)  
1.4 Terminal Basics  
1.5 Getting Help (`man`, `--help`, `info`)

---

## 2. File & Directory Management
2.1 Navigation: `pwd`, `ls`, `cd`  
2.2 Creating/Deleting: `touch`, `mkdir`, `rmdir`, `rm`  
2.3 Copy/Move/Rename: `cp`, `mv`  
2.4 Viewing Files: `cat`, `more`, `less`, `head`, `tail`  
2.5 Find & Search: `find`, `locate`, `which`, `whereis`  
2.6 Text Search: `grep`, `egrep`, `fgrep`

---

## 3. File Permissions & Ownership
3.1 Permission Types (r, w, x)  
3.2 Users, Groups, Others  
3.3 Change Permissions: `chmod`  
3.4 Change Ownership: `chown`, `chgrp`  
3.5 Special Permissions (SUID, SGID, Sticky Bit)

---

## 4. File Content & Editors
4.1 `nano` Editor Basics  
4.2 `vim`/`vi` Basics  
4.3 Redirection: `>`, `>>`, `<`  
4.4 Pipes: `|`  
4.5 `tee` Command

---

## 5. Users, Groups & Authentication
5.1 Add/Modify/Delete Users: `useradd`, `usermod`, `userdel`  
5.2 Add/Modify/Delete Groups: `groupadd`, `groupmod`, `groupdel`  
5.3 Switch User: `su`, `sudo`  
5.4 Password Management: `passwd`  
5.5 User Info Files: `/etc/passwd`, `/etc/shadow`, `/etc/group`

---

## 6. Process Management
6.1 View Processes: `ps`, `top`, `htop`  
6.2 Process Tree: `pstree`  
6.3 Kill Processes: `kill`, `killall`, `pkill`  
6.4 Job Control: `&`, `jobs`, `fg`, `bg`, `nohup`  
6.5 Priority: `nice`, `renice`

---

## 7. System Information & Monitoring
7.1 System Info: `uname`, `hostname`, `uptime`  
7.2 Hardware Info: `lscpu`, `lsblk`, `lspci`, `lsusb`, `df`, `du`  
7.3 Memory & CPU: `free`, `vmstat`, `iostat`, `sar`  
7.4 Logs Overview: `/var/log`

---

## 8. Disk, Partitions & File Systems
8.1 List Disks & Partitions: `lsblk`, `fdisk -l`, `blkid`  
8.2 Mount/Unmount: `mount`, `umount`  
8.3 File System Usage: `df`, `du`  
8.4 Disk Check & Repair: `fsck`  
8.5 Swap Management

---

## 9. Package Management (by Distro)
9.1 Debian/Ubuntu: `apt`, `apt-get`, `dpkg`  
9.2 RHEL/CentOS/Amazon Linux: `yum`, `dnf`, `rpm`  
9.3 Common Tasks: install, remove, update, upgrade, search

---

## 10. Networking
10.1 Check IP & Interfaces: `ip a`, `ifconfig`  
10.2 Routing: `ip route`, `route`  
10.3 Connectivity: `ping`, `traceroute`, `curl`, `wget`  
10.4 DNS: `nslookup`, `dig`, `/etc/hosts`, `/etc/resolv.conf`  
10.5 Ports & Services: `netstat`, `ss`, `lsof -i`  
10.6 SSH & SCP: `ssh`, `scp`, `sftp`

---

## 11. Services & Systemd
11.1 `systemd` Basics  
11.2 Manage Services: `systemctl start|stop|restart|status`  
11.3 Enable/Disable at Boot: `systemctl enable|disable`  
11.4 Logs: `journalctl`  
11.5 Legacy: `service`, `chkconfig` (old systems)

---

## 12. Scheduling & Automation
12.1 `cron` Jobs: `crontab -e`  
12.2 System-Wide Cron: `/etc/crontab`, `/etc/cron.*`  
12.3 `at` Command  
12.4 Simple Backups with `tar`, `rsync`

---

## 13. Compression & Archiving
13.1 `tar` Basics  
13.2 `gzip`, `gunzip`  
13.3 `zip`, `unzip`  
13.4 `bzip2`, `xz`

---

## 14. Shell Basics & Scripting
14.1 Shell Types (`bash`, `sh`, `zsh`)  
14.2 Environment Variables: `export`, `.bashrc`, `.bash_profile`  
14.3 Aliases: `alias`  
14.4 Basic Shell Script Structure (`#!/bin/bash`)  
14.5 Variables, Conditions (`if`), Loops (`for`, `while`)  
14.6 Functions in Shell Scripts  
14.7 Exit Codes (`$?`)

---

## 15. Security & Firewall
15.1 File Permissions Review  
15.2 SSH Hardening (`sshd_config`)  
15.3 Firewalls: `ufw`, `firewalld`, `iptables`  
15.4 SELinux (Basics only)

---

## 16. Logs & Troubleshooting
16.1 Important Log Files: `/var/log/messages`, `/var/log/syslog`, `/var/log/auth.log`  
16.2 Check Service Logs with `journalctl`  
16.3 Disk, Memory & CPU Issues  
16.4 Network Troubleshooting Steps

---

## 17. Linux for DevOps (Quick Link Section)
17.1 Linux Commands for Docker & Kubernetes  
17.2 Linux Commands for CI/CD Pipelines  
17.3 Linux on Cloud (AWS, GCP, Azure)  
17.4 Common Production Troubleshooting Commands

---

## 18. Cheat Sheets
18.1 Daily-use Commands  
18.2 Permission Cheat Sheet  
18.3 Networking Cheat Sheet  
18.4 `systemctl` Cheat Sheet  
18.5 Shell Script Patterns
