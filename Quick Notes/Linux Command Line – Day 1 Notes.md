# Linux Command Line – Day 1 Notes

## 1. What is Linux?

**Linux** is an open-source operating system based on the Linux kernel. It is widely used in:

- Servers
- Cloud computing
- AWS
- DevOps
- Cybersecurity
- Software development
- Networking
- Embedded systems

Linux can be operated using two major interfaces:

### GUI – Graphical User Interface
Users interact with the system using:

- Windows
- Icons
- Menus
- Mouse

### CLI – Command Line Interface
Users interact with the system by typing commands.

Example:

```bash
ls
```

The command displays files and directories.

---

# 2. What is the Terminal?

A **Terminal** is an application that allows us to interact with the operating system using commands.

Examples:

- Linux Terminal
- macOS Terminal
- Windows Terminal
- Termux on Android

### Important Difference

```text
Terminal ≠ Shell ≠ Linux
```

### Terminal

A program that provides an interface for entering commands.

### Shell

A program that interprets commands and executes them.

Common shells:

```text
Bash
Zsh
Fish
```

### Linux

The operating system/kernel environment on which commands and programs run.

---

# 3. Command Prompt

When we open a terminal, we usually see something similar to:

```text
akash@ubuntu:~$
```

Different parts represent different information:

```text
akash     → Username
@         → Separator
ubuntu    → Hostname
~         → Current directory
$         → Normal user
```

A root user generally sees:

```text
#
```

For example:

```text
root@ubuntu:/#
```

### `$` vs `#`

```text
$ → Normal user
# → Root user
```

The root user has administrative privileges.

> **Warning:** Do not use `sudo` or root privileges unnecessarily. A wrong command executed as root can seriously affect the system.

---

# 4. Linux File System

Linux uses a hierarchical file system.

The top-level directory is:

```text
/
```

This is called the **root directory**.

Example:

```text
                    /
                    |
       +------------+------------+
       |            |            |
      home         etc          var
       |
       |
    student
       |
   +---+---------+
   |             |
Documents     Downloads
```

Some important directories:

| Directory | Purpose |
|---|---|
| `/` | Root of the filesystem |
| `/home` | Home directories of users |
| `/etc` | Configuration files |
| `/var` | Variable data such as logs |
| `/tmp` | Temporary files |
| `/usr` | User programs and utilities |

---

# 5. Special Directory Symbols

Linux uses special symbols to represent locations.

### `/`

Root directory.

Example:

```bash
cd /
```

Moves to the root directory.

### `~`

Current user's home directory.

Example:

```bash
cd ~
```

### `.`

Current directory.

```text
.
```

means "the directory I am currently in."

### `..`

Parent directory.

Example:

```bash
cd ..
```

Moves one level up.

---

# 6. Basic Linux Command Syntax

Most Linux commands follow a general pattern:

```bash
command [options] [arguments]
```

Example:

```bash
ls -l /home
```

Here:

```text
ls       → Command
-l       → Option
/home    → Argument
```

Another example:

```bash
mkdir linux
```

```text
mkdir    → Command
linux    → Argument
```

---

# 7. `pwd` – Print Working Directory

### Purpose

Displays the current directory.

### Syntax

```bash
pwd
```

### Example

```bash
pwd
```

Output:

```text
/home/akash
```

This tells us where we currently are.

### Remember

```text
pwd = Print Working Directory
```

---

# 8. `ls` – List Files and Directories

### Purpose

Displays files and directories in the current location.

### Syntax

```bash
ls
```

Example:

```bash
ls
```

Output:

```text
Documents
Downloads
notes.txt
projects
```

---

## `ls -l`

Displays detailed information.

```bash
ls -l
```

Example output:

```text
-rw-r--r-- 1 akash akash 120 Sep 1 notes.txt
```

It provides information such as:

- File permissions
- Owner
- Group
- File size
- Date
- File name

---

## `ls -a`

Displays hidden files.

```bash
ls -a
```

Linux hidden files usually start with:

```text
.
```

Example:

```text
.
..
.bashrc
.profile
notes.txt
```

---

## `ls -la`

Combines both options:

```bash
ls -la
```

It displays:

- Detailed information
- Hidden files

---

# 9. `cd` – Change Directory

### Purpose

Used to move from one directory to another.

### Syntax

```bash
cd directory_name
```

Example:

```bash
cd Documents
```

Now we enter the `Documents` directory.

---

### Go to Parent Directory

```bash
cd ..
```

Example:

```text
/home/akash/Documents
```

After:

```bash
cd ..
```

we move to:

```text
/home/akash
```

---

### Go to Home Directory

```bash
cd ~
```

---

### Go to Root Directory

```bash
cd /
```

---

### Go to Previous Directory

```bash
cd -
```

This switches to the previous working directory.

---

# 10. `mkdir` – Make Directory

### Purpose

Creates a new directory.

### Syntax

```bash
mkdir directory_name
```

Example:

```bash
mkdir linux
```

Check:

```bash
ls
```

You should see:

```text
linux
```

---

# 11. `touch` – Create a File

### Purpose

Creates an empty file if the file does not already exist.

### Syntax

```bash
touch filename
```

Example:

```bash
touch notes.txt
```

Create multiple files:

```bash
touch file1.txt file2.txt file3.txt
```

Check:

```bash
ls
```

---

# 12. `cp` – Copy Files

### Purpose

Copies a file or directory.

### Syntax

```bash
cp source destination
```

Example:

```bash
cp file1.txt file2.txt
```

This creates a copy of `file1.txt` named `file2.txt`.

Another example:

```bash
cp notes.txt backup.txt
```

---

# 13. `mv` – Move or Rename

The `mv` command is used for two common purposes:

1. Move files/directories
2. Rename files/directories

---

## Rename a File

```bash
mv old.txt new.txt
```

Example:

```bash
mv file1.txt student.txt
```

---

## Move a File

```bash
mv student.txt Documents/
```

The file is moved into the `Documents` directory.

---

# 14. `rm` – Remove

### Purpose

Deletes files.

### Syntax

```bash
rm filename
```

Example:

```bash
rm file1.txt
```

Check:

```bash
ls
```

The file will no longer appear.

### Important

Be careful with `rm`.

Unlike a normal GUI recycle bin, deleted files may not be easily recoverable.

Do not blindly execute commands such as:

```bash
rm -rf
```

especially with administrative privileges.

---

# 15. `echo` – Display Text

### Purpose

Displays text on the terminal.

Example:

```bash
echo "Hello Linux"
```

Output:

```text
Hello Linux
```

---

## Using `echo` to Write to a File

```bash
echo "Hello Linux" > notes.txt
```

Now:

```bash
cat notes.txt
```

Output:

```text
Hello Linux
```

---

# 16. Output Redirection

The `>` symbol redirects output into a file.

Example:

```bash
echo "Hello" > file.txt
```

If the file does not exist:

```text
File is created
```

If the file already exists:

```text
Existing content is overwritten
```

---

## `>>` – Append

The `>>` operator adds content to the end of a file.

Example:

```bash
echo "Second Line" >> file.txt
```

Now the previous content remains and the new content is added.

### Difference

```text
>    → Overwrite
>>   → Append
```

---

# 17. `cat` – Display File Content

### Purpose

Displays the contents of a file.

### Syntax

```bash
cat filename
```

Example:

```bash
cat notes.txt
```

Output:

```text
Hello Linux
Second Line
```

---

# 18. `whoami` – Current User

### Purpose

Displays the username of the currently logged-in user.

```bash
whoami
```

Example output:

```text
akash
```

---

# 19. `date` – Display Date and Time

```bash
date
```

Example output:

```text
Tue Sep 1 12:30:00 IST 2026
```

The exact output depends on the system.

---

# 20. `uname` – System Information

### Basic command

```bash
uname
```

Displays the operating system/kernel name.

Example:

```text
Linux
```

### Detailed information

```bash
uname -a
```

This provides detailed system information such as:

- Kernel name
- Hostname
- Kernel version
- Architecture
- Operating system information

---

# 21. `clear` – Clear Terminal

### Purpose

Clears the visible terminal screen.

```bash
clear
```

Shortcut in many terminals:

```text
Ctrl + L
```

---

# 22. `history` – Command History

### Purpose

Displays previously executed commands.

```bash
history
```

Example:

```text
1  pwd
2  ls
3  cd Documents
4  mkdir linux
5  ls
```

This is useful when you want to find or repeat a previous command.

---

# 23. `man` – Manual Pages

Linux provides documentation for many commands.

### Syntax

```bash
man command
```

Example:

```bash
man ls
```

This opens the manual page for `ls`.

To exit:

```text
q
```

---

# 24. `--help`

Many commands provide quick help using:

```bash
--help
```

Example:

```bash
ls --help
```

This provides information about the command and its available options.

---

# 25. Important Commands – Quick Reference

| Command | Meaning | Purpose |
|---|---|---|
| `pwd` | Print Working Directory | Show current location |
| `ls` | List | Show files/directories |
| `cd` | Change Directory | Move between directories |
| `mkdir` | Make Directory | Create directory |
| `touch` | — | Create empty file |
| `cp` | Copy | Copy files/directories |
| `mv` | Move | Move or rename |
| `rm` | Remove | Delete files |
| `cat` | Concatenate | Display file contents |
| `echo` | — | Display/write text |
| `whoami` | — | Show current user |
| `date` | — | Show date/time |
| `uname` | Unix Name | Show system information |
| `clear` | — | Clear terminal |
| `history` | — | Show command history |
| `man` | Manual | Open command documentation |

---

# 26. Practical Example

Let's perform a complete small task.

### Step 1: Check current location

```bash
pwd
```

### Step 2: Create a directory

```bash
mkdir linux_lab
```

### Step 3: Enter the directory

```bash
cd linux_lab
```

### Step 4: Create files

```bash
touch student.txt linux.txt commands.txt
```

### Step 5: Check files

```bash
ls
```

### Step 6: Rename a file

```bash
mv linux.txt linux_commands.txt
```

### Step 7: Copy a file

```bash
cp student.txt student_backup.txt
```

### Step 8: Add content

```bash
echo "I am learning Linux" > student.txt
```

### Step 9: Display content

```bash
cat student.txt
```

Output:

```text
I am learning Linux
```

### Step 10: Go back

```bash
cd ..
```

### Step 11: Enter again

```bash
cd linux_lab
```

### Step 12: Show all files

```bash
ls -la
```

---

# 27. Day 1 Practice Task

Complete the following without looking at the commands above.

### Task

Starting from your home directory:

1. Create a directory named `linux_practice`.
2. Enter the directory.
3. Create the following files:
   - `student.txt`
   - `linux.txt`
   - `commands.txt`
4. Display all files.
5. Rename `linux.txt` to `linux_commands.txt`.
6. Create a backup of `student.txt`.
7. Write the following text into `student.txt`:

```text
I am learning Linux Command Line.
```

8. Display the contents of `student.txt`.
9. Add another line:

```text
Linux is widely used in servers and cloud computing.
```

10. Display the file again.
11. Go to the parent directory.
12. Enter `linux_practice` again.
13. Display detailed information including hidden files.

### Commands you should be able to use

```text
pwd
ls
ls -la
cd
mkdir
touch
cp
mv
echo
cat
```

---

# 28. Key Points to Remember

### File system

```text
/       → Root directory
~       → Home directory
.       → Current directory
..      → Parent directory
```

### File operations

```text
touch   → Create
cp      → Copy
mv      → Move/Rename
rm      → Delete
```

### Viewing information

```text
pwd     → Current location
ls      → Files/directories
cat     → File content
whoami  → Current user
uname   → System information
```

### Redirection

```text
>       → Overwrite
>>      → Append
```

### Getting help

```bash
man command
```

or:

```bash
command --help
```

---

# Day 1 Goal

By the end of this class, you should be able to:

- Understand what CLI and Terminal are.
- Understand the basic Linux filesystem.
- Navigate directories using `pwd`, `ls`, and `cd`.
- Create files and directories.
- Copy, move, rename and delete files.
- Read file contents.
- Write content to files.
- Understand basic output redirection.
- Check basic system/user information.
- Find help using `man` and `--help`.

**Don't try to memorize every command.** Focus on understanding what problem each command solves and practice using it repeatedly.