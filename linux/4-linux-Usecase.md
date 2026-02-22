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
