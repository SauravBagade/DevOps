# 🟢 1️⃣ Introduction to Shell 

---

# 1.1 What is an Operating System (OS)?

An **Operating System (OS)** is system software that manages computer hardware and software resources and provides services for programs.

### ✅ Main Responsibilities of OS:

* Process management
* Memory management
* File system management
* Device management
* Security & user management

### ✅ Examples of Operating Systems:

* Linux
* Windows
* macOS
* Unix

### Simple Definition:

> OS is the middle layer between **User** and **Hardware**.

Without an OS, you cannot use a computer effectively.

---

# 1.2 What is Kernel?

The **Kernel** is the core part of the Operating System.

It directly interacts with:

* CPU
* Memory (RAM)
* Disk
* Devices

### ✅ Kernel Responsibilities:

* Process scheduling
* Memory allocation
* Device communication
* System calls handling

### Flow:

User → Shell → Kernel → Hardware

The kernel is always running in the background.

---

# 1.3 What is Shell?

A **Shell** is a program that allows users to interact with the operating system.

It acts as a bridge between:

* User
* Kernel

When you type a command:

1. Shell reads the command
2. Shell sends it to Kernel
3. Kernel executes it
4. Output returns to Shell
5. Shell displays output to user

### Example:

```
ls
```

Shell sends this command to kernel → kernel reads directory → output displayed.

---

# 1.4 Types of Shell

Different shells provide different features.

### 1️⃣ sh (Bourne Shell)

* Oldest Unix shell
* Basic scripting support
* Limited features

### 2️⃣ bash (Bourne Again Shell)

* Most widely used shell
* Default in most Linux systems
* Advanced scripting features

### 3️⃣ ksh (Korn Shell)

* Improved version of sh
* Used in enterprise Unix systems

### 4️⃣ zsh (Z Shell)

* Advanced interactive shell
* Powerful auto-completion
* Popular among developers

---

# 1.5 What is Bash?

**Bash (Bourne Again Shell)** is:

* Default shell in most Linux distributions
* Open-source
* Powerful scripting language
* Backward compatible with sh

### Why Bash is Popular?

* Easy syntax
* Automation friendly
* DevOps compatible
* Works with Linux servers
* Used in CI/CD pipelines

---

# 1.6 Shell vs Terminal vs CLI

Many beginners confuse these terms.

### 🔹 Terminal

A program that opens a command interface window.

Examples:

* GNOME Terminal
* Windows Terminal
* macOS Terminal

### 🔹 Shell

The program running inside the terminal that executes commands.

Example:

* bash
* zsh

### 🔹 CLI (Command Line Interface)

The method of interacting with computer using text commands.

### Simple Understanding:

Terminal → Opens → Shell → Accepts → CLI commands

---

# 1.7 Why Shell Scripting is Important?

Shell scripting allows automation of tasks.

### Without Shell:

You must manually execute commands.

### With Shell Script:

You write once → run many times.

---

### Real Benefits:

✅ Automation
✅ Saves time
✅ Reduces human error
✅ Essential in DevOps
✅ Server management
✅ Log analysis
✅ Backup automation
✅ Deployment automation

---

# 1.8 Real-World Use Cases

### 🔹 System Administration

* User creation
* Backup scripts
* Disk monitoring

### 🔹 DevOps

* Docker container automation
* CI/CD pipelines
* Deployment scripts

### 🔹 Cloud Automation

* AWS CLI automation
* EC2 instance management
* Infrastructure setup

### 🔹 Monitoring

* CPU monitoring script
* Memory alert script
* Log analyzer

---

# 🟢 2️⃣ Shell Execution & Environment 

---

# 2.1 Login vs Non-Login Shell

When you open a shell, it can start in different modes.

## 🔹 Login Shell

A login shell starts when you:

* Log into a system (SSH)
* Log in through console
* Start a new login session

It reads specific startup files like:

* `/etc/profile`
* `~/.bash_profile`
* `~/.profile`

### Example:

```bash
ssh user@server
```

This starts a login shell.

---

## 🔹 Non-Login Shell

A non-login shell starts when:

* You open a terminal inside GUI
* You open a new tab
* You run a script

It usually reads:

* `~/.bashrc`

---

### 🔥 Important Difference

| Login Shell           | Non-Login Shell               |
| --------------------- | ----------------------------- |
| Reads `.bash_profile` | Reads `.bashrc`               |
| Used for full session | Used for interactive terminal |

---

# 2.2 Interactive vs Non-Interactive Shell

## 🔹 Interactive Shell

* Takes user input
* Shows prompt
* Executes commands immediately

Example:

```bash
ls
cd /home
```

You type → shell responds.

---

## 🔹 Non-Interactive Shell

* Runs scripts
* No user input
* No prompt

Example:

```bash
./backup.sh
```

---

### Quick Comparison

| Type            | User Input | Prompt | Used For    |
| --------------- | ---------- | ------ | ----------- |
| Interactive     | Yes        | Yes    | Manual work |
| Non-Interactive | No         | No     | Automation  |

---

# 2.3 Shell Startup Files

When Bash starts, it reads configuration files.

## 🔹 `.bash_profile`

* Executed in login shell
* Used to set environment variables
* Usually calls `.bashrc`

## 🔹 `.bashrc`

* Executed in non-login interactive shell
* Used for aliases
* Functions
* Prompt customization

## 🔹 `.profile`

* Used in sh-compatible shells
* More generic

---

### Best Practice

Inside `.bash_profile`:

```bash
if [ -f ~/.bashrc ]; then
    . ~/.bashrc
fi
```

This ensures `.bashrc` runs in login shell too.

---

# 2.4 PATH Variable (Basic + Deep Explanation)

## What is PATH?

`PATH` is an environment variable that tells shell:

👉 Where to search for executable commands.

---

### Example:

When you type:

```bash
ls
```

Shell searches directories listed in `$PATH` to find `ls`.

---

### Check PATH

```bash
echo $PATH
```

Output example:

```
/usr/local/bin:/usr/bin:/bin:/usr/sbin
```

Each directory is separated by `:`.

---

### Add Custom Path

```bash
export PATH=$PATH:/home/user/scripts
```

Now you can run scripts without writing full path.

---

### Deep Understanding

If PATH does not contain the directory:

* Command not found error occurs.

---

# 2.5 Environment Variables

Environment variables:

* Store configuration values
* Available to child processes

Examples:

* HOME
* USER
* PATH
* SHELL

Check all variables:

```bash
env
```

---

# 2.6 Local vs Export Variables

## 🔹 Local Variable

```bash
name="Saurav"
```

Only available in current shell.

---

## 🔹 Export Variable

```bash
export name="Saurav"
```

Available in:

* Current shell
* Child processes
* Subshells

---

### Difference

| Type   | Visible in Subshell? |
| ------ | -------------------- |
| Local  | ❌ No                 |
| Export | ✅ Yes                |

---

# 2.7 Subshell Concept

A subshell is a child shell started by current shell.

Example:

```bash
( ls )
```

The command inside parentheses runs in subshell.

---

### Important Behavior

Changes inside subshell do NOT affect parent shell.

Example:

```bash
( cd /tmp )
pwd
```

Working directory will NOT change in parent.

---

# 2.8 Command Substitution

Used to capture command output into variable.

## Modern Syntax (Recommended)

```bash
var=$(date)
```

## Old Syntax (Backticks)

```bash
var=`date`
```

---

### Why $( ) is Better?

* Easy to nest
* More readable
* Modern standard

---

# 2.9 Process Substitution

Used to treat command output as file input.

Example:

```bash
diff <(ls dir1) <(ls dir2)
```

Shell creates temporary file descriptors.

---

# 2.10 Shell Options (`set`, `shopt`)

## 🔹 set Command

Controls shell behavior.

Examples:

```bash
set -e
set -u
set -x
```

| Option | Meaning                     |
| ------ | --------------------------- |
| -e     | Exit on error               |
| -u     | Error on undefined variable |
| -x     | Debug mode                  |

---

## 🔹 shopt Command

Controls bash-specific options.

Example:

```bash
shopt -s nullglob
```

Enable advanced shell features.

---

# 🟢 3️⃣ Getting Started 

---

# 3.1 Installing Bash (Linux / WSL / macOS)

## 🔹 On Linux

Most Linux distributions already have **Bash installed by default**.

Check version:

```bash
bash --version
```

If not installed:

### Ubuntu / Debian:

```bash
sudo apt update
sudo apt install bash
```

### RHEL / CentOS:

```bash
sudo yum install bash
```

---

## 🔹 On macOS

macOS already includes Bash.

Check:

```bash
bash --version
```

To install latest version (using Homebrew):

```bash
brew install bash
```

---

## 🔹 On Windows (Using WSL – Recommended)

Install **WSL (Windows Subsystem for Linux)**:

```powershell
wsl --install
```

Then install Ubuntu from Microsoft Store.

After installation:

```bash
bash --version
```

---

# 3.2 Writing First Shell Script

A shell script is a text file containing commands.

---

## Step 1: Create a file

```bash
touch first_script.sh
```

---

## Step 2: Open in editor

```bash
nano first_script.sh
```

---

## Step 3: Write code

```bash
#!/bin/bash
echo "Hello, World!"
```

---

## Step 4: Save and exit

---

## Step 5: Give execute permission

```bash
chmod +x first_script.sh
```

---

## Step 6: Run script

```bash
./first_script.sh
```

Output:

```
Hello, World!
```

---

# 3.3 Script Naming Standards

Good naming practice is very important in real-world environments.

## ✅ Naming Rules:

* Use lowercase letters
* Use `.sh` extension
* Avoid spaces
* Use underscore `_` if needed

### Good Examples:

* backup_script.sh
* deploy_app.sh
* monitor_cpu.sh

### ❌ Bad Examples:

* My Script.sh
* script 1.sh
* test

---

# 3.4 Shebang (`#!/bin/bash`)

Shebang is the first line in a script.

```bash
#!/bin/bash
```

It tells the system:

👉 Which interpreter should execute this script.

---

### How It Works

When you run:

```bash
./script.sh
```

System reads first line → launches `/bin/bash` → executes script.

---

### Alternative (Portable Method)

```bash
#!/usr/bin/env bash
```

This finds bash in system PATH.

Recommended in production.

---

# 3.5 File Permissions (`chmod`)

Linux follows permission model:

* Read (r)
* Write (w)
* Execute (x)

---

## Check permissions:

```bash
ls -l script.sh
```

Example:

```
-rw-r--r-- 1 user user 1200 script.sh
```

---

## Make file executable:

```bash
chmod +x script.sh
```

---

## Numeric Mode (Advanced)

```bash
chmod 755 script.sh
```

Meaning:

| Number | Permission |
| ------ | ---------- |
| 7      | rwx        |
| 5      | r-x        |
| 5      | r-x        |

---

# 3.6 Running Script Methods

There are multiple ways to run a script.

---

## Method 1 (Recommended)

```bash
./script.sh
```

Requires execute permission.

---

## Method 2

```bash
bash script.sh
```

Does NOT require execute permission.

---

## Method 3

```bash
sh script.sh
```

⚠ Might not support bash-specific features.

---

## Method 4 (Absolute Path)

```bash
/home/user/script.sh
```

---

# 3.7 Common Beginner Errors

### ❌ Permission Denied

Cause:

* No execute permission

Fix:

```bash
chmod +x script.sh
```

---

### ❌ Command Not Found

Cause:

* Script not in PATH
* Missing `./`

Fix:

```bash
./script.sh
```

---

### ❌ Bad Interpreter Error

Example:

```
/bin/bash^M: bad interpreter
```

Cause:

* Windows line endings

Fix:

```bash
dos2unix script.sh
```

---

### ❌ Syntax Error

Cause:

* Missing quotes
* Missing fi
* Missing done

Use debug:

```bash
bash -x script.sh
```

---

# 🟢 4️⃣ Basic Linux Commands 

These commands are the foundation of **Shell Scripting + DevOps + Linux Administration**.

---

# 4.1 `echo`

Used to print output on terminal.

```bash
echo "Hello World"
```

### Use Cases:

* Print messages
* Debug scripts
* Print variable values

Example:

```bash
name="Saurav"
echo $name
```

---

# 4.2 `pwd` (Print Working Directory)

Shows current directory.

```bash
pwd
```

Output:

```
/home/saurav
```

---

# 4.3 `ls`

Lists files and directories.

```bash
ls
```

### Useful Options:

```bash
ls -l      # Long listing
ls -a      # Show hidden files
ls -lh     # Human readable sizes
ls -la     # Combined
```

---

# 4.4 `cd` (Change Directory)

Move between directories.

```bash
cd /home
cd ..
cd ~
cd -
```

| Command | Meaning            |
| ------- | ------------------ |
| `cd ..` | Go back one level  |
| `cd ~`  | Go to home         |
| `cd -`  | Previous directory |

---

# 4.5 `cat`

Displays file content.

```bash
cat file.txt
```

### Create file using cat:

```bash
cat > file.txt
```

Press `CTRL + D` to save.

---

# 4.6 `touch`

Creates empty file.

```bash
touch test.txt
```

Also updates timestamp.

---

# 4.7 `mkdir`

Creates directory.

```bash
mkdir myfolder
```

Create nested directories:

```bash
mkdir -p project/app/logs
```

---

# 4.8 `rm`

Deletes files or directories.

```bash
rm file.txt
rm -r folder
rm -rf folder
```

⚠ `-rf` is dangerous (force delete).

---

# 4.9 `cp`

Copy files or directories.

```bash
cp file1.txt file2.txt
cp -r folder1 folder2
```

---

# 4.10 `mv`

Move or rename files.

```bash
mv old.txt new.txt
mv file.txt /home/user/
```

---

# 4.11 `head`

Shows first 10 lines of file.

```bash
head file.txt
```

Custom lines:

```bash
head -5 file.txt
```

---

# 4.12 `tail`

Shows last 10 lines.

```bash
tail file.txt
```

Live log monitoring:

```bash
tail -f logfile.log
```

Very important in DevOps.

---

# 4.13 `less`

Used to view large files page by page.

```bash
less file.txt
```

Navigation:

* Space → Next page
* q → Quit
* / → Search

---

# 4.14 `find`

Search files.

```bash
find /home -name file.txt
```

Search by type:

```bash
find . -type f
find . -type d
```

---

# 4.15 `locate`

Faster file search (uses database).

```bash
locate file.txt
```

If not working:

```bash
sudo updatedb
```

---

# 📌 Important Beginner Concept

All Linux commands follow this pattern:

```
command [options] [arguments]
```

Example:

```
ls -l /home
```

* `ls` → command
* `-l` → option
* `/home` → argument

---

# 🟢 5️⃣ Variables & Parameters 

Variables are the **most important concept in shell scripting**.

Without variables → No automation
With variables → Dynamic scripts

---

# 5.1 Defining Variables

In Bash, variables are defined like this:

```bash
name="Saurav"
age=25
```

⚠ **Important Rule:**

* No space before or after `=`

❌ Wrong:

```bash
name = "Saurav"
```

---

### Access Variable

```bash
echo $name
```

or

```bash
echo ${name}
```

Both are valid.

---

# 5.2 Variable Naming Rules

### ✅ Allowed:

* Letters (a-z, A-Z)
* Numbers (0-9)
* Underscore (_)

### ❌ Not Allowed:

* Space
* Special characters
* Starting with number

---

### ✅ Good Examples:

```bash
user_name="admin"
file_count=10
```

### ❌ Bad Examples:

```bash
1name="test"
user-name="admin"
```

---

# 5.3 Read User Input

Use `read` command.

```bash
echo "Enter your name:"
read name
echo "Hello $name"
```

---

### Read silently (for passwords)

```bash
read -s password
```

---

### Read with prompt

```bash
read -p "Enter username: " username
```

---

# 5.4 Command Line Arguments

Arguments are passed when running script.

Example:

```bash
./script.sh Saurav 25
```

---

Inside script:

```bash
echo $1   # First argument
echo $2   # Second argument
```

---

### Example Script:

```bash
#!/bin/bash
echo "Name: $1"
echo "Age: $2"
```

Run:

```bash
./script.sh Saurav 25
```

---

# 5.5 Special Variables

These are built-in variables.

| Variable | Meaning                    |
| -------- | -------------------------- |
| `$0`     | Script name                |
| `$1`     | First argument             |
| `$#`     | Number of arguments        |
| `$@`     | All arguments              |
| `$?`     | Last command exit status   |
| `$$`     | Current process ID         |
| `$!`     | Last background process ID |

---

### Example:

```bash
echo "Script Name: $0"
echo "Total Arguments: $#"
echo "All Arguments: $@"
```

---

### `$?` Example

```bash
ls file.txt
echo $?
```

If file exists → `0`
If error → non-zero value

0 = Success
Non-zero = Error

Very important in DevOps.

---

# 5.6 Default Values

You can provide default value if variable is empty.

```bash
echo ${name:-"Guest"}
```

Meaning:
If `name` is empty → print Guest.

---

### Assign Default

```bash
name=${name:-"Guest"}
```

---

# 5.7 Parameter Expansion (Powerful Feature)

Parameter expansion modifies variables.

---

### Remove Prefix

```bash
file="backup.tar.gz"
echo ${file#backup.}
```

Output:

```
tar.gz
```

---

### Remove Suffix

```bash
echo ${file%.gz}
```

Output:

```
backup.tar
```

---

### Replace String

```bash
name="Saurav Bagade"
echo ${name/Bagade/Kumar}
```

Output:

```
Saurav Kumar
```

---

### Length of Variable

```bash
echo ${#name}
```

Returns character count.

---

# 🔥 Important Concept

Difference between:

```bash
echo $var
echo "$var"
```

Always use double quotes in scripts:

```bash
echo "$var"
```

Why?

Because it:

* Prevents word splitting
* Prevents glob expansion
* Avoids unexpected bugs

---

# 🟢 6️⃣ Operators – Arithmetic, Relational, Boolean, String & File Tests

Operators allow you to perform:

* Calculations
* Comparisons
* Logical decisions
* File checks

They are mainly used inside:

```bash
if
while
[[ ]]
(( ))
```

---

# 6.1 Arithmetic Operators

Used for mathematical calculations.

## Method 1 (Recommended – Modern)

```bash
(( result = 10 + 5 ))
echo $result
```

---

## Method 2

```bash
result=$((10 + 5))
echo $result
```

---

## Available Arithmetic Operators

| Operator | Meaning        |
| -------- | -------------- |
| `+`      | Addition       |
| `-`      | Subtraction    |
| `*`      | Multiplication |
| `/`      | Division       |
| `%`      | Modulus        |
| `++`     | Increment      |
| `--`     | Decrement      |

---

### Example:

```bash
a=10
b=3

echo $((a + b))
echo $((a - b))
echo $((a * b))
echo $((a / b))
echo $((a % b))
```

---

# 6.2 Relational Operators (Numeric Comparison)

Used to compare numbers.

Used inside:

```bash
[ ]
```

---

| Operator | Meaning          |
| -------- | ---------------- |
| `-eq`    | Equal            |
| `-ne`    | Not equal        |
| `-gt`    | Greater than     |
| `-lt`    | Less than        |
| `-ge`    | Greater or equal |
| `-le`    | Less or equal    |

---

### Example:

```bash
a=10
b=20

if [ $a -lt $b ]; then
    echo "a is smaller"
fi
```

---

# 6.3 Boolean Operators

Used for logical conditions.

---

| Operator | Meaning |   |    |
| -------- | ------- | - | -- |
| `&&`     | AND     |   |    |
| `        |         | ` | OR |
| `!`      | NOT     |   |    |

---

### Example:

```bash
age=25
salary=50000

if [[ $age -gt 18 && $salary -gt 30000 ]]; then
    echo "Eligible"
fi
```

---

# 6.4 String Operators

Used to compare strings.

---

| Operator | Meaning             |
| -------- | ------------------- |
| `=`      | Equal               |
| `!=`     | Not equal           |
| `-z`     | String is empty     |
| `-n`     | String is not empty |

---

### Example:

```bash
name="Saurav"

if [ "$name" = "Saurav" ]; then
    echo "Match"
fi
```

---

### Check Empty String

```bash
if [ -z "$name" ]; then
    echo "Empty"
fi
```

---

# 6.5 File Test Operators

Very important in real-world scripting.

Used to check file/directory properties.

---

| Operator | Meaning                |
| -------- | ---------------------- |
| `-f`     | File exists            |
| `-d`     | Directory exists       |
| `-e`     | File exists (any type) |
| `-r`     | Readable               |
| `-w`     | Writable               |
| `-x`     | Executable             |
| `-s`     | File not empty         |

---

### Example:

```bash
if [ -f "file.txt" ]; then
    echo "File exists"
fi
```

---

### Check Directory:

```bash
if [ -d "/home/user" ]; then
    echo "Directory exists"
fi
```

---

# 6.6 `[[ ]]` vs `[ ]`

This is a very important concept.

---

## `[ ]` → Traditional Test Command

Older syntax.

```bash
if [ $a -lt 10 ]; then
    echo "Small"
fi
```

Limitations:

* Word splitting issues
* Must quote variables carefully

---

## `[[ ]]` → Modern Bash Test

Recommended for Bash scripts.

```bash
if [[ $a -lt 10 ]]; then
    echo "Small"
fi
```

Advantages:

* Safer
* Supports pattern matching
* No need for heavy quoting

---

### Example Pattern Matching

```bash
name="Saurav"

if [[ $name == S* ]]; then
    echo "Starts with S"
fi
```

---

# 🔥 Important Best Practice

Always prefer:

```bash
[[ condition ]]
```

instead of:

```bash
[ condition ]
```

In production Bash scripts.

---

# 🟢 7️⃣ Conditional Statements – if, elif, case, Pattern Matching

Conditionals allow your script to **make decisions**.

Without condition → Script runs line by line.
With condition → Script becomes intelligent.

---

# 7.1 `if` Statement

Basic syntax:

```bash
if [[ condition ]]; then
    commands
fi
```

---

### Example:

```bash
age=20

if [[ $age -ge 18 ]]; then
    echo "You are eligible to vote"
fi
```

If condition is true → block executes.

---

# 7.2 `if-else`

Used when you need two possible outcomes.

```bash
if [[ condition ]]; then
    commands_if_true
else
    commands_if_false
fi
```

---

### Example:

```bash
number=10

if [[ $number -gt 0 ]]; then
    echo "Positive"
else
    echo "Negative or Zero"
fi
```

---

# 7.3 `if-elif-else`

Used when there are multiple conditions.

```bash
if [[ condition1 ]]; then
    commands1
elif [[ condition2 ]]; then
    commands2
else
    commands3
fi
```

---

### Example:

```bash
marks=75

if [[ $marks -ge 90 ]]; then
    echo "Grade A"
elif [[ $marks -ge 60 ]]; then
    echo "Grade B"
else
    echo "Grade C"
fi
```

---

# 7.4 Nested `if`

You can place an `if` inside another `if`.

```bash
if [[ condition1 ]]; then
    if [[ condition2 ]]; then
        commands
    fi
fi
```

---

### Example:

```bash
age=25
country="India"

if [[ $age -ge 18 ]]; then
    if [[ $country == "India" ]]; then
        echo "Eligible Indian voter"
    fi
fi
```

---

⚠ Avoid too many nested ifs → Makes script complex.

---

# 7.5 `case` Statement

Used when checking multiple fixed values.

Better alternative to many `elif`.

---

## Syntax:

```bash
case $variable in
    value1)
        commands
        ;;
    value2)
        commands
        ;;
    *)
        default_commands
        ;;
esac
```

---

### Example:

```bash
day="Monday"

case $day in
    Monday)
        echo "Start of week"
        ;;
    Friday)
        echo "Weekend coming"
        ;;
    *)
        echo "Normal day"
        ;;
esac
```

---

# 7.6 Pattern Matching

Bash supports wildcard pattern matching.

Used inside:

```bash
[[ ]]
case
```

---

## Wildcards

| Pattern | Meaning          |
| ------- | ---------------- |
| `*`     | Any characters   |
| `?`     | Single character |
| `[abc]` | Match a, b, or c |
| `[a-z]` | Match range      |

---

### Example 1 – Starts With

```bash
name="Saurav"

if [[ $name == S* ]]; then
    echo "Starts with S"
fi
```

---

### Example 2 – Ends With

```bash
file="backup.tar.gz"

if [[ $file == *.gz ]]; then
    echo "Gzip file"
fi
```

---

### Example 3 – Using `case` with pattern

```bash
file="test.sh"

case $file in
    *.sh)
        echo "Shell Script"
        ;;
    *.txt)
        echo "Text File"
        ;;
    *)
        echo "Unknown type"
        ;;
esac
```

---

# 🔥 Important Real-World Use Cases

### 1️⃣ Check if file exists

```bash
if [[ -f "config.txt" ]]; then
    echo "File found"
else
    echo "File missing"
fi
```

---

### 2️⃣ Validate user input

```bash
read -p "Enter age: " age

if [[ $age -lt 18 ]]; then
    echo "Minor"
else
    echo "Adult"
fi
```

---

### 3️⃣ Check service status (DevOps Example)

```bash
if systemctl is-active --quiet nginx; then
    echo "Nginx is running"
else
    echo "Nginx is not running"
fi
```

---

# 🟢 8️⃣ Loops – for, while, until, break, continue

Loops allow you to **repeat commands multiple times**.

Without loops → Repetitive manual work
With loops → Automation

---

# 8.1 `for` Loop

Used when:

* You know how many times to run
* You want to iterate over list, files, numbers

---

## 🔹 Basic Syntax

```bash
for variable in list
do
    commands
done
```

---

## Example 1 – Loop Through List

```bash
for name in Saurav Rahul Amit
do
    echo "Hello $name"
done
```

---

## Example 2 – Loop Through Numbers

```bash
for i in 1 2 3 4 5
do
    echo "Number: $i"
done
```

---

## Example 3 – C-Style Loop (Advanced & Recommended)

```bash
for (( i=1; i<=5; i++ ))
do
    echo "Count: $i"
done
```

---

## Example 4 – Loop Through Files

```bash
for file in *.txt
do
    echo "Processing $file"
done
```

Very useful in DevOps & automation.

---

# 8.2 `while` Loop

Used when:

* Condition must be checked before every iteration
* You don’t know exact number of loops

---

## Syntax

```bash
while [[ condition ]]
do
    commands
done
```

---

## Example 1 – Counter

```bash
count=1

while [[ $count -le 5 ]]
do
    echo "Count: $count"
    ((count++))
done
```

---

## Example 2 – Read File Line by Line

```bash
while read line
do
    echo "$line"
done < file.txt
```

Very important in log processing.

---

# 8.3 `until` Loop

Opposite of while.

Runs until condition becomes true.

---

## Syntax

```bash
until [[ condition ]]
do
    commands
done
```

---

## Example

```bash
count=1

until [[ $count -gt 5 ]]
do
    echo "Count: $count"
    ((count++))
done
```

Runs until count becomes greater than 5.

---

# 8.4 `break`

Used to exit loop immediately.

---

## Example

```bash
for i in 1 2 3 4 5
do
    if [[ $i -eq 3 ]]; then
        break
    fi
    echo "$i"
done
```

Output:

```
1
2
```

Loop stops at 3.

---

# 8.5 `continue`

Skips current iteration and moves to next.

---

## Example

```bash
for i in 1 2 3 4 5
do
    if [[ $i -eq 3 ]]; then
        continue
    fi
    echo "$i"
done
```

Output:

```
1
2
4
5
```

3 is skipped.

---

# 8.6 Looping Through Files (Real-World DevOps Use)

---

## Example 1 – Backup All Logs

```bash
for file in /var/log/*.log
do
    cp "$file" /backup/
done
```

---

## Example 2 – Check Disk Usage Multiple Times

```bash
while true
do
    df -h
    sleep 10
done
```

Runs continuously every 10 seconds.

---

# 🔥 Infinite Loop

```bash
while true
do
    echo "Running..."
done
```

Stop using:

```
CTRL + C
```

---

# 🔥 Important Best Practice

Always:

* Use quotes `"${var}"`
* Use `[[ ]]` for conditions
* Avoid infinite loops without break condition

---

# 🟡 9️⃣ Functions – Creating Reusable Code Blocks

Functions allow you to:

* Reuse code
* Organize scripts
* Reduce repetition
* Write modular scripts

In real-world DevOps and production scripts, **functions are mandatory**.

---

# 9.1 Creating Functions

## 🔹 Basic Syntax (Recommended Style)

```bash
function_name() {
    commands
}
```

---

## Example 1 – Simple Function

```bash
greet() {
    echo "Hello, World!"
}

greet
```

Output:

```
Hello, World!
```

---

## Example 2 – Without `function` Keyword (Also Valid)

```bash
function greet {
    echo "Hello"
}
```

Both styles work in Bash.

---

# 9.2 Passing Arguments to Function

Functions can take parameters like scripts.

---

## Example

```bash
greet() {
    echo "Hello $1"
}

greet Saurav
```

Output:

```
Hello Saurav
```

---

## Multiple Arguments

```bash
add() {
    echo $(($1 + $2))
}

add 10 5
```

Output:

```
15
```

---

Inside function:

* `$1` → First argument
* `$2` → Second argument
* `$@` → All arguments
* `$#` → Number of arguments

---

# 9.3 Returning Values

⚠ Important Concept:

Functions do NOT return values like other programming languages.

`return` only returns exit status (0–255).

---

## Example – Return Status

```bash
check_number() {
    if [[ $1 -gt 0 ]]; then
        return 0
    else
        return 1
    fi
}

check_number 5
echo $?
```

Output:

```
0
```

---

## Returning Actual Value (Using echo)

```bash
multiply() {
    echo $(($1 * $2))
}

result=$(multiply 4 5)
echo "Result: $result"
```

Output:

```
Result: 20
```

This is the correct way to "return" values.

---

# 9.4 Local vs Global Variables

By default, variables in Bash are global.

---

## Global Variable Example

```bash
name="Saurav"

show() {
    echo $name
}

show
```

Accessible everywhere.

---

## Local Variable Example (Recommended)

```bash
show() {
    local message="Hello"
    echo $message
}

show
```

---

### Why Use `local`?

* Prevents variable conflict
* Safer in large scripts
* Required in production scripts

---

# 9.5 Modular Scripts

Modular scripting means:

* Breaking script into small reusable functions
* Each function does one job

---

## Example – Structured Script

```bash
#!/bin/bash

check_file() {
    if [[ -f "$1" ]]; then
        echo "File exists"
    else
        echo "File not found"
    fi
}

main() {
    check_file "test.txt"
}

main
```

---

### Why Use `main()`?

In production:

* Improves readability
* Controls execution flow
* Standard coding practice

---

# 🔥 Best Practices for Functions

✅ Use descriptive function names
✅ Use `local` variables
✅ Keep functions small
✅ One function = One responsibility
✅ Always quote variables `"${var}"`

---

# 🔥 Real-World DevOps Example

```bash
check_service() {
    if systemctl is-active --quiet "$1"; then
        echo "$1 is running"
    else
        echo "$1 is not running"
    fi
}

check_service nginx
```

Reusable service check function.

---

# 🟡 🔟 Arrays & Data Structures 

Arrays allow you to store **multiple values in a single variable**.

Without arrays → Only one value
With arrays → List of values

Very useful in:

* DevOps automation
* Server lists
* File lists
* User lists

---

# 10.1 Indexed Arrays

Indexed arrays store values using numeric index.

Index starts from **0**.

---

## 🔹 Creating Array

```bash id="l2w0za"
names=("Saurav" "Rahul" "Amit")
```

---

## 🔹 Access Elements

```bash id="k0mdol"
echo ${names[0]}
echo ${names[1]}
```

Output:

```id="7o5x8z"
Saurav
Rahul
```

---

## 🔹 Print All Elements

```bash id="7k9mop"
echo ${names[@]}
```

---

## 🔹 Print Indexes

```bash id="g3jlfu"
echo ${!names[@]}
```

---

# 10.2 Associative Arrays

Associative arrays use **key-value pairs**.

⚠ Available only in Bash 4+

---

## 🔹 Declare Associative Array

```bash id="9f8nxa"
declare -A user
```

---

## 🔹 Add Values

```bash id="9fdxlj"
user[name]="Saurav"
user[role]="DevOps"
```

---

## 🔹 Access Value

```bash id="7k2mql"
echo ${user[name]}
```

Output:

```id="nmdk6a"
Saurav
```

---

## 🔹 Print All Keys

```bash id="whz10r"
echo ${!user[@]}
```

---

## 🔹 Print All Values

```bash id="s5n9oh"
echo ${user[@]}
```

---

# 10.3 Looping Arrays

---

## 🔹 Loop Through Values

```bash id="m7z0nl"
for name in "${names[@]}"
do
    echo "$name"
done
```

Always use quotes `"${array[@]}"`

---

## 🔹 Loop Using Index

```bash id="3qvtsz"
for i in "${!names[@]}"
do
    echo "Index: $i Value: ${names[$i]}"
done
```

---

# 10.4 Array Length

---

## 🔹 Total Elements

```bash id="5tyjsd"
echo ${#names[@]}
```

Returns number of elements.

---

## 🔹 Length of Specific Element

```bash id="5p8hs1"
echo ${#names[0]}
```

Returns character count of element.

---

# 10.5 Array Slicing

You can extract part of array.

---

## 🔹 Syntax

```bash id="ay3t9x"
${array[@]:start:length}
```

---

## Example

```bash id="m87w3o"
echo ${names[@]:1:2}
```

Starts from index 1 → print 2 elements.

---

# 🔥 Adding Elements to Array

```bash id="6jzpw4"
names+=("Rohit")
```

---

# 🔥 Removing Element

```bash id="3a6ix1"
unset names[1]
```

---

# 🔥 Real-World DevOps Example

## Loop Through Multiple Servers

```bash id="mbrpqs"
servers=("server1" "server2" "server3")

for server in "${servers[@]}"
do
    echo "Checking $server"
    ping -c 1 "$server"
done
```

Very common in infrastructure automation.

---

# 🔥 Important Best Practices

✅ Always quote arrays `"${array[@]}"`
✅ Use `declare -A` for associative arrays
✅ Avoid sparse index mistakes
✅ Prefer arrays over space-separated strings

---

# 🟡 1️⃣1️⃣ String Manipulation – Powerful Text Operations

Strings are everywhere in Shell scripting:

* File names
* Logs
* User input
* API responses
* Configuration values

Mastering string manipulation = Powerful scripting 💪

---

# 11.1 Length of String

Get number of characters in a string.

---

## 🔹 Syntax

```bash
${#variable}
```

---

## Example

```bash
name="Saurav"
echo ${#name}
```

Output:

```
6
```

---

# 11.2 Substring Extraction

Extract part of a string.

---

## 🔹 Syntax

```bash
${variable:start:length}
```

---

## Example

```bash
text="DevOpsEngineer"

echo ${text:0:6}
```

Output:

```
DevOps
```

---

## Example – Without Length

```bash
echo ${text:6}
```

Output:

```
Engineer
```

---

# 11.3 Replace String

Replace part of string.

---

## 🔹 Replace First Occurrence

```bash
name="Saurav Bagade"

echo ${name/Bagade/Kumar}
```

Output:

```
Saurav Kumar
```

---

## 🔹 Replace All Occurrences

```bash
sentence="apple mango apple"

echo ${sentence//apple/orange}
```

Output:

```
orange mango orange
```

---

# 11.4 Remove Prefix / Suffix

Very useful for file processing.

---

## 🔹 Remove Shortest Prefix

```bash
file="backup.tar.gz"

echo ${file#backup.}
```

Output:

```
tar.gz
```

---

## 🔹 Remove Longest Prefix

```bash
echo ${file##*.}
```

Output:

```
gz
```

---

## 🔹 Remove Shortest Suffix

```bash
echo ${file%.gz}
```

Output:

```
backup.tar
```

---

## 🔹 Remove Longest Suffix

```bash
echo ${file%%.*}
```

Output:

```
backup
```

---

# 11.5 Case Conversion

Convert string to uppercase or lowercase.

---

## 🔹 To Uppercase

```bash
name="saurav"

echo ${name^^}
```

Output:

```
SAURAV
```

---

## 🔹 To Lowercase

```bash
name="SAURAV"

echo ${name,,}
```

Output:

```
saurav
```

---

## 🔹 Capitalize First Letter

```bash
name="saurav"

echo ${name^}
```

Output:

```
Saurav
```

---

# 11.6 Advanced Parameter Expansion

These are powerful built-in features of Bash.

---

## 🔹 Default Value

```bash
echo ${username:-"Guest"}
```

If username empty → prints Guest.

---

## 🔹 Assign Default

```bash
username=${username:-"Guest"}
```

---

## 🔹 Error if Variable Not Set

```bash
echo ${username:? "Username not set"}
```

Script stops if variable missing.

---

## 🔹 Replace Pattern Using Wildcards

```bash
path="/home/user/docs/file.txt"

echo ${path##*/}
```

Output:

```
file.txt
```

Extract filename from path.

---

## 🔹 Remove Directory Path

```bash
echo ${path%/*}
```

Output:

```
/home/user/docs
```

Extract directory path.

---

# 🔥 Important Best Practice

Always quote variables:

```bash
echo "$variable"
```

Why?

* Prevent word splitting
* Prevent glob expansion
* Avoid script breaking

---

# 🔥 Real-World DevOps Example

## Extract File Extension

```bash
file="nginx.conf"

extension=${file##*.}
echo "Extension: $extension"
```

---

## Extract Filename Without Extension

```bash
name=${file%.*}
echo "Filename: $name"
```

---

# 🟡 1️⃣2️⃣ Input / Output & Redirection 

Understanding I/O redirection is **critical for DevOps, automation, logging, and production scripts**.

Every Linux command works with 3 standard streams.

---

# 12.1 Standard Input / Output / Error

Every process has 3 file descriptors:

| FD | Name   | Description     |
| -- | ------ | --------------- |
| 0  | STDIN  | Standard Input  |
| 1  | STDOUT | Standard Output |
| 2  | STDERR | Standard Error  |

---

### Example

```bash
ls file.txt
```

If file exists → output goes to **STDOUT (1)**
If file missing → error goes to **STDERR (2)**

---

# 12.2 `>` and `>>`

Used to redirect output.

---

## 🔹 `>` (Overwrite)

```bash
echo "Hello" > file.txt
```

If file exists → it will be overwritten.

---

## 🔹 `>>` (Append)

```bash
echo "World" >> file.txt
```

Adds content without deleting previous data.

---

# 12.3 `2>` (Redirect Error)

Redirect only errors.

```bash
ls missingfile 2> error.log
```

Error message goes to `error.log`.

---

# 12.4 `2>&1` (Combine Output + Error)

Redirect STDERR to STDOUT.

```bash
ls file.txt > output.log 2>&1
```

Both success + error go to same file.

---

### Explanation:

* `2` → STDERR
* `>` → redirect
* `&1` → to STDOUT

---

# 12.5 `&>` (Shortcut)

Redirect both STDOUT and STDERR.

```bash
ls file.txt &> all.log
```

Same as:

```bash
ls file.txt > all.log 2>&1
```

---

# 12.6 Pipes (`|`)

Pipe sends output of one command as input to another.

---

## Syntax

```bash
command1 | command2
```

---

## Example

```bash
ls -l | grep ".txt"
```

`ls -l` output → passed to `grep`

---

## Example 2

```bash
ps aux | grep nginx
```

Very common in DevOps.

---

# 12.7 `tee`

Displays output AND writes to file.

---

## Example

```bash
echo "Deploy started" | tee deploy.log
```

Output:

* Printed on screen
* Saved to deploy.log

---

## Append Mode

```bash
echo "Next step" | tee -a deploy.log
```

---

# 12.8 Here Document (`<<EOF`)

Used to provide multi-line input.

---

## Syntax

```bash
command <<EOF
text
EOF
```

---

## Example

```bash
cat <<EOF
Hello
Welcome to Shell
EOF
```

---

## Create File Using Here Doc

```bash
cat <<EOF > config.txt
PORT=8080
ENV=production
EOF
```

Very useful for automation scripts.

---

# 12.9 Here String (`<<<`)

Pass single string as input.

---

## Example

```bash
grep "Hello" <<< "Hello World"
```

Works like temporary input.

---

# 12.10 File Descriptors (0,1,2)

We already saw:

| FD | Meaning |
| -- | ------- |
| 0  | STDIN   |
| 1  | STDOUT  |
| 2  | STDERR  |

---

## Explicit Example

```bash
echo "Hello" 1> out.txt
ls missingfile 2> error.txt
```

---

## Redirect STDIN

```bash
cat < file.txt
```

File content becomes input.

---

# 12.11 Named Pipes (FIFO)

FIFO = First In First Out pipe.

Creates special file for inter-process communication.

---

## Create Named Pipe

```bash
mkfifo mypipe
```

---

## Terminal 1

```bash
cat mypipe
```

---

## Terminal 2

```bash
echo "Hello" > mypipe
```

Message appears in Terminal 1.

Used in:

* Advanced scripting
* Process communication
* Logging pipelines

---

# 🔥 Real-World DevOps Examples

---

## 1️⃣ Save Logs with Timestamp

```bash
date >> app.log
echo "App started" >> app.log
```

---

## 2️⃣ Capture Both Output & Errors

```bash
./deploy.sh > deploy.log 2>&1
```

---

## 3️⃣ Monitor Logs in Real-Time

```bash
tail -f app.log | grep ERROR
```

---

## 4️⃣ Prevent Error Messages

```bash
ls missingfile 2> /dev/null
```

`/dev/null` = Black hole (discards output)

---

# 🔥 Best Practices

✅ Always log errors in production
✅ Use `>>` instead of `>` in logging
✅ Use `2>&1` when debugging
✅ Use pipes for efficient data processing
✅ Avoid overwriting important files

---

# 🟡 1️⃣3️⃣ Text Processing Tools – grep, awk, sed, cut, sort, uniq, tr, xargs, Regex

Text processing is the **core power of Linux + Shell scripting**.

In DevOps, you constantly process:

* Logs
* Config files
* CSV files
* API outputs
* Command outputs

---

# 13.1 `grep` – Search Text

Used to search patterns in files.

---

## 🔹 Basic Syntax

```bash
grep "pattern" file.txt
```

---

## Example

```bash
grep "ERROR" app.log
```

---

## Useful Options

```bash
grep -i "error" app.log     # Ignore case
grep -r "nginx" /etc        # Recursive
grep -n "root" file.txt     # Show line number
grep -v "INFO" app.log      # Invert match
```

---

## Real DevOps Example

```bash
ps aux | grep nginx
```

---

# 13.2 `awk` – Powerful Text Processor

`awk` works column-wise.

Default separator = space.

---

## 🔹 Basic Syntax

```bash
awk '{print $1}' file.txt
```

---

## Example

```bash
awk '{print $1}' users.txt
```

Prints first column.

---

## Print Multiple Columns

```bash
awk '{print $1, $3}' file.txt
```

---

## Use Custom Separator

```bash
awk -F: '{print $1}' /etc/passwd
```

`-F:` sets colon as separator.

---

## Real DevOps Example

```bash
df -h | awk '{print $5}'
```

Extract disk usage column.

---

# 13.3 `sed` – Stream Editor

Used to:

* Replace text
* Delete lines
* Modify files

---

## 🔹 Replace Text

```bash
sed 's/old/new/' file.txt
```

---

## Replace All Occurrences

```bash
sed 's/old/new/g' file.txt
```

---

## Delete Line

```bash
sed '3d' file.txt
```

Delete line 3.

---

## Edit File Directly

```bash
sed -i 's/8080/9090/g' config.txt
```

Very common in automation.

---

# 13.4 `cut` – Extract Columns

Used for column extraction.

---

## Example

```bash
cut -d: -f1 /etc/passwd
```

* `-d:` → delimiter
* `-f1` → field 1

---

# 13.5 `sort`

Sort lines alphabetically or numerically.

---

```bash
sort file.txt
sort -n numbers.txt     # Numeric
sort -r file.txt        # Reverse
```

---

# 13.6 `uniq`

Remove duplicate lines.

⚠ Must use after `sort`.

---

```bash
sort file.txt | uniq
```

---

## Count duplicates

```bash
sort file.txt | uniq -c
```

---

# 13.7 `tr` – Translate Characters

Used to:

* Convert case
* Replace characters
* Remove characters

---

## Convert to Uppercase

```bash
echo "hello" | tr 'a-z' 'A-Z'
```

---

## Remove Characters

```bash
echo "hello123" | tr -d '0-9'
```

---

# 13.8 `xargs`

Converts input into arguments.

---

## Example

```bash
echo "file1 file2" | xargs rm
```

Same as:

```bash
rm file1 file2
```

---

## Real DevOps Example

```bash
find . -name "*.log" | xargs rm
```

Delete all log files.

---

# 13.9 Regular Expressions (Regex)

Regex = Pattern matching language.

Used in:

* grep
* sed
* awk

---

## Common Patterns

| Pattern | Meaning       |
| ------- | ------------- |
| `.`     | Any character |
| `*`     | Zero or more  |
| `^`     | Start of line |
| `$`     | End of line   |
| `[abc]` | Match a, b, c |
| `[0-9]` | Match digits  |
| `+`     | One or more   |
| `?`     | Optional      |

---

## Examples

### Match line starting with root

```bash
grep "^root" /etc/passwd
```

---

### Match lines ending with .log

```bash
grep "\.log$" file.txt
```

---

### Match numbers

```bash
grep "[0-9]" file.txt
```

---

# 🔥 Real-World DevOps Example

Find top 5 memory-consuming processes:

```bash
ps aux | sort -nrk 4 | head -5
```

---

Find ERROR logs and count:

```bash
grep "ERROR" app.log | wc -l
```

---

Extract username from passwd file:

```bash
awk -F: '{print $1}' /etc/passwd
```

---

# 🔥 Best Practices

✅ Use `grep -r` carefully (large directories)
✅ Use `sed -i` cautiously (modifies file)
✅ Combine tools with pipes
✅ Always test regex before production
✅ Quote patterns properly

---


# 🟡 1️⃣4️⃣ Process Management – ps, top, kill, bg, fg, nohup, wait, Background Jobs

Understanding process management is **very important for DevOps, server administration, and production troubleshooting**.

---

# 14.1 `ps` – Process Status

Used to display running processes.

---

## 🔹 Basic

```bash
ps
```

Shows processes of current terminal.

---

## 🔹 Show All Processes

```bash
ps aux
```

* `a` → All users
* `u` → User format
* `x` → Background processes

---

## 🔹 Filter Using grep

```bash
ps aux | grep nginx
```

---

## Important Columns

| Column  | Meaning       |
| ------- | ------------- |
| PID     | Process ID    |
| USER    | Process owner |
| %CPU    | CPU usage     |
| %MEM    | Memory usage  |
| COMMAND | Command name  |

---

# 14.2 `top` – Real-Time Process Monitor

Shows live CPU and memory usage.

```bash
top
```

---

Controls inside `top`:

* `q` → Quit
* `k` → Kill process
* `M` → Sort by memory
* `P` → Sort by CPU

---

## Alternative (Better UI)

```bash
htop
```

(May need installation)

---

# 14.3 `kill`

Used to terminate processes.

---

## 🔹 Kill by PID

```bash
kill 1234
```

---

## 🔹 Force Kill

```bash
kill -9 1234
```

`-9` = SIGKILL (Force stop)

---

## Common Signals

| Signal  | Number | Meaning       |
| ------- | ------ | ------------- |
| SIGTERM | 15     | Graceful stop |
| SIGKILL | 9      | Force stop    |
| SIGHUP  | 1      | Reload        |

---

# 14.4 `killall`

Kill process by name.

```bash
killall nginx
```

Instead of finding PID manually.

---

# 14.5 `bg` & `fg`

Used for job control.

---

## 🔹 Run Process in Foreground

```bash
sleep 100
```

Press:

```
CTRL + Z
```

Process stops (suspended).

---

## 🔹 Send to Background

```bash
bg
```

---

## 🔹 Bring Back to Foreground

```bash
fg
```

---

# 14.6 `nohup`

Run process that continues even after logout.

---

```bash
nohup ./script.sh &
```

* `nohup` → No hangup
* `&` → Run in background

Output saved in:

```
nohup.out
```

Very important in production servers.

---

# 14.7 `wait`

Wait for background process to finish.

---

```bash
./script1.sh &
./script2.sh &

wait
echo "Both scripts completed"
```

Ensures scripts complete before continuing.

---

# 14.8 Background Jobs (`&`)

Add `&` to run command in background.

---

## Example

```bash
sleep 30 &
```

---

## Check Background Jobs

```bash
jobs
```

Shows job number and status.

---

## Example Output

```
[1]+ Running    sleep 30 &
```

---

# 🔥 Real-World DevOps Examples

---

## 1️⃣ Check If Service Running

```bash
ps aux | grep nginx
```

---

## 2️⃣ Restart Stuck Process

```bash
kill -9 <PID>
```

---

## 3️⃣ Run Long Deployment Script

```bash
nohup ./deploy.sh > deploy.log 2>&1 &
```

---

## 4️⃣ Monitor High CPU Process

```bash
top
```

---

# 🔥 Important Best Practices

✅ Use `kill -15` before `kill -9`
✅ Avoid killing system processes
✅ Use `nohup` for long-running jobs
✅ Monitor CPU & memory in production
✅ Use `wait` in automation scripts

---

# 🟠 1️⃣5️⃣ Error Handling & Strict Mode

In production scripts:

❌ Ignoring errors = Dangerous
✅ Handling errors properly = Professional

This chapter is very important for **DevOps, automation, CI/CD, and infrastructure scripts**.

---

# 15.1 Exit Codes

Every Linux command returns an exit status.

---

## Check Exit Status

```bash
ls file.txt
echo $?
```

---

### Meaning:

| Exit Code | Meaning |
| --------- | ------- |
| 0         | Success |
| Non-zero  | Error   |

---

### Example

```bash
ls missingfile
echo $?
```

Output:

```
2
```

---

# 15.2 Custom Exit Status

You can manually exit with custom code.

---

## Syntax

```bash
exit <number>
```

---

## Example

```bash
#!/bin/bash

if [[ ! -f "config.txt" ]]; then
    echo "Config file missing"
    exit 1
fi

echo "Script running"
```

---

### Common Exit Codes

| Code | Meaning            |
| ---- | ------------------ |
| 0    | Success            |
| 1    | General error      |
| 2    | Misuse of command  |
| 126  | Permission problem |
| 127  | Command not found  |

---

# 15.3 `set -euo pipefail` (Strict Mode)

This is mandatory in production scripts.

Add at top of script:

```bash
set -euo pipefail
```

---

### Explanation

| Option        | Meaning                               |
| ------------- | ------------------------------------- |
| `-e`          | Exit immediately if command fails     |
| `-u`          | Error on undefined variable           |
| `-o pipefail` | Fail if any command in pipeline fails |

---

## Example Without Strict Mode (Danger)

```bash
#!/bin/bash

rm important.txt
echo "Deployment complete"
```

If rm fails → script still continues.

---

## With Strict Mode

```bash
#!/bin/bash
set -euo pipefail
```

Now script stops immediately if error occurs.

---

# 15.4 `trap` Command

Used to catch signals and perform cleanup.

Very important in:

* Temporary files
* Service shutdown
* Script interruption

---

## Syntax

```bash
trap 'commands' SIGNAL
```

---

## Example – Cleanup on Exit

```bash
#!/bin/bash
set -euo pipefail

cleanup() {
    echo "Cleaning up..."
    rm -f temp.txt
}

trap cleanup EXIT

touch temp.txt
echo "Running script"
```

Even if script crashes → cleanup runs.

---

## Catch CTRL + C

```bash
trap 'echo "Interrupted"; exit 1' SIGINT
```

---

# 15.5 Retry Mechanism

Used when:

* Network unstable
* API calls fail
* Service temporarily unavailable

---

## Example – Retry 3 Times

```bash
retry=0
max_retries=3

until curl -s http://example.com; do
    ((retry++))
    if [[ $retry -ge $max_retries ]]; then
        echo "Failed after retries"
        exit 1
    fi
    echo "Retrying..."
    sleep 2
done
```

Very common in cloud automation.

---

# 15.6 Graceful Shutdown

Stop processes safely.

---

## Example

```bash
cleanup() {
    echo "Shutting down service..."
    kill $child_pid
}

trap cleanup SIGTERM

./long_running_script.sh &
child_pid=$!

wait
```

When SIGTERM received → cleanup runs.

Used in:

* Docker containers
* Kubernetes pods
* CI/CD pipelines

---

# 🔥 Production Script Template (Recommended)

```bash
#!/usr/bin/env bash
set -euo pipefail

readonly SCRIPT_NAME=$(basename "$0")

log() {
    echo "[$(date +'%Y-%m-%d %H:%M:%S')] $1"
}

cleanup() {
    log "Cleaning up resources..."
}

trap cleanup EXIT

main() {
    log "Script started"
}

main "$@"
```

---

# 🔥 Real-World DevOps Example

## Fail Deployment if Build Fails

```bash
set -e

make build
make test
make deploy
```

If build fails → deploy never runs.

---

# 🔥 Best Practices

✅ Always use `set -euo pipefail`
✅ Use `trap` for cleanup
✅ Check exit codes
✅ Fail fast (do not continue on error)
✅ Use meaningful exit codes
✅ Log errors clearly

---

# 🟠 1️⃣6️⃣ Debugging & Logging 

In real-world DevOps:

If script fails and you cannot debug it → ❌ Production issue
If script logs properly → ✅ Easy troubleshooting

Debugging + Logging = Professional scripting.

---

# 16.1 `bash -x` (Debug Mode)

Run script in debug mode.

```bash
bash -x script.sh
```

It prints:

* Each command
* Expanded variables
* Execution flow

---

## Example

```bash
#!/bin/bash
name="Saurav"
echo "Hello $name"
```

Run:

```bash
bash -x script.sh
```

Output:

```
+ name=Saurav
+ echo 'Hello Saurav'
Hello Saurav
```

Very useful for troubleshooting.

---

# 16.2 `set -x`

Enable debugging inside script.

---

## Example

```bash
#!/bin/bash
set -x

a=10
b=5
echo $((a + b))
```

---

## Disable Debug Mode

```bash
set +x
```

Useful when debugging only specific part.

---

# 16.3 Custom Logging Function

Production scripts must use logging function.

---

## Example

```bash
log() {
    echo "[$(date +'%Y-%m-%d %H:%M:%S')] $1"
}

log "Script started"
log "Deployment complete"
```

Output:

```
[2026-02-27 18:30:10] Script started
```

---

# 16.4 Log Levels (INFO, WARN, ERROR)

Professional logging uses levels.

---

## Example

```bash
log_info() {
    echo "[INFO] $(date +'%H:%M:%S') - $1"
}

log_warn() {
    echo "[WARN] $(date +'%H:%M:%S') - $1"
}

log_error() {
    echo "[ERROR] $(date +'%H:%M:%S') - $1" >&2
}
```

---

## Usage

```bash
log_info "Starting deployment"
log_warn "Disk usage high"
log_error "Service failed"
```

---

# 16.5 Writing Logs to File

---

## Simple Logging

```bash
./script.sh >> app.log 2>&1
```

---

## Inside Script

```bash
log() {
    echo "[$(date)] $1" >> app.log
}
```

---

## Advanced Logging with tee

```bash
log() {
    echo "[$(date)] $1" | tee -a app.log
}
```

Prints on screen + saves to file.

---

# 16.6 Script Tracing

Trace specific function.

---

## Example

```bash
set -x
deploy_app
set +x
```

Only `deploy_app` is traced.

---

## Debug Only When Needed

```bash
if [[ "${DEBUG:-false}" == "true" ]]; then
    set -x
fi
```

Run with:

```bash
DEBUG=true ./script.sh
```

Professional approach.

---

# 16.7 ShellCheck & Linting

ShellCheck is static analysis tool for shell scripts.

It finds:

* Syntax mistakes
* Unquoted variables
* Dangerous patterns
* Bad practices

---

## Install (Ubuntu)

```bash
sudo apt install shellcheck
```

---

## Run

```bash
shellcheck script.sh
```

---

## Example Warning

It may warn:

```
Double quote to prevent globbing and word splitting.
```

Very important for production quality.

---

# 🔥 Real-World DevOps Logging Example

```bash
#!/usr/bin/env bash
set -euo pipefail

LOG_FILE="deploy.log"

log() {
    echo "[$(date +'%Y-%m-%d %H:%M:%S')] $1" | tee -a "$LOG_FILE"
}

main() {
    log "Starting deployment"

    if systemctl restart nginx; then
        log "Nginx restarted successfully"
    else
        log "Nginx restart failed"
        exit 1
    fi

    log "Deployment finished"
}

main "$@"
```

---

# 🔥 Debugging Checklist

If script fails:

1. Run with `bash -x`
2. Check exit code `$?`
3. Check log file
4. Enable strict mode
5. Use ShellCheck
6. Validate input variables

---

# 🔥 Best Practices

✅ Always log important actions
✅ Use log levels
✅ Write logs to file in production
✅ Enable debug only when needed
✅ Use ShellCheck before deployment
✅ Never ignore errors

---

# 🔴 1️⃣7️⃣ Security Best Practices – Safe & Secure Shell Scripts

Security is extremely important in:

* Production servers
* DevOps pipelines
* CI/CD automation
* Cloud infrastructure

A small mistake in shell script can:

❌ Delete data
❌ Leak secrets
❌ Allow command injection
❌ Break servers

This chapter teaches **secure scripting practices**.

---

# 17.1 Avoid Hardcoding Secrets

❌ Never hardcode:

* Passwords
* API keys
* Tokens
* Database credentials

---

## ❌ Wrong

```bash
DB_PASSWORD="mypassword123"
```

---

## ✅ Correct Approach – Use Environment Variables

```bash
DB_PASSWORD="${DB_PASSWORD:-}"
```

Set externally:

```bash
export DB_PASSWORD="mypassword123"
```

---

## ✅ Even Better – Use `.env` File

Example `.env`:

```
DB_USER=admin
DB_PASSWORD=secret
```

Load safely:

```bash
set -a
source .env
set +a
```

---

# 17.2 Environment Files

Use restricted permissions:

```bash
chmod 600 .env
```

Permission meaning:

* Owner: Read + Write
* Others: No access

---

## Secure Practice

Add `.env` to `.gitignore`

Never commit secrets to Git.

---

# 17.3 File Permission Security

Always set correct permissions for:

* Scripts
* Logs
* Config files

---

## Make Script Executable (Owner Only)

```bash
chmod 700 script.sh
```

---

## Restrict Log Files

```bash
chmod 600 app.log
```

---

## Check Permissions

```bash
ls -l
```

---

# 17.4 Prevent Command Injection

Command injection happens when user input is executed directly.

---

## ❌ Dangerous Code

```bash
read filename
rm $filename
```

If user enters:

```
* 
```

It deletes everything.

---

## ❌ Worse Example

```bash
read input
eval "$input"
```

Never use `eval` with user input.

---

## ✅ Safe Practice

Always quote variables:

```bash
rm -- "$filename"
```

`--` prevents option injection.

---

## Validate Input

```bash
if [[ "$filename" =~ ^[a-zA-Z0-9._-]+$ ]]; then
    rm -- "$filename"
else
    echo "Invalid filename"
fi
```

---

# 17.5 Secure Temporary Files

Never create predictable temp files.

---

## ❌ Unsafe

```bash
tempfile="/tmp/myfile.txt"
```

Attacker could replace it.

---

## ✅ Safe Method

Use `mktemp`

```bash
tempfile=$(mktemp)
```

---

## Cleanup After Use

```bash
trap 'rm -f "$tempfile"' EXIT
```

---

# 🔥 Additional Security Best Practices

---

## 1️⃣ Use Strict Mode

```bash
set -euo pipefail
```

Prevents unexpected behavior.

---

## 2️⃣ Disable Unnecessary Features

Avoid:

* `eval`
* Backticks (`)
* Unquoted variables
* Wildcard expansion

---

## 3️⃣ Avoid Running as Root

Only use sudo when required.

---

## 4️⃣ Validate External Data

If using:

* curl
* wget
* user input
* API data

Always validate before using.

---

## 5️⃣ Restrict PATH

In secure scripts:

```bash
PATH="/usr/bin:/bin"
```

Prevents malicious path hijacking.

---

# 🔥 Real-World DevOps Secure Script Example

```bash
#!/usr/bin/env bash
set -euo pipefail

readonly LOG_FILE="app.log"
readonly PATH="/usr/bin:/bin"

log() {
    echo "[$(date)] $1" >> "$LOG_FILE"
}

cleanup() {
    log "Cleaning temporary files"
    rm -f "$tempfile"
}

trap cleanup EXIT

tempfile=$(mktemp)

log "Secure script started"
```

---

# 🔥 Security Checklist Before Production

✅ No hardcoded secrets
✅ Use environment variables
✅ Validate user input
✅ Quote all variables
✅ Use mktemp for temp files
✅ Use strict mode
✅ Set correct file permissions
✅ Avoid eval
✅ Add .env to .gitignore

---

# 🔴 1️⃣8️⃣ Performance & Optimization – High Efficiency Scripts

In small scripts → performance may not matter.
In production systems → performance is critical.

Poorly written shell scripts can:

* Consume high CPU
* Slow down servers
* Block pipelines
* Increase deployment time

This chapter teaches you how to write **efficient & optimized shell scripts**.

---

# 18.1 Parallel Execution

By default, shell runs commands sequentially.

```bash
command1
command2
```

`command2` waits until `command1` finishes.

---

## 🔹 Run in Parallel (Background)

```bash
command1 &
command2 &
wait
```

* `&` → Run in background
* `wait` → Wait for all to finish

---

## Example

```bash
#!/bin/bash

sleep 5 &
sleep 5 &
wait

echo "Done"
```

Runs both sleeps together → saves time.

---

## ⚠ Best Practice

Always use `wait` to avoid unfinished background tasks.

---

# 18.2 GNU Parallel

More advanced parallel execution tool.

Install:

```bash
sudo apt install parallel
```

---

## Example

```bash
parallel echo ::: 1 2 3 4 5
```

---

## Real Example – Process Multiple Files

```bash
ls *.log | parallel gzip
```

Compress multiple files simultaneously.

---

## Why GNU Parallel?

* Better CPU utilization
* Controlled parallelism
* Production-grade batching

---

# 18.3 `xargs` Optimization

`xargs` improves performance when processing large inputs.

---

## ❌ Slow Way

```bash
for file in *.log; do
    rm "$file"
done
```

---

## ✅ Faster Way

```bash
find . -name "*.log" | xargs rm
```

---

## Parallel with xargs

```bash
find . -name "*.log" | xargs -P 4 rm
```

* `-P 4` → Run 4 processes in parallel

---

# 18.4 Efficient Script Design

Optimization is not only about speed — also about design.

---

## 🔹 Avoid Useless Subshells

❌ Slow:

```bash
cat file.txt | grep "ERROR"
```

✅ Better:

```bash
grep "ERROR" file.txt
```

---

## 🔹 Avoid Multiple External Calls

❌ Inefficient:

```bash
for user in $(cat users.txt)
```

Word splitting problem + slow.

---

✅ Better:

```bash
while read -r user; do
    echo "$user"
done < users.txt
```

---

## 🔹 Use Built-in Bash Features

Bash built-ins are faster than external commands.

Example:

Instead of:

```bash
echo "$var" | wc -c
```

Use:

```bash
echo ${#var}
```

---

## 🔹 Avoid Fork Bomb Patterns

Bad:

```bash
while true; do
    command &
done
```

Can crash server.

---

# 18.5 Performance Benchmarking

Measure execution time.

---

## 🔹 Using `time`

```bash
time ./script.sh
```

Output shows:

* Real time
* User CPU time
* System time

---

## 🔹 Compare Two Methods

```bash
time grep "ERROR" file.txt
time awk '/ERROR/' file.txt
```

Choose faster option.

---

## 🔹 Manual Timer

```bash
start=$(date +%s)

sleep 2

end=$(date +%s)

echo "Execution time: $((end - start)) seconds"
```

---

# 🔥 Real-World DevOps Optimization Examples

---

## 1️⃣ Parallel Server Health Checks

```bash
servers=("server1" "server2" "server3")

for server in "${servers[@]}"; do
    ping -c 1 "$server" &
done

wait
```

---

## 2️⃣ Parallel Build Tasks

```bash
make -j4
```

Use multiple CPU cores.

---

## 3️⃣ Batch Log Processing

```bash
find /var/log -name "*.log" | xargs -P 4 grep "ERROR"
```

---

# 🔥 Performance Best Practices

✅ Use parallel execution wisely
✅ Use built-in Bash features
✅ Avoid unnecessary pipes
✅ Avoid spawning too many processes
✅ Use xargs with -P
✅ Benchmark using time
✅ Prefer grep over awk if only searching
✅ Minimize disk I/O

---

# 🔴 1️⃣9️⃣ Production-Ready Script Design – Industry Standards

This chapter transforms you from:

🟢 Script writer → 🔴 Production Engineer

In real companies, scripts must be:

* Readable
* Maintainable
* Versioned
* Documented
* Safe
* Modular

---

# 19.1 Strict Mode Template (Mandatory)

Every production script should start like this:

```bash
#!/usr/bin/env bash
set -euo pipefail
IFS=$'\n\t'
```

---

### Explanation

| Setting    | Purpose                     |
| ---------- | --------------------------- |
| `set -e`   | Exit on error               |
| `set -u`   | Undefined variable error    |
| `pipefail` | Fail if pipeline fails      |
| `IFS`      | Prevent word-splitting bugs |

---

# 19.2 Script Header Documentation Standard

Always document your script.

---

## Example Header

```bash
#!/usr/bin/env bash
set -euo pipefail

# ==================================================
# Script Name: deploy.sh
# Description: Automates application deployment
# Author: Saurav
# Version: 1.0.0
# Usage: ./deploy.sh --env production
# ==================================================
```

---

Why important?

✅ Easy maintenance
✅ Easy onboarding
✅ Professional standard

---

# 19.3 Versioning Inside Script

Maintain version variable.

---

```bash
VERSION="1.0.0"
```

---

## Show Version

```bash
if [[ "${1:-}" == "--version" ]]; then
    echo "Version: $VERSION"
    exit 0
fi
```

---

Helps in CI/CD & troubleshooting.

---

# 19.4 Help Menu (`--help`)

Professional scripts always provide help.

---

## Example

```bash
show_help() {
    cat <<EOF
Usage: $(basename "$0") [OPTIONS]

Options:
  --help        Show this help message
  --version     Show script version
  --env VALUE   Set environment
EOF
}
```

---

## Call Help

```bash
if [[ "${1:-}" == "--help" ]]; then
    show_help
    exit 0
fi
```

---

# 19.5 Argument Parsing (`getopts`)

For handling CLI options properly.

---

## Basic Example

```bash
while getopts "e:v" opt; do
    case "$opt" in
        e) ENV="$OPTARG" ;;
        v) echo "Version: $VERSION"; exit 0 ;;
        *) echo "Invalid option"; exit 1 ;;
    esac
done
```

---

Run:

```bash
./script.sh -e production
```

---

## Long Options (Advanced)

Use manual parsing:

```bash
while [[ $# -gt 0 ]]; do
    case "$1" in
        --env)
            ENV="$2"
            shift 2
            ;;
        --help)
            show_help
            exit 0
            ;;
        *)
            echo "Unknown option: $1"
            exit 1
            ;;
    esac
done
```

---

# 19.6 Modular Project Structure

In real-world projects:

Avoid single large script.

---

## Recommended Structure

```
project/
│
├── main.sh
├── lib/
│   ├── logging.sh
│   ├── validation.sh
│   └── utils.sh
├── config/
│   └── app.env
└── logs/
```

---

## Import Modules

```bash
source lib/logging.sh
source lib/utils.sh
```

---

# 🔥 Complete Production Script Example

```bash
#!/usr/bin/env bash
set -euo pipefail
IFS=$'\n\t'

readonly VERSION="1.0.0"
readonly LOG_FILE="app.log"

log() {
    echo "[$(date +'%Y-%m-%d %H:%M:%S')] $1" | tee -a "$LOG_FILE"
}

show_help() {
    echo "Usage: $(basename "$0") --env ENVIRONMENT"
}

parse_args() {
    while [[ $# -gt 0 ]]; do
        case "$1" in
            --env)
                ENV="$2"
                shift 2
                ;;
            --help)
                show_help
                exit 0
                ;;
            --version)
                echo "$VERSION"
                exit 0
                ;;
            *)
                echo "Unknown option: $1"
                exit 1
                ;;
        esac
    done
}

main() {
    log "Starting deployment for environment: $ENV"
}

parse_args "$@"
main
```

---

# 🔥 Production Script Checklist

Before deploying script:

✅ Strict mode enabled
✅ Header documentation added
✅ Version defined
✅ Help menu available
✅ Proper argument parsing
✅ Logging implemented
✅ Input validated
✅ Secrets externalized
✅ Modular structure used
✅ ShellCheck passed

---

# 🔥 Enterprise-Level Improvements

For large systems:

* Use Makefile
* Use Dockerized execution
* Add CI linting
* Use logging format standard
* Use consistent naming convention
* Add retry logic
* Add monitoring hooks

---

# 🔵 2️⃣0️⃣ Cron Jobs & Automation – Scheduling Scripts

Automation is one of the **most powerful features of Linux + Shell scripting**.

Instead of running scripts manually, you can schedule them to run:

* Every minute
* Every hour
* Daily
* Weekly
* Monthly
* At reboot

This is done using **cron**.

---

# 20.1 `crontab`

`crontab` is used to schedule jobs.

---

## 🔹 Edit Cron Jobs

```bash
crontab -e
```

Opens cron editor.

---

## 🔹 View Cron Jobs

```bash
crontab -l
```

---

## 🔹 Remove All Cron Jobs

```bash
crontab -r
```

⚠ This deletes all scheduled jobs.

---

# 20.2 Crontab Syntax

Each cron entry has 5 time fields + command.

---

## Format

```text
* * * * * command_to_execute
| | | | |
| | | | └── Day of Week (0-7) (Sunday=0 or 7)
| | | └──── Month (1-12)
| | └────── Day of Month (1-31)
| └──────── Hour (0-23)
└────────── Minute (0-59)
```

---

## Example

```bash
0 2 * * * /home/user/backup.sh
```

Runs daily at 2:00 AM.

---

# 20.3 Scheduling Examples

---

## 🔹 Every Minute

```bash
* * * * * /path/script.sh
```

---

## 🔹 Every 5 Minutes

```bash
*/5 * * * * /path/script.sh
```

---

## 🔹 Every Hour

```bash
0 * * * * /path/script.sh
```

---

## 🔹 Every Day at Midnight

```bash
0 0 * * * /path/script.sh
```

---

## 🔹 Every Sunday at 3 AM

```bash
0 3 * * 0 /path/script.sh
```

---

## 🔹 At System Reboot

```bash
@reboot /path/script.sh
```

---

# ⚠ Important: Always Use Full Path

Cron does NOT use your normal PATH.

❌ Wrong:

```bash
backup.sh
```

✅ Correct:

```bash
/home/user/backup.sh
```

---

# 20.4 Log Rotation

If cron script runs daily and logs output → logs will grow.

Use redirection:

```bash
0 2 * * * /home/user/backup.sh >> /var/log/backup.log 2>&1
```

---

## Rotate Logs Manually

```bash
mv backup.log backup.log.old
```

---

## Use `logrotate` (Production Method)

System tool that rotates logs automatically.

Example config:

```text
/var/log/backup.log {
    daily
    rotate 7
    compress
}
```

Keeps 7 days of logs.

---

# 20.5 systemd vs Cron

Modern Linux systems use **systemd timers** as alternative to cron.

---

## Cron

✅ Simple
✅ Easy to use
❌ Limited error handling

---

## systemd Timer

✅ Better logging
✅ Dependency control
✅ Service management
✅ Better production support

---

## Example systemd Timer Concept

1. Create service file:

```text
/etc/systemd/system/backup.service
```

2. Create timer file:

```text
/etc/systemd/system/backup.timer
```

3. Enable timer:

```bash
systemctl enable backup.timer
```

---

# 🔥 Real-World DevOps Examples

---

## 1️⃣ Daily Database Backup

```bash
0 1 * * * /home/user/db_backup.sh >> /var/log/db_backup.log 2>&1
```

---

## 2️⃣ Monitor Disk Every 10 Minutes

```bash
*/10 * * * * /home/user/check_disk.sh
```

---

## 3️⃣ Clear Temp Files Weekly

```bash
0 4 * * 0 /home/user/cleanup.sh
```

---

# 🔥 Cron Debugging Tips

If cron not working:

1️⃣ Check cron service:

```bash
systemctl status cron
```

2️⃣ Check logs:

```bash
grep CRON /var/log/syslog
```

3️⃣ Use full paths in script
4️⃣ Add logging
5️⃣ Test script manually

---

# 🔥 Best Practices

✅ Always use absolute paths
✅ Redirect output to log file
✅ Use strict mode in scripts
✅ Test script manually before scheduling
✅ Avoid heavy tasks during peak hours
✅ Use systemd for enterprise systems

---

# 🟣 2️⃣2️⃣ Testing & CI Integration – Professional Script Validation

In production:

❌ “It works on my machine” is not acceptable
✅ Scripts must be tested automatically

Testing ensures:

* No regression
* No syntax errors
* No unexpected behavior
* CI/CD reliability

---

# 22.1 Writing Test Cases

Shell scripts should have test cases like any programming language.

---

## 🔹 Simple Manual Test Structure

Example script: `add.sh`

```bash
add() {
    echo $(($1 + $2))
}
```

Test it:

```bash
result=$(add 5 3)

if [[ "$result" -eq 8 ]]; then
    echo "Test Passed"
else
    echo "Test Failed"
fi
```

---

## 🔹 Automated Test Script

Create `test_add.sh`

```bash
#!/usr/bin/env bash
set -euo pipefail

source ./add.sh

run_test() {
    expected=8
    result=$(add 5 3)

    if [[ "$result" -eq "$expected" ]]; then
        echo "PASS"
    else
        echo "FAIL"
        exit 1
    fi
}

run_test
```

---

# 22.2 Mocking in Shell

Mocking replaces real commands with fake ones during testing.

Used when:

* API calls
* AWS CLI
* Docker commands
* kubectl commands

---

## 🔹 Example – Mocking AWS CLI

Original script:

```bash
aws ec2 start-instances --instance-ids "$INSTANCE_ID"
```

Mock version (during testing):

```bash
aws() {
    echo "Mock AWS called with: $@"
}
```

Now real AWS won’t execute.

---

## 🔹 Conditional Mocking

```bash
if [[ "${TEST_MODE:-false}" == "true" ]]; then
    aws() {
        echo "Mock AWS: $@"
    }
fi
```

Run:

```bash
TEST_MODE=true ./script.sh
```

---

# 22.3 Static Code Analysis

Before deploying, always lint your script.

---

## 🔹 ShellCheck

```bash
shellcheck script.sh
```

Detects:

* Unquoted variables
* Dangerous patterns
* Syntax issues
* Useless commands

---

## 🔹 Syntax Check Only

```bash
bash -n script.sh
```

Checks syntax without running script.

---

# 22.4 CI/CD Integration

Testing scripts in CI pipeline ensures reliability.

---

## 🔹 Example – GitHub Actions (Concept)

Workflow steps:

1️⃣ Checkout code
2️⃣ Run ShellCheck
3️⃣ Run syntax check
4️⃣ Execute test scripts

---

## Example CI Steps

```bash
bash -n script.sh
shellcheck script.sh
./test_script.sh
```

If any step fails → pipeline fails.

---

# 🔥 Professional CI Pipeline Flow

Example order:

1️⃣ Lint
2️⃣ Unit test
3️⃣ Integration test
4️⃣ Build
5️⃣ Deploy

---

# 🔥 Example – Test Before Deployment

```bash
#!/usr/bin/env bash
set -euo pipefail

echo "Running lint..."
shellcheck script.sh

echo "Checking syntax..."
bash -n script.sh

echo "Running tests..."
./test_script.sh

echo "All checks passed."
```

Used in CI.

---

# 🔥 Best Practices for Testing Shell Scripts

✅ Write small functions (easy to test)
✅ Separate logic from execution
✅ Use mocking for external tools
✅ Use ShellCheck before commit
✅ Run `bash -n` in CI
✅ Fail fast on test failure
✅ Avoid testing in production

---

# 🔥 Advanced Testing Tools (Optional)

For large projects:

* Bats (Bash Automated Testing System)
* shUnit2
* Docker-based test environments

Example Bats concept:

```bash
@test "addition works" {
    run add 5 3
    [ "$status" -eq 0 ]
}
```

---

# 🟣 2️⃣3️⃣ Interview Questions – Beginner to Advanced DevOps Level

This section prepares you for:

* Linux Administrator interviews
* DevOps Engineer interviews
* Cloud Engineer interviews
* Production Support roles

Questions are divided into:

1️⃣ Beginner
2️⃣ Intermediate
3️⃣ Advanced / DevOps Level

---

# 🟢 Beginner Level Questions

---

### 1️⃣ What is Shell?

Shell is a command-line interpreter that acts as an interface between user and kernel.

---

### 2️⃣ What is the difference between Shell and Bash?

* Shell → Generic interface
* Bash → Specific type of shell (Bourne Again Shell)

---

### 3️⃣ What is Shebang?

`#!/bin/bash`

It tells system which interpreter to use.

---

### 4️⃣ What is the difference between `>` and `>>`?

| Operator | Meaning        |
| -------- | -------------- |
| `>`      | Overwrite file |
| `>>`     | Append to file |

---

### 5️⃣ What is `$?` in shell?

Stores exit status of last command.

0 → Success
Non-zero → Failure

---

### 6️⃣ Difference between `[ ]` and `[[ ]]`?

* `[ ]` → Traditional test
* `[[ ]]` → Modern, safer, supports pattern matching

---

### 7️⃣ How do you pass arguments to a script?

Using:

```bash
$1 $2 $@
```

---

### 8️⃣ What is `chmod 755`?

* Owner → rwx
* Group → r-x
* Others → r-x

---

# 🟡 Intermediate Level Questions

---

### 9️⃣ What is `set -euo pipefail`?

Production strict mode:

* `-e` → Exit on error
* `-u` → Undefined variable error
* `pipefail` → Fail pipeline if any command fails

---

### 🔟 What is a subshell?

A child shell started using:

```bash
( command )
```

Changes inside subshell do not affect parent.

---

### 11️⃣ Difference between `$@` and `$*`?

* `$@` → Preserves argument separation
* `$*` → Combines arguments into single string

Best practice: Use `$@`

---

### 12️⃣ How do you debug a shell script?

* `bash -x script.sh`
* `set -x`
* Check exit code
* Use logging
* Use ShellCheck

---

### 13️⃣ What is the difference between `exec` and `source`?

* `source file.sh` → Runs in current shell
* `exec` → Replaces current process

---

### 14️⃣ How do you schedule a script daily?

Using cron:

```bash
0 2 * * * /path/script.sh
```

---

### 15️⃣ How to prevent command injection?

* Quote variables
* Avoid eval
* Validate input
* Use `--` before filenames

---

# 🔴 Advanced / DevOps Level Questions

---

### 16️⃣ How would you design a production-ready shell script?

Include:

* Strict mode
* Logging
* Error handling
* Argument parsing
* Help menu
* Modular structure
* Security validation

---

### 17️⃣ How do you handle retry logic?

Use loop with counter + sleep + exit condition.

---

### 18️⃣ How do you handle graceful shutdown?

Use `trap` with SIGTERM.

Example:

```bash
trap cleanup SIGTERM
```

---

### 19️⃣ How do you test shell scripts in CI?

* bash -n
* ShellCheck
* Unit tests
* Mock external dependencies
* Fail pipeline on error

---

### 20️⃣ How to optimize large log processing script?

* Avoid useless pipes
* Use grep instead of awk when possible
* Use xargs -P for parallelism
* Use built-in Bash features
* Benchmark using time

---

### 21️⃣ How to securely store secrets in shell scripts?

* Use environment variables
* Use .env file with 600 permission
* Use secret managers (AWS Secrets Manager, Vault)

---

### 22️⃣ How to monitor background jobs?

* `jobs`
* `ps aux`
* `wait`
* Logging + exit codes

---

### 23️⃣ What are common production mistakes?

❌ Not using strict mode
❌ Not quoting variables
❌ Using eval
❌ Hardcoding secrets
❌ Not handling errors
❌ Ignoring exit codes

---

# 🔥 Scenario-Based Interview Questions

---

### Scenario 1:

Disk usage is 95%.
How will you automate alert?

Answer:

* Write script using `df`
* Extract usage using `awk`
* Compare threshold
* Send alert (mail / webhook)
* Schedule using cron

---

### Scenario 2:

Deployment script continues even if build fails.

Answer:
Use:

```bash
set -e
```

Or check exit code explicitly.

---

### Scenario 3:

Script works manually but fails in cron.

Possible Reasons:

* PATH issue
* Missing environment variables
* Relative path used
* Permission problem

---

# 🔥 Bonus DevOps Question

### How do you make shell scripts idempotent?

Idempotent = Running multiple times does not break system.

Example:

Instead of:

```bash
mkdir folder
```

Use:

```bash
mkdir -p folder
```

---

# 🟣 2️⃣4️⃣ Real-World Projects – Complete Practical Implementations

This chapter gives you **real, industry-style projects**.

These projects are useful for:

* Resume
* Interview discussion
* DevOps portfolio
* Production understanding

---

# 🟢 Project 1 – Server Monitoring Script

## 🎯 Objective

Monitor:

* CPU usage
* Memory usage
* Disk usage
* Service status

---

## 📜 Script: `server_monitor.sh`

```bash
#!/usr/bin/env bash
set -euo pipefail

THRESHOLD=80
LOG_FILE="monitor.log"

log() {
    echo "[$(date +'%Y-%m-%d %H:%M:%S')] $1" | tee -a "$LOG_FILE"
}

check_disk() {
    usage=$(df / | awk 'NR==2 {print $5}' | tr -d '%')
    if [[ "$usage" -gt "$THRESHOLD" ]]; then
        log "Disk usage high: $usage%"
    else
        log "Disk usage normal: $usage%"
    fi
}

check_memory() {
    free_mem=$(free | awk '/Mem/ {printf("%.0f"), $4/$2 * 100}')
    log "Free memory: $free_mem%"
}

check_service() {
    if systemctl is-active --quiet nginx; then
        log "Nginx running"
    else
        log "Nginx down"
    fi
}

main() {
    check_disk
    check_memory
    check_service
}

main
```

---

## 🕒 Schedule with Cron

```bash
*/10 * * * * /home/user/server_monitor.sh >> monitor.log 2>&1
```

---

# 🟢 Project 2 – Docker Auto Deployment Script

## 🎯 Objective

Automate:

* Pull latest code
* Build Docker image
* Restart container

---

## 📜 Script: `deploy_docker.sh`

```bash
#!/usr/bin/env bash
set -euo pipefail

APP_NAME="myapp"
CONTAINER="myapp_container"

log() {
    echo "[$(date +'%Y-%m-%d %H:%M:%S')] $1"
}

log "Pulling latest code..."
git pull origin main

log "Building Docker image..."
docker build -t "$APP_NAME" .

log "Stopping old container..."
docker rm -f "$CONTAINER" 2>/dev/null || true

log "Starting container..."
docker run -d --name "$CONTAINER" -p 8080:80 "$APP_NAME"

log "Deployment complete."
```

---

# 🟢 Project 3 – Log Analyzer Script

## 🎯 Objective

Analyze logs:

* Count ERROR
* Count WARNING
* Show top 5 frequent messages

---

## 📜 Script: `log_analyzer.sh`

```bash
#!/usr/bin/env bash
set -euo pipefail

LOG_FILE="$1"

if [[ ! -f "$LOG_FILE" ]]; then
    echo "Log file not found"
    exit 1
fi

echo "Total ERROR count:"
grep -c "ERROR" "$LOG_FILE"

echo "Total WARNING count:"
grep -c "WARNING" "$LOG_FILE"

echo "Top 5 frequent lines:"
sort "$LOG_FILE" | uniq -c | sort -nr | head -5
```

---

## Run:

```bash
./log_analyzer.sh app.log
```

---

# 🟢 Project 4 – AWS EC2 Automation

## 🎯 Objective

Start/Stop EC2 instance safely.

---

## 📜 Script: `ec2_control.sh`

```bash
#!/usr/bin/env bash
set -euo pipefail

INSTANCE_ID="$1"
ACTION="$2"

if [[ "$ACTION" == "start" ]]; then
    aws ec2 start-instances --instance-ids "$INSTANCE_ID"
elif [[ "$ACTION" == "stop" ]]; then
    aws ec2 stop-instances --instance-ids "$INSTANCE_ID"
else
    echo "Usage: $0 <instance-id> <start|stop>"
    exit 1
fi
```

---

## Run:

```bash
./ec2_control.sh i-123456 start
```

---

# 🟢 Project 5 – CI/CD Deployment Pipeline Script

## 🎯 Objective

Automate:

* Code pull
* Test
* Build
* Deploy
* Restart service

---

## 📜 Script: `ci_deploy.sh`

```bash
#!/usr/bin/env bash
set -euo pipefail

log() {
    echo "[$(date +'%Y-%m-%d %H:%M:%S')] $1"
}

log "Pulling code..."
git pull origin main

log "Running tests..."
npm test

log "Building project..."
npm run build

log "Restarting service..."
sudo systemctl restart myapp

log "Deployment successful."
```

---

# 🔥 How to Add These to Resume

You can write:

> Developed production-ready shell scripts for server monitoring, Docker automation, AWS EC2 management, log analysis, and CI/CD deployment pipelines.

---

# 🔥 How to Improve These Projects

To make them enterprise-level:

✅ Add argument parsing
✅ Add logging to file
✅ Add help menu
✅ Add retry logic
✅ Add environment configuration
✅ Add unit tests
✅ Add CI validation
✅ Dockerize scripts

---

# 📌 Final Summary – What You Learned

You now understand:

✔ Shell basics
✔ Variables & operators
✔ Loops & conditionals
✔ Functions & arrays
✔ Text processing
✔ Process management
✔ Error handling
✔ Debugging & logging
✔ Security best practices
✔ Performance optimization
✔ Production-ready script design
✔ Cron automation
✔ DevOps scripting
✔ Testing & CI integration
✔ Real-world projects

---

