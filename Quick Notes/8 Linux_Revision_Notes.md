# Linux & Shell Scripting -- Revision Notes

## Computer Fundamentals, Linux Basics, Terminal, Files, Searching and Redirection

**Level:** Beginner / First-year students\
**Platforms:** Ubuntu Linux and macOS Terminal\
**Purpose:** Revision after a study break and independent practical
preparation

------------------------------------------------------------------------

## Learning Outcomes

After studying these notes, you should be able to:

1.  Explain basic computer components and the role of an operating
    system.
2.  Differentiate the Linux kernel, shell and terminal.
3.  Navigate the filesystem using terminal commands.
4.  Create, copy, move, rename and delete files and directories.
5.  Read and write text files from the terminal.
6.  Explain Linux's directory hierarchy.
7.  Search for files using `find` and search file contents using `grep`.
8.  Redirect command output and connect commands using pipes.
9.  Complete a small file-management and search task independently.

------------------------------------------------------------------------

# Part 1 -- Computer Fundamentals

## 1. What is a Computer?

A computer is an electronic device that accepts input, processes data,
stores information and produces output.

The basic working cycle is:

``` mermaid
flowchart LR
    A[Input] --> B[Processing]
    B --> C[Output]
    B <--> D[Storage]
    classDef input fill:#dbeafe,stroke:#2563eb,color:#1e3a8a
    classDef process fill:#fef3c7,stroke:#d97706,color:#78350f
    classDef output fill:#dcfce7,stroke:#16a34a,color:#14532d
    classDef storage fill:#f3e8ff,stroke:#9333ea,color:#581c87
    class A input
    class B process
    class C output
    class D storage
```

### Example: Opening a web browser

1.  You click the browser icon -- input.
2.  The operating system loads the application into RAM.
3.  The CPU executes the required instructions -- processing.
4.  The browser window appears -- output.
5.  Browser data may be saved on storage.

## 2. Hardware vs Software

  -----------------------------------------------------------------------
  Hardware                            Software
  ----------------------------------- -----------------------------------
  Physical parts of a computer        Programs and instructions

  Can be physically touched           Cannot be physically touched

  Examples: CPU, RAM, SSD, keyboard   Examples: Linux, macOS, Chrome, VS
                                      Code
  -----------------------------------------------------------------------

### Important hardware components

-   **CPU (Central Processing Unit):** Executes instructions and
    performs calculations.
-   **RAM (Random Access Memory):** Temporary working memory used by
    running programs. It is volatile, meaning its contents are normally
    lost when power is removed.
-   **Storage (HDD/SSD):** Stores files, applications and the operating
    system even when the computer is switched off.
-   **Input devices:** Keyboard, mouse, microphone and camera.
-   **Output devices:** Monitor, speakers and printer.

### RAM vs Storage

  -----------------------------------------------------------------------
  RAM                                 Storage
  ----------------------------------- -----------------------------------
  Temporary working area              Long-term data storage

  Usually faster                      Usually slower than RAM

  Holds data used by active programs  Holds files and installed
                                      applications

  Volatile                            Non-volatile
  -----------------------------------------------------------------------

**Analogy:** Storage is like a cupboard where books are kept. RAM is
like the desk where you place the books you are currently studying.

------------------------------------------------------------------------

# Part 2 -- Operating System Fundamentals

## 3. What is an Operating System?

An **Operating System (OS)** is system software that manages computer
hardware and provides services to applications and users.

Examples include:

-   Windows
-   Linux
-   macOS
-   Android
-   iOS

Without an operating system, applications would have to manage hardware
directly, making the computer difficult to use.

## 4. Major Functions of an OS

  -----------------------------------------------------------------------
  Function                What it means           Example
  ----------------------- ----------------------- -----------------------
  Process management      Manages running         Running a browser and
                          programs                music player

  Memory management       Allocates and manages   Giving memory to a
                          RAM                     program

  File management         Organizes files and     Creating, reading and
                          folders                 deleting files

  Device management       Coordinates hardware    Using a printer or USB
                          devices                 drive

  Security and protection Controls access to      User accounts and
                          resources               permissions

  User interface          Provides a way to       Desktop GUI or terminal
                          interact                CLI
  -----------------------------------------------------------------------

## 5. CLI vs GUI

**GUI (Graphical User Interface):** Interaction through windows, icons,
menus and buttons.

**CLI (Command-Line Interface):** Interaction by typing commands into a
terminal.

  GUI                       CLI
  ------------------------- ------------------------------------------
  Visual interaction        Text-based interaction
  Easy for many new users   Requires command knowledge
  Useful for visual tasks   Useful for automation and administration
  Example: Finder           Example: `ls` in Terminal

------------------------------------------------------------------------

# Part 3 -- Introduction to Linux

## 6. What is Linux?

Linux is an open-source, Unix-like operating-system kernel.
Operating-system distributions combine the Linux kernel with system
tools, libraries, package managers and applications.

Examples of Linux distributions:

-   Ubuntu
-   Fedora
-   Debian
-   Linux Mint
-   Arch Linux

### Kernel vs Distribution

-   **Kernel:** The core part of the operating system. It manages CPU
    time, memory, devices and communication between software and
    hardware.
-   **Distribution (distro):** A complete operating-system package built
    around the Linux kernel.

For example, Ubuntu is a Linux distribution.

## 7. Linux Architecture

A simplified view of Linux architecture:

``` mermaid
flowchart TB
    A[User] --> B[Applications and Commands]
    B --> C[Shell]
    C --> D[System Libraries and System Calls]
    D --> E[Linux Kernel]
    E --> F[Hardware: CPU, RAM, Disk, Devices]
    classDef user fill:#dbeafe,stroke:#2563eb,color:#1e3a8a
    classDef app fill:#dcfce7,stroke:#16a34a,color:#14532d
    classDef shell fill:#fef3c7,stroke:#d97706,color:#78350f
    classDef kernel fill:#f3e8ff,stroke:#9333ea,color:#581c87
    classDef hardware fill:#fee2e2,stroke:#dc2626,color:#7f1d1d
    class A user
    class B app
    class C shell
    class D,E kernel
    class F hardware
```

### Kernel

The kernel is the core of the operating system. It manages:

-   CPU scheduling
-   Memory
-   Processes
-   Hardware devices
-   Filesystems
-   System calls

### Shell

A shell is a command interpreter. It accepts commands, interprets them
and requests services from the operating system.

Examples:

-   Bash
-   Zsh
-   Fish

### Terminal

A terminal is the application or interface where you type and view
command-line input and output.

**Remember:**

-   Terminal = where you type.
-   Shell = program that interprets your commands.
-   Kernel = core that manages hardware and system resources.

### What happens when you execute a command?

For example, when you type `ls`:

1.  You enter `ls` in the terminal.
2.  The shell reads and interprets the command.
3.  The shell runs the `ls` program.
4.  The program requests filesystem information from the operating
    system.
5.  The output is displayed in the terminal.

## 8. Linux, Windows and macOS

  -----------------------------------------------------------------------
  Feature           Linux             Windows           macOS
  ----------------- ----------------- ----------------- -----------------
  Main system       Unix-like         Windows NT family Unix-based
  design                                                

  Source model      Open-source       Mostly            Proprietary OS
                    kernel;           proprietary       with open-source
                    distributions                       components
                    vary                                

  Common command    Bash is common    PowerShell / CMD  Zsh by default
  shell                                                 

  Common use        Servers,          Desktops,         Apple computers
                    desktops,         business, gaming  
                    embedded systems                    

  Filesystem root   `/`               Drive roots such  `/`
                                      as `C:\`          
  -----------------------------------------------------------------------

### Where is Linux used?

-   Web servers and cloud infrastructure
-   Supercomputers
-   Android devices (Linux kernel)
-   Routers and embedded devices
-   Development environments
-   Containers and DevOps systems

------------------------------------------------------------------------

# Part 4 -- Terminal and Shell Basics

## 9. Opening the Terminal

### Ubuntu

Open the application named **Terminal**. A common keyboard shortcut is
`Ctrl + Alt + T`.

### macOS

Open **Applications → Utilities → Terminal**, or search for Terminal
using Spotlight.

macOS uses Zsh by default on modern installations. Ubuntu commonly uses
Bash by default. The basic commands in these notes work on both systems.

## 10. Command Structure

A command commonly follows this structure:

``` text
command [options] [arguments]
```

Example:

``` bash
ls -la /Users
```

-   `ls` -- command
-   `-la` -- options
-   `/Users` -- argument

Another example:

``` bash
mkdir College
```

-   `mkdir` -- command
-   `College` -- directory name supplied as an argument

## 11. First Terminal Commands

  Command      Purpose
  ------------ --------------------------------------
  `whoami`     Displays the current username
  `pwd`        Prints the current working directory
  `date`       Displays date and time
  `uname -a`   Displays system/kernel information
  `clear`      Clears the visible terminal screen
  `ls`         Lists directory contents

Try:

``` bash
whoami
pwd
date
uname -a
ls
```

**Tip:** `clear` clears the screen; it does not delete files or command
history.

## 12. Understanding Paths

A path tells the operating system where a file or directory is located.

### Absolute path

An absolute path starts from the filesystem root `/`.

Example on Ubuntu:

``` text
/home/student/Documents/notes.txt
```

Example on macOS:

``` text
/Users/student/Documents/notes.txt
```

### Relative path

A relative path is interpreted from the current working directory.

If the current directory is `/home/student`, then:

``` text
Documents/notes.txt
```

refers to the same file as the absolute path above.

### Special path symbols

  Symbol   Meaning
  -------- -------------------------------
  `/`      Filesystem root
  `~`      Current user's home directory
  `.`      Current directory
  `..`     Parent directory

## 13. Navigation Commands

  Command          Meaning
  ---------------- ------------------------------
  `pwd`            Show current directory
  `ls`             List contents
  `cd Documents`   Enter Documents
  `cd ..`          Move to parent directory
  `cd ~`           Go to home directory
  `cd /`           Go to filesystem root
  `cd -`           Return to previous directory

### Useful `ls` options

``` bash
ls
ls -l
ls -a
ls -la
```

-   `ls` -- normal listing.
-   `ls -l` -- long/detailed listing.
-   `ls -a` -- includes hidden entries.
-   `ls -la` -- combines long format and hidden entries.

On Unix-like systems, a name beginning with `.` is normally treated as
hidden in ordinary directory listings.

------------------------------------------------------------------------

# Part 5 -- Creating and Managing Files and Directories

## 14. Creating Directories: `mkdir`

The `mkdir` command creates directories.

``` bash
mkdir College
mkdir Java
mkdir Linux
```

Create nested directories:

``` bash
mkdir -p College/Java/Notes
```

The `-p` option creates missing parent directories as needed.

## 15. Creating Files: `touch`

The `touch` command creates an empty file if it does not exist. If the
file already exists, it normally updates its timestamps.

``` bash
touch notes.txt
touch program.java
touch commands.txt
```

## 16. Copying Files: `cp`

The `cp` command copies files or directories.

``` bash
cp notes.txt notes_backup.txt
```

This creates a copy named `notes_backup.txt`.

Copy a file into a directory:

``` bash
cp notes.txt College/
```

Copy a directory and its contents:

``` bash
cp -R Java Java_Backup
```

`-R` means recursive.

## 17. Moving and Renaming: `mv`

The `mv` command moves or renames files and directories.

Rename:

``` bash
mv old.txt new.txt
```

Move a file:

``` bash
mv notes.txt College/
```

Move and rename:

``` bash
mv notes.txt College/java_notes.txt
```

## 18. Deleting Files and Directories

### `rm`

Removes files:

``` bash
rm notes.txt
```

### `rmdir`

Removes an empty directory:

``` bash
rmdir EmptyFolder
```

### Remove a directory and its contents

``` bash
rm -r FolderName
```

**Safety warning:** Deletion commands can permanently remove data. Check
your current directory with `pwd` and inspect the target with `ls`
before deleting. Do not experiment with recursive deletion on important
folders or system directories.

## 19. Build a Folder Structure

Try creating this structure:

``` text
College/
├── Java/
├── Linux/
├── DSA/
└── Projects/
```

One possible command sequence:

``` bash
mkdir College
cd College
mkdir Java Linux DSA Projects
ls -l
```

Create files:

``` bash
touch Java/notes.txt
touch Linux/commands.txt
touch DSA/topics.txt
touch Projects/ideas.txt
```

------------------------------------------------------------------------

# Part 6 -- Reading and Writing Files

## 20. Display File Content: `cat`

The `cat` command displays file contents.

``` bash
cat notes.txt
```

It can also display multiple files:

``` bash
cat file1.txt file2.txt
```

## 21. Read Long Files: `less`

``` bash
less notes.txt
```

Useful keys while viewing:

-   `Space` -- next page
-   `b` -- previous page
-   `/word` -- search for a word
-   `q` -- quit

## 22. Display the Beginning: `head`

By default, `head` displays the first 10 lines.

``` bash
head notes.txt
```

Display the first 3 lines:

``` bash
head -n 3 notes.txt
```

## 23. Display the End: `tail`

By default, `tail` displays the last 10 lines.

``` bash
tail notes.txt
```

Display the last 2 lines:

``` bash
tail -n 2 notes.txt
```

## 24. Print Text: `echo`

``` bash
echo "Hello Students"
```

This displays the text in the terminal.

## 25. Write and Append Using Redirection

Redirection sends command output somewhere other than the terminal,
commonly into a file.

### Output redirection: `>`

``` bash
echo "Welcome to Linux" > notes.txt
```

This writes the text into `notes.txt`. If the file already contains
data, `>` overwrites its previous contents.

### Append redirection: `>>`

``` bash
echo "Today we are learning Linux" >> notes.txt
```

This adds content at the end without replacing existing content.

### Input redirection: `<`

``` bash
wc -l < notes.txt
```

This supplies the contents of `notes.txt` as standard input to `wc`.

### Comparison

  Operator   Meaning           Existing file
  ---------- ----------------- --------------------
  `>`        Redirect output   Overwrites
  `>>`       Append output     Preserves and adds
  `<`        Redirect input    Reads from file

**Important:** Be careful with `>` because it can erase the previous
contents of a file.

------------------------------------------------------------------------

# Part 7 -- Linux Directory Structure

## 26. What is the Root Directory?

Linux organizes files and directories in a hierarchy. The topmost
directory is called the **root directory**, represented by `/`.

A simplified Linux directory tree:

``` text
/
├── home/
│   ├── student/
│   └── teacher/
├── etc/
├── var/
│   ├── log/
│   └── cache/
├── usr/
│   ├── bin/
│   ├── lib/
│   └── share/
├── dev/
├── proc/
├── tmp/
└── boot/
```

### Important Linux directories

  -----------------------------------------------------------------------
  Directory               Purpose                 Example
  ----------------------- ----------------------- -----------------------
  `/`                     Root of the entire      Starting point
                          filesystem hierarchy    

  `/home`                 Regular users' home     `/home/student`
                          directories             

  `/etc`                  System-wide             `/etc/hosts`
                          configuration files     

  `/var`                  Variable data such as   `/var/log`
                          logs and caches         

  `/usr`                  Many user-space         `/usr/bin`
                          programs, libraries and 
                          shared data             

  `/dev`                  Device files and        `/dev/null`
                          interfaces              

  `/proc`                 Virtual filesystem      `/proc/cpuinfo`
                          exposing process and    
                          kernel information      

  `/tmp`                  Temporary files         Temporary application
                                                  data

  `/boot`                 Files needed during     Kernel and
                          system startup          bootloader-related
                                                  files
  -----------------------------------------------------------------------

### Important concepts

-   `/home` is not the same as `/`. It is a directory inside the root.
-   `/etc` generally stores configuration; it is not the place for
    personal documents.
-   `/var/log` commonly contains system and application logs.
-   `/dev` contains device interfaces, not ordinary documents.
-   `/proc` is a virtual filesystem. Much of its information is
    generated by the kernel rather than stored as ordinary files on
    disk.

## 27. Exploring Directory Structure

On Ubuntu, try:

``` bash
ls /
ls /home
ls /etc
ls /var
ls /usr
ls /dev
ls /proc
```

You can inspect CPU information on Linux with:

``` bash
cat /proc/cpuinfo
```

And memory information with:

``` bash
cat /proc/meminfo
```

Avoid changing or deleting system files while exploring.

## 28. Linux Directory Structure vs macOS

macOS is Unix-based and shares many filesystem concepts with Linux, but
its directory layout is not identical.

  Linux location     macOS location / note
  ------------------ -------------------------------------------------
  `/home/username`   `/Users/username`
  `/etc`             `/etc` exists, often linked to `/private/etc`
  `/var`             `/var` is commonly linked to `/private/var`
  `/usr`             `/usr` exists, with macOS-specific organization
  `/dev`             `/dev` exists
  `/proc`            No standard Linux-style `/proc` filesystem

On macOS, explore:

``` bash
ls /
ls /Users
ls /etc
ls /var
ls /usr
ls /dev
```

To inspect processes on macOS, use:

``` bash
ps aux
```

To inspect system information, use:

``` bash
uname -a
sysctl -a
```

**Remember:** Do not assume every Linux directory or command option
behaves exactly the same on macOS.

------------------------------------------------------------------------

# Part 8 -- Searching for Files Using `find`

## 29. What is `find`?

The `find` command searches for files and directories based on
conditions such as name, type, size and modification time.

**Remember:** `find` searches the filesystem for matching paths. It does
not search inside the text of a file.

### General syntax

``` bash
find [starting-location] [conditions]
```

### Example 1: Find a file by name

``` bash
find . -name "notes.txt"
```

-   `find` -- search command.
-   `.` -- start in the current directory.
-   `-name` -- match a name.
-   `"notes.txt"` -- target filename.

### Example 2: Find all text files

``` bash
find . -name "*.txt"
```

The `*` wildcard represents any sequence of characters.

### Example 3: Find Java files

``` bash
find . -name "*.java"
```

### Example 4: Find directories only

``` bash
find . -type d
```

### Example 5: Find regular files only

``` bash
find . -type f
```

### Example 6: Ignore uppercase/lowercase differences

``` bash
find . -iname "NOTES.TXT"
```

### Example 7: Search inside the home directory

``` bash
find ~ -name "*.pdf"
```

### Example 8: Find files larger than 1 MB

``` bash
find . -type f -size +1M
```

### Example 9: Find files modified in the last 7 days

``` bash
find . -type f -mtime -7
```

`-mtime -7` matches files modified less than seven 24-hour periods ago,
subject to `find`'s time rounding rules.

### Useful `find` options

  Option      Meaning
  ----------- -----------------------------------
  `-name`     Match filename (case-sensitive)
  `-iname`    Match filename (case-insensitive)
  `-type f`   Regular files
  `-type d`   Directories
  `-size`     Match file size
  `-mtime`    Match modification age in days

------------------------------------------------------------------------

# Part 9 -- Searching Text Using `grep`

## 30. What is `grep`?

`grep` searches for text patterns inside files and displays matching
lines.

**Remember the difference:**

-   `find` -- searches for files and directories.
-   `grep` -- searches inside files for matching text.

### General syntax

``` bash
grep [options] "search_text" filename
```

### Example 1: Search for a word

Suppose `students.txt` contains:

``` text
Akash - Linux
Rahul - Java
Amit - Linux
Priya - Python
Neha - Linux
```

Run:

``` bash
grep "Linux" students.txt
```

Output:

``` text
Akash - Linux
Amit - Linux
Neha - Linux
```

### Example 2: Ignore case

``` bash
grep -i "linux" students.txt
```

This matches `Linux`, `linux` and other uppercase/lowercase
combinations.

### Example 3: Display line numbers

``` bash
grep -n "Linux" students.txt
```

Example output:

``` text
1:Akash - Linux
3:Amit - Linux
5:Neha - Linux
```

### Example 4: Display lines that do not match

``` bash
grep -v "Linux" students.txt
```

### Example 5: Count matching lines

``` bash
grep -c "Linux" students.txt
```

This counts matching lines, not necessarily every occurrence of the
word.

### Example 6: Search recursively

``` bash
grep -r "Linux" .
```

This searches files inside the current directory and its subdirectories.

### Example 7: Search all text files in the current directory

``` bash
grep "Java" *.txt
```

### Useful `grep` options

  Option   Meaning
  -------- -------------------------
  `-i`     Ignore case
  `-n`     Display line numbers
  `-v`     Show non-matching lines
  `-c`     Count matching lines
  `-r`     Search recursively

------------------------------------------------------------------------

# Part 10 -- Redirection and Pipes

## 31. Standard Input, Output and Error

Command-line programs commonly use three standard streams:

  Stream                         Number Meaning
  ---------------------------- -------- -----------------------------
  Standard input (`stdin`)            0 Input received by a program
  Standard output (`stdout`)          1 Normal output
  Standard error (`stderr`)           2 Error messages

By default, input often comes from the keyboard and output appears in
the terminal.

## 32. Output Redirection

Save the output of a command:

``` bash
ls > files.txt
```

The list of files is saved in `files.txt`.

Append more output:

``` bash
date >> files.txt
```

## 33. Error Redirection

Save error messages separately:

``` bash
ls missing_folder 2> errors.txt
```

Here, `2>` redirects standard error.

Save normal output and errors into separate files:

``` bash
find . -name "*.txt" > found.txt 2> errors.txt
```

## 34. Pipes: `|`

A pipe connects the standard output of one command to the standard input
of another command.

``` bash
cat students.txt | grep "Linux"
```

Flow:

``` mermaid
flowchart LR
    A[students.txt] --> B[cat]
    B -->|Text output| C[Pipe]
    C --> D[grep Linux]
    D --> E[Matching lines]
    classDef file fill:#dbeafe,stroke:#2563eb,color:#1e3a8a
    classDef command fill:#dcfce7,stroke:#16a34a,color:#14532d
    classDef pipe fill:#fef3c7,stroke:#d97706,color:#78350f
    class A,E file
    class B,D command
    class C pipe
```

A shorter way to achieve the same result is:

``` bash
grep "Linux" students.txt
```

### Another pipe example

Count the number of lines in a file:

``` bash
cat students.txt | wc -l
```

Or simply:

``` bash
wc -l students.txt
```

Pipes are useful when combining small commands to perform larger tasks.

------------------------------------------------------------------------

# Part 11 -- Guided Hands-on Practical

## 35. Create a Linux Practice Workspace

Complete these steps in your Ubuntu terminal. macOS users can use the
same commands.

### Step 1: Create the main directory

``` bash
mkdir ~/Linux_Practical
cd ~/Linux_Practical
```

### Step 2: Create subject directories

``` bash
mkdir Java Linux DSA Projects
```

### Step 3: Create files

``` bash
touch Java/notes.txt
touch Java/programs.txt
touch Linux/commands.txt
touch Linux/practical.txt
touch DSA/topics.txt
touch Projects/ideas.txt
```

### Step 4: Add content

``` bash
echo "Java is an object-oriented programming language" > Java/notes.txt
echo "Linux is an open-source operating system kernel" > Linux/commands.txt
echo "Linux supports shell scripting" >> Linux/commands.txt
echo "Practice terminal commands" > Linux/practical.txt
echo "Arrays and Strings" > DSA/topics.txt
echo "Build a student management application" > Projects/ideas.txt
```

### Step 5: Explore the structure

``` bash
pwd
ls
ls -R
```

### Step 6: Read file contents

``` bash
cat Linux/commands.txt
head -n 1 Linux/commands.txt
tail -n 1 Linux/commands.txt
```

### Step 7: Search for files

``` bash
find . -name "*.txt"
find . -type d
```

### Step 8: Search for content

``` bash
grep -n "Linux" Linux/commands.txt
grep -r "Linux" .
```

### Step 9: Save search results

``` bash
grep -r "Linux" . > search_results.txt
cat search_results.txt
```

### Step 10: Append a completion message

``` bash
echo "Search practical completed" >> search_results.txt
cat search_results.txt
```

------------------------------------------------------------------------

# Part 12 -- Independent Student Assignment

## 36. Linux File Manager Challenge

**Scenario:** You are a college student managing your academic work
through the terminal. Your task is to create a workspace, organize
subject files, update notes and search for information without using the
graphical file manager.

### Part A -- Workspace Creation

Create the following structure using only terminal commands:

``` text
College/
├── Java/
│   ├── notes.txt
│   └── programs.txt
├── Linux/
│   ├── commands.txt
│   └── practical.txt
├── DSA/
│   └── topics.txt
└── Projects/
    └── ideas.txt
```

Tasks:

1.  Create the `College` directory.
2.  Create all subject directories.
3.  Create all specified files.
4.  Add at least five lines of content to `commands.txt`.

### Part B -- File Operations

1.  Copy `commands.txt` into the Projects directory.
2.  Rename `ideas.txt` to `project_ideas.txt`.
3.  Move `programs.txt` into the Projects directory.
4.  Display the contents of each subject folder.
5.  Create a backup copy of `notes.txt`.

### Part C -- Reading and Writing

1.  Display the complete content of `commands.txt`.
2.  Display only the first three lines.
3.  Display only the last two lines.
4.  Add a new Linux command using `echo`.
5.  Append a message to `practical.txt`.
6.  Save the output of `ls -R College` into `folder_report.txt`.

### Part D -- Searching

1.  Find all `.txt` files inside College.
2.  Find all directories inside College.
3.  Search for the word `Linux` inside all text files.
4.  Display matching lines with line numbers.
5.  Save the matching results into `search_results.txt`.
6.  Count the matching lines.

### Part E -- Final Verification

1.  Display the complete folder structure.
2.  Display `folder_report.txt`.
3.  Display `search_results.txt`.
4.  Verify that all required files exist.

------------------------------------------------------------------------

## 37. Bonus Challenges

Attempt these without referring to the examples above.

1.  Find all files larger than 1 KB.
2.  Find all files modified within the last 7 days.
3.  Search for `java` without considering uppercase or lowercase.
4.  Find all files ending with `.java`.
5.  Count the number of `.txt` files.
6.  Display lines that do not contain the word `Java`.
7.  Use a pipe to count the number of matching lines.
8.  Create a report containing all `.txt` filenames.
9.  Redirect normal output and error output into separate files.
10. Search recursively for a word across all subject folders.

------------------------------------------------------------------------

# Part 13 -- Submission Guidelines

Submit the following items:

    No. Submission                                 Format
  ----- ------------------------------------------ -----------
      1 Commands used to complete the assignment   `.txt`
      2 Screenshot of final folder structure       Image
      3 `folder_report.txt`                        Text file
      4 `search_results.txt`                       Text file
      5 Screenshot showing final terminal output   Image

### Rules

-   Complete the assignment individually.
-   Use terminal commands for all file and directory operations.
-   Do not create the folder structure using a graphical file manager.
-   Do not submit screenshots alone; submit the actual output files.
-   Be prepared to explain any command used in your assignment.

------------------------------------------------------------------------

# Part 14 -- Quick Revision Questions

## A. Computer and OS Fundamentals

1.  What is a computer?
2.  Differentiate hardware and software.
3.  What is the difference between RAM and storage?
4.  What is an operating system?
5.  Explain any five functions of an operating system.
6.  Differentiate CLI and GUI.

## B. Linux Fundamentals

1.  What is Linux?
2.  What is the difference between a kernel and a distribution?
3.  What is the role of the Linux kernel?
4.  Differentiate terminal and shell.
5.  Name three Linux distributions.
6.  Where is Linux used in real life?

## C. Terminal and File Management

1.  What is the purpose of `pwd`?
2.  Differentiate `ls` and `cd`.
3.  What is the difference between an absolute and relative path?
4.  What is the use of `mkdir` and `touch`?
5.  Differentiate `cp` and `mv`.
6.  What is the difference between `rm` and `rmdir`?
7.  What does `ls -la` display?

## D. Reading, Writing and Searching

1.  Differentiate `cat` and `less`.
2.  What is the use of `head` and `tail`?
3.  Differentiate `>` and `>>`.
4.  What is the purpose of the pipe operator?
5.  What is the difference between `find` and `grep`?
6.  Explain `grep -i` and `grep -n`.
7.  What is the purpose of `/etc`?
8.  What information is available in `/proc`?

------------------------------------------------------------------------

# Part 15 -- Command Quick Reference

  Command    Use                       Example
  ---------- ------------------------- ------------------------
  `whoami`   Current username          `whoami`
  `pwd`      Current directory         `pwd`
  `date`     Date and time             `date`
  `uname`    System information        `uname -a`
  `clear`    Clear screen              `clear`
  `ls`       List files                `ls -la`
  `cd`       Change directory          `cd Documents`
  `mkdir`    Create directory          `mkdir College`
  `touch`    Create empty file         `touch notes.txt`
  `cp`       Copy                      `cp a.txt b.txt`
  `mv`       Move or rename            `mv a.txt b.txt`
  `rm`       Delete file               `rm a.txt`
  `rmdir`    Remove empty directory    `rmdir Demo`
  `cat`      Display file              `cat notes.txt`
  `less`     Read page by page         `less notes.txt`
  `head`     First lines               `head -n 3 notes.txt`
  `tail`     Last lines                `tail -n 3 notes.txt`
  `echo`     Print text                `echo "Hello"`
  `find`     Search paths              `find . -name "*.txt"`
  `grep`     Search text               `grep "Linux" a.txt`
  `wc`       Count lines/words/bytes   `wc -l a.txt`

------------------------------------------------------------------------

# Final Learning Checklist

Before moving to the next Linux topic, make sure you can:

-   [ ] Explain CPU, RAM and storage.
-   [ ] Explain the purpose of an operating system.
-   [ ] Differentiate kernel, shell and terminal.
-   [ ] Navigate directories using `pwd`, `ls` and `cd`.
-   [ ] Create files and folders using `touch` and `mkdir`.
-   [ ] Copy, move, rename and delete files.
-   [ ] Read files using `cat`, `less`, `head` and `tail`.
-   [ ] Write and append content using `echo`, `>` and `>>`.
-   [ ] Explain the important Linux directories.
-   [ ] Search for files using `find`.
-   [ ] Search inside files using `grep`.
-   [ ] Combine commands using pipes and redirection.

**The most important practice rule:** Do not just memorize commands.
Understand what each command does, predict its output, execute it and
verify the result.
