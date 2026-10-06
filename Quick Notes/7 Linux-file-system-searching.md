# 7 Linux File System & Searching

Mastering the Linux operating system requires a clear mental model of how files are organized and how to locate specific information quickly. In this class, we explore the hierarchical Linux directory structure, compare it with Unix-based systems like macOS, and build hands-on mastery over essential command-line search tools including `find`, `grep`, pipes (`|`), and stream redirection operators (`>` and `>>`).

---

## 1. Quick Revision & Terminal Warmup (5–7 min)

To build intuition before diving into directory mechanics, every student should open a Terminal session and run a series of foundational inspection commands. This brief warmup establishes your current location in the filesystem tree and introduces the ultimate origin point of all Linux files.

Begin by running these commands in sequence:

```bash
pwd
ls
ls -l
cd ~
cd ..
cd /
```

When you execute `pwd`, the terminal prints your current working directory path. Running `ls` displays the contents of the current directory, while `ls -l` presents a detailed long-listing view showing file permissions, owner information, size, and modification timestamps. Changing directories using `cd ~` brings you back to your personal home directory, `cd ..` moves up one level to the parent directory, and `cd /` navigates directly to the root of the entire system.

At this point, execute `ls /` and consider the essential question: **"What is `/`?"**

In Linux, the single forward slash `/` represents the **root directory**. Unlike Windows, which uses separate drive letters like `C:\` or `D:\`, Linux organizes everything into a single inverted tree structure where every file, folder, storage device, and process interface originates directly from `/`.

---

## 2. Linux Directory Structure & Hierarchy

Linux organizes files in a hierarchical tree. Understanding this layout prevents confusion when configuring services, inspecting log files, or installing software applications. The top-level system directories housed directly under `/` serve distinct administrative and operational purposes.

The major directories inside the Linux root directory include:

```
/
├── home
├── etc
├── var
├── usr
├── bin
├── sbin
├── dev
├── tmp
├── opt
├── boot
└── proc
```

### Key Linux System Directories

#### 1. The Root Directory (`/`)
The absolute top level of the Linux filesystem hierarchy. Standard user documents are never stored directly in `/`; instead, it holds the core system directories required to boot and manage the operating system.

#### 2. User Home Directories (`/home`)
Contains personal user accounts, personal configuration files, and user documents.

```bash
ls /home
```

A typical listing reveals user folders such as `/home/akash`, `/home/student`, or `/home/admin`. Inside a specific user directory like `/home/akash`, you will find personal folders such as `Documents`, `Downloads`, `Pictures`, `Desktop`, and `Videos`.

> **Important Distinction:** Do not confuse `/home` with `/home/akash`. `/home` is the parent system directory holding all user home folders, whereas `/home/akash` is the specific isolated workspace for the user Akash.

#### 3. System Configuration (`/etc`)
Holds all system-wide configuration files and administrative settings. If you need to edit network settings, user account lists, or service parameters, you will work inside `/etc`.

```bash
ls /etc
```

Common configuration files located here include:
* `/etc/hosts` — Local network hostname to IP mappings.
* `/etc/passwd` — System user account attributes and shell assignments.
* `/etc/fstab` — Storage device and filesystem mounting configurations.
* `/etc/ssh/` — Secure Shell (SSH) daemon configuration and key files.

#### 4. Variable & Runtime Data (`/var`)
Derived from the word *variable*, `/var` stores data that grows and changes dynamically during system operation, such as log records, cache files, and lock files.

```bash
ls /var
ls /var/log
```

The `/var/log` directory is vital for troubleshooting. System services, kernel events, and applications record activity logs here, including login attempts, system errors, and service activity events.

#### 5. User Programs & Resources (`/usr`)
Derived historically from *User System Resources*, `/usr` contains shared user-space software binaries, libraries, documentation, and program support files. It does not mean "my personal user files."

```bash
ls /usr
ls /usr/bin | head
```

Key subdirectories include `/usr/bin` for user commands, `/usr/sbin` for non-essential administrative binaries, `/usr/lib` for system libraries, and `/usr/share` for architecture-independent shared data.

#### 6. Essential Executable Commands (`/bin`)
Contains fundamental executable command binaries required for basic system operation, such as `ls`, `cp`, `mv`, `cat`, and `echo`. On modern Linux distributions, `/bin` is frequently configured as a symbolic link pointing directly to `/usr/bin`. Inspecting this with `ls -ld /bin` demonstrates how modern distributions consolidate binary locations.

#### 7. System Administration Commands (`/sbin`)
Contains essential system administration utilities intended for system maintenance and root tasks, such as `fsck` (filesystem check), `mount`, and `shutdown`. On modern systems, `/sbin` may also be linked to `/usr/sbin`.

#### 8. Hardware & Device Interfaces (`/dev`)
Linux adheres to the design principle that hardware devices can be represented as file-like interfaces. The `/dev` directory contains special device nodes representing physical and virtual devices.

```bash
ls /dev
```

Examples include `/dev/sda` (hard disk drive), `/dev/random` (entropy generator), and `/dev/null` (the black hole device). For instance, redirecting text to `/dev/null` causes the data to be discarded immediately:

```bash
echo "hello" > /dev/null
```

#### 9. Temporary Storage (`/tmp`)
Provides a temporary storage area for processes and users. Files created in `/tmp` are generally cleared upon system reboot or periodically by automated maintenance scripts.

```bash
echo "temporary data" > /tmp/test.txt
cat /tmp/test.txt
rm /tmp/test.txt
```

#### 10. Optional Software Packages (`/opt`)
Reserved for standalone, third-party application software packages installed outside the standard distribution package manager (for example, `/opt/application-name`).

#### 11. Boot Configuration (`/boot`)
Contains static files required to boot the operating system, including the Linux kernel, bootloader configurations (such as GRUB), and the initial RAM disk (`initramfs`).

The boot sequence links directly to these files:
Power ON → BIOS/UEFI → Bootloader → Kernel → systemd → System Services.

#### 12. Virtual Process & Kernel Interface (`/proc`)
A pseudo-filesystem dynamically generated in memory by the Linux kernel rather than stored on disk. It exposes live kernel data and active process metrics.

```bash
ls /proc
cat /proc/cpuinfo
cat /proc/meminfo
```

Directories named with numbers (such as `/proc/1`) represent active Process IDs (PIDs), where `/proc/1` exposes attributes of the initial system process (`systemd` or `init`).

---

## 3. Comparative Analysis: Linux vs. macOS Directory Layout

Many Unix-like operating systems share historical conventions, but implementations differ across operating systems. Comparing Linux with macOS helps clarify core architectural concepts for students working in Mac terminal environments.

When running `cd /` and `ls` on macOS, the directory listing reveals names such as `Applications`, `Library`, `System`, `Users`, `Volumes`, `private`, and `cores`.

### Key macOS Directory Differences

* **`/Applications`**: Stores graphic user interface (GUI) software installed for users or the system (such as `Safari.app` or `Visual Studio Code.app`).
* **`/Users`**: Holds personal user home directories. Where Linux uses `/home/akash`, macOS uses `/Users/akash`.
* **`/Library`**: Contains system-wide application support files, preferences, caches, and launch agents. User-specific settings reside in `~/Library`.
* **`/System`**: Houses protected macOS operating system core files, guarded by System Integrity Protection (SIP).
* **`/private`**: Houses underlying Unix directories. On macOS, `/etc`, `/tmp`, and `/var` are symbolic links pointing to `/private/etc`, `/private/tmp`, and `/private/var`.
* **`/Volumes`**: Mount point for external hard drives, USB thumb drives, and disk images (such as `/Volumes/MyUSB`).
* **`/opt`**: Frequently used by package managers on macOS. On Apple Silicon Macs, Homebrew installs packages into `/opt/homebrew`.
* **`/cores`**: Used by macOS to store core dump files generated during process crashes, depending on system diagnostic settings.

### Linux vs. macOS Comparison Matrix

The table below summarizes equivalent concepts across Linux and macOS environments:

| System Concept | Linux Implementation Path | macOS Implementation Path |
| :--- | :--- | :--- |
| **User Home Directories** | `/home/akash` | `/Users/akash` |
| **System Configuration** | `/etc` | `/etc` (symlinked to `/private/etc`) |
| **User Binaries & Resources** | `/usr` | `/usr` |
| **Device Special Files** | `/dev` | `/dev` |
| **Temporary Files** | `/tmp` | `/tmp` (symlinked to `/private/tmp`) |
| **Variable / Log Data** | `/var` | `/var` (symlinked to `/private/var`) |
| **GUI Applications** | Distribution specific | `/Applications` |
| **Mounted External Storage** | `/media/user` or `/mnt` | `/Volumes` |
| **Core Operating System** | Standard Linux tree layout | `/System` |

---

## 4. File Searching with `find`

Locating files across a deep filesystem tree requires systematic search tools. The `find` command searches for files and directories within a directory hierarchy based on metadata, names, file types, and modification attributes.

### Initializing the Lab Environment

To practice search commands effectively, set up a sample directory workspace:

```bash
mkdir -p ~/linux-lab/{notes,programs,output}
cd ~/linux-lab

touch notes/linux.txt notes/os.txt programs/java.txt programs/shell.txt

echo "Linux is an operating system" > notes/linux.txt
echo "Operating System concepts" > notes/os.txt
echo "Java programming" > programs/java.txt
echo "Shell scripting and Linux" > programs/shell.txt
```

Verify your workspace structure by executing `find .`, which recursively lists all files and directories starting from your current position.

### Syntax and Mechanics of `find`

The general syntax for `find` is:

```bash
find [starting-location] [selection-criteria]
```

#### Searching by Name (`-name`)
To match files by name or pattern, use the `-name` option paired with quote-enclosed expressions:

```bash
find . -name "*.txt"
```

* `find`: The command invocation.
* `.`: Starts searching recursively from the current working directory.
* `-name`: Evaluates the file name against a pattern.
* `"*.txt"`: Wildcard expression matching any string ending with `.txt`. The asterisk `*` represents zero or more arbitrary characters.

#### Searching by Object Type (`-type`)
Filesystems contain regular files, directories, and links. The `-type` flag filters search results based on the object's filesystem classification:

* `f` — Regular files
* `d` — Directories
* `l` — Symbolic links

```bash
find . -type f
find . -type d
```

#### Combining Type and Name Criteria
Criteria can be combined to refine results. The following command locates objects that are regular files AND have names ending with `.txt`:

```bash
find . -type f -name "*.txt"
```

#### Controlling Search Scope
The starting location parameter governs where traversal begins. `find` recursively descends into subdirectories under the target location:

```bash
find ~/linux-lab -type f
find /Users/akash/linux-lab -type f
```

---

## 5. Content Searching with `grep`

While `find` locates files based on file attributes and names, `grep` (Global Regular Expression Print) searches inside files for specific text patterns or matching strings.

### Fundamental `grep` Syntax

```bash
grep [options] "pattern" [file-target]
```

To search for the string `"Linux"` inside `notes/linux.txt`:

```bash
grep "Linux" notes/linux.txt
```

### Essential `grep` Flags

#### 1. Display Line Numbers (`-n`)
Prefixes each matching output line with its original line number within the file:

```bash
grep -n "Linux" notes/linux.txt
```

#### 2. Case-Insensitive Matching (`-i`)
Ignores character case distinctions, matching strings like `Linux`, `linux`, `LINUX`, or `LiNuX`:

```bash
grep -i "linux" notes/linux.txt
```

#### 3. Recursive Directory Search (`-R` or `-r`)
Searches all files inside the current directory and recursively traverses all subdirectories:

```bash
grep -R "Linux" .
```

---

## 6. Advanced Integration: Combining `find` and `grep`

Combining search tools allows you to filter specific files with `find` and inspect their contents using `grep`. The `-exec` flag in `find` passes matching files directly to `grep`.

Execute the combined search command:

```bash
find . -type f -name "*.txt" -exec grep -n "Linux" {} \;
```

### Anatomy of the Combined Command

* `find .`: Begins searching from the current working directory.
* `-type f`: Restricts search results strictly to regular files.
* `-name "*.txt"`: Filters files ending with the `.txt` extension.
* `-exec`: Executes an external command on every matching item found.
* `grep -n "Linux"`: The command executed against each file.
* `{}`: A dynamic placeholder substituted with the path of each found file.
* `\;`: Terminates the `-exec` command argument list. The backslash protects the semicolon from shell interpretation.

---

## 7. Data Flow Control: Pipes (`|`) and Redirection (`>` and `>>`)

Command-line efficiency relies on connecting tools and redirecting standard input and output streams.

### Process Chaining with Pipes (`|`)
A pipe (`|`) redirects the standard output of one command to serve as the standard input for another command.

```bash
find . -type f | grep ".txt"
```

In this example, `find . -type f` generates a list of all files, and `|` passes that stream into `grep ".txt"`, which filters and displays lines containing `.txt`.

### Output Stream Redirection (`>` and `>>`)

By default, command output is sent to the terminal display. Stream redirection operators redirect output to disk files.

#### 1. Overwrite Redirection Operator (`>`)
Writes output to a specified file. If the target file already exists, its contents are completely overwritten.

```bash
find . -type f > output/files.txt
cat output/files.txt
```

#### 2. Append Redirection Operator (`>>`)
Appends new output lines to the end of an existing file without deleting prior contents.

```bash
find . -type f >> output/files.txt
```

#### Combining Search and Redirection
You can capture recursive text search results directly into output reports:

```bash
grep -R "Linux" . > output/linux-search.txt
cat output/linux-search.txt
```

---

## 8. Hands-On Student Challenge & Practical Tasks

To consolidate your understanding of filesystem search, navigation, and stream manipulation, complete the following practical tasks within your `~/linux-lab` directory environment.

### Lab Setup Verification
Ensure your environment contains the `notes/`, `programs/`, and `output/` folders along with sample text files before attempting the tasks.

```bash
cd ~/linux-lab
```

### Practical Tasks

#### Task 1: Find All Directories
Find all directory objects starting from the current location.
* **Command:** `find . -type d`

#### Task 2: Find All Regular Files
Find all regular files within the workspace tree.
* **Command:** `find . -type f`

#### Task 3: Find All Text Files
Find all files ending with a `.txt` file extension.
* **Command:** `find . -type f -name "*.txt"`

#### Task 4: Search File Contents for a Keyword
Search for the pattern `"Linux"` specifically inside all `.txt` files using `-exec`.
* **Command:** `find . -type f -name "*.txt" -exec grep "Linux" {} \;`

#### Task 5: Recursive Search with Line Numbers
Recursively search for `"Linux"` across all files, displaying matching line numbers.
* **Command:** `grep -Rn "Linux" .`

#### Task 6: Save File Paths to an Output File
Locate all `.txt` files and write their paths into `output/text-files.txt` (overwriting existing content).
* **Command:** `find . -type f -name "*.txt" > output/text-files.txt`

#### Task 7: Save Search Matches to an Output File
Search recursively for the word `"Linux"` and save the matching lines into `output/linux-results.txt`.
* **Command:** `grep -R "Linux" . > output/linux-results.txt`

#### Task 8: Append File Listings to an Existing Report
Append the list of all files in the directory tree to `output/linux-results.txt` without overwriting prior search matches.
* **Command:** `find . -type f >> output/linux-results.txt`

#### Task 9: Final Integrated Search Challenge
Find all `.txt` files under the current directory, search their contents for the string `"Linux"`, and save the matching results with line numbers into `output/final.txt`.
* **Command:** `find . -type f -name "*.txt" -exec grep -n "Linux" {} \; > output/final.txt`

---

## 9. Core Mental Model & Quick Reference Guide

When working in the Linux command line, selection of tools depends on whether you are querying file metadata or file content. Use this mental model to guide command choices:

1. **Where are files located?** → Use `find`.
2. **Which files do I want?** → Filter with `find` flags (`-name`, `-type`).
3. **What text is inside the files?** → Search contents with `grep`.
4. **How do I connect tools?** → Link command streams with pipes (`|`).
5. **Where should output go?** → Direct streams to file storage using `>` (overwrite) or `>>` (append).

### Tool Summary Matrix

| Tool / Operator | Primary Function | Typical Use Case |
| :--- | :--- | :--- |
| **`find`** | Searches for **files and directories** by name, path, or type. | `find . -type f -name "*.sh"` |
| **`grep`** | Searches for **text patterns inside** files. | `grep -Rn "error" /var/log` |
| **`|` (Pipe)** | Sends standard output of one command to standard input of another. | `ls -l /usr/bin \| grep "python"` |
| **`>` (Overwrite)** | Redirects output stream to a file, replacing existing file content. | `find . -type f > manifest.txt` |
| **`>>` (Append)** | Redirects output stream to a file, appending to existing content. | `echo "New Entry" >> log.txt` |

### Core Takeaway
> **`find` finds the files, `grep` finds the text, `|` connects commands, and `>` / `>>` save the output.**
