# 11 File Permissions & Ownership 

---
## 11.1 Permission Model

Each file has 3 permission groups:

1. User (owner)
2. Group
3. Others

Check permissions:

```
ls -l
```

Example:

```
-rwxr-xr-- 1 user dev 4096 file.txt
```

---

## 11.2 Read / Write / Execute

| Symbol | Meaning |
| ------ | ------- |
| r      | read    |
| w      | write   |
| x      | execute |

For files:
r → view contents
w → modify file
x → run program

For directories:
r → list files
w → create/delete files
x → enter directory (cd)

---

## 11.3 Numeric Permissions (Octal)

| Number | Permission |
| ------ | ---------- |
| 0      | ---        |
| 1      | --x        |
| 2      | -w-        |
| 3      | -wx        |
| 4      | r--        |
| 5      | r-x        |
| 6      | rw-        |
| 7      | rwx        |

Example:

```
chmod 755 script.sh
```

---

## 11.4 Symbolic Permissions

Add execute:

```
chmod u+x script.sh
```

Remove write:

```
chmod g-w file.txt
```

---

## 11.5 chmod — Change Permissions

```
chmod 644 file
chmod 755 script
chmod -R 755 dir
```

---

## 11.6 chown — Change Owner

```
sudo chown user file
sudo chown user:group file
sudo chown -R user:group dir
```

---

## 11.7 chgrp — Change Group

```
chgrp developers file
```

---

## 11.8 umask — Default Permissions

Check:

```
umask
```

Example umask 022:
Files → 644
Directories → 755

---

## 11.9 SUID (Set User ID)

Executable runs as file owner (usually root)

```
chmod u+s program
```

Example: passwd command

Security risk if misused.

---

## 11.10 SGID (Set Group ID)

Directory files inherit group ownership

```
chmod g+s shared_dir
```

Used in shared team directories

---

## 11.11 Sticky Bit

Only owner can delete files inside directory

```
chmod +t /shared
```

Example: /tmp

---

### Real Production Scenarios

Shared project folder:

```
chown -R :devteam /project
chmod 2775 /project
```

Secure private key:

```
chmod 600 id_rsa
```

Executable script:

```
chmod 755 deploy.sh
```

---

# 12 Links (Hard Links & Soft Links) 

---

## 12.1 What is a Link?

A link is another name (reference) pointing to a file’s data.
Linux supports two types:

1. Hard Link
2. Soft Link (Symbolic Link)

---

## 12.2 Inodes Concept (Foundation)

Every file has an inode number (metadata + pointer to data blocks).
Check inode:

```
ls -li file.txt
```

Hard links share SAME inode.
Soft links have DIFFERENT inode and point to path.

---

## 12.3 Hard Links

Create:

```
ln original.txt hardlink.txt
```

Characteristics:

* Same inode number
* No difference between original and link
* Works even if original filename deleted
* Cannot cross filesystems
* Cannot link directories (normally)

Example check:

```
ls -li original.txt hardlink.txt
```

Both inode numbers identical.

---

## 12.4 Soft Links (Symbolic Links)

Create:

```
ln -s original.txt symlink.txt
```

Characteristics:

* Different inode
* Stores file path
* Breaks if original removed (dangling link)
* Can cross filesystems
* Can link directories

Check:

```
ls -l
```

Shows -> pointer

---

## 12.5 Differences (Important for Interviews)

| Feature          | Hard Link   | Soft Link     |
| ---------------- | ----------- | ------------- |
| Inode            | Same        | Different     |
| Survives delete  | Yes         | No            |
| Cross filesystem | No          | Yes           |
| Directory link   | No          | Yes           |
| Size             | Actual file | Small pointer |

---

## 12.6 Real Production Usage

Current release deployment:

```
/var/www/app -> /var/www/releases/v5
```

Switch instantly by changing symlink.

Shared config file:

```
ln -s /etc/nginx/sites-available/app.conf /etc/nginx/sites-enabled/
```

---

## 12.7 Find Links

Find broken symlinks:

```
find / -xtype l
```

Find files with same inode:

```
find / -inum 12345
```

---

# 13 User & Group Management 

---
## 13.1 User Concept

Every person or service runs under a user account.
Types:

* root (UID 0) — superuser
* system users — services (nginx, mysql, docker)
* normal users — humans

Check current user:

```
whoami
id
```

---

## 13.2 Group Concept

Groups allow permission sharing among users.
A user can belong to multiple groups.

Check groups:

```
groups username
id username
```

---

## 13.3 useradd — Low Level User Creation

```
sudo useradd dev1
```

Does NOT create home directory by default (on many distros).

Create with home & bash:

```
sudo useradd -m -s /bin/bash dev1
```

---

## 13.4 adduser — Recommended (Interactive)

```
sudo adduser dev1
```

Creates home, password and configs automatically.

---

## 13.5 usermod — Modify User

Add to group:

```
sudo usermod -aG docker dev1
```

Change shell:

```
sudo usermod -s /bin/zsh dev1
```

Lock account:

```
sudo usermod -L dev1
```

---

## 13.6 userdel — Delete User

```
sudo userdel dev1
sudo userdel -r dev1   # remove home directory
```

---

## 13.7 groupadd

```
sudo groupadd developers
```

## 13.8 groupdel

```
sudo groupdel developers
```

## 13.9 groupmod

```
sudo groupmod -n devteam developers
```

---

## 13.10 passwd — Password Management

Set password:

```
sudo passwd dev1
```

Expire password:

```
sudo passwd -e dev1
```

Lock account:

```
sudo passwd -l dev1
```

---

## 13.11 Important System Files

/etc/passwd → user account info
/etc/shadow → encrypted passwords
/etc/group → group memberships

View safely:

```
cat /etc/passwd
sudo cat /etc/shadow
```

---

## 13.12 Switch User (su & sudo)

Switch user:

```
su - dev1
```

Run command as root:

```
sudo command
```

Sudo privileges configured in:

```
/etc/sudoers
```

Edit safely:

```
sudo visudo
```

---

### Real Production Scenarios

Create deployment user:

```
sudo adduser deploy
sudo usermod -aG docker deploy
```

Disable login but keep service:

```
sudo usermod -s /usr/sbin/nologin nginx
```

---

# 14 Package Management 

---
# 14.1 Package Concepts

Package = compiled software + metadata + dependencies + scripts
Repositories = trusted software sources

Common actions:

* install
* remove
* upgrade
* search
* verify

---

# Debian / Ubuntu Family (APT)

## 14.2 apt (Modern Command)

Update repository index:

```
sudo apt update
```

Upgrade packages:

```
sudo apt upgrade
```

Install package:

```
sudo apt install nginx
```

Remove package:

```
sudo apt remove nginx
sudo apt purge nginx
```

Search:

```
apt search docker
```

Show info:

```
apt show nginx
```

Autoremove unused deps:

```
sudo apt autoremove
```

---

## 14.3 apt-get (Legacy but used in scripts)

```
sudo apt-get update
sudo apt-get install curl
sudo apt-get remove curl
```

Preferred in automation because stable output.

---

# RedHat / Rocky / Alma / CentOS (DNF/YUM)

## 14.4 dnf (modern replacement of yum)

Install:

```
sudo dnf install httpd
```

Update:

```
sudo dnf update
```

Remove:

```
sudo dnf remove httpd
```

Search:

```
dnf search nginx
```

List installed:

```
dnf list installed
```

## 14.5 yum (older systems)

```
sudo yum install httpd
sudo yum update
```

---

## 14.6 rpm — Low Level Tool

Used for manual package files (.rpm)
No dependency resolution

Install local file:

```
sudo rpm -ivh pkg.rpm
```

Remove:

```
sudo rpm -e pkg
```

Verify:

```
rpm -qa | grep nginx
```

---

## 14.7 Repositories

List repos:
Debian:

```
cat /etc/apt/sources.list
ls /etc/apt/sources.list.d/
```

RedHat:

```
ls /etc/yum.repos.d/
```

Add repo (example pattern):

* import GPG key
* add repo file
* update cache

---

## 14.8 GPG Keys (Security)

Packages are signed to ensure authenticity.
Without key → install blocked.

Example:

```
sudo rpm --import key.gpg
sudo apt-key add key.gpg
```

---

### Real Production Scenarios

Install exact version:

```
sudo apt install nginx=1.18.*
```

Prevent upgrade:

```
sudo apt-mark hold nginx
```

Clean cache:

```
sudo apt clean
sudo dnf clean all
```

---

# 15 Process Management 

---
## 15.1 Process Lifecycle

States:
R → Running
S → Sleeping
D → Uninterruptible (I/O wait)
T → Stopped
Z → Zombie (dead but not cleaned)

Parent process creates child processes (fork/exec).
PID 1 = init/systemd (root of all processes)

---

## 15.2 PID — Process ID

Every process has unique PID.

Find PID:

```
pidof nginx
pgrep nginx
```

---

## 15.3 ps — Snapshot View

```
ps
ps aux
ps -ef
ps aux --sort=-%cpu | head
```

Fields:
USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND

---

## 15.4 top — Live Monitoring

```
top
```

Keys:
P → CPU sort
M → Memory sort
k → kill process
1 → per‑core CPU
q → quit

---

## 15.5 htop / atop — Advanced Monitors

```
sudo apt install htop
htop
```

Interactive process tree and kill menu.

---

## 15.6 kill — Send Signal

Graceful stop:

```
kill PID
```

Force kill:

```
kill -9 PID
```

Signals:
15 SIGTERM → safe stop
9 SIGKILL → immediate

---

## 15.7 killall & pkill

By name:

```
killall nginx
pkill nginx
pkill -f java
```

---

## 15.8 nice & renice — Priority

Lower value = higher priority

Start with priority:

```
nice -n 10 command
```

Change running process:

```
renice -n 5 -p PID
```

---

## 15.9 Background & Foreground Jobs

Run in background:

```
command &
```

Pause:
Ctrl+Z

Resume:

```
bg %1
fg %1
```

Run after logout:

```
nohup command &
```

---

## 15.10 pstree — Process Hierarchy

```
pstree -p
```

Shows parent‑child relationships

---

### Real Production Scenarios

Find high CPU process:

```
top
```

Kill stuck deployment:

```
pkill -f deploy.sh
```

Run long backup safely:

```
nohup tar -czf backup.tar.gz /data &
```

---

# 16 Disk & Storage Management 

---
## 16.1 Disk Concepts

Disk → Partition → Filesystem → Mount Point

Physical disk example:
/dev/sda
Partitions:
/dev/sda1
/dev/sda2

Linux does NOT use drive letters (C:, D:). Everything attaches into the directory tree.

---

## 16.2 lsblk — View Block Devices

```
lsblk
lsblk -f
```

Shows disks, partitions, filesystem and mount points.

---

## 16.3 df — Disk Usage (Mounted Filesystems)

```
df -h
df -i
```

-h → human readable
-i → inode usage (very important when disk not full but writes fail)

---

## 16.4 du — Directory Usage

```
du -sh *
du -sh /var/log/*
```

Used to locate large folders causing disk full.

---

## 16.5 Partitions

Two partition tables:
MBR (old, max 2TB)
GPT (modern, large disks)

---

## 16.6 fdisk — Partition Tool (Common)

List disks:

```
sudo fdisk -l
```

Create partition:

```
sudo fdisk /dev/sdb
n → new
w → write
```

---

## 16.7 parted — Advanced Partitioning (Large disks)

```
sudo parted /dev/sdb
mklabel gpt
mkpart primary ext4 0% 100%
quit
```

---

## 16.8 Filesystems

Common types:

| FS    | Usage         |
| ----- | ------------- |
| ext4  | default Linux |
| xfs   | large servers |
| btrfs | snapshots     |

Create filesystem:

```
sudo mkfs.ext4 /dev/sdb1
sudo mkfs.xfs /dev/sdb1
```

---

## 16.9 Mounting

Create mount directory:

```
sudo mkdir /data
```

Mount manually:

```
sudo mount /dev/sdb1 /data
```

Verify:

```
df -h
```

---

## 16.10 umount

```
sudo umount /data
```

If busy:

```
lsof +D /data
```

---

## 16.11 Persistent Mount (/etc/fstab)

Auto mount on boot.

Find UUID:

```
blkid
```

Add entry:

```
UUID=xxxx  /data  ext4  defaults  0 2
```

Test safely:

```
sudo mount -a
```

---

## 16.12 Swap (Important for Memory Pressure)

Create swap file:

```
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
```

Persist in fstab:

```
/swapfile none swap sw 0 0
```

---

### Real Production Scenarios

Disk full troubleshooting:

```
df -h
du -sh /*
du -sh /var/*
```

Check inode exhaustion:

```
df -i
```

Mount not appearing after reboot:
Check /etc/fstab syntax and run mount -a

---

# 17 Networking Basics

---
## 17.1 IP Address

An IP address uniquely identifies a device on a network.

IPv4 example:
192.168.1.10

Two parts:
Network ID + Host ID

Private ranges:
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16

Public IP → Internet reachable
Private IP → Internal network only

---

## 17.2 Subnet Mask

Defines network vs host portion.

Example:
IP: 192.168.1.10
Mask: 255.255.255.0 (/24)

Meaning:
Network = 192.168.1.0
Hosts = 1‑254
Broadcast = 192.168.1.255

CIDR notation:
/8 /16 /24 /32

---

## 17.3 Gateway

Router that connects your network to another network (usually Internet).

If gateway missing → internet won’t work but local network works.

---

## 17.4 DNS (Domain Name System)

Translates domain → IP

Example:
google.com → 142.250.x.x

If DNS fails:
ping 8.8.8.8 works
ping google.com fails

---

## 17.5 Ports

Ports identify services on a machine.

Common ports:
22 → SSH
80 → HTTP
443 → HTTPS
3306 → MySQL
5432 → PostgreSQL
8080 → Applications

IP = building
Port = room number

---

## 17.6 TCP vs UDP

TCP:
Reliable
Connection oriented
Used in SSH, HTTP, DB

UDP:
Fast
No guarantee
Used in DNS, streaming

---

### Troubleshooting Flow (Important)

1. Check IP assigned
2. Check gateway reachable
3. Check internet IP reachable
4. Check DNS resolution

---

# 18 Networking Commands & Troubleshooting 

---
## 18.1 Check IP & Interfaces

```
ip a
ip link
ifconfig   # legacy
```

Bring interface up/down:

```
sudo ip link set eth0 up
sudo ip link set eth0 down
```

---

## 18.2 Routing

```
ip route
route -n
```

Add temporary route:

```
sudo ip route add 10.0.0.0/24 via 192.168.1.1
```

---

## 18.3 Connectivity Tests

Ping host:

```
ping 8.8.8.8
ping google.com
```

Trace path:

```
traceroute google.com
```

HTTP test:

```
curl -I https://example.com
wget --spider https://example.com
```

---

## 18.4 DNS & Name Resolution

```
nslookup google.com
dig google.com
cat /etc/resolv.conf
cat /etc/hosts
```

---

## 18.5 Ports & Services

```
ss -tulnp
netstat -tulnp   # legacy
lsof -i :80
```

---

## 18.6 Remote Access & Transfer

```
ssh user@host
scp file user@host:/tmp
sftp user@host
telnet host 80
nc -zv host 22
```

---

## 18.7 Network Interface Management

```
nmcli device status
nmtui
ifup eth0
ifdown eth0
```

---

## 18.8 Security & Troubleshooting

Firewall:

```
sudo ufw status
sudo firewall-cmd --list-all
```

Packet capture:

```
sudo tcpdump -i eth0 port 80
```

Scan ports:

```
nmap localhost
```

ARP:

```
arp -a
ip neigh
```

---

## 18.9 Monitoring Bandwidth

```
iftop
nload
bmon
```

---

## 18.10 Host & Identity

```
hostname
hostnamectl
```

---

## 18.11 IPv6

```
ip -6 a
ip -6 route
```

---

### Real Troubleshooting Flow

1. ip a (IP assigned?)
2. ip route (gateway?)
3. ping gateway
4. ping 8.8.8.8
5. nslookup domain
6. curl service
7. ss -tulnp check port

---

# 19 Compression & Archiving 

---

## 19.1 tar — Archive Tool

Create archive:

```
tar -cvf archive.tar dir/
```

Extract:

```
tar -xvf archive.tar
```

List contents:

```
tar -tvf archive.tar
```

---

## 19.2 gzip / gunzip

Compress:

```
gzip file
```

Decompress:

```
gunzip file.gz
```

Keep original:

```
gzip -k file
```

---

## 19.3 tar + gzip (Most Common)

Create compressed archive:

```
tar -czvf backup.tar.gz /data
```

Extract:

```
tar -xzvf backup.tar.gz
```

---

## 19.4 bzip2 & xz (Higher Compression)

```
tar -cjvf backup.tar.bz2 dir
tar -xjvf backup.tar.bz2

tar -cJvf backup.tar.xz dir
tar -xJvf backup.tar.xz
```

---

## 19.5 zip / unzip (Cross‑platform)

```
zip -r files.zip dir
unzip files.zip
```

---

### Compression Comparison

Fast → gzip
Balanced → bzip2
Smallest → xz

---

### Real Production Usage

Backup logs:

```
tar -czf logs_$(date +%F).tar.gz /var/log
```

Transfer build artifacts:

```
tar -czf build.tar.gz build/
scp build.tar.gz server:/tmp
```

---

# 20 Searching & Text Processing 

Tools covered:
grep, egrep, fgrep, find, locate, awk, sed, cut, paste, sort, uniq, wc, tr

---
## 20.1 grep — Pattern Search

Basic search:

```
grep ERROR app.log
```

Ignore case:

```
grep -i error app.log
```

Show line numbers:

```
grep -n failed auth.log
```

Recursive:

```
grep -r "DB_HOST" /etc/
```

Invert match:

```
grep -v INFO app.log
```

---

## 20.2 egrep / fgrep

Extended regex:

```
egrep "error|fail|panic" app.log
```

Literal search (fast):

```
fgrep "127.0.0.1" access.log
```

(Modern equivalent: grep -E and grep -F)

---

## 20.3 find — File Search

```
find /var/log -name "*.log"
find / -size +100M
find . -mtime -1
```

Execute command:

```
find . -name "*.tmp" -delete
```

---

## 20.4 locate — Fast Search (database based)

```
locate nginx.conf
```

Update DB:

```
sudo updatedb
```

---

## 20.5 awk — Column Processing (VERY IMPORTANT)

Print column:

```
awk '{print $1}' file
```

Filter condition:

```
awk '$3 > 100 {print}' data.txt
```

Custom separator:

```
awk -F: '{print $1}' /etc/passwd
```

---

## 20.6 sed — Stream Editor

Replace text:

```
sed 's/http/https/' file
```

Replace globally:

```
sed -i 's/localhost/127.0.0.1/g' config.txt
```

Delete line:

```
sed '3d' file
```

---

## 20.7 cut — Extract Fields

```
cut -d: -f1 /etc/passwd
cut -c1-10 file
```

---

## 20.8 paste — Merge Files

```
paste file1 file2
```

---

## 20.9 sort & uniq

Sort:

```
sort file
```

Unique:

```
sort file | uniq
sort file | uniq -c | sort -nr
```

---

## 20.10 wc — Count

```
wc -l file
wc -w file
wc -c file
```

---

## 20.11 tr — Character Transform

Uppercase:

```
tr 'a-z' 'A-Z' < file
```

Remove spaces:

```
tr -d ' ' < file
```

---

### Real Log Analysis Example

Top IP hitting server:

```
awk '{print $1}' access.log | sort | uniq -c | sort -nr | head
```

Count errors today:

```
grep "$(date +%F)" app.log | grep ERROR | wc -l
```

---
