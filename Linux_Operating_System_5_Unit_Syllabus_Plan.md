# Linux Operating System — Complete Syllabus Plan

## Course Context

**Target Students:** 1st Year Engineering / Computer Science Students  
**Prerequisite:** No prior Linux or Operating System knowledge required  
**Weekly Teaching Time:** 3 Hours  
**Suggested Duration:** 15 Weeks  
**Total Teaching Hours:** 45 Hours  
**Units:** 5

---

# Course Philosophy

This course is designed for first-year students who may have limited knowledge of computers.

The teaching approach should be:

> **Concept → Demonstration → Hands-on Practice → Challenge → Real-World Connection**

The course should not be taught as a list of Linux commands. Students should gradually understand:

```text
Computer
   ↓
Hardware
   ↓
Operating System
   ↓
Linux
   ↓
Kernel
   ↓
Shell
   ↓
Commands
   ↓
Files & Permissions
   ↓
Processes
   ↓
Networking
   ↓
Shell Scripting
   ↓
Automation / Mini Project
```

## Recommended Weekly Structure

| Activity | Time |
|---|---:|
| Concept / Theory | 40–50 min |
| Live Demonstration | 20–30 min |
| Hands-on Lab | 90 min |
| Challenge / Discussion | 20–30 min |
| **Total** | **3 Hours** |

---

# UNIT 1 — Computer Fundamentals, OS & Introduction to Linux

**Suggested Duration:** 3 Weeks  
**Hours:** 9

## Learning Objective

Students should understand what a computer is, how hardware and software interact, why an Operating System is required, and what Linux is.

---

## 1.1 Computer Fundamentals

### Topics

- What is a Computer?
- Hardware vs Software
- CPU
- RAM
- Storage
- Input Devices
- Output Devices
- Motherboard
- Basic understanding of programs
- Application Software vs System Software

### Practical / Demonstration

Show what happens when a student opens an application:

```text
Application stored on Disk
        ↓
Loaded into RAM
        ↓
CPU executes instructions
        ↓
Output displayed
```

---

## 1.2 Operating System Fundamentals

### Topics

- What is an Operating System?
- Why do we need an OS?
- Major functions of an OS
- Resource Management
- Process Management
- Memory Management
- File Management
- Device Management
- Security and Protection
- User Interface

### Important Concept

```text
User
  ↓
Application
  ↓
Operating System
  ↓
Hardware
```

---

## 1.3 Linux Introduction

### Topics

- What is Linux?
- Linux Kernel
- Linux Distribution
- Linux vs Windows vs macOS
- Linux Desktop vs Linux Server
- Open Source concept
- Advantages of Linux
- Where Linux is used
- Linux in servers
- Linux in cloud computing
- Linux in Android
- Linux in embedded systems
- Linux in cybersecurity
- Linux in supercomputers

### Linux Distributions

Introduce:

- Ubuntu
- Debian
- Fedora
- Arch Linux
- Linux Mint
- Rocky Linux

Focus practically on **Ubuntu**.

---

## 1.4 Linux Architecture

```text
+----------------------+
|        User          |
+----------------------+
           ↓
+----------------------+
|    Applications      |
+----------------------+
           ↓
+----------------------+
|   Shell / Utilities  |
+----------------------+
           ↓
+----------------------+
|    Linux Kernel      |
+----------------------+
           ↓
+----------------------+
|      Hardware        |
+----------------------+
```

### Topics

- Kernel
- Shell
- User Space
- Kernel Space
- System Calls
- Hardware

---

## UNIT 1 PRACTICALS

Students should perform:

```bash
whoami
pwd
date
uname
clear
ls
```

### Mini Challenge

> Explore the Linux environment and identify the current user, current directory, operating system information and kernel information.

---

# UNIT 2 — Linux Terminal, Files & File System

**Suggested Duration:** 3 Weeks  
**Hours:** 9

## Learning Objective

Students should become comfortable using the Linux command line and managing files/directories without a GUI.

---

# 2.1 Linux Terminal & Shell

### Topics

- What is Terminal?
- What is Shell?
- Terminal vs Shell
- Bash
- Command Structure

```text
command [options] [arguments]
```

Example:

```bash
ls -l /home
```

---

# 2.2 Navigation Commands

### Commands

```bash
pwd
ls
cd
```

### Options

```bash
ls -l
ls -a
ls -la
```

### Practice

Navigate through:

```text
/home
/home/student
Documents
Downloads
```

---

# 2.3 Creating and Managing Files

### Commands

```bash
mkdir
touch
cp
mv
rm
rmdir
```

### Practical

Create:

```text
College/
├── Java/
├── Linux/
├── DSA/
└── Projects/
```

---

# 2.4 Reading and Writing Files

### Commands

```bash
cat
less
head
tail
echo
```

### Redirection

```bash
>
>>
<
```

Example:

```bash
echo "Hello Linux" > notes.txt
echo "Operating System" >> notes.txt
cat notes.txt
```

---

# 2.5 Linux File System

### Linux Directory Structure

```text
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
├── tmp
├── usr
└── var
```

### Important Directories

| Directory | Purpose |
|---|---|
| `/` | Root directory |
| `/home` | User home directories |
| `/etc` | Configuration files |
| `/tmp` | Temporary files |
| `/var` | Variable data and logs |
| `/usr` | User programs/utilities |
| `/dev` | Device files |
| `/proc` | Process/kernel information |

---

# 2.6 Searching

### Commands

```bash
find
grep
```

Examples:

```bash
find . -name "*.txt"
```

```bash
grep "Java" notes.txt
```

---

# UNIT 2 PRACTICALS

Students should be able to:

1. Create directories.
2. Create files.
3. Copy files.
4. Move files.
5. Delete files.
6. Read files.
7. Search files.
8. Search text inside files.
9. Navigate the Linux file system.

### Challenge

Create:

```text
College/
├── Java/
│   ├── notes.txt
│   └── programs/
├── Linux/
│   ├── notes.txt
│   └── commands/
└── DSA/
    └── questions/
```

Then:

- Add content to the files.
- Search for a specific word.
- Find all `.txt` files.
- Save search results into another file.

---

# UNIT 3 — Linux Permissions, Users, Processes & System Management

**Suggested Duration:** 3 Weeks  
**Hours:** 9

## Learning Objective

Students should understand how Linux controls access to files, manages users, and manages running programs/processes.

---

# 3.1 Linux Users

### Topics

- User concept
- Root user
- Normal user
- User ID
- Group ID
- Groups

### Commands

```bash
whoami
id
groups
who
```

---

# 3.2 File Permissions

### Understanding

```bash
ls -l
```

Example:

```text
-rwxr-xr--
```

Breakdown:

```text
-    rwx    r-x    r--
     ↓      ↓      ↓
    User   Group  Others
```

### Permissions

```text
r = Read
w = Write
x = Execute
```

---

# 3.3 chmod

### Symbolic Mode

```bash
chmod u+x script.sh
chmod u-w file.txt
chmod g+r file.txt
```

### Numeric Mode

```bash
chmod 755 script.sh
chmod 644 notes.txt
```

Explain:

```text
4 = read
2 = write
1 = execute
```

---

# 3.4 Ownership

### Commands

```bash
chown
chgrp
```

Explain:

```text
File
 ↓
Owner
 ↓
Group
 ↓
Permissions
```

---

# 3.5 Processes

### Concepts

- Program vs Process
- Process ID
- Process State
- Foreground Process
- Background Process
- Process Creation
- Process Termination

### Commands

```bash
ps
top
htop
kill
jobs
```

---

# 3.6 Background Processes

### Commands

```bash
command &
jobs
fg
bg
```

Example:

```bash
sleep 100 &
```

---

# 3.7 System Information

### Commands

```bash
uname
uptime
free
df
du
hostname
```

Students should understand:

- CPU
- Memory
- Disk
- Uptime
- Kernel
- System information

---

# UNIT 3 PRACTICALS

### Practical 1

Create a file and experiment with:

```bash
chmod
```

### Practical 2

Create a shell script and make it executable.

### Practical 3

Start a process, find its PID and terminate it.

### Practical 4

Check system RAM and disk usage.

### Challenge

Create a script that:

```text
Displays:
------------------------
System Information
------------------------
Username
Hostname
Kernel
RAM
Disk
Uptime
------------------------
```

---

# UNIT 4 — Shell Scripting, Pipes, Networking & Package Management

**Suggested Duration:** 3 Weeks  
**Hours:** 9

## Learning Objective

Students should learn how to automate Linux tasks using Bash and understand basic networking and package management.

---

# 4.1 Bash Shell Scripting

### First Script

```bash
#!/bin/bash

echo "Hello Linux"
```

Run:

```bash
chmod +x script.sh
./script.sh
```

---

# 4.2 Variables

```bash
name="Akash"

echo $name
```

### Topics

- Variables
- Environment variables
- Command substitution

Example:

```bash
today=$(date)
echo $today
```

---

# 4.3 User Input

```bash
read name
echo "Hello $name"
```

---

# 4.4 Conditional Statements

### if / else

```bash
if [ $age -ge 18 ]
then
    echo "Adult"
else
    echo "Minor"
fi
```

### Operators

- `-eq`
- `-ne`
- `-gt`
- `-lt`
- `-ge`
- `-le`

---

# 4.5 Loops

### for loop

```bash
for i in 1 2 3 4 5
do
    echo $i
done
```

### while loop

```bash
i=1

while [ $i -le 5 ]
do
    echo $i
    i=$((i+1))
done
```

---

# 4.6 Functions

```bash
greet() {
    echo "Hello Linux"
}

greet
```

---

# 4.7 Pipes

### Concept

```text
Command A
    ↓
    |
    ↓
Command B
```

Example:

```bash
ps aux | grep java
```

---

# 4.8 Redirection

```bash
>
>>
<
|
```

Examples:

```bash
ls > files.txt
```

```bash
cat file.txt | grep Java
```

---

# 4.9 Basic Networking

### Topics

- Network basics
- IP Address
- Hostname
- Client and Server
- Internet basics

### Commands

```bash
ip addr
ping
curl
wget
hostname
```

Examples:

```bash
ping google.com
```

```bash
curl example.com
```

---

# 4.10 Package Management

For Ubuntu:

```bash
sudo apt update
sudo apt install
sudo apt remove
```

### Concepts

- Package
- Repository
- Package Manager
- `sudo`
- Software installation in Linux

---

# UNIT 4 PRACTICALS

### Practical 1

Write a Bash script to take a student's name and marks and display the result.

### Practical 2

Write a script to print numbers from 1 to 10.

### Practical 3

Write a script to check whether a number is even or odd.

### Practical 4

Use pipes to search running processes.

### Practical 5

Check the system's IP address and test network connectivity.

### Practical 6

Install and remove a package using `apt`.

---

# UNIT 5 — Linux Administration, System Calls, Automation & Mini Project

**Suggested Duration:** 3 Weeks  
**Hours:** 9

## Learning Objective

Students should connect Linux usage with Operating System concepts and build a small practical automation project.

---

# 5.1 Linux System Administration Basics

### Topics

- Root privileges
- `sudo`
- Users and groups
- File permissions
- Environment variables
- Services
- Logs
- System monitoring

---

# 5.2 Services

Introduce:

```bash
systemctl
```

Examples:

```bash
systemctl status
```

Explain the concept of:

```text
Service
   ↓
Background Process
   ↓
Provides functionality to system/users
```

---

# 5.3 Logs

Introduce:

```bash
/var/log
```

Basic commands:

```bash
cat
less
tail
grep
```

Example:

```bash
tail /var/log/syslog
```

---

# 5.4 System Calls

Connect Linux to Operating System concepts.

```text
Application
     ↓
System Call
     ↓
Linux Kernel
     ↓
Hardware
```

Introduce:

```text
open()
read()
write()
close()
fork()
exec()
wait()
```

Explain the purpose of system calls rather than going deeply into kernel programming.

---

# 5.5 Process Creation Concepts

Introduce:

- Process creation
- Parent process
- Child process
- `fork()`
- `exec()`
- `wait()`

Conceptual flow:

```text
Parent Process
      |
    fork()
      |
  +---+---+
  |       |
Parent   Child
          |
        exec()
          |
      New Program
```

---

# 5.6 Automation

Students should understand why scripting matters.

Example:

Instead of manually executing:

```bash
df
free
uptime
ip addr
```

Create:

```bash
system-info.sh
```

and execute:

```bash
./system-info.sh
```

---

# 5.7 Mini Project

Students should complete one Linux/Bash project.

## Project Option 1 — Student Management System

Features:

```text
=========================
 Student Management
=========================

1. Add Student
2. View Students
3. Search Student
4. Delete Student
5. Exit
```

Concepts used:

- Bash
- Variables
- Functions
- Files
- `grep`
- Conditions
- Loops
- User input

---

## Project Option 2 — Linux System Information Tool

Output:

```text
============================
 Linux System Information
============================

User:
Hostname:
OS:
Kernel:
RAM:
Disk:
IP Address:
Uptime:

============================
```

Commands used:

```bash
whoami
hostname
uname
free
df
ip
uptime
```

---

## Project Option 3 — Backup Automation Tool

Create:

```bash
backup.sh
```

The script should:

1. Ask for a directory.
2. Create a backup directory.
3. Copy files.
4. Add date/time to backup name.
5. Display backup status.

Example:

```text
backup_2026-08-11_10-30
```

---

# 15-WEEK COURSE PLAN

| Week | Unit | Main Topics | Practical Focus |
|---|---|---|---|
| 1 | Unit 1 | Computer Fundamentals | CPU, RAM, Storage |
| 2 | Unit 1 | Operating System | OS functions |
| 3 | Unit 1 | Linux Introduction | Ubuntu + Linux architecture |
| 4 | Unit 2 | Terminal & Shell | `pwd`, `ls`, `cd` |
| 5 | Unit 2 | Files & Directories | `mkdir`, `touch`, `cp`, `mv`, `rm` |
| 6 | Unit 2 | File System & Searching | `cat`, `find`, `grep`, redirection |
| 7 | Unit 3 | Users & Permissions | `whoami`, `chmod`, `chown` |
| 8 | Unit 3 | Processes | `ps`, `top`, `kill` |
| 9 | Unit 3 | System Management | RAM, disk, system information |
| 10 | Unit 4 | Bash Basics | Variables, input, output |
| 11 | Unit 4 | Conditions & Loops | `if`, `for`, `while` |
| 12 | Unit 4 | Pipes & Networking | `|`, `grep`, `ping`, `curl` |
| 13 | Unit 5 | Package Management & Services | `apt`, `systemctl` |
| 14 | Unit 5 | System Calls & Automation | `fork`, `exec`, scripts |
| 15 | Unit 5 | Mini Project | Project presentation |

---

# Core Linux Commands Checklist

Students should be comfortable with these commands by the end of the course.

## Basic

```bash
pwd
ls
cd
clear
whoami
date
uname
```

## Files

```bash
touch
mkdir
cp
mv
rm
rmdir
```

## Reading

```bash
cat
less
head
tail
echo
```

## Searching

```bash
find
grep
```

## Permissions

```bash
chmod
chown
chgrp
```

## Users

```bash
whoami
id
groups
who
```

## Processes

```bash
ps
top
htop
kill
jobs
fg
bg
```

## System

```bash
free
df
du
uptime
hostname
```

## Networking

```bash
ip
ping
curl
wget
```

## Packages

```bash
apt
sudo
```

## Services

```bash
systemctl
```

---

# Assessment Strategy

## 1. Weekly Linux Challenges

Every week give 3–5 practical problems.

Example:

> Create a directory called `assignment`, create three files, add content, search for a word and save the result into `output.txt`.

---

## 2. Practical Assignments

Suggested assignments:

### Assignment 1
Linux terminal navigation

### Assignment 2
File and directory management

### Assignment 3
Searching and redirection

### Assignment 4
File permissions

### Assignment 5
Process management

### Assignment 6
Bash variables and input

### Assignment 7
Conditions and loops

### Assignment 8
Pipes and networking

### Assignment 9
System information script

### Assignment 10
Mini Linux automation project

---

# Suggested Evaluation

| Component | Weight |
|---|---:|
| Weekly Linux Challenges | 15% |
| Practical Assignments | 20% |
| Mid-Term Practical | 15% |
| Theory / Quiz | 10% |
| Mini Project | 25% |
| Final Practical / Viva | 15% |
| **Total** | **100%** |

---

# Course Outcomes

After completing the course, students should be able to:

### CO1
Explain basic computer hardware, Operating System concepts and Linux architecture.

### CO2
Use the Linux command line to navigate and manage files and directories.

### CO3
Apply Linux permissions, user management and process management concepts.

### CO4
Write basic Bash shell scripts for automation and problem solving.

### CO5
Perform basic Linux networking, package management and system monitoring.

### CO6
Connect Operating System concepts such as processes, system calls and resource management with practical Linux behavior.

### CO7
Develop a small Linux/Bash automation project.

---

# Teaching Rules for the Instructor

## Rule 1 — Don't teach commands in isolation

Avoid:

> "Today we will learn 15 commands."

Prefer:

> "Today we need to solve this problem. Which Linux commands can help us?"

---

## Rule 2 — Every lecture should contain a practical

Even theory classes should include a short terminal demonstration.

---

## Rule 3 — Students should type the commands

Do not let the class become:

```text
Teacher types
       ↓
Students watch
       ↓
Students forget
```

Prefer:

```text
Explain
   ↓
Demonstrate
   ↓
Students type
   ↓
Students modify
   ↓
Students solve challenge
```

---

# Recommended First Lecture Sequence From Here

Since the first OS overview lecture is already completed, the next lectures should be:

### Next Lecture

**Computer Fundamentals + What Happens When You Open an Application?**

```text
Application
    ↓
RAM
    ↓
CPU
    ↓
OS
    ↓
Hardware
```

### Following Lecture

**Linux Introduction**

- Linux
- Kernel
- Distribution
- Ubuntu
- Linux vs Windows
- Linux use cases

### Following Practical

**Your First Linux Terminal**

```bash
pwd
ls
whoami
date
uname
clear
```

Then immediately give students a challenge.

---

# Final Course Goal

The course should take students from:

```text
"I don't know what Linux is."
```

to:

```text
"I can use Linux."
```

and finally:

```text
"I can solve problems and automate tasks using Linux."
```

The ultimate outcome should be **practical confidence**, not command memorization.
