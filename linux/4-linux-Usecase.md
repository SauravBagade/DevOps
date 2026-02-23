# 👥 Linux User & Group Management

---

# 📌 1️⃣ User Concept

## 🔹 What is a User in Linux?

A **user** is an account that allows a person or service to log in and access system resources.

Linux is a **multi-user operating system**.

### 🔹 Types of Users

| Type          | UID Range      | Purpose                 |
| ------------- | -------------- | ----------------------- |
| Root User     | 0              | Super Administrator     |
| System Users  | 1–999 (varies) | Services (nginx, mysql) |
| Regular Users | 1000+          | Human users             |

---

## 🔹 Root User

* Username: `root`
* UID: `0`
* Full control over system

⚠ Never use root directly in production. Use `sudo`.

---

## 🔹 User Identification Fields

Each user has:

* Username
* UID (User ID)
* GID (Primary Group ID)
* Home Directory
* Default Shell

---

# 📌 2️⃣ Group Concept

## 🔹 What is a Group?

A group is a collection of users.

Used to:

* Manage permissions
* Control access
* Simplify administration

### 🔹 Types of Groups

| Type            | Description                   |
| --------------- | ----------------------------- |
| Primary Group   | Assigned during user creation |
| Secondary Group | Additional groups             |

---

# 📌 3️⃣ useradd (Low-Level Command)

Used in scripting and automation.

### 🔹 Syntax

```bash
useradd [options] username
```

### 🔹 Important Options

| Option | Meaning               |
| ------ | --------------------- |
| -m     | Create home directory |
| -d     | Custom home directory |
| -s     | Default shell         |
| -u     | Custom UID            |
| -g     | Primary group         |
| -G     | Secondary groups      |
| -c     | Comment (Full name)   |

---

### 🔹 Example

```bash
useradd -m -s /bin/bash -c "DevOps User" devuser
```

Check:

```bash
id devuser
```

---

# 📌 4️⃣ adduser (Interactive Command)

High-level wrapper around `useradd`.

More user-friendly.

```bash
adduser devuser
```

It will:

* Create home directory
* Ask password
* Create group
* Setup defaults

✔ Recommended for beginners
✔ Used in Debian/Ubuntu

---

# 📌 5️⃣ usermod (Modify User)

### 🔹 Change Username

```bash
usermod -l newname oldname
```

### 🔹 Change Home Directory

```bash
usermod -d /new/home -m username
```

### 🔹 Add to Secondary Group

```bash
usermod -aG docker username
```

⚠ Always use `-a` with `-G` or existing groups will be removed.

---

# 📌 6️⃣ userdel (Delete User)

```bash
userdel username
```

Remove with home directory:

```bash
userdel -r username
```

Production Tip:
Always backup home directory before deletion.

---

# 📌 7️⃣ groupadd

```bash
groupadd developers
```

Custom GID:

```bash
groupadd -g 1050 devops
```

---

# 📌 8️⃣ groupdel

```bash
groupdel developers
```

---

# 📌 9️⃣ groupmod

Rename group:

```bash
groupmod -n newgroup oldgroup
```

Change GID:

```bash
groupmod -g 1100 devops
```

---

# 📌 🔟 passwd Command

Set password:

```bash
passwd username
```

Lock user:

```bash
passwd -l username
```

Unlock:

```bash
passwd -u username
```

Expire password:

```bash
passwd -e username
```

Check status:

```bash
passwd -S username
```

---

# 📌 11️⃣ /etc/passwd

File storing user information.

```bash
cat /etc/passwd
```

Format:

```
username:x:UID:GID:comment:home:shell
```

Example:

```
devuser:x:1001:1001:DevOps User:/home/devuser:/bin/bash
```

---

# 📌 12️⃣ /etc/shadow

Stores encrypted passwords.

```bash
sudo cat /etc/shadow
```

Format:

```
username:encrypted_password:last_change:min:max:warn:inactive:expire
```

Only root can read.

---

# 📌 13️⃣ /etc/group

Stores group info.

```bash
cat /etc/group
```

Format:

```
groupname:x:GID:user1,user2
```

---

# 📌 14️⃣ Switch User

## 🔹 su (Switch User)

Switch to root:

```bash
su -
```

Switch to another user:

```bash
su - devuser
```

Requires password of target user.

---

## 🔹 sudo (Super User Do)

Run command as root:

```bash
sudo apt update
```

Grant sudo access:

```bash
usermod -aG sudo devuser
```

Sudo config file:

```bash
/etc/sudoers
```

Edit safely:

```bash
visudo
```

---

# 🔥 REAL PRODUCTION USE CASE (Step-by-Step)

## 🎯 Scenario

You are DevOps Engineer in a company.

You must:

* Create new employee account
* Assign groups
* Give limited sudo access
* Setup secure permissions
* Remove employee safely

---

## 🧩 Step 1: Create Groups

```bash
groupadd developers
groupadd docker
```

---

## 🧩 Step 2: Create User

```bash
useradd -m -s /bin/bash -G developers,docker john
passwd john
```

---

## 🧩 Step 3: Verify

```bash
id john
```

---

## 🧩 Step 4: Give Sudo Access (Limited)

Edit sudoers:

```bash
visudo
```

Add:

```
john ALL=(ALL) /usr/bin/systemctl restart nginx
```

Now john can only restart nginx.

---

## 🧩 Step 5: Secure Home Directory

```bash
chmod 700 /home/john
```

---

## 🧩 Step 6: Lock User (Temporary Leave)

```bash
passwd -l john
```

---

## 🧩 Step 7: Delete User (Employee Resigned)

```bash
tar -czvf john_backup.tar.gz /home/john
userdel -r john
```

---

# 🏭 Advanced Production Concepts

## 🔹 Password Policies

Check:

```bash
chage -l username
```

Set expiry:

```bash
chage -M 90 username
```

---

## 🔹 Disable Login Shell

```bash
usermod -s /sbin/nologin username
```

Used for service accounts.

---

## 🔹 Bulk User Creation (Automation)

```bash
for user in dev1 dev2 dev3
do
  useradd -m $user
done
```

---
# 🔐 Linux File Permissions & Ownership
---

# 📌 1️⃣ Permission Model (Linux Security Foundation)

Linux uses a **three-layer permission model**:

```
[ User ]  [ Group ]  [ Others ]
```

Each file/directory has:

* **Owner (User)**
* **Group**
* **Others (Everyone else)**

---

## 🔎 View Permissions

```bash
ls -l
```

Example:

```
-rwxr-xr-- 1 john developers 4096 Feb 22 script.sh
```

Breakdown:

| Part | Meaning            |
| ---- | ------------------ |
| -    | File type          |
| rwx  | Owner permissions  |
| r-x  | Group permissions  |
| r--  | Others permissions |

---

## 🔹 File Types

| Symbol | Type             |
| ------ | ---------------- |
| -      | Regular file     |
| d      | Directory        |
| l      | Symbolic link    |
| c      | Character device |
| b      | Block device     |

---

# 📌 2️⃣ Read / Write / Execute

| Permission | Symbol | Meaning (File) | Meaning (Directory) |
| ---------- | ------ | -------------- | ------------------- |
| Read       | r      | View content   | List files          |
| Write      | w      | Modify content | Create/delete files |
| Execute    | x      | Run file       | Enter directory     |

---

### 🔹 Directory Example

If directory has:

```
drwxr-x---
```

* Owner → Full access
* Group → Can enter and list
* Others → No access

---

# 📌 3️⃣ Numeric Permissions (Octal Method)

Each permission has a numeric value:

| Permission | Value |
| ---------- | ----- |
| Read       | 4     |
| Write      | 2     |
| Execute    | 1     |

Add values:

| Permission | Number |
| ---------- | ------ |
| rwx        | 7      |
| rw-        | 6      |
| r-x        | 5      |
| r--        | 4      |

---

## 🔹 Example

```bash
chmod 755 script.sh
```

Meaning:

```
Owner → 7 → rwx
Group → 5 → r-x
Others → 5 → r-x
```

---

# 📌 4️⃣ Symbolic Permissions

Format:

```
chmod [who][operator][permission] file
```

| Who | Meaning |
| --- | ------- |
| u   | User    |
| g   | Group   |
| o   | Others  |
| a   | All     |

| Operator | Meaning     |
| -------- | ----------- |
| +        | Add         |
| -        | Remove      |
| =        | Set exactly |

---

## 🔹 Examples

```bash
chmod u+x script.sh
chmod g-w file.txt
chmod o=r file.txt
chmod a+r file.txt
```

---

# 📌 5️⃣ chmod (Change Mode)

### 🔹 Basic

```bash
chmod 644 file.txt
```

### 🔹 Recursive

```bash
chmod -R 755 project/
```

⚠ Use recursive carefully in production.

---

# 📌 6️⃣ chown (Change Owner)

### 🔹 Syntax

```bash
chown user file
chown user:group file
```

---

### 🔹 Example

```bash
chown john script.sh
chown john:developers script.sh
```

---

### 🔹 Recursive

```bash
chown -R john:developers project/
```

---

# 📌 7️⃣ chgrp (Change Group)

```bash
chgrp developers file.txt
```

Recursive:

```bash
chgrp -R developers project/
```

---

# 📌 8️⃣ umask (Default Permission Control)

## 🔹 What is umask?

Controls default permission when creating files.

---

### 🔹 Default Creation

| Type      | Default Before umask |
| --------- | -------------------- |
| File      | 666                  |
| Directory | 777                  |

---

### 🔹 Example

If umask = 022

```
File → 666 - 022 = 644
Directory → 777 - 022 = 755
```

Check:

```bash
umask
```

Set:

```bash
umask 027
```

Persistent location:

```
/etc/profile
~/.bashrc
```

---

# 📌 9️⃣ SUID (Set User ID)

When set on executable:

* File runs as owner
* Even if another user executes

---

## 🔹 Identify

```
-rwsr-xr-x
```

Notice `s` instead of `x`

---

## 🔹 Set SUID

```bash
chmod u+s file
chmod 4755 file
```

---

## 🔹 Example

```bash
ls -l /usr/bin/passwd
```

Password change works because of SUID.

---

# 📌 🔟 SGID (Set Group ID)

### 🔹 On File

Runs as group owner.

### 🔹 On Directory

Files created inherit directory group.

---

## 🔹 Identify

```
drwxr-sr-x
```

---

## 🔹 Set SGID

```bash
chmod g+s folder
chmod 2755 folder
```

---

# 📌 11️⃣ Sticky Bit

Used on shared directories.

Prevents users from deleting others' files.

---

## 🔹 Identify

```
drwxrwxrwt
```

`t` indicates sticky bit.

---

## 🔹 Set Sticky Bit

```bash
chmod +t folder
chmod 1777 folder
```

---

## 🔹 Real Example

```
/tmp
```

Check:

```bash
ls -ld /tmp
```

---

# 🔥 REAL PRODUCTION USE CASE (Step-by-Step)

---

## 🧩 Step 1: Create Group

```bash
groupadd devteam
```

---

## 🧩 Step 2: Create Users

```bash
useradd -m -G devteam dev1
useradd -m -G devteam dev2
```

---

## 🧩 Step 3: Create Project Directory

```bash
mkdir /project
chown root:devteam /project
chmod 2775 /project
```

Explanation:

* 2 → SGID
* 775 → rwxrwxr-x

Now:
✔ Group ownership inherited
✔ Team collaboration enabled

---

## 🧩 Step 4: Protect Sensitive File

```bash
touch /project/config.yml
chmod 640 /project/config.yml
```

Meaning:

* Owner → read/write
* Group → read
* Others → no access

---

## 🧩 Step 5: Prevent Deletion in Shared Folder

```bash
mkdir /project/shared
chmod 1777 /project/shared
```

Sticky bit applied.

---

## 🧩 Step 6: Secure Script with SUID (Careful!)

```bash
chmod 4750 secure_script.sh
```

⚠ Only use SUID when absolutely required.

---
# 🔗 Linux Hard Links & Soft Links (Symbolic Links)

---

# 📌 1️⃣ Hard Links

## 🔹 What is a Hard Link?

A **hard link** is another name (reference) to the **same inode** of a file.

👉 Both files point to the same data on disk.

---

## 🔎 Understanding Inode

Linux stores:

* File Name → Points to → **Inode**
* Inode → Points to → Actual Data Blocks

Check inode:

```bash
ls -li file.txt
```

Example output:

```
123456 -rw-r--r-- 2 user user 100 Feb 22 file.txt
```

`123456` → inode number
`2` → link count

---

## 🔹 Create Hard Link

```bash
ln original.txt hardlink.txt
```

Verify:

```bash
ls -li original.txt hardlink.txt
```

✔ Same inode
✔ Same link count

---

## 🔹 Key Characteristics

| Feature                     | Hard Link                |
| --------------------------- | ------------------------ |
| Same inode?                 | Yes                      |
| Cross filesystem?           | ❌ No                     |
| Link to directory?          | ❌ Not allowed (normally) |
| Survives original deletion? | ✔ Yes                    |

---

## 🔥 Example

```bash
echo "DevOps" > file1.txt
ln file1.txt file2.txt
```

Delete original:

```bash
rm file1.txt
cat file2.txt
```

✔ File still exists because inode still referenced.

---

# 📌 2️⃣ Soft Links (Symbolic Links)

## 🔹 What is a Symbolic Link?

A **symbolic link** is a shortcut pointing to another file.

👉 Like Windows shortcut.

---

## 🔹 Create Soft Link

```bash
ln -s original.txt symlink.txt
```

Check:

```bash
ls -l
```

Output:

```
lrwxrwxrwx 1 user user 12 Feb 22 symlink.txt -> original.txt
```

`l` → symbolic link

---

## 🔹 Key Characteristics

| Feature                     | Soft Link          |
| --------------------------- | ------------------ |
| Same inode?                 | ❌ No               |
| Cross filesystem?           | ✔ Yes              |
| Link to directory?          | ✔ Yes              |
| Survives original deletion? | ❌ No (broken link) |

---

## 🔥 Example

```bash
echo "Linux" > fileA.txt
ln -s fileA.txt fileB.txt
```

Delete original:

```bash
rm fileA.txt
cat fileB.txt
```

❌ Broken link

---

# 📌 3️⃣ ln Command (Create Links)

## 🔹 Syntax

```bash
ln [options] source target
```

---

## 🔹 Common Options

| Option | Meaning              |
| ------ | -------------------- |
| -s     | Create symbolic link |
| -f     | Force overwrite      |
| -i     | Interactive          |
| -v     | Verbose              |

---

## 🔹 Examples

Hard link:

```bash
ln file1.txt file2.txt
```

Soft link:

```bash
ln -s /var/log/nginx/access.log access.log
```

Force overwrite:

```bash
ln -sf newfile.txt link.txt
```

---

# 🧠 Hard vs Soft Link (Interview Table)

| Feature      | Hard Link           | Soft Link             |
| ------------ | ------------------- | --------------------- |
| Inode        | Same                | Different             |
| File Type    | Regular             | Special file (l)      |
| Cross FS     | No                  | Yes                   |
| Directory    | No                  | Yes                   |
| Broken Link  | No                  | Yes                   |
| Data removal | When link count = 0 | When original removed |

---

# 🔍 Deep Technical Understanding

## 🔹 Link Count

Check:

```bash
ls -li file.txt
```

If link count = 3
Means → 3 filenames reference same inode.

File deleted only when link count = 0.

---

## 🔹 Why Hard Link Cannot Cross Filesystem?

Because inode numbers are unique only inside a filesystem.

---

# 🔥 REAL PRODUCTION USE CASE (Step-by-Step)

---

# 🎯 Scenario 1: Application Log Management

You are DevOps Engineer.

Requirement:

* Application writes logs in `/opt/app/logs/app.log`
* Central log collector reads `/var/log/app.log`
* Avoid duplicate files

---

## 🧩 Step 1: Create Hard Link (Same Filesystem)

```bash
ln /opt/app/logs/app.log /var/log/app.log
```

✔ Same data
✔ No duplication
✔ Efficient

---

# 🎯 Scenario 2: Version Deployment (Blue-Green Deployment)

Production directory:

```
/var/www/app_v1
/var/www/app_v2
```

Active app:

```
/var/www/current
```

---

## 🧩 Step 1: Create Symlink

```bash
ln -s /var/www/app_v1 /var/www/current
```

---

## 🧩 Step 2: Switch Version Instantly

```bash
ln -sfn /var/www/app_v2 /var/www/current
```

✔ Zero downtime
✔ Instant rollback possible

Rollback:

```bash
ln -sfn /var/www/app_v1 /var/www/current
```

---

# 🎯 Scenario 3: Shared Storage Optimization

Multiple users need same large ISO file.

Instead of copying:

```bash
ln bigfile.iso user1.iso
ln bigfile.iso user2.iso
```

✔ Saves disk space
✔ Same inode

---

# 🎯 Scenario 4: Docker & Kubernetes

Inside containers:

* `/var/run` often symlinked
* `/etc/alternatives` uses symlinks

Example:

```bash
ls -l /etc/alternatives
```

Used to switch Java versions safely.

---

# 🔐 Security Considerations

✔ Avoid hard links in shared writable directories
✔ Monitor symlink attacks
✔ Use `nosuid` mount option
✔ Validate symlink paths in scripts

Check broken links:

```bash
find / -xtype l
```

---

# 🏭 Advanced Concepts

## 🔹 Remove Link

Hard link:

```bash
rm file2.txt
```

Soft link:

```bash
rm symlink.txt
```

Only link removed — not original.

---

## 🔹 Find All Hard Links of File

```bash
find / -samefile file.txt 2>/dev/null
```

---

## 🔹 Readlink

Show target:

```bash
readlink symlink.txt
```

---
# ⚙️ Linux Process Management
---

# 📌 1️⃣ Process Lifecycle

## 🔹 What is a Process?

A **process** is a running instance of a program.

Example:

```bash
firefox
nginx
java
```

---

## 🔄 Process Lifecycle States

```
New → Ready → Running → Waiting → Terminated
```

In Linux, common states:

| State      | Code | Meaning                   |
| ---------- | ---- | ------------------------- |
| Running    | R    | Executing on CPU          |
| Sleeping   | S    | Waiting for resource      |
| Disk Sleep | D    | Waiting for I/O           |
| Stopped    | T    | Suspended                 |
| Zombie     | Z    | Completed but not cleaned |

---

## 🔹 Zombie Process

* Process finished execution
* Parent didn’t read exit status
* Appears as `Z`

Check:

```bash
ps aux | grep Z
```

---

# 📌 2️⃣ PID (Process ID)

Each process has a unique **PID**.

Check current shell PID:

```bash
echo $$
```

Check parent PID:

```bash
echo $PPID
```

---

## 🔹 Important PIDs

| PID   | Meaning        |
| ----- | -------------- |
| 1     | init/systemd   |
| 0     | Scheduler      |
| >1000 | User processes |

Check PID 1:

```bash
ps -p 1
```

---

# 📌 3️⃣ ps (Process Status)

Displays snapshot of running processes.

---

## 🔹 Common Usage

```bash
ps
ps -e
ps -ef
ps aux
```

Most used in production:

```bash
ps aux | grep nginx
```

Columns:

| Column  | Meaning          |
| ------- | ---------------- |
| USER    | Owner            |
| PID     | Process ID       |
| %CPU    | CPU usage        |
| %MEM    | Memory usage     |
| STAT    | State            |
| COMMAND | Executed command |

---

# 📌 4️⃣ top

Real-time process monitoring.

```bash
top
```

Displays:

* CPU usage
* Memory usage
* Load average
* Running processes

---

## 🔹 Useful Shortcuts in top

| Key | Action         |
| --- | -------------- |
| P   | Sort by CPU    |
| M   | Sort by Memory |
| k   | Kill process   |
| q   | Quit           |

---

# 📌 5️⃣ htop

Enhanced version of top (colorful UI).

Install:

```bash
sudo apt install htop
```

Run:

```bash
htop
```

Features:
✔ Mouse support
✔ Tree view
✔ Easy kill

---

# 📌 6️⃣ atop

Advanced monitoring tool.

Install:

```bash
sudo apt install atop
```

Run:

```bash
atop
```

Used in production for:

* Historical performance logs
* CPU, Memory, Disk analysis

---

# 📌 7️⃣ kill

Terminates process by PID.

---

## 🔹 Syntax

```bash
kill PID
```

---

## 🔹 Common Signals

| Signal  | Number | Meaning       |
| ------- | ------ | ------------- |
| SIGTERM | 15     | Graceful stop |
| SIGKILL | 9      | Force kill    |
| SIGHUP  | 1      | Restart       |
| SIGSTOP | 19     | Pause         |

Example:

```bash
kill -15 1234
kill -9 1234
```

⚠ Always try `-15` before `-9`

---

# 📌 8️⃣ killall

Kill by process name.

```bash
killall nginx
```

---

# 📌 9️⃣ pkill

Kill by pattern.

```bash
pkill -f java
```

Useful in automation scripts.

---

# 📌 🔟 nice

Sets process priority (niceness).

Range:

```
-20 (highest priority)
19 (lowest priority)
```

Start process with priority:

```bash
nice -n 10 python script.py
```

---

# 📌 11️⃣ renice

Change priority of running process.

```bash
renice 5 -p 1234
```

---

# 📌 12️⃣ jobs, nohup &

## 🔹 Background Process (&)

```bash
sleep 100 &
```

---

## 🔹 jobs

```bash
jobs
```

Shows background jobs.

---

## 🔹 nohup (Run After Logout)

```bash
nohup python app.py &
```

Output saved in `nohup.out`

Used in production when SSH disconnects.

---

# 📌 13️⃣ bg / fg

Bring job to background:

```bash
bg %1
```

Bring job to foreground:

```bash
fg %1
```

Stop running job:

Press:

```
Ctrl + Z
```

---

# 📌 14️⃣ pstree

Shows process hierarchy (parent-child).

```bash
pstree
```

Specific PID:

```bash
pstree 1
```

Used to analyze orphan/zombie processes.

---

# 🔥 REAL PRODUCTION USE CASE (Step-by-Step)

---

# 🎯 Scenario: Production Server High CPU Issue

You are DevOps Engineer.

Alert:
CPU 95% usage.

---

## 🧩 Step 1: Check Load

```bash
top
```

Or:

```bash
htop
```

Sort by CPU (`P`).

---

## 🧩 Step 2: Identify Problem Process

Example:

```
java PID 4567 90% CPU
```

Verify:

```bash
ps -fp 4567
```

---

## 🧩 Step 3: Check Parent Process

```bash
pstree -p 4567
```

---

## 🧩 Step 4: Try Graceful Restart

```bash
kill -15 4567
```

Wait few seconds.

---

## 🧩 Step 5: If Not Stopping

```bash
kill -9 4567
```

---

## 🧩 Step 6: Lower Priority Instead of Killing (Alternative)

```bash
renice 15 -p 4567
```

---

## 🧩 Step 7: Monitor Again

```bash
top
```

---

# 🎯 Scenario 2: Run Backup Script After Logout

```bash
nohup bash backup.sh &
```

Check:

```bash
ps aux | grep backup
```

---

# 🎯 Scenario 3: Background Job Control

Run:

```bash
vim largefile.txt
```

Pause:

```
Ctrl + Z
```

Send to background:

```bash
bg
```

Return:

```bash
fg
```

---

# 🔍 Advanced Production Concepts

---

## 🔹 Orphan Process

* Parent dies
* Adopted by PID 1 (systemd)

Check:

```bash
pstree
```

---

## 🔹 Zombie Cleanup

Fix parent process or restart service.

---

## 🔹 Process Limits

Check limits:

```bash
ulimit -a
```

---

## 🔹 Monitor Specific User

```bash
ps -u username
```

---

## 🔹 Continuous Monitoring

```bash
watch -n 1 "ps aux | head"
```
---
# 🌐 Linux Networking – Complete Industry-Level Guide

---

# 1️⃣ Check IP & Network Interfaces

---

## 🔹 `ip a` (Modern & Recommended)

```bash
ip a
```

Shows:

* IP address
* MAC address
* Interface state (UP/DOWN)
* IPv4 & IPv6

Example Output:

```bash
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP>
    inet 10.0.0.15/24
```

---

## 🔹 `ifconfig` (Legacy)

```bash
ifconfig
```

⚠ Deprecated in modern systems (replaced by `ip`)

Install if needed:

```bash
sudo apt install net-tools
```

---

## 🔹 `ip link`

Shows interface status only:

```bash
ip link
```

Bring interface up/down:

```bash
sudo ip link set eth0 down
sudo ip link set eth0 up
```

---

# 2️⃣ Routing

---

## 🔹 `ip route` (Modern)

```bash
ip route
```

Example:

```bash
default via 10.0.0.1 dev eth0
10.0.0.0/24 dev eth0 proto kernel
```

Add route:

```bash
sudo ip route add 192.168.1.0/24 via 10.0.0.1
```

---

## 🔹 `route` (Legacy)

```bash
route -n
```

---

# 3️⃣ Connectivity & Data Transfer

---

## 🔹 `ping`

```bash
ping google.com
```

Check:

* Connectivity
* Latency
* Packet loss

Limit packets:

```bash
ping -c 4 8.8.8.8
```

---

## 🔹 `traceroute`

Shows packet path:

```bash
traceroute google.com
```

Install if needed:

```bash
sudo apt install traceroute
```

---

## 🔹 `curl`

Test APIs & HTTP:

```bash
curl https://example.com
curl -I https://example.com
```

POST request:

```bash
curl -X POST -d "name=test" https://api.site.com
```

---

## 🔹 `wget`

Download files:

```bash
wget https://example.com/file.zip
```

---

# 4️⃣ DNS & Name Resolution

---

## 🔹 `nslookup`

```bash
nslookup google.com
```

---

## 🔹 `dig` (Advanced)

```bash
dig google.com
dig google.com +short
```

---

## 🔹 `/etc/hosts`

Local DNS override:

```bash
sudo nano /etc/hosts
```

Example:

```bash
127.0.0.1   myapp.local
```

---

## 🔹 `/etc/resolv.conf`

DNS server configuration:

```bash
nameserver 8.8.8.8
```

---

# 5️⃣ Ports, Sockets & Services

---

## 🔹 `netstat` (Legacy)

```bash
netstat -tulnp
```

---

## 🔹 `ss` (Modern Replacement)

```bash
ss -tulnp
```

Shows:

* Listening ports
* PID
* Protocol

---

## 🔹 `lsof -i`

Check port usage:

```bash
lsof -i :80
```

---

# 6️⃣ Remote Access & File Transfer

---

## 🔹 `ssh`

```bash
ssh user@server_ip
```

With key:

```bash
ssh -i key.pem ubuntu@ec2-ip
```

---

## 🔹 `scp`

Copy file:

```bash
scp file.txt user@server:/home/user
```

---

## 🔹 `sftp`

```bash
sftp user@server
```

---

## 🔹 `telnet`

```bash
telnet google.com 80
```

Used for testing open ports.

---

## 🔹 `nc` (Netcat)

Port testing:

```bash
nc -zv google.com 443
```

Start listener:

```bash
nc -l 9000
```

---

# 7️⃣ Network Interface Management

---

## 🔹 `nmcli`

CLI tool for NetworkManager.

Show connections:

```bash
nmcli connection show
```

Activate:

```bash
nmcli connection up eth0
```

---

## 🔹 `nmtui`

Interactive UI:

```bash
nmtui
```

---

## 🔹 `ifup` / `ifdown`

```bash
sudo ifdown eth0
sudo ifup eth0
```

---

# 8️⃣ Network Security & Troubleshooting

---

## 🔹 `iptables`

View rules:

```bash
sudo iptables -L
```

Allow port 80:

```bash
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
```

---

## 🔹 `ufw` (Ubuntu Firewall)

Enable:

```bash
sudo ufw enable
```

Allow SSH:

```bash
sudo ufw allow 22
```

---

## 🔹 `firewalld`

```bash
sudo firewall-cmd --list-all
```

---

## 🔹 `tcpdump`

Capture traffic:

```bash
sudo tcpdump -i eth0
```

Capture specific port:

```bash
sudo tcpdump port 80
```

---

## 🔹 `nmap`

Scan ports:

```bash
nmap localhost
```

---

## 🔹 `arp`

```bash
arp -a
```

---

## 🔹 `arping`

```bash
arping 192.168.1.1
```

---

## 🔹 `ip neigh`

```bash
ip neigh
```

---

# 9️⃣ Network Monitoring

---

## 🔹 `iftop`

Real-time bandwidth usage:

```bash
sudo iftop
```

---

## 🔹 `nload`

```bash
nload
```

---

## 🔹 `bmon`

```bash
bmon
```

---

# 🔟 Host & Identity

---

## 🔹 `hostname`

```bash
hostname
```

---

## 🔹 `hostnamectl`

Change hostname:

```bash
sudo hostnamectl set-hostname dev-server
```

---

# 1️⃣1️⃣ IPv6

---

## 🔹 Check IPv6 Address

```bash
ip -6 a
```

---

## 🔹 IPv6 Routing

```bash
ip -6 route
```

---

# 🔥 REAL PRODUCTION USE CASE (Step-by-Step)

---

# 🎯 Scenario 1: Website Not Accessible on EC2

---

## 🧩 Step 1: Check IP

```bash
ip a
```

---

## 🧩 Step 2: Check Service Running

```bash
ss -tulnp | grep 80
```

---

## 🧩 Step 3: Test Locally

```bash
curl localhost
```

---

## 🧩 Step 4: Check Firewall

```bash
sudo ufw status
sudo iptables -L
```

---

## 🧩 Step 5: Check Security Group (AWS)

Ensure port 80 open.

---

## 🧩 Step 6: Test from Local Machine

```bash
nc -zv ec2-ip 80
```

---

# 🎯 Scenario 2: DNS Not Working

---

## 🧩 Step 1: Ping IP Directly

```bash
ping 8.8.8.8
```

If works → DNS issue.

---

## 🧩 Step 2: Check DNS

```bash
cat /etc/resolv.conf
```

---

## 🧩 Step 3: Test with dig

```bash
dig google.com
```

---

# 🎯 Scenario 3: Server High Network Usage

---

## 🧩 Step 1: Monitor

```bash
iftop
```

---

## 🧩 Step 2: Capture Traffic

```bash
tcpdump -i eth0
```

---

## 🧩 Step 3: Identify Suspicious Ports

```bash
ss -tulnp
```

---
# ⏰ Linux Scheduling & Automation

---

# 1️⃣ cron (Time-Based Job Scheduler)

## 🔹 What is cron?

`cron` is a background service (daemon) that executes scheduled tasks automatically.

It runs continuously in background.

Check service:

```bash id="k0x3nv"
systemctl status cron
```

Start/Enable:

```bash id="3d8nka"
sudo systemctl start cron
sudo systemctl enable cron
```

---

# 2️⃣ crontab (User-Level Scheduling)

Each user can define their own scheduled jobs.

---

## 🔹 Edit Crontab

```bash id="a9d1lm"
crontab -e
```

List:

```bash id="mf1z9r"
crontab -l
```

Remove:

```bash id="p3hs7k"
crontab -r
```

---

## 🔹 Cron Syntax (VERY IMPORTANT – Interview Question)

```bash id="9z0zq4"
* * * * * command
│ │ │ │ │
│ │ │ │ └── Day of Week (0-7)
│ │ │ └──── Month (1-12)
│ │ └────── Day of Month (1-31)
│ └──────── Hour (0-23)
└────────── Minute (0-59)
```

---

## 🔹 Examples

Run every minute:

```bash id="7qj52p"
* * * * * echo "Hello" >> /tmp/test.log
```

Run at 2 AM daily:

```bash id="c1wv92"
0 2 * * * /backup.sh
```

Run every Sunday at 3 AM:

```bash id="6o1qzj"
0 3 * * 0 /cleanup.sh
```

---

# 3️⃣ at (One-Time Scheduling)

Schedule single future task.

```bash id="29a1be"
at 5pm
```

Then type:

```bash id="kq91sz"
echo "Maintenance" >> /tmp/log.txt
```

Press:

```bash id="p5a0mf"
Ctrl + D
```

---

# 4️⃣ atq (Check Scheduled at Jobs)

```bash id="3ozc0n"
atq
```

Shows:

* Job number
* Scheduled time

---

# 5️⃣ atrm (Remove at Job)

```bash id="bbavqg"
atrm 2
```

---

# 6️⃣ batch

Runs job when system load is low.

```bash id="x7k2un"
batch
```

Useful for:

* Heavy scripts
* Log processing
* Backup compression

---

# 7️⃣ watch

Repeatedly runs a command.

```bash id="tavh4v"
watch -n 2 df -h
```

Runs every 2 seconds.

---

# 8️⃣ /etc/crontab (System-Wide Cron)

System cron file.

```bash id="rkf5je"
cat /etc/crontab
```

Format:

```bash id="1krh52"
* * * * * user command
```

Difference from user crontab:
✔ Includes username field

Example:

```bash id="a3ct0b"
0 1 * * * root /backup.sh
```

---

# 9️⃣ /etc/cron.hourly

Place scripts here to run hourly.

```bash id="4f3k0g"
sudo nano /etc/cron.hourly/myscript
```

Make executable:

```bash id="xq72jl"
sudo chmod +x /etc/cron.hourly/myscript
```

---

# 🔟 /etc/cron.daily

Runs once daily.

Example use:

* Log cleanup
* Database backup

---

# 1️⃣1️⃣ /etc/cron.weekly

Weekly tasks:

* System cleanup
* Security scans

---

# 1️⃣2️⃣ /etc/cron.monthly

Monthly tasks:

* Reporting
* Archiving logs

---

# 1️⃣3️⃣ /etc/cron.allow

Defines who CAN use cron.

```bash id="v4u61n"
sudo nano /etc/cron.allow
```

If exists → only listed users allowed.

---

# 1️⃣4️⃣ /etc/cron.deny

Defines who CANNOT use cron.

```bash id="38x2ow"
sudo nano /etc/cron.deny
```

---

# 1️⃣5️⃣ /etc/at.allow

Users allowed to use `at`.

---

# 1️⃣6️⃣ /etc/at.deny

Users denied from using `at`.

---

# 1️⃣7️⃣ cron service (systemctl)

Restart cron:

```bash id="i8m7cl"
sudo systemctl restart cron
```

Enable on boot:

```bash id="6nq7w3"
sudo systemctl enable cron
```

---

# 1️⃣8️⃣ Cron Logs

Check cron logs:

Ubuntu:

```bash id="1pr7np"
grep CRON /var/log/syslog
```

Or:

```bash id="h7x2s1"
journalctl -u cron
```

---

# 🔥 REAL PRODUCTION USE CASES (Step-by-Step)

---

# 🎯 Scenario 1: Daily Database Backup (EC2 Production)

Requirement:

* Backup MySQL every day at 2 AM
* Save to /backup
* Log success

---

## 🧩 Step 1: Create Backup Script

```bash id="yw17kd"
sudo nano /usr/local/bin/db_backup.sh
```

```bash id="2kx0w9"
#!/bin/bash
DATE=$(date +%F)
mysqldump -u root -pPASSWORD mydb > /backup/db_$DATE.sql
echo "Backup completed on $DATE" >> /var/log/db_backup.log
```

Make executable:

```bash id="0zw6xy"
sudo chmod +x /usr/local/bin/db_backup.sh
```

---

## 🧩 Step 2: Add Cron Job

```bash id="wbdm3t"
crontab -e
```

Add:

```bash id="tzzrci"
0 2 * * * /usr/local/bin/db_backup.sh
```

---

## 🧩 Step 3: Verify Logs

```bash id="vdq8pg"
tail -f /var/log/db_backup.log
```

---

# 🎯 Scenario 2: Cleanup Logs Every Sunday

```bash id="r9kg92"
0 3 * * 0 find /var/log -type f -mtime +7 -delete
```

---

# 🎯 Scenario 3: One-Time Server Restart

```bash id="d8r3fs"
at 23:00
```

Inside:

```bash id="q3sd7h"
sudo reboot
```

---

# 🎯 Scenario 4: Restrict User from Cron

Add user to deny file:

```bash id="v2kt7p"
echo username | sudo tee -a /etc/cron.deny
```

---

# 🎯 Scenario 5: Monitor Disk Every 5 Minutes

```bash id="d4r1pv"
*/5 * * * * df -h >> /var/log/disk_monitor.log
```

---
# 📊 Linux System Monitoring (Production-Level Guide)

---

# 1️⃣ CPU Monitoring

## 🔹 Check CPU Usage – `top`

```bash
top
```

Shows:

* CPU usage %
* Running processes
* Load average

Press:

* `P` → Sort by CPU
* `1` → Show per-core usage

---

## 🔹 Modern Alternative – `htop`

```bash
sudo apt install htop
htop
```

✔ Visual per-core usage
✔ Easy process kill

---

## 🔹 Detailed CPU Stats – `mpstat`

```bash
sudo apt install sysstat
mpstat -P ALL 1
```

Shows:

* Per CPU core stats
* Idle %
* User %
* System %

---

## 🔹 Quick CPU Info

```bash
lscpu
```

---

# 🔥 Production CPU Use Case

### 🎯 Alert: CPU 95% on EC2

Step 1:

```bash
top
```

Step 2: Identify high CPU PID

Step 3:

```bash
ps -fp PID
```

Step 4: Reduce priority instead of killing

```bash
renice 10 -p PID
```

---

# 2️⃣ Memory Monitoring

---

## 🔹 Check Memory – `free`

```bash
free -h
```

Important fields:

* total
* used
* free
* buff/cache

---

## 🔹 Real-time Memory – `top` or `htop`

Press `M` in top → Sort by memory.

---

## 🔹 Detailed Memory Stats

```bash
vmstat 1
```

Shows:

* Swap usage
* Memory pressure
* IO wait

---

## 🔹 Check Swap

```bash
swapon --show
```

---

# 🔥 Production Memory Use Case

### 🎯 Application crashing (OOM issue)

Step 1:

```bash
free -h
```

Step 2:

```bash
dmesg | grep -i kill
```

Step 3:
Add swap if needed:

```bash
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
```

---

# 3️⃣ Disk Monitoring

---

## 🔹 Disk Space – `df`

```bash
df -h
```

---

## 🔹 Directory Usage – `du`

```bash
du -sh /var/log
```

---

## 🔹 Inode Usage

```bash
df -i
```

---

## 🔹 Disk IO – `iostat`

```bash
iostat -xz 1
```

Shows:

* Read/write speed
* IO wait

---

# 🔥 Production Disk Use Case

### 🎯 Root partition 100% full

Step 1:

```bash
df -h
```

Step 2:

```bash
du -sh /* | sort -hr
```

Step 3:
Clear logs or extend disk.

---

# 4️⃣ Process Monitoring

---

## 🔹 View All Processes

```bash
ps aux
```

---

## 🔹 Tree View

```bash
pstree
```

---

## 🔹 Kill Process

```bash
kill -15 PID
```

---

## 🔹 Monitor Specific User

```bash
ps -u username
```

---

# 🔥 Production Process Use Case

### 🎯 Zombie Process Found

```bash
ps aux | grep Z
```

Find parent PID:

```bash
pstree -p
```

Restart parent service.

---

# 5️⃣ Network Monitoring

---

## 🔹 Interface Traffic – `iftop`

```bash
sudo iftop
```

---

## 🔹 Bandwidth – `nload`

```bash
nload
```

---

## 🔹 Socket Stats – `ss`

```bash
ss -tulnp
```

---

## 🔹 Packet Capture – `tcpdump`

```bash
sudo tcpdump -i eth0
```

---

# 🔥 Production Network Use Case

### 🎯 High Network Usage Alert

Step 1:

```bash
iftop
```

Step 2:

```bash
ss -tulnp
```

Step 3:

```bash
tcpdump port 443
```

Identify suspicious traffic.

---

# 6️⃣ System Load & Uptime

---

## 🔹 Uptime

```bash
uptime
```

Output:

```bash
14:32:01 up 10 days, load average: 0.50, 0.30, 0.20
```

Load Average Meaning:

* 1 min
* 5 min
* 15 min

Rule:
If load > number of CPU cores → overload.

---

## 🔹 Check Load Only

```bash
cat /proc/loadavg
```

---

# 🔥 Production Load Use Case

### 🎯 Load Average = 15 on 2 CPU machine

Step 1:

```bash
top
```

Step 2:
Check IO wait:

```bash
iostat
```

Step 3:
Check memory:

```bash
free -h
```

---

# 7️⃣ Performance Statistics

---

## 🔹 vmstat

```bash
vmstat 1
```

Key columns:

* r → running processes
* free → free memory
* si/so → swap in/out

---

## 🔹 iostat

```bash
iostat -xz 1
```

Check:

* %util
* await

---

## 🔹 sar (Historical Data)

```bash
sar -u 1 5
```

CPU stats history.

Enable sysstat:

```bash
sudo systemctl enable sysstat
```

---

## 🔹 pidstat

```bash
pidstat 1
```

Per-process stats.

---

# 🔥 Complete Production Incident Example

---

# 🎯 Scenario: Website Slow on EC2

---

## Step 1: Check Load

```bash
uptime
```

---

## Step 2: CPU

```bash
top
```

---

## Step 3: Memory

```bash
free -h
```

---

## Step 4: Disk IO

```bash
iostat -xz 1
```

---

## Step 5: Network

```bash
iftop
```

---

## Step 6: Identify Root Cause

✔ High CPU → Optimize app
✔ High Memory → Add RAM
✔ High IO wait → Upgrade disk
✔ High Load → Scale horizontally

---
# 📜 Linux Logging & Journals (Industry-Level Guide)

---

# 1️⃣ Log Files (Concept)

## 🔹 What is a Log?

A **log file** records system events, errors, warnings, and activities.

Logs are used for:

* Debugging
* Security auditing
* Monitoring
* Incident investigation
* Compliance

---

## 🔹 Log Flow in Linux

```text
Application → syslog/journald → /var/log files
```

---

# 2️⃣ `/var/log` Directory

Main log directory in Linux.

```bash
ls -lh /var/log
```

Stores:

* System logs
* Application logs
* Authentication logs
* Kernel logs

---

# 3️⃣ Common Log Files (Ubuntu/Debian)

| Log File                    | Purpose              |
| --------------------------- | -------------------- |
| `/var/log/syslog`           | General system logs  |
| `/var/log/auth.log`         | Authentication logs  |
| `/var/log/kern.log`         | Kernel logs          |
| `/var/log/dpkg.log`         | Package manager logs |
| `/var/log/nginx/access.log` | Nginx access logs    |
| `/var/log/nginx/error.log`  | Nginx errors         |

---

## 🔹 View Logs

```bash
tail -f /var/log/syslog
```

Search inside logs:

```bash
grep "error" /var/log/syslog
```

---

# 4️⃣ rsyslog

## 🔹 What is rsyslog?

`rsyslog` is a log processing service that:

* Collects logs
* Filters logs
* Stores logs
* Forwards logs to remote server

Check status:

```bash
systemctl status rsyslog
```

---

## 🔹 Config File

```bash
/etc/rsyslog.conf
/etc/rsyslog.d/
```

Restart after changes:

```bash
sudo systemctl restart rsyslog
```

---

# 5️⃣ journalctl (systemd Logs)

Modern Linux uses **systemd-journald**.

---

## 🔹 View All Logs

```bash
journalctl
```

---

## 🔹 Real-Time Logs

```bash
journalctl -f
```

---

## 🔹 Filter by Service

```bash
journalctl -u nginx
```

---

## 🔹 Filter by Time

```bash
journalctl --since "1 hour ago"
journalctl --since "2025-01-01"
```

---

# 6️⃣ journald

`journald` collects logs in binary format.

Config file:

```bash
/etc/systemd/journald.conf
```

Restart:

```bash
sudo systemctl restart systemd-journald
```

---

# 7️⃣ Log Levels (Very Important – Interview)

| Level   | Description               |
| ------- | ------------------------- |
| emerg   | System unusable           |
| alert   | Immediate action required |
| crit    | Critical condition        |
| err     | Error                     |
| warning | Warning                   |
| notice  | Normal but important      |
| info    | Informational             |
| debug   | Debugging                 |

Filter by priority:

```bash
journalctl -p err
```

---

# 8️⃣ logger (Manual Log Entry)

Send custom message to syslog.

```bash
logger "Backup completed successfully"
```

With priority:

```bash
logger -p user.error "Application crashed"
```

---

# 9️⃣ Log Rotation

## 🔹 Why Rotate Logs?

If logs are not rotated:

* Disk becomes full
* System crashes
* Services fail

Log rotation:

* Compresses old logs
* Deletes old logs
* Renames logs

---

# 🔟 logrotate

Manages log rotation automatically.

Check:

```bash
logrotate --version
```

Manual run:

```bash
sudo logrotate -f /etc/logrotate.conf
```

---

# 1️⃣1️⃣ `/etc/logrotate.conf`

Main configuration file.

```bash
cat /etc/logrotate.conf
```

Example:

```bash
weekly
rotate 4
compress
create
```

Meaning:

* Rotate weekly
* Keep 4 backups
* Compress old logs

---

# 1️⃣2️⃣ `/etc/logrotate.d/`

Application-specific rotation configs.

Example:

```bash
ls /etc/logrotate.d/
```

Nginx example:

```bash
cat /etc/logrotate.d/nginx
```

---

# 1️⃣3️⃣ Persistent Journals

By default, journald logs may be temporary.

Enable persistent logging:

```bash
sudo mkdir -p /var/log/journal
sudo systemctl restart systemd-journald
```

Verify:

```bash
journalctl --disk-usage
```

---

# 🔥 REAL PRODUCTION USE CASES

---

# 🎯 Scenario 1: Website Down on EC2

Step 1: Check nginx logs

```bash
tail -f /var/log/nginx/error.log
```

Step 2: Check service logs

```bash
journalctl -u nginx
```

Step 3: Check system logs

```bash
tail -f /var/log/syslog
```

Root Cause Example:
✔ Port conflict
✔ Permission denied
✔ Disk full

---

# 🎯 Scenario 2: User Login Failure

Check auth logs:

```bash
tail -f /var/log/auth.log
```

Look for:

```text
Failed password for user
```

---

# 🎯 Scenario 3: Disk Full Due to Logs

Step 1:

```bash
df -h
```

Step 2:

```bash
du -sh /var/log/*
```

Step 3: Force rotation

```bash
sudo logrotate -f /etc/logrotate.conf
```

---

# 🎯 Scenario 4: Debug Application Crash

Step 1:

```bash
journalctl -u myapp --since "30 minutes ago"
```

Step 2:

```bash
journalctl -p err
```

Step 3:

```bash
dmesg | tail
```

---

# 🎯 Scenario 5: Send Custom Monitoring Log

Inside backup script:

```bash
logger "Database backup successful"
```

Then monitor:

```bash
tail -f /var/log/syslog
```

---

# 🧠 Advanced Production Concepts

---

## 🔹 Centralized Logging

Forward logs to:

* ELK Stack
* Splunk
* CloudWatch

Using rsyslog remote config.

---

## 🔹 Limit Journal Size

Edit:

```bash
sudo nano /etc/systemd/journald.conf
```

Set:

```bash
SystemMaxUse=500M
```

---

## 🔹 Clear Journal Logs

```bash
sudo journalctl --vacuum-time=7d
```

---
# 🔐 SSH & Remote Access (Production-Level Guide)


---

# 1️⃣ SSH Basics

## 🔹 What is SSH?

**SSH (Secure Shell)** is a secure protocol used to:

* Access remote servers
* Execute commands remotely
* Transfer files securely
* Create encrypted tunnels

Default Port:

```bash
22
```

---

## 🔹 Basic SSH Command

```bash
ssh username@server_ip
```

Example (EC2 Ubuntu):

```bash
ssh ubuntu@3.110.10.20
```

---

## 🔹 SSH Flow

```text
Client → Encrypted Connection → SSH Server → Shell Access
```

---

# 2️⃣ Password Authentication

## 🔹 Login Using Password

```bash
ssh user@server
```

Server asks for password.

---

## 🔹 Enable Password Auth (Server Side)

Edit config:

```bash
sudo nano /etc/ssh/sshd_config
```

Set:

```bash
PasswordAuthentication yes
```

Restart:

```bash
sudo systemctl restart ssh
```

⚠ Not recommended for production (security risk).

---

# 3️⃣ Key Authentication (Recommended in Production)

## 🔹 Step 1: Generate Key Pair (Client)

```bash
ssh-keygen -t rsa -b 4096
```

Files created:

```bash
~/.ssh/id_rsa      (Private Key)
~/.ssh/id_rsa.pub  (Public Key)
```

---

## 🔹 Step 2: Copy Public Key to Server

```bash
ssh-copy-id user@server_ip
```

OR manually:

```bash
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
```

---

## 🔹 Step 3: Login Using Key

```bash
ssh -i ~/.ssh/id_rsa user@server
```

---

## 🔐 Why Key Auth is Better?

✔ No password brute-force
✔ More secure
✔ Used in EC2
✔ Required in automation

---

# 4️⃣ Common SSH Commands

---

## 🔹 Specify Port

```bash
ssh -p 2222 user@server
```

---

## 🔹 Verbose Mode

```bash
ssh -v user@server
```

---

## 🔹 Run Remote Command

```bash
ssh user@server "df -h"
```

---

## 🔹 SSH Config File (Client)

```bash
nano ~/.ssh/config
```

Example:

```bash
Host prod
  HostName 3.110.10.20
  User ubuntu
  IdentityFile ~/.ssh/prod.pem
```

Now connect using:

```bash
ssh prod
```

---

# 5️⃣ SSH Server

## 🔹 Install SSH Server (Ubuntu)

```bash
sudo apt install openssh-server
```

Check:

```bash
sudo systemctl status ssh
```

Enable on boot:

```bash
sudo systemctl enable ssh
```

---

# 6️⃣ SSH Configuration

Main config:

```bash
/etc/ssh/sshd_config
```

Important options:

```bash
Port 22
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
MaxAuthTries 3
```

After changes:

```bash
sudo systemctl restart ssh
```

---

# 7️⃣ Key Management

---

## 🔹 Generate Different Key Types

```bash
ssh-keygen -t ed25519
ssh-keygen -t rsa -b 4096
```

---

## 🔹 Change Key Permission

```bash
chmod 600 ~/.ssh/id_rsa
chmod 700 ~/.ssh
```

---

## 🔹 Remove Compromised Key

Edit:

```bash
nano ~/.ssh/authorized_keys
```

Delete old key.

---

# 8️⃣ Security Hardening (Very Important)

---

## 🔒 Disable Root Login

```bash
PermitRootLogin no
```

---

## 🔒 Disable Password Login

```bash
PasswordAuthentication no
```

---

## 🔒 Change Default Port

```bash
Port 2222
```

---

## 🔒 Limit Users

```bash
AllowUsers ubuntu devuser
```

---

## 🔒 Enable Firewall

```bash
sudo ufw allow 22
sudo ufw enable
```

---

## 🔒 Fail2ban Protection

```bash
sudo apt install fail2ban
```

Prevents brute-force attacks.

---

# 9️⃣ Port Forwarding & Tunneling

---

## 🔹 Local Port Forwarding

Access remote DB locally:

```bash
ssh -L 3306:localhost:3306 user@server
```

Now local port 3306 forwards to remote MySQL.

---

## 🔹 Remote Port Forwarding

```bash
ssh -R 9000:localhost:3000 user@server
```

---

## 🔹 Dynamic (SOCKS Proxy)

```bash
ssh -D 1080 user@server
```

Used for secure browsing.

---

# 🔟 Debugging SSH Issues

---

## 🔹 Verbose Mode

```bash
ssh -vvv user@server
```

---

## 🔹 Check SSH Logs

Ubuntu:

```bash
tail -f /var/log/auth.log
```

---

## 🔹 Check Port Listening

```bash
ss -tulnp | grep 22
```

---

## 🔹 Firewall Check

```bash
sudo ufw status
```

---

# 1️⃣1️⃣ rsync over SSH

Used for secure file sync.

---

## 🔹 Basic Usage

```bash
rsync -avz file.txt user@server:/home/user/
```

---

## 🔹 Sync Directory

```bash
rsync -avz project/ user@server:/var/www/project/
```

---

## 🔹 Use Custom SSH Port

```bash
rsync -avz -e "ssh -p 2222" project/ user@server:/var/www/
```

---

# 🔥 REAL PRODUCTION USE CASES

---

# 🎯 Scenario 1: Secure EC2 Setup

Step 1: Launch EC2
Step 2: Login using key

```bash
ssh -i mykey.pem ubuntu@ec2-ip
```

Step 3: Harden SSH

Edit:

```bash
sudo nano /etc/ssh/sshd_config
```

Set:

```bash
PermitRootLogin no
PasswordAuthentication no
```

Restart:

```bash
sudo systemctl restart ssh
```

---

# 🎯 Scenario 2: MySQL Secure Access Without Public Exposure

MySQL running on private server.

Use SSH tunnel:

```bash
ssh -L 3306:localhost:3306 ubuntu@server-ip
```

Now connect locally:

```bash
mysql -h 127.0.0.1 -u root -p
```

✔ No need to open port 3306 publicly.

---

# 🎯 Scenario 3: Deploy Application via rsync

From local machine:

```bash
rsync -avz --delete project/ ubuntu@server:/var/www/app/
```

Then:

```bash
ssh ubuntu@server "sudo systemctl restart nginx"
```

---

# 🎯 Scenario 4: SSH Connection Refused

Checklist:

1️⃣ Is SSH running?

```bash
systemctl status ssh
```

2️⃣ Is port open?

```bash
ss -tulnp | grep 22
```

3️⃣ Firewall open?

```bash
ufw status
```

4️⃣ Security Group open? (AWS)

---

# 🛠️ Boot Troubleshooting & Recovery (Linux)

---

# 📌 Understanding the Linux Boot Flow (Very Important)

```text
BIOS/UEFI → GRUB → Kernel → initramfs → systemd → Login
```

If system fails to boot, problem usually in:

* GRUB
* Kernel
* Filesystem
* Initramfs
* Root password
* Service crash

---

# 1️⃣ Single User Mode

## 🔹 What is Single User Mode?

* Minimal boot environment
* Only root user
* No networking
* Used for maintenance

---

## 🔹 How to Enter (Ubuntu)

1. Reboot system
2. Press **Shift** (or Esc in cloud/VM)
3. Select Ubuntu
4. Press `e` to edit
5. Find line starting with:

```bash
linux /boot/vmlinuz...
```

Add at end:

```bash
single
```

OR

```bash
init=/bin/bash
```

Press:

```text
Ctrl + X
```

System boots into root shell.

---

## 🔥 Use Case

### 🎯 System not booting properly

Boot into single-user → Disable problematic service:

```bash
systemctl disable nginx
reboot
```

---

# 2️⃣ Rescue Mode

## 🔹 What is Rescue Mode?

* Loads basic system
* Mounts filesystem
* Allows service repair

---

## 🔹 Enter Rescue Mode

In GRUB:

Add:

```bash
systemd.unit=rescue.target
```

Boot with:

```text
Ctrl + X
```

---

## 🔥 Use Case

### 🎯 Corrupted configuration file

Example:

```bash
nano /etc/fstab
```

Fix wrong entry → reboot.

---

# 3️⃣ Emergency Mode

## 🔹 What is Emergency Mode?

* Minimal shell
* Filesystems NOT mounted automatically
* Used for serious corruption

Enter in GRUB:

```bash
systemd.unit=emergency.target
```

---

## 🔥 Use Case

### 🎯 Broken /etc/fstab entry

Fix:

```bash
mount -o remount,rw /
nano /etc/fstab
```

Correct entry → reboot.

---

# 4️⃣ GRUB Commands

GRUB = Bootloader.

---

## 🔹 Common GRUB Actions

Edit boot parameters:
Press `e`

Boot manually:

```bash
linux /boot/vmlinuz root=/dev/sda1 ro
initrd /boot/initrd.img
boot
```

---

## 🔹 Reinstall GRUB (If Broken)

```bash
sudo grub-install /dev/sda
sudo update-grub
```

---

# 🔥 Use Case

### 🎯 GRUB missing after disk issue

Boot from live CD → reinstall GRUB.

---

# 5️⃣ Reset Root Password

---

## 🔹 Method (Ubuntu)

1. Enter GRUB
2. Edit boot entry
3. Add:

```bash
init=/bin/bash
```

4. Boot

Remount root:

```bash
mount -o remount,rw /
```

Change password:

```bash
passwd root
```

Reboot:

```bash
exec /sbin/init
```

---

# 🔥 Use Case

### 🎯 Forgot root password

Recover without reinstalling OS.

---

# 6️⃣ fsck in Recovery

## 🔹 What is fsck?

File System Check tool.

Used when:

* Disk corruption
* Improper shutdown
* Mount errors

---

## 🔹 Run fsck

From recovery mode:

```bash
fsck /dev/sda1
```

Force check:

```bash
fsck -f /dev/sda1
```

Auto-fix:

```bash
fsck -y /dev/sda1
```

---

## 🔥 Use Case

### 🎯 Server shows:

```text
UNEXPECTED INCONSISTENCY; RUN fsck MANUALLY
```

Solution:

Boot recovery → run fsck → reboot.

---

# 7️⃣ Initramfs Rebuild

## 🔹 What is initramfs?

Temporary root filesystem used during boot.

If corrupted → system won’t boot.

---

## 🔹 Rebuild Initramfs

```bash
update-initramfs -u
```

For specific kernel:

```bash
update-initramfs -u -k all
```

---

## 🔥 Use Case

### 🎯 After kernel update → boot failure

Rebuild initramfs → update grub:

```bash
update-grub
```

---

# 8️⃣ Boot Logs

Logs help diagnose boot failure.

---

## 🔹 View Previous Boot Logs

```bash
journalctl -b -1
```

---

## 🔹 Current Boot

```bash
journalctl -b
```

---

## 🔹 Kernel Logs

```bash
dmesg | less
```

---

## 🔥 Use Case

### 🎯 Service failing on boot

Check:

```bash
journalctl -xe
journalctl -u nginx
```

---

# 🚨 COMPLETE PRODUCTION INCIDENT SCENARIO

---

# 🎯 Scenario: EC2 Ubuntu Not Booting After Disk Full

---

## Step 1: Enter Recovery Mode

Use EC2 serial console.

---

## Step 2: Check Disk

```bash
df -h
```

Root 100% full.

---

## Step 3: Clear Logs

```bash
rm -rf /var/log/*.gz
```

---

## Step 4: Run fsck

```bash
fsck -y /dev/nvme0n1p1
```

---

## Step 5: Reboot

```bash
reboot
```

Server restored.

---

# 🎯 Scenario: System Stuck in Emergency Mode

Error:

```text
Dependency failed for /data
```

Fix:

```bash
mount -o remount,rw /
nano /etc/fstab
```

Correct wrong UUID → reboot.

---

# 🎯 Scenario: Kernel Panic

Check:

```bash
journalctl -b -1
```

Rollback kernel:

In GRUB → select older kernel.

---
# 🛠️ Linux Troubleshooting (Production Playbook)

---

# 🧠 Golden Troubleshooting Method (ALWAYS FOLLOW)

```text
1️⃣ Identify Problem
2️⃣ Collect Data
3️⃣ Isolate Root Cause
4️⃣ Apply Fix
5️⃣ Verify
6️⃣ Prevent Recurrence
```

---

# 1️⃣ Disk Full Issue

---

## 🎯 Scenario: Website Down – “No space left on device”

---

## 🔎 Step 1: Check Disk Space

```bash
df -h
```

If root `/` is 100% → continue.

---

## 🔎 Step 2: Find Large Directories

```bash
du -sh /* 2>/dev/null | sort -hr
```

Drill down:

```bash
du -sh /var/* | sort -hr
```

---

## 🔎 Step 3: Check Inodes

```bash
df -i
```

If inodes 100% → too many small files.

---

## 🔧 Common Fixes

### 🔹 Clear Logs

```bash
truncate -s 0 /var/log/syslog
```

### 🔹 Remove Old Logs

```bash
rm -rf /var/log/*.gz
```

### 🔹 Clean Package Cache

```bash
apt clean
```

### 🔹 Rotate Logs

```bash
logrotate -f /etc/logrotate.conf
```

---

## ✅ Verify

```bash
df -h
```

---

## 🏭 Prevention

✔ Enable logrotate
✔ Monitor disk alerts
✔ Separate data partition

---

# 2️⃣ High CPU Issue

---

## 🎯 Scenario: CPU 95% Alert on EC2

---

## 🔎 Step 1: Check Load

```bash
uptime
```

If load > CPU cores → overloaded.

---

## 🔎 Step 2: Identify Process

```bash
top
```

Sort by CPU (`P`)

---

## 🔎 Step 3: Inspect Process

```bash
ps -fp PID
```

---

## 🔧 Fix Options

### ✔ Graceful Kill

```bash
kill -15 PID
```

### ✔ Force Kill (last option)

```bash
kill -9 PID
```

### ✔ Lower Priority

```bash
renice 10 -p PID
```

---

## 🏭 Prevention

✔ Optimize application
✔ Use autoscaling
✔ Monitor CPU alarms

---

# 3️⃣ High Memory Issue

---

## 🎯 Scenario: Application Crash (Out of Memory)

---

## 🔎 Step 1: Check Memory

```bash
free -h
```

---

## 🔎 Step 2: Check Top Memory Users

```bash
top
```

Sort by Memory (`M`)

---

## 🔎 Step 3: Check OOM Killer

```bash
dmesg | grep -i kill
```

---

## 🔧 Fix

### ✔ Restart Service

```bash
systemctl restart myapp
```

### ✔ Add Swap

```bash
fallocate -l 2G /swapfile
chmod 600 /swapfile
mkswap /swapfile
swapon /swapfile
```

---

## 🏭 Prevention

✔ Increase RAM
✔ Optimize queries
✔ Set memory limits

---

# 4️⃣ Zombie Process

---

## 🎯 Scenario: Zombie Found in Monitoring

---

## 🔎 Identify Zombies

```bash
ps aux | grep Z
```

State `Z` = zombie.

---

## 🔎 Find Parent Process

```bash
pstree -p
```

---

## 🔧 Fix

Restart parent service:

```bash
systemctl restart service_name
```

OR kill parent:

```bash
kill -15 PARENT_PID
```

---

## 🧠 Why Zombies Occur?

Parent did not read child exit status.

---

# 5️⃣ Network Not Working

---

## 🎯 Scenario: Cannot Access Internet

---

## 🔎 Step 1: Check IP

```bash
ip a
```

---

## 🔎 Step 2: Check Gateway

```bash
ip route
```

Look for:

```
default via x.x.x.x
```

---

## 🔎 Step 3: Ping Gateway

```bash
ping gateway_ip
```

---

## 🔎 Step 4: Test DNS

```bash
ping 8.8.8.8
```

If works → DNS issue.

Check:

```bash
cat /etc/resolv.conf
```

---

## 🔎 Step 5: Restart Network

```bash
systemctl restart NetworkManager
```

---

# 6️⃣ SSH Login Failed

---

## 🎯 Scenario: “Permission denied”

---

## 🔎 Step 1: Check SSH Service

```bash
systemctl status ssh
```

---

## 🔎 Step 2: Check Logs

```bash
tail -f /var/log/auth.log
```

---

## 🔎 Step 3: Check Key Permission

```bash
chmod 600 ~/.ssh/id_rsa
chmod 700 ~/.ssh
```

---

## 🔎 Step 4: Check sshd_config

```bash
nano /etc/ssh/sshd_config
```

Ensure:

```
PasswordAuthentication yes/no
PubkeyAuthentication yes
```

Restart:

```bash
systemctl restart ssh
```

---

## 🔎 Step 5: Check Firewall

```bash
ufw status
```

---

# 7️⃣ Service Not Starting

---

## 🎯 Scenario: Nginx Not Starting

---

## 🔎 Step 1: Check Status

```bash
systemctl status nginx
```

---

## 🔎 Step 2: Check Logs

```bash
journalctl -u nginx
```

---

## 🔎 Step 3: Check Port Conflict

```bash
ss -tulnp | grep 80
```

---

## 🔎 Step 4: Check Config

```bash
nginx -t
```

---

## 🔧 Fix

✔ Free port
✔ Fix config syntax
✔ Correct file permissions

---

# 8️⃣ Boot Failure

---

## 🎯 Scenario: Server Not Booting

---

## 🔎 Step 1: Enter Recovery Mode

From GRUB → Recovery

---

## 🔎 Step 2: Check Disk

```bash
fsck -y /dev/sda1
```

---

## 🔎 Step 3: Check fstab

```bash
nano /etc/fstab
```

Fix wrong UUID.

---

## 🔎 Step 4: Check Boot Logs

```bash
journalctl -b -1
```

---

## 🔎 Step 5: Rebuild Initramfs

```bash
update-initramfs -u
update-grub
```

---

# 🚨 FULL PRODUCTION INCIDENT (Example)

---

## 🎯 EC2 Website Down

Symptoms:

* 502 Bad Gateway
* SSH slow

---

### Step 1: SSH Login

```bash
ssh ubuntu@server
```

---

### Step 2: Check Load

```bash
uptime
```

---

### Step 3: Check CPU

```bash
top
```

---

### Step 4: Check Memory

```bash
free -h
```

---

### Step 5: Check Disk

```bash
df -h
```

---

### Step 6: Check Nginx

```bash
systemctl status nginx
journalctl -u nginx
```

---

### Root Cause Example:

✔ Disk full → Logs filled
✔ Cleared logs → Service restarted
✔ Issue resolved

---
