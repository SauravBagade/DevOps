# 🔐 File Permissions & Ownership in Linux

Linux uses a **permission model** to control access to files and directories.  
Each file/directory has an **owner**, a **group**, and **permissions** for who can read, write, or execute it.  

---

## **1. File Ownership**
- **User (Owner)** → The person who created the file (or assigned owner).
- **Group** → A collection of users who share permissions.
- **Others** → All other users on the system.

### Check ownership:
```bash
ls -l
````

Example output:

```
-rwxr-xr--  1 alice  developers  1234 Sep 28 12:00 script.sh
```

Explanation:

* **alice** → Owner
* **developers** → Group
* **1234** → File size in bytes

---

## **2. File Permissions**

Permissions are shown as **rwx**:

* **r** = Read
* **w** = Write (modify)
* **x** = Execute (run as program/script)

They apply separately to:

* **User (u)** – file owner
* **Group (g)** – group members
* **Others (o)** – everyone else

Example:

```
-rwxr-xr--
```

* **Owner (u)** → `rwx` → read, write, execute
* **Group (g)** → `r-x` → read, execute
* **Others (o)** → `r--` → read only

---

## **3. Changing Ownership**

Change **file owner**:

```bash
sudo chown newuser filename
```

Change **file group**:

```bash
sudo chgrp newgroup filename
```

Change **both**:

```bash
sudo chown newuser:newgroup filename
```

---

## **4. Changing Permissions**

### Using `chmod` (symbolic mode):

```bash
chmod u+x script.sh   # Add execute permission to user
chmod g-w report.txt  # Remove write permission for group
chmod o+r file.txt    # Give read permission to others
```

### Using `chmod` (numeric mode):

Each permission has a value:

* **r = 4, w = 2, x = 1**

Add them up:

* `7 = rwx`
* `6 = rw-`
* `5 = r-x`
* `4 = r--`

Examples:

```bash
chmod 755 script.sh   # rwx for user, r-x for group & others
chmod 644 file.txt    # rw- for user, r-- for group & others
chmod 700 secret.txt  # rwx only for user
```

---

## **5. Use Cases**

### ✅ Protect Sensitive Files

```bash
chmod 600 id_rsa
```

* Only the owner can read/write (used for SSH private keys).

---

### ✅ Shared Project Directory

```bash
sudo chown -R :developers /project
chmod -R 770 /project
```

* Group `developers` has full access.
* Others have **no access**.

---

### ✅ Publicly Accessible File

```bash
chmod 644 index.html
```

* Owner can edit.
* Everyone can read (common for web servers).

---

### ✅ Executable Scripts

```bash
chmod +x backup.sh
./backup.sh
```

* Script becomes executable.

---

## **6. Special Permissions**

* **SUID (Set User ID)** → Run as file’s owner.
* **SGID (Set Group ID)** → Run as file’s group.
* **Sticky Bit** → On directories, only file owner can delete their files.

Examples:

```bash
chmod u+s program      # SUID
chmod g+s shared_dir   # SGID
chmod +t /tmp          # Sticky bit
```

----------------------------------------------------------------------------------------------------------------
# ⏰ Cron Jobs – Task Scheduling in Linux

## **1. What is a Cron Job?**
- A **cron job** is a scheduled task in Linux that runs **automatically** at specified times or intervals.  
- Managed by the **cron daemon (`crond`)**.  
- Commonly used for backups, log rotation, system maintenance, monitoring, etc.

---
### On Debian/Ubuntu:
```bash
sudo apt update
sudo apt install cron -y

## **2. Crontab Basics**
Each user can create/edit their own **crontab file**.

### View crontab
```bash
crontab -l
````

### Edit crontab

```bash
crontab -e
```

### Remove crontab

```bash
crontab -r
```

---

## **3. Crontab Syntax**

Format:

```
* * * * * command_to_execute
- - - - -
| | | | |
| | | | +---- Day of week (0–6) (Sunday=0)
| | | +------ Month (1–12)
| | +-------- Day of month (1–31)
| +---------- Hour (0–23)
+------------ Minute (0–59)
```

Examples:

* `0 5 * * * /home/user/backup.sh` → Run every day at **5:00 AM**.
* `*/10 * * * * /script.sh` → Run every **10 minutes**.
* `0 0 * * 0 /cleanup.sh` → Run every **Sunday at midnight**.

---

## **4. Use Cases for Cron Jobs**

### ✅ **Automated Backups**

```bash
0 2 * * * tar -czf /backup/home-$(date +\%F).tar.gz /home/user
```

* Runs daily at **2 AM**.
* Creates a compressed backup of `/home/user`.

---

### ✅ **Log Cleanup**

```bash
0 0 * * 7 find /var/log -type f -name "*.log" -delete
```

* Runs every **Sunday midnight**.
* Deletes old `.log` files.

---

### ✅ **System Updates**

```bash
0 3 * * 1 apt update && apt upgrade -y
```

* Runs every **Monday 3 AM**.
* Updates & upgrades packages.

---

### ✅ **Database Backup**

```bash
30 1 * * * mysqldump -u root -pMyPass mydb > /backup/mydb-$(date +\%F).sql
```

* Runs daily at **1:30 AM**.
* Dumps MySQL database into backup folder.

---

### ✅ **Custom Script Execution**

```bash
*/5 * * * * /home/user/scripts/monitor.sh
```

* Runs every **5 minutes**.
* Useful for monitoring, alerts, or automated tasks.

---

## **5. Special Keywords**

Instead of numbers, you can use keywords:

* `@reboot` → Run once at system startup.
* `@hourly` → Run every hour.
* `@daily` → Run once a day (midnight).
* `@weekly` → Run once a week.
* `@monthly` → Run once a month.
* `@yearly` → Run once a year.

Example:

```bash
@reboot /home/user/startup.sh
```

* Runs a script automatically after system reboot.

---

## **6. Cron Log Monitoring**

* Cron logs are usually stored in:

```bash
/var/log/cron
/var/log/syslog
```

To check logs:

```bash
grep CRON /var/log/syslog
```

-----------------------------------------------------------------------

# 📄 File Viewing & Editing in Linux

Linux provides multiple commands and editors to **view, read, and modify files**.  
These tools are essential for system admins, developers, and everyday users.  

---

## **1. Viewing Files**

### ✅ `less` – View file with navigation

```bash
less file.txt
```

* Scroll up/down with **↑ ↓ PgUp PgDn**.
* Quit with `q`.

---

### ✅ `more` – Page-by-page viewing

```bash
more file.txt
```

* Displays one screen at a time.
* Press **Space** to go forward.

---

### ✅ `head` – Show first lines

```bash
head -n 20 file.txt
```

* Shows the first 20 lines.

---

### ✅ `tail` – Show last lines

```bash
tail -n 50 logfile.log
```

* Shows last 50 lines.
* **Follow updates in real time**:

```bash
tail -f logfile.log
```

---

## **2. Editing Files**

### ✅ `nano` – Beginner-friendly text editor

```bash
nano file.txt
```

* Easy to use, shows shortcuts at bottom.
* Save: `CTRL+O`, Exit: `CTRL+X`.

---

### ✅ `vim` – Powerful text editor

```bash
vim file.txt
```

* Modes:

  * **Command mode** (default) → for navigation.
  * **Insert mode** → press `i` to edit.
  * **Save & quit** → `:wq`
  * **Quit without saving** → `:q!`

---

### ✅ `gedit` – GUI text editor

```bash
gedit file.txt
```

* Graphical editor for desktop Linux environments.

---

## **3. Use Cases**

### 📑 **Viewing Logs**

```bash
tail -f /var/log/syslog
```

* Continuously monitor system log in real time.

---

### 📝 **Quick Config File Edit**

```bash
nano filename
````

* Opens an existing file or creates a new one.
* Example:

```bash
nano notes.txt
```

---

## ** Basic Controls**

* `CTRL + O` → Save (Write Out)
* `CTRL + X` → Exit nano
* `CTRL + R` → Insert another file into current file
* `CTRL + W` → Search for text
* `CTRL + K` → Cut selected line
* `CTRL + U` → Paste (Uncut) line
* `CTRL + J` → Justify (format text)
* `CTRL + G` → Show help menu

👉 **Tip**: All commands are shown at the bottom of the editor screen.

---

## ** Editing Text**

* Start typing directly after opening the file.
* Use **Arrow Keys** to move around.
* To **insert a new line**, press `Enter`.

---

## ** Saving & Exiting**

* `CTRL + O` → Save changes

  * Press `Enter` to confirm filename.
* `CTRL + X` → Exit

  * If changes are unsaved, it will prompt:

    * `Y` → Save before exit
    * `N` → Exit without saving
    * `CTRL + C` → Cancel exit

---

## ** Searching & Replacing**

* `CTRL + W` → Search for text
* Type the keyword → Press `Enter`
* `CTRL + \` → Search & Replace

  * Enter search term
  * Enter replacement term
  * Confirm with `Y` or skip with `N`

---

## ** Cutting, Copying & Pasting**

* `CTRL + K` → Cut (removes current line)
* `CTRL + U` → Paste (uncut text)
* `ALT + 6` → Copy current line (without cutting)

---

## ** Navigation Shortcuts**

* `CTRL + A` → Move to beginning of line
* `CTRL + E` → Move to end of line
* `CTRL + Y` → Page up
* `CTRL + V` → Page down
* `CTRL + _` → Jump to a specific line number

---

## ** Common Use Cases**

✅ **Edit Config Files**

```bash
sudo nano /etc/hosts
```

✅ **Quick Script Editing**

```bash
nano deploy.sh
```


### ⚡ **Large File Analysis**

```bash
less /var/log/messages
```

* Navigate large log files without loading entire file into memory.

---

### 🛠️ **Monitoring Application Logs**

```bash
tail -n 100 -f /opt/app/logs/app.log
```

### **Viewing Files**
```bash
cat [options] [file...]
````

### **Common Options**

* `cat file.txt` → Display file content.
* `cat -n file.txt` → Show line numbers.
* `cat -b file.txt` → Show line numbers (non-blank only).
* `cat -s file.txt` → Squeeze multiple blank lines into one.

---

### **Use Cases**

✅ **View File Contents**

```bash
cat notes.txt
```

✅ **View Multiple Files Together**

```bash
cat file1.txt file2.txt
```

* Prints both files in sequence.

✅ **Create a New File**

```bash
cat > newfile.txt
```

(Type content → press `CTRL+D` to save & exit)

✅ **Append Data to a File**

```bash
cat >> existing.txt
```

(Add text → press `CTRL+D`)

✅ **Redirect Output to Another File**

```bash
cat file1.txt > file2.txt
```

* Overwrites `file2.txt` with `file1.txt`.

✅ **Combine Files**

```bash
cat file1.txt file2.txt > merged.txt
```

✅ **Numbered Display**

```bash
cat -n script.sh
```

* Displays line numbers.

---

---

## **2. `vim` Command (Vi IMproved Editor)**

`vim` is a **powerful text editor** that extends the classic `vi`.
It is widely used for editing **configuration files, scripts, and code**.

### **Launch vim**

```bash
vim filename
```

* Opens an existing file or creates a new one.

---

### **Modes in vim**

Vim operates in different modes:

1. **Normal Mode** (default)

   * For navigation & commands.
   * Press `Esc` to return here.

2. **Insert Mode**

   * For inserting/editing text.
   * Enter by pressing `i`, `a`, or `o`.

3. **Command Mode**

   * For saving, quitting, searching.
   * Access by pressing `:` in normal mode.

---

### **Basic Navigation**

* `h` → Move left
* `l` → Move right
* `j` → Move down
* `k` → Move up
* `:set number` → Show line numbers
* `:set nonumber` → Hide line numbers

---

### **Insert Text**

* `i` → Insert at cursor
* `a` → Insert after cursor
* `o` → Open new line below
* `O` → Open new line above

---

### **Save & Exit**

* `:w` → Save (write changes)
* `:q` → Quit
* `:wq` or `ZZ` → Save & quit
* `:q!` → Quit without saving

---

### **Editing & Deleting**

* `x` → Delete character
* `dd` → Delete line
* `yy` → Copy (yank) line
* `p` → Paste after cursor
* `u` → Undo
* `CTRL+r` → Redo

---

### **Searching**

* `/word` → Search for `word` forward
* `?word` → Search backward
* `n` → Repeat search in same direction
* `N` → Repeat search in opposite direction

---

### **Replacing Text**

* `:s/old/new/` → Replace first match in line
* `:s/old/new/g` → Replace all matches in line
* `:%s/old/new/g` → Replace all matches in file
* `:%s/old/new/gc` → Replace with confirmation

---

### **Multiple Files in vim**

Open multiple files:

```bash
vim file1 file2
```

Switch between files:

* `:n` → Next file
* `:prev` → Previous file
* `:ls` → List open files
* `:e filename` → Open another file

---

### **Split Windows**

* `:split file.txt` → Horizontal split
* `:vsplit file.txt` → Vertical split
* `CTRL+w w` → Switch between windows
* `CTRL+w q` → Close current split

---

### **Use Cases**

✅ **Edit Config File**

```bash
sudo vim /etc/hosts
```

✅ **Edit a Script**

```bash
vim deploy.sh
```

✅ **Search & Replace in Code**

```bash
:%s/localhost/127.0.0.1/g
```

✅ **Multi-file Editing**

```bash
vim *.txt
```
---

## **4. Quick Comparison of File Tools**

| Command/Editor | Usage                            |
| -------------- | -------------------------------- |
| `cat`          | Show small files quickly         |
| `less`         | Scroll through large files       |
| `head`         | See first few lines              |
| `tail`         | See last few lines (follow logs) |
| `nano`         | Easy command-line editing        |
| `vim`          | Advanced, powerful editing       |
| `gedit`        | Simple GUI editing               |

---

# 📦 Archiving & Compression in Linux

Archiving and compression are used to **bundle multiple files into one** and/or **reduce file size**.  
Common tools: `tar`, `gzip`, `bzip2`, `xz`, `zip`, `unzip`.

---

## **1. `tar` (Tape Archive)**

The `tar` command is mainly used for **archiving multiple files/folders into a single file** (with or without compression).

### **Syntax**
```bash
tar [options] archive_name.tar files...
````

### **Options**

* `-c` → Create archive
* `-x` → Extract archive
* `-v` → Verbose (show progress)
* `-f` → File name
* `-z` → Use gzip compression
* `-j` → Use bzip2 compression
* `-J` → Use xz compression

---

### **Examples**

✅ **Create an archive (no compression)**

```bash
tar -cvf backup.tar file1.txt file2.txt dir1/
```

✅ **Extract an archive**

```bash
tar -xvf backup.tar
```

✅ **Create a gzip-compressed archive**

```bash
tar -czvf backup.tar.gz file1.txt file2.txt dir1/
```

✅ **Extract a gzip-compressed archive**

```bash
tar -xzvf backup.tar.gz
```

✅ **Create a bzip2-compressed archive**

```bash
tar -cjvf backup.tar.bz2 file1.txt file2.txt
```

✅ **Extract a bzip2 archive**

```bash
tar -xjvf backup.tar.bz2
```

✅ **Create an xz-compressed archive**

```bash
tar -cJvf backup.tar.xz dir1/
```

✅ **Extract an xz archive**

```bash
tar -xJvf backup.tar.xz
```

✅ **List contents of a tar archive**

```bash
tar -tvf backup.tar
```

---

## **2. gzip / gunzip**

`gzip` compresses files, while `gunzip` extracts them.
It works only on **single files**, not directories.

✅ **Compress a file**

```bash
gzip file.txt
```

* Output → `file.txt.gz`

✅ **Decompress a file**

```bash
gunzip file.txt.gz
```

✅ **Keep original file while compressing**

```bash
gzip -k file.txt
```

---

## **3. bzip2 / bunzip2**

`bzip2` provides **better compression** than `gzip` but is slower.

✅ **Compress**

```bash
bzip2 file.txt
```

* Output → `file.txt.bz2`

✅ **Decompress**

```bash
bunzip2 file.txt.bz2
```

---

## **4. xz / unxz**

`xz` provides **highest compression ratio** (better than gzip/bzip2).

✅ **Compress**

```bash
xz file.txt
```

* Output → `file.txt.xz`

✅ **Decompress**

```bash
unxz file.txt.xz
```

✅ **Keep original file**

```bash
xz -k file.txt
```

---

## **5. zip & unzip**

Unlike `gzip`, `zip` can **compress multiple files/folders** into one archive.

✅ **Compress files into zip**

```bash
zip archive.zip file1.txt file2.txt
```

✅ **Compress a directory**

```bash
zip -r project.zip project_folder/
```

✅ **Extract a zip file**

```bash
unzip archive.zip
```

✅ **List contents without extracting**

```bash
unzip -l archive.zip
```

---

## **6. Real-World Use Cases**

✅ **Backup a project directory**

```bash
tar -czvf project_backup.tar.gz /home/user/project/
```

✅ **Extract a software package**

```bash
tar -xzvf software.tar.gz
```

✅ **Compress logs before sending**

```bash
gzip access.log
```

✅ **Share project as zip (cross-platform)**

```bash
zip -r project.zip /home/user/project/
```

---

## **Cheat Sheet**

| Tool    | Best For                                                                 |
| ------- | ------------------------------------------------------------------------ |
| `tar`   | Archiving multiple files into one (with/without compression).            |
| `gzip`  | Fast single-file compression.                                            |
| `bzip2` | Better compression ratio, slower.                                        |
| `xz`    | Best compression ratio, slowest.                                         |
| `zip`   | Widely used, compresses multiple files/directories (Windows compatible). |

---

# ⚙️ Process Management in Linux

A **process** is a running instance of a program.  
Linux provides multiple commands to **view, control, and manage processes**.

---

## **1. Viewing Processes**

### 🔹 `ps` – Process Status
Shows running processes for the current user/session.

**Examples**
```bash
ps                # List processes in the current shell
ps -e             # List all processes
ps -f             # Full format (UID, PID, PPID, start time, etc.)
ps -ef            # List all processes in full format
ps aux            # Show all processes (BSD style)
````

---

### 🔹 `top` – Real-Time Process Monitoring

Interactive tool to monitor CPU/memory usage of processes.

**Examples**

```bash
top               # Open real-time process view
top -u username   # Show processes of a specific user
```

Controls inside `top`:

* `q` → quit
* `k` → kill a process
* `h` → help
* `M` → sort by memory usage
* `P` → sort by CPU usage

---

### 🔹 `htop` – Improved `top` (if installed)

Colorful, interactive process viewer (easier than `top`).

```bash
htop
```

---

### 🔹 `pgrep` – Search for Processes

Finds PIDs by process name.

**Examples**

```bash
pgrep firefox      # Find PID(s) of firefox
pgrep -u user1     # List processes owned by a user
```

---

## **2. Managing Processes**

### 🔹 `kill` – Terminate Process by PID

Sends a signal to a process (default: `SIGTERM`).

**Examples**

```bash
kill 1234           # Kill process with PID 1234
kill -9 1234        # Force kill (SIGKILL)
kill -15 1234       # Graceful stop (SIGTERM)
```

---

### 🔹 `pkill` – Kill by Process Name

Kills processes by name instead of PID.

**Examples**

```bash
pkill firefox       # Kill all firefox processes
pkill -u user1      # Kill all processes of user1
```

---

### 🔹 `jobs` – List Background Jobs

Shows jobs started in the current terminal.

```bash
jobs
```

---

### 🔹 `fg` – Bring Job to Foreground

```bash
fg %1
```

(Brings job ID 1 to foreground)

---

### 🔹 `bg` – Resume Job in Background

```bash
bg %1
```

---

### 🔹 `nice` & `renice` – Process Priority

Processes have a **priority value (niceness)** from **-20 (highest priority) to 19 (lowest priority)**.

**Examples**

```bash
nice -n 10 ./script.sh   # Start script with lower priority
renice -n -5 -p 1234     # Change priority of PID 1234 to -5
```

---

## **3. Process States**

* **R** → Running
* **S** → Sleeping (waiting for event)
* **D** → Uninterruptible sleep (usually I/O)
* **T** → Stopped (paused)
* **Z** → Zombie (terminated but not cleaned)

---

## **4. Real-World Use Cases**

✅ **Find and kill a process using name**

```bash
pgrep -f "python app.py"
kill -9 <PID>
```

✅ **Check memory-hungry processes**

```bash
top -o %MEM
```

✅ **Run a process in the background**

```bash
./long_script.sh &
```

✅ **Check background jobs and bring one back**

```bash
jobs
fg %2
```

✅ **Start a program with low CPU priority**

```bash
nice -n 15 tar -czf backup.tar.gz /home/user/
```

---

## **Cheat Sheet**

| Command  | Purpose                             |
| -------- | ----------------------------------- |
| `ps`     | Show running processes              |
| `top`    | Real-time monitoring                |
| `htop`   | Interactive monitoring (better top) |
| `pgrep`  | Find PID by name                    |
| `kill`   | Kill by PID                         |
| `pkill`  | Kill by name                        |
| `jobs`   | Show background jobs                |
| `fg`     | Bring job to foreground             |
| `bg`     | Resume job in background            |
| `nice`   | Start with priority                 |
| `renice` | Change priority of running process  |

---
# 💾 Disk & Storage Management in Ubuntu (Complete Industry-Level Guide)

---

# 1️⃣ Storage Fundamentals

## 1.1 What is Disk Storage?

Storage devices are physical or virtual components that store data permanently.

### Types of Storage Devices

![Image](https://www.tpstech.in/cdn/shop/products/ToshibaN3004TBNAS3.5-inchInternalHardDiskDrive-FromTPSTech-06.jpg?v=1633942947\&width=1445)

![Image](https://images.openai.com/static-rsc-3/ddYbtiiyojDmEiTThfB7e7gLqCZOg8SyvC5qbnRTSuW-S6wW4rdV5-VEgS3hPfkCNPtbCoAvW_TqVsCr5uVmmbbKYIogkR344U42ShdMlRg?purpose=fullsize\&v=1)

![Image](https://m.media-amazon.com/images/I/91NqHZmJPsL.jpg)

![Image](https://m.media-amazon.com/images/I/51qcc-MJ1nL.jpg)

| Type     | Description   | Speed     | Usage              |
| -------- | ------------- | --------- | ------------------ |
| HDD      | Magnetic disk | Slow      | Backup, archival   |
| SSD      | Flash storage | Fast      | OS, Applications   |
| NVMe     | PCIe SSD      | Very Fast | Production servers |
| External | USB storage   | Depends   | Portable storage   |

---

# 2️⃣ Understanding Linux Storage Architecture

## 2.1 Storage Stack

```
Physical Disk
   ↓
Partition
   ↓
Filesystem
   ↓
Mount Point
   ↓
Directory Structure
```

---

# 3️⃣ Important Disk Commands (Must Know)

| Command   | Purpose                     |
| --------- | --------------------------- |
| `lsblk`   | List block devices          |
| `fdisk`   | Manage partitions           |
| `parted`  | Advanced partitioning       |
| `df`      | Disk usage                  |
| `du`      | Directory usage             |
| `mount`   | Mount filesystem            |
| `umount`  | Unmount filesystem          |
| `blkid`   | Show UUID                   |
| `mkfs`    | Create filesystem           |
| `fsck`    | Filesystem check            |
| `tune2fs` | Modify ext filesystem       |
| `wipefs`  | Remove filesystem signature |

---

# 4️⃣ Listing Disks & Partitions

## 4.1 lsblk (Industry Standard)

```bash
lsblk
lsblk -f
lsblk -o NAME,SIZE,FSTYPE,MOUNTPOINT
```

Output Example:

```
sda      100G
├─sda1    1G   ext4   /boot
├─sda2   50G   ext4   /
└─sda3   49G   ext4   /data
```

---

## 4.2 Check Disk Usage

```bash
df -h
df -Th
```

### Difference:

| Command | Usage            |
| ------- | ---------------- |
| df      | Filesystem usage |
| du      | Directory usage  |

```bash
du -sh /var/log
du -h --max-depth=1 /
```

---

# 5️⃣ Disk Partitioning (Beginner → Advanced)

## 5.1 Using fdisk (MBR Based)

```bash
sudo fdisk /dev/sdb
```

Inside fdisk:

| Option | Action           |
| ------ | ---------------- |
| n      | New partition    |
| d      | Delete partition |
| p      | Print            |
| w      | Write changes    |
| q      | Quit             |

---

## 5.2 Using parted (GPT Recommended)

```bash
sudo parted /dev/sdb
```

Commands inside:

```
mklabel gpt
mkpart primary ext4 1MiB 100%
print
quit
```

---

# 6️⃣ Creating Filesystem

## 6.1 ext4 (Most Common in Ubuntu)

```bash
sudo mkfs.ext4 /dev/sdb1
```

## 6.2 XFS (Enterprise)

```bash
sudo mkfs.xfs /dev/sdb1
```

---

# 7️⃣ Mounting Filesystem

## 7.1 Temporary Mount

```bash
sudo mkdir /data
sudo mount /dev/sdb1 /data
```

Verify:

```bash
df -h
```

---

## 7.2 Permanent Mount (Production Level)

Get UUID:

```bash
sudo blkid
```

Edit:

```bash
sudo nano /etc/fstab
```

Add:

```
UUID=xxxx-xxxx  /data  ext4  defaults  0  2
```

Test:

```bash
sudo mount -a
```

---

# 8️⃣ Filesystem Types in Ubuntu

![Image](https://opensource.com/sites/default/files/images/life-uploads/inodesanddataallocation-01_0.png)

![Image](https://images.wondershare.com/recoverit/article/xfs-file-system-structure.jpg)

![Image](https://www.researchgate.net/publication/316994448/figure/fig1/AS%3A669542586003474%401536642800213/Figure-23-The-NTFS-file-Structure.png)

![Image](https://ntfs.com/images/screenshots/NTFS-MFT-structure.gif)

| Filesystem | Use Case              |
| ---------- | --------------------- |
| ext4       | Default Ubuntu        |
| XFS        | Large storage servers |
| NTFS       | Windows compatibility |
| swap       | Virtual memory        |

---

# 9️⃣ Swap Management

Check swap:

```bash
swapon --show
free -h
```

Create swap file:

```bash
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
```

Add to fstab:

```
/swapfile none swap sw 0 0
```

---

# 🔟 LVM (Logical Volume Manager) – Advanced

## Why LVM?

* Resize storage online
* Flexible volume management
* Enterprise usage

---

## LVM Architecture

![Image](https://miro.medium.com/v2/resize%3Afit%3A1400/1%2Ag0H1kb7u6ZAQ-vObWEY1EA.png)

![Image](https://access.redhat.com/webassets/avalon/d/Red_Hat_Enterprise_Linux-7-Logical_Volume_Manager_Administration-en-US/images/aa96fde158c47229d69b70d319d41677/basic-lvm-volume.png)

![Image](https://access.redhat.com/webassets/avalon/d/Red_Hat_Enterprise_Linux-9-Configuring_and_managing_logical_volumes-en-US/images/31bd96635c4120abe3e771a423f61cd6/basic-lvm-volume-components.png)

![Image](https://www.redhat.com/rhdc/managed-files/sysadmin/2020-03/basic-lvm-volume_0.png)

### Layers:

| Layer | Meaning         |
| ----- | --------------- |
| PV    | Physical Volume |
| VG    | Volume Group    |
| LV    | Logical Volume  |

---

## Create LVM Step-by-Step

### Step 1: Create PV

```bash
sudo pvcreate /dev/sdb1
```

### Step 2: Create VG

```bash
sudo vgcreate data_vg /dev/sdb1
```

### Step 3: Create LV

```bash
sudo lvcreate -L 10G -n data_lv data_vg
```

### Step 4: Create Filesystem

```bash
sudo mkfs.ext4 /dev/data_vg/data_lv
```

### Step 5: Mount

```bash
sudo mount /dev/data_vg/data_lv /data
```

---

# 1️⃣1️⃣ Resize Disk (Production Scenario)

## Extend Logical Volume

```bash
sudo lvextend -L +5G /dev/data_vg/data_lv
sudo resize2fs /dev/data_vg/data_lv
```

---

# 1️⃣2️⃣ Disk Troubleshooting

| Issue              | Command         |
| ------------------ | --------------- |
| Disk full          | `df -h`         |
| Large files        | `du -sh *`      |
| Filesystem error   | `fsck`          |
| Corrupt superblock | `fsck -b 32768` |

---

# 1️⃣3️⃣ Real Production Use Case (Step-by-Step)

## 🎯 Scenario:

Add new 100GB disk to Ubuntu server for application data.

---

### Step 1: Verify Disk

```bash
lsblk
```

---

### Step 2: Partition Disk

```bash
sudo parted /dev/sdb
mklabel gpt
mkpart primary ext4 0% 100%
quit
```

---

### Step 3: Create Filesystem

```bash
sudo mkfs.ext4 /dev/sdb1
```

---

### Step 4: Create Mount Directory

```bash
sudo mkdir /appdata
```

---

### Step 5: Mount Disk

```bash
sudo mount /dev/sdb1 /appdata
```

---

### Step 6: Permanent Mount

```bash
sudo blkid
sudo nano /etc/fstab
```

Add:

```
UUID=xxxx /appdata ext4 defaults 0 2
```

---

### Step 7: Set Ownership (Production Important)

```bash
sudo chown appuser:appgroup /appdata
sudo chmod 755 /appdata
```

---

# 1️⃣4️⃣ Interview Questions

### Beginner

* What is difference between df and du?
* What is mount point?
* What is swap?

### Intermediate

* Difference between MBR & GPT?
* What is UUID?
* How to extend LVM?

### Advanced

* How to recover corrupted filesystem?
* How to troubleshoot disk full in production?
* How to migrate disk without downtime?

---

# 1️⃣5️⃣ Production Best Practices

✅ Always use UUID in fstab
✅ Prefer GPT over MBR
✅ Use LVM in production
✅ Monitor disk using `df -h`
✅ Keep separate partitions for:

* `/`
* `/var`
* `/home`
* `/data`

---

# 1️⃣6️⃣ Quick Revision Sheet

```bash
lsblk
df -h
du -sh *
sudo fdisk /dev/sdb
sudo mkfs.ext4 /dev/sdb1
sudo mount /dev/sdb1 /data
sudo blkid
sudo nano /etc/fstab
```

---
