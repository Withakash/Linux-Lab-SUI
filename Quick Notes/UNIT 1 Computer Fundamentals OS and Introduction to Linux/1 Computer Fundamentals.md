# 1 Computer Fundamentals

> **Beginner-friendly notes \| Computer Fundamentals, Operating System
> Fundamentals, and Linux Introduction**
>
> These notes explain the concepts from Lectures 4, 5, and 6 with
> everyday examples, simple diagrams, comparison tables, and practical
> commands for Linux and macOS.

------------------------------------------------------------------------

# Part 1: Computer Fundamentals

## 1. What is a Computer?

A **computer** is an electronic device that accepts data as input,
processes that data according to instructions, stores information, and
produces a result as output.

In simple words:

-   **Input:** We give data or instructions to the computer.
-   **Processing:** The computer works on that data.
-   **Storage:** It can save data for later use.
-   **Output:** It shows or produces the result.

### The IPO cycle

IPO stands for **Input → Process → Output**.

``` mermaid
flowchart LR
    A["INPUT<br/>Keyboard, Mouse"] --> B["PROCESS<br/>CPU"]
    B --> C["OUTPUT<br/>Monitor, Speaker"]
    B <--> D[("STORAGE<br/>SSD / HDD")]
    classDef input fill:#dbeafe,stroke:#2563eb,color:#172554,stroke-width:2px
    classDef process fill:#fef3c7,stroke:#d97706,color:#78350f,stroke-width:2px
    classDef output fill:#dcfce7,stroke:#16a34a,color:#14532d,stroke-width:2px
    classDef storage fill:#f3e8ff,stroke:#9333ea,color:#581c87,stroke-width:2px
    class A input
    class B process
    class C output
    class D storage
```

**Example: Calculating 10 + 20**

1.  You enter `10 + 20` using a keyboard.
2.  The CPU processes the instruction.
3.  The result `30` appears on the screen.
4.  If you save the result in a file, it is stored on the storage
    device.

A computer does not understand a task in the same way a human does. It
follows instructions provided by software.

## 2. Hardware vs Software

A computer system has two major parts: **hardware** and **software**.

### Hardware

**Hardware** means the physical parts of a computer that we can see and
touch.

Examples:

-   Monitor
-   Keyboard
-   Mouse
-   Motherboard
-   CPU
-   RAM
-   SSD or HDD
-   Speakers
-   Webcam

### Software

**Software** is a collection of programs and instructions that tells the
hardware what to do.

Examples:

-   Operating systems: Windows, macOS, Ubuntu Linux
-   Browsers: Chrome, Firefox, Safari
-   Editors: VS Code, Notepad
-   Applications: MS Word, VLC, Calculator

### Comparison

  Hardware                                 Software
  ---------------------------------------- ---------------------------------
  Physical components                      Programs and instructions
  Can generally be touched                 Cannot be physically touched
  Needs software to perform useful tasks   Needs hardware to run
  Example: RAM, CPU, keyboard              Example: Linux, Chrome, VS Code

### How hardware and software work together

Think about a music player:

-   The **music application** is software.
-   The **CPU** runs the application's instructions.
-   **RAM** holds the application and currently used data.
-   The **SSD** stores the music files.
-   The **speaker** produces sound.

``` mermaid
flowchart TB
    A["USER"] --> B["APPLICATION SOFTWARE<br/>Music Player"]
    B --> C["OPERATING SYSTEM"]
    C --> D["HARDWARE"]
    D --> E["CPU"]
    D --> F["RAM"]
    D --> G["SSD"]
    D --> H["Speaker"]
    classDef user fill:#e0f2fe,stroke:#0284c7,color:#0c4a6e
    classDef software fill:#f3e8ff,stroke:#9333ea,color:#581c87
    classDef os fill:#fef3c7,stroke:#d97706,color:#78350f
    classDef hardware fill:#dcfce7,stroke:#16a34a,color:#14532d
    class A user
    class B software
    class C os
    class D,E,F,G,H hardware
```

**Remember:** Hardware is the body of a computer; software provides the
instructions that make it useful. This is only an analogy---the actual
relationship is more complex.

## 3. Main Components of a Computer

### 3.1 CPU --- Central Processing Unit

The **CPU** is the main processor of a computer. It executes program
instructions and performs calculations and logical operations.

It is often called the *brain of the computer*.

The CPU performs tasks such as:

-   Performing arithmetic calculations.
-   Comparing values.
-   Following program instructions.
-   Coordinating operations with memory and other components.

Important CPU terms:

  -----------------------------------------------------------------------
  Term                                Meaning
  ----------------------------------- -----------------------------------
  Core                                An individual processing unit
                                      inside a CPU

  Clock speed                         The rate at which a CPU clock
                                      cycles, commonly measured in GHz

  Cache                               Small, very fast memory located in
                                      or close to the CPU

  Thread                              A sequence of instructions that can
                                      be scheduled for execution; CPU
                                      hardware may support multiple
                                      threads per core
  -----------------------------------------------------------------------

**Example:** When you open a calculator and calculate `25 × 4`, the CPU
executes the instructions needed to produce the answer.

**Important:** A higher GHz value does not automatically mean a CPU is
faster. CPU design, core count, cache, power limits, and workload also
matter.

### 3.2 RAM --- Random Access Memory

**RAM** is the computer's main working memory. It temporarily holds the
programs and data that are currently being used.

Examples of what may be in RAM:

-   An open browser.
-   Open browser tabs.
-   A running code editor.
-   A document you are editing.
-   Data currently being processed.

Key points:

-   RAM is much faster to access than normal SSD/HDD storage.
-   RAM is generally **volatile**: its contents are lost when power is
    removed.
-   More RAM can help when several applications or large files are open.
-   RAM is not the same as storage.

**Analogy:** Think of RAM as your study table. You keep the books you
are currently using on the table. When the table is larger, you can keep
more books open at the same time.

### 3.3 Storage --- HDD and SSD

Storage keeps files and programs for long-term use, even after the
computer is switched off.

Examples:

-   Operating system files.
-   Photos and videos.
-   Documents.
-   Installed applications.
-   Projects and source code.

Two common storage technologies:

  -----------------------------------------------------------------------
  HDD                                 SSD
  ----------------------------------- -----------------------------------
  Uses spinning magnetic disks        Uses flash memory

  Has moving mechanical parts         Has no moving mechanical parts

  Usually slower for random access    Usually much faster for random
                                      access

  Often cheaper per GB                Often costs more per GB
  -----------------------------------------------------------------------

An SSD may use SATA or NVMe interfaces. NVMe SSDs commonly use the PCIe
interface and can provide very high transfer speeds.

**RAM vs Storage**

  RAM                           Storage
  ----------------------------- ------------------------------------
  Temporary working area        Long-term file storage
  Usually volatile              Non-volatile
  Holds currently active data   Holds files and installed programs
  Typically faster              Typically slower than RAM

**Example:** A 512 GB SSD tells you the approximate storage capacity. A
16 GB RAM specification tells you the amount of working memory.

### 3.4 Motherboard

The **motherboard** is the main circuit board that connects important
computer components.

It provides connections for:

-   CPU
-   RAM
-   Storage
-   USB ports
-   Network hardware
-   Graphics hardware
-   Power connections

``` mermaid
flowchart TB
    M["MOTHERBOARD"]
    M --- C["CPU"]
    M --- R["RAM"]
    M --- S["SSD / HDD"]
    M --- U["USB / I-O PORTS"]
    M --- N["NETWORK / OTHER DEVICES"]
    classDef board fill:#e0e7ff,stroke:#4f46e5,color:#312e81,stroke-width:3px
    classDef part fill:#ecfccb,stroke:#65a30d,color:#365314
    class M board
    class C,R,S,U,N part
```

### 3.5 Input Devices

Input devices send data or instructions to a computer.

Examples:

-   Keyboard --- enters text and commands.
-   Mouse --- controls the pointer.
-   Microphone --- captures sound.
-   Webcam --- captures images and video.
-   Scanner --- converts paper documents into digital form.
-   Touchscreen --- accepts touch input.

### 3.6 Output Devices

Output devices present the results of computer processing.

Examples:

-   Monitor --- displays text, images, and video.
-   Printer --- produces paper output.
-   Speaker --- produces sound.
-   Headphones --- provide audio output.
-   Projector --- displays output on a larger surface.

Some devices perform both input and output. For example, a touchscreen
displays information and accepts touch input.

## 4. What Happens When You Open an App?

Let's understand what happens when you open Google Chrome, VS Code, or
another application.

### Step-by-step process

1.  **You request the application:** You click its icon or run a
    command.
2.  **The operating system receives the request:** It checks the
    application and manages the launch.
3.  **Program files are read from storage:** The required executable and
    other files are loaded.
4.  **Memory is allocated:** The OS provides the application with the
    memory it needs.
5.  **The CPU executes instructions:** The processor runs the
    application's instructions.
6.  **Output is produced:** The application displays its interface or
    performs its task.
7.  **More data may be loaded:** As you work, the application may read
    additional files or communicate over a network.

### Disk → RAM → CPU → Output

``` mermaid
flowchart LR
    A[("SSD / HDD<br/>Application files")] -->|"Load required code and data"| B["RAM<br/>Working memory"]
    B -->|"Instructions and data"| C["CPU<br/>Execute instructions"]
    C --> D["OUTPUT<br/>Screen / Sound"]
    C <--> B
    classDef storage fill:#f3e8ff,stroke:#9333ea,color:#581c87,stroke-width:2px
    classDef ram fill:#dbeafe,stroke:#2563eb,color:#172554,stroke-width:2px
    classDef cpu fill:#fef3c7,stroke:#d97706,color:#78350f,stroke-width:2px
    classDef output fill:#dcfce7,stroke:#16a34a,color:#14532d,stroke-width:2px
    class A storage
    class B ram
    class C cpu
    class D output
```

This is a simplified learning model. In a real computer, the CPU,
memory, storage, operating system, and devices work together
continuously. The CPU does not simply wait for the entire application to
be copied into RAM before doing anything.

### What if RAM is insufficient?

When physical RAM is under pressure, an operating system may use storage
to support memory management. On Linux this can include swap; on macOS,
the system can use swap files. Storage is much slower than RAM, so heavy
memory pressure can make the computer feel slow.

## 5. Understanding Your Computer's Specifications

When someone asks, "What are your computer specifications?", they
usually mean details such as:

-   Processor model and core information.
-   Installed RAM capacity.
-   Storage capacity and type.
-   Graphics processor (GPU).
-   Operating system and version.

### Linux commands

``` bash
# Operating system information
cat /etc/os-release

# Kernel and machine information
uname -a

# CPU information
lscpu

# RAM usage
free -h

# Storage devices
lsblk

# Disk space usage
df -h
```

Some commands, such as `lscpu`, `free`, and `lsblk`, are commonly
available on Linux but may not be installed by default on macOS.

### macOS commands

``` bash
# macOS version
sw_vers

# CPU / hardware overview
system_profiler SPHardwareDataType

# Memory details
system_profiler SPMemoryDataType

# Storage overview
diskutil list

# Available disk space
df -h
```

### Windows options

-   Open **Settings → System → About** for processor and RAM details.
-   Open **Task Manager → Performance** for CPU, memory, and disk
    information.
-   Open **Disk Management** to inspect storage devices and partitions.

### Practical activity: Inspect your own computer

Prepare a short report with these details:

  Component          What to record
  ------------------ ---------------------------------------
  Device             Laptop or desktop; manufacturer/model
  Processor          CPU model
  RAM                Total installed RAM
  Storage            SSD/HDD and capacity, if known
  Graphics           GPU model, if available
  Operating system   Name and version

Do not open a laptop or desktop cabinet just to complete this activity.
Use system information tools unless you are trained and authorized to
inspect internal components.

## 6. Class Discussion: Real-World Examples

Discuss these questions:

1.  Why does a computer need both RAM and storage?
2.  What happens if a computer has very little RAM?
3.  Is a keyboard an input device or an output device?
4.  Can a touchscreen be both an input and output device?
5.  Why does an application need an operating system?
6.  If a file is saved and the computer is switched off, why does the
    file remain available?

------------------------------------------------------------------------

# Part 2: Operating System Fundamentals

## 7. What is an Operating System?

An **Operating System (OS)** is system software that manages computer
hardware and software resources and provides services to application
programs.

In simple words, the operating system acts as a manager between
applications, users, and computer hardware.

Examples:

-   Microsoft Windows
-   Apple macOS
-   Linux distributions such as Ubuntu and Fedora
-   Android
-   iOS

### Why do we need an OS?

Imagine using a computer without an operating system. Every application
would need to manage hardware devices, memory, files, and many low-level
operations on its own. This would make software development and computer
use extremely difficult.

The OS makes the computer easier and safer to use by providing common
services.

### OS as an intermediary

``` mermaid
flowchart TB
    U["USER"] --> A["APPLICATIONS<br/>Browser, Editor, Player"]
    A --> O["OPERATING SYSTEM"]
    O --> H["HARDWARE"]
    H --> CPU["CPU"]
    H --> MEM["RAM"]
    H --> DISK["STORAGE"]
    H --> IO["INPUT / OUTPUT DEVICES"]
    classDef user fill:#dbeafe,stroke:#2563eb,color:#172554
    classDef app fill:#f3e8ff,stroke:#9333ea,color:#581c87
    classDef os fill:#fef3c7,stroke:#d97706,color:#78350f,stroke-width:3px
    classDef hw fill:#dcfce7,stroke:#16a34a,color:#14532d
    class U user
    class A app
    class O os
    class H,CPU,MEM,DISK,IO hw
```

**Example:** When you save a document, the application asks the OS to
save the data. The OS manages the file operation and communicates with
the storage system.

## 8. Major Functions of an Operating System

An operating system performs several important functions. The major ones
are process management, memory management, file management, device
management, security, and providing a user interface.

### 8.1 Process Management

A **program** is a set of instructions stored on a device. A **process**
is a program that is currently executing.

Examples:

-   Chrome running on your computer is a process.
-   A music player running in the background is a process.
-   A code editor executing your program creates or manages processes.

The OS manages processes by:

-   Creating and terminating processes.
-   Giving processes CPU time.
-   Switching the CPU between processes.
-   Managing process states.
-   Supporting communication between processes.

**Real-world example:** You are listening to music, downloading a file,
and typing in a code editor. The OS coordinates these activities so that
they can make progress.

### 8.2 Memory Management

Memory management is the OS function responsible for managing main
memory (RAM).

The OS:

-   Tracks which memory areas are in use.
-   Allocates memory to processes when required.
-   Reclaims memory when it is no longer needed.
-   Protects processes from incorrectly accessing one another's memory.
-   Manages virtual memory.

**Real-world example:** When you open a browser, the OS arranges memory
for it. When you close the browser, memory used by its processes can be
reclaimed.

### 8.3 File Management

File management allows users and applications to create, read, write,
rename, organize, and delete files and directories.

The OS manages:

-   Files and folders.
-   File names and directory structures.
-   File permissions.
-   Storage space and file-system operations.

Examples:

-   Saving an assignment as `OS_Assignment.pdf`.
-   Creating a folder named `Linux_Practicals`.
-   Renaming a file.
-   Deleting an unwanted document.

**Real-world example:** When you save a file in a folder, the
application requests the OS to perform the file operation.

### 8.4 Device Management

Device management controls and coordinates hardware devices through
device drivers and OS services.

Examples of devices:

-   Keyboard
-   Mouse
-   Printer
-   Webcam
-   USB drive
-   Network adapter

**Real-world example:** When you connect a USB drive, the OS detects the
device, communicates with it, and may make its files available through
the file manager.

A **device driver** is software that helps the operating system
communicate with a particular hardware device.

### 8.5 Security and Protection

The OS helps protect the system, user accounts, files, and running
processes.

Common security and protection features include:

-   User accounts and authentication.
-   File and directory permissions.
-   Process isolation.
-   Access control.
-   System updates and security mechanisms.

**Example:** A normal user may be allowed to read a file but not modify
it. An administrator or root account may have broader privileges.

Security is not provided by the OS alone. Safe user behavior,
application security, updates, and network configuration also matter.

### 8.6 User Interface

A **User Interface (UI)** allows a person to interact with a computer.

Two common types are:

#### GUI --- Graphical User Interface

A GUI uses graphical elements such as:

-   Windows
-   Icons
-   Menus
-   Buttons
-   Pointer
-   Dialog boxes

Examples: Windows desktop, macOS desktop, and Ubuntu's graphical
desktop.

#### CLI --- Command-Line Interface

A CLI allows a user to interact with the system by entering text
commands.

Example:

``` bash
pwd
```

This command displays the current working directory on Linux and macOS.

### CLI vs GUI

  -----------------------------------------------------------------------
  GUI                                 CLI
  ----------------------------------- -----------------------------------
  Uses graphical elements             Uses text commands

  Often easier for beginners          Requires learning commands

  Good for visual interaction         Good for automation and repeatable
                                      tasks

  May use more system resources       Often uses fewer resources for
                                      simple tasks

  Example: File Manager               Example: Terminal
  -----------------------------------------------------------------------

**Important:** CLI is not the same thing as Linux. Linux can be used
through a GUI, and Windows and macOS also provide command-line tools.

## 9. How the OS Manages Multiple Activities

Suppose you are doing all these tasks:

-   Playing a video.
-   Downloading a file.
-   Typing an assignment.
-   Listening to music.

The OS coordinates processes, memory, storage, and devices so these
activities can run together.

``` mermaid
flowchart TB
    A["RUNNING APPLICATIONS"] --> B["OPERATING SYSTEM"]
    B --> C["PROCESS MANAGEMENT<br/>CPU scheduling"]
    B --> D["MEMORY MANAGEMENT<br/>RAM allocation"]
    B --> E["FILE MANAGEMENT<br/>Files and folders"]
    B --> F["DEVICE MANAGEMENT<br/>Keyboard, display, USB"]
    B --> G["SECURITY & PROTECTION<br/>Permissions and isolation"]
    classDef app fill:#dbeafe,stroke:#2563eb,color:#172554
    classDef os fill:#fef3c7,stroke:#d97706,color:#78350f,stroke-width:3px
    classDef fn fill:#dcfce7,stroke:#16a34a,color:#14532d
    class A app
    class B os
    class C,D,E,F,G fn
```

## 10. Recap Quiz

Try answering these questions without looking at the notes.

1.  What is an operating system?
2.  Give four examples of operating systems.
3.  What is the difference between a program and a process?
4.  Which OS function manages RAM?
5.  Which OS function manages files and folders?
6.  What is a device driver?
7.  What is the difference between CLI and GUI?
8.  Why does an operating system need process management?
9.  Give one real-world example of memory management.
10. Why are user permissions important?

------------------------------------------------------------------------

# Part 3: Linux Introduction & Architecture

## 11. What is Linux?

**Linux** is an open-source, Unix-like operating system family built
around the Linux kernel.

The Linux kernel is the core component that manages hardware resources
and provides essential services to the rest of the system.

Linux is widely used in:

-   Web servers.
-   Cloud infrastructure.
-   Supercomputers.
-   Embedded devices.
-   Networking equipment.
-   Developer workstations.
-   Android-based devices (Android uses the Linux kernel, with a
    different user-space environment).

### Is Linux an OS or a kernel?

Technically, **Linux is the kernel**. A complete Linux operating system
normally combines the Linux kernel with system tools, libraries, package
management, applications, and other components.

This complete operating system is commonly called a **Linux
distribution** or **distro**.

## 12. Kernel vs Distribution

### Kernel

The **kernel** is the central part of the operating system. It runs with
high privileges and manages important system resources.

Its responsibilities include:

-   Process scheduling.
-   Memory management.
-   Device management.
-   System calls.
-   File-system support.
-   Networking.

### Distribution

A **Linux distribution** packages the Linux kernel with other software
to provide a usable operating system.

Examples:

-   Ubuntu
-   Fedora
-   Debian
-   Linux Mint
-   Arch Linux
-   Red Hat Enterprise Linux

### Kernel and distribution relationship

``` mermaid
flowchart TB
    A["LINUX DISTRIBUTION<br/>Example: Ubuntu"] --> B["APPLICATIONS<br/>Browser, Editor, Tools"]
    A --> C["SYSTEM LIBRARIES & UTILITIES"]
    A --> D["LINUX KERNEL"]
    D --> E["HARDWARE<br/>CPU, RAM, Disk, Devices"]
    classDef distro fill:#dbeafe,stroke:#2563eb,color:#172554,stroke-width:2px
    classDef apps fill:#f3e8ff,stroke:#9333ea,color:#581c87
    classDef kernel fill:#fef3c7,stroke:#d97706,color:#78350f,stroke-width:3px
    classDef hardware fill:#dcfce7,stroke:#16a34a,color:#14532d
    class A distro
    class B,C apps
    class D kernel
    class E hardware
```

**Analogy:** The kernel is like the engine of a vehicle. A distribution
is the complete vehicle with the engine, controls, seats, and other
components. The analogy is not exact, but it helps distinguish the
kernel from the complete system.

## 13. Linux vs Windows vs macOS

  -----------------------------------------------------------------------
  Feature           Linux             Windows           macOS
  ----------------- ----------------- ----------------- -----------------
  Developer         Open-source       Microsoft         Apple
                    community and                       
                    organizations                       

  Source model      Mostly open       Primarily         Primarily
                    source; varies by proprietary       proprietary, with
                    component                           some open-source
                                                        components

  Common use        Servers, cloud,   Desktops,         Apple computers,
                    development,      business, gaming  creative work,
                    desktops                            development

  User interface    Many desktop      GUI and CLI       GUI and Terminal
                    environments; CLI                   
                    available                           

  Customization     Very high         Moderate          More controlled

  Distributions /   Ubuntu, Fedora,   Windows editions  macOS releases
  editions          Debian, etc.                        
  -----------------------------------------------------------------------

### Important points

-   Linux is not one single desktop product. It has many distributions.
-   Windows and macOS also provide command-line environments.
-   Linux, Windows, and macOS all support multitasking, files, users,
    and networking.
-   The commands and directory structures can differ between operating
    systems.

## 14. What Does Open Source Mean?

**Open-source software** makes its source code available under a license
that allows users to use, inspect, and often modify and redistribute it
according to that license.

Benefits may include:

-   Transparency.
-   Community collaboration.
-   Customization.
-   Learning from real source code.
-   Independent development and improvement.

**Example:** Ubuntu is a popular Linux distribution that uses many
open-source components.

**Important:** Open source does not automatically mean that every use is
free of conditions. Users must follow the software's license.

## 15. Where Is Linux Used?

Linux is used in many areas of technology.

  Area               Example use
  ------------------ ----------------------------------------------------
  Web servers        Hosting websites and APIs
  Cloud computing    Running virtual machines and cloud workloads
  Supercomputers     High-performance scientific computing
  Cybersecurity      Security testing and analysis environments
  Embedded systems   Routers, smart devices, and appliances
  Development        Programming, compiling, containers, and automation
  Android            Android uses the Linux kernel

### Why do developers use Linux?

-   Powerful command-line tools.
-   Strong programming and server ecosystem.
-   Package managers for installing software.
-   Automation through shell scripts.
-   Common use in cloud and server environments.
-   Open-source tools and customization.

## 16. Linux Architecture

Linux architecture can be understood as layers. Each layer has a role in
connecting the user and applications to the hardware.

The three broad areas introduced in this lecture are:

1.  User Space
2.  Shell
3.  Kernel

Hardware is below the kernel.

### 16.1 User Space

**User space** is the area where normal applications and many system
utilities run.

Examples:

-   Web browsers.
-   Text editors.
-   Terminal applications.
-   File managers.
-   Shell programs.
-   User commands such as `ls` and `cat`.

Applications normally cannot directly perform privileged hardware
operations. They request services from the kernel through defined
interfaces.

### 16.2 Shell

A **shell** is a program that provides an interface for users to
interact with the operating system, commonly by entering commands.

Examples of shells:

-   Bash
-   Zsh
-   Fish
-   Dash

Example:

``` bash
pwd
```

The shell reads the command and runs the corresponding program or
built-in operation.

**Important:** A terminal and a shell are not the same thing.

-   **Terminal:** The application or interface where you type and view
    text.
-   **Shell:** The command interpreter running inside the terminal.

For example, Terminal on macOS is a terminal application. It commonly
opens Zsh as the shell.

### 16.3 Kernel

The **kernel** is the core of the operating system. It manages system
resources and provides services to applications.

Important responsibilities:

-   Process scheduling.
-   Memory management.
-   Device drivers and device access.
-   File systems.
-   Networking.
-   System calls.

### 16.4 Hardware

Hardware includes the physical components:

-   CPU
-   RAM
-   Storage
-   Keyboard
-   Mouse
-   Display
-   Network devices

### Linux architecture diagram

``` mermaid
flowchart TB
    U["USER"] --> A["APPLICATIONS<br/>Browser, Editor, File Manager"]
    A --> S["SHELL / SYSTEM UTILITIES<br/>Bash, Zsh, Commands"]
    S -->|"System calls when required"| K["LINUX KERNEL<br/>Process • Memory • Files • Devices • Network"]
    K --> H["HARDWARE<br/>CPU • RAM • Storage • I/O"]
    classDef user fill:#dbeafe,stroke:#2563eb,color:#172554
    classDef apps fill:#f3e8ff,stroke:#9333ea,color:#581c87
    classDef shell fill:#fef3c7,stroke:#d97706,color:#78350f
    classDef kernel fill:#ffedd5,stroke:#ea580c,color:#7c2d12,stroke-width:3px
    classDef hardware fill:#dcfce7,stroke:#16a34a,color:#14532d
    class U user
    class A apps
    class S shell
    class K kernel
    class H hardware
```

This is a simplified conceptual diagram. Applications can make system
calls directly through libraries; they do not all have to pass through a
shell. The shell is mainly a user interface for commands.

## 17. What Happens When You Run a Linux Command?

Suppose you open a terminal and type:

``` bash
ls
```

A simplified explanation:

1.  You type `ls` in the terminal.
2.  The shell reads and interprets the command.
3.  The shell locates and runs the `ls` program (unless it is a shell
    built-in).
4.  The program requests directory information using operating-system
    interfaces.
5.  The kernel performs the required protected operations.
6.  The result is returned to the program.
7.  The output appears in the terminal.

``` mermaid
sequenceDiagram
    actor User
    participant Terminal
    participant Shell
    participant Program as ls Program
    participant Kernel
    User->>Terminal: Type ls
    Terminal->>Shell: Send command input
    Shell->>Program: Locate and run ls
    Program->>Kernel: Request directory information
    Kernel-->>Program: Return directory entries
    Program-->>Terminal: Print names
    Terminal-->>User: Display output
```

## 18. Hands-on: First Linux Terminal Commands

A **terminal** lets you interact with the system using text commands.
These commands are useful on Linux and, in many cases, on macOS too.

> Open Terminal on your Linux machine or macOS. Type each command and
> observe the output.

### 18.1 `whoami` --- Current User

Displays the username of the account running the command.

``` bash
whoami
```

Example output:

``` text
akash
```

**Where is it useful?**

-   Checking which account is active.
-   Confirming which user is running a command.
-   Troubleshooting permission problems.

### 18.2 `pwd` --- Present Working Directory

Displays the full path of your current directory.

``` bash
pwd
```

Example output on Linux:

``` text
/home/akash
```

Example output on macOS:

``` text
/Users/akash
```

**Where is it useful?**

-   Finding your current location in the file system.
-   Confirming where a file or folder will be created.
-   Avoiding mistakes when working with paths.

### 18.3 `date` --- Current Date and Time

Displays the system date and time.

``` bash
date
```

**Where is it useful?**

-   Checking the system clock.
-   Recording when a command was run.
-   Understanding timestamps in logs.

### 18.4 `uname` --- System and Kernel Information

Displays basic system information.

``` bash
uname
```

Displays the kernel name. For more details:

``` bash
uname -a
```

The `-a` option requests all information available through this command,
such as kernel name, version, and machine architecture.

**Where is it useful?**

-   Identifying the kernel.
-   Checking machine architecture.
-   Troubleshooting system compatibility.

**Note:** On macOS, `uname` reports Darwin as the kernel name. macOS is
not a Linux distribution; it uses the Darwin/XNU operating-system
foundation.

### 18.5 `clear` --- Clear the Terminal Screen

Clears the visible terminal screen.

``` bash
clear
```

It does not delete files or erase command history. It only clears the
current visible display.

### 18.6 `ls` --- List Files and Directories

Displays the contents of the current directory.

``` bash
ls
```

Useful variations:

``` bash
# Detailed listing
ls -l

# Include hidden files
ls -a

# Detailed listing including hidden files
ls -la

# Human-readable file sizes in a long listing
ls -lh
```

**Where is it useful?**

-   Checking which files exist in a folder.
-   Finding project files.
-   Viewing hidden configuration files.
-   Checking file permissions and sizes.

### Quick command reference

  Command      Purpose                                    Example
  ------------ ------------------------------------------ ------------
  `whoami`     Shows current username                     `whoami`
  `pwd`        Shows current directory                    `pwd`
  `date`       Shows date and time                        `date`
  `uname`      Shows kernel name                          `uname`
  `uname -a`   Shows detailed system/kernel information   `uname -a`
  `clear`      Clears visible terminal screen             `clear`
  `ls`         Lists files and directories                `ls -la`

## 19. Linux and macOS: Important Path Differences

Linux and macOS both have Unix-like command-line environments, so many
basic commands are similar. However, their directory structures and
system details are not identical.

  -----------------------------------------------------------------------
  Purpose                 Linux example           macOS example
  ----------------------- ----------------------- -----------------------
  Home directory          `/home/akash`           `/Users/akash`

  Root directory          `/`                     `/`

  System configuration    `/etc`                  `/etc` (many paths link
                                                  into other system
                                                  locations)

  Temporary files         `/tmp`                  `/tmp`

  Applications            Varies by distribution; `/Applications`
                          often `/usr`, `/opt`,   
                          etc.                    

  User files              `/home/username`        `/Users/username`

  External volumes        Often under `/media` or `/Volumes`
                          `/mnt`                  
  -----------------------------------------------------------------------

### Useful macOS directories

-   `/Applications` --- Many installed graphical applications.
-   `/Users` --- Home folders for user accounts.
-   `/Volumes` --- Mounted drives and volumes.
-   `/System` --- Protected system files.
-   `/private` --- Contains important private system directories; `/tmp`
    and `/var` commonly point into it.

### Useful Linux directories

-   `/home` --- Home directories for regular users.
-   `/root` --- Home directory of the root account.
-   `/etc` --- System-wide configuration files.
-   `/bin` and `/usr/bin` --- Common executable programs; exact layout
    varies.
-   `/var` --- Variable data such as logs and caches.
-   `/tmp` --- Temporary files.
-   `/dev` --- Device files.
-   `/proc` --- Virtual file system exposing process and kernel
    information.

**Remember:** A path beginning with `/` is an absolute path. A path that
does not begin with `/` is generally interpreted relative to the current
working directory.

## 20. Practical Exercise: Explore Your System

Run the following commands one by one:

``` bash
whoami
pwd
date
uname
uname -a
ls
ls -la
clear
```

Then collect operating-system information.

### On Linux

``` bash
cat /etc/os-release
```

This displays information about the Linux distribution.

### On macOS

``` bash
sw_vers
```

This displays macOS product and version information.

### Practical submission

Create a text file named `Lec6_Terminal_Activity.txt` and include:

1.  Your current username.
2.  Your current working directory.
3.  The date and time shown by the terminal.
4.  The output of `uname -a`.
5.  Your operating system name and version.
6.  A short explanation of what `ls -la` displays.

You may copy terminal output into the text file. Do not include
passwords, private keys, access tokens, or other confidential
information.

------------------------------------------------------------------------

# Part 4: Revision and Self-Assessment

## 21. Important Differences to Remember

### Hardware vs Software

-   Hardware is the physical part of a computer.
-   Software is the set of programs and instructions.

### RAM vs Storage

-   RAM holds data currently being used.
-   Storage keeps files and programs for long-term use.

### CPU vs RAM

-   CPU executes instructions.
-   RAM holds the data and instructions currently needed by running
    programs.

### Program vs Process

-   A program is a set of stored instructions.
-   A process is an executing instance of a program.

### Kernel vs Shell

-   Kernel manages hardware and core system resources.
-   Shell provides a command interface to the operating system.

### Terminal vs Shell

-   Terminal is the application/interface that displays text input and
    output.
-   Shell interprets commands entered by the user.

### Linux vs Ubuntu

-   Linux is the kernel.
-   Ubuntu is a Linux distribution that includes the Linux kernel and
    other software.

### CLI vs GUI

-   CLI uses text commands.
-   GUI uses graphical elements such as windows, icons, and menus.

## 22. Short-Answer Questions

1.  Define a computer and explain the IPO cycle.
2.  Differentiate between hardware and software with four examples each.
3.  What is the function of a CPU?
4.  What is RAM? Why is it called volatile memory?
5.  Differentiate between RAM and storage.
6.  What is the function of a motherboard?
7.  Explain input and output devices with examples.
8.  What happens when you open an application?
9.  Define an operating system.
10. Why is an operating system required?
11. Explain process management.
12. Explain memory management.
13. What is file management?
14. What is a device driver?
15. Differentiate between CLI and GUI.
16. What is Linux?
17. Differentiate between the Linux kernel and a Linux distribution.
18. What does open source mean?
19. Explain the three major areas introduced in Linux architecture: user
    space, shell, and kernel.
20. Differentiate between a terminal and a shell.

## 23. Practical / Application-Based Questions

1.  You have opened a browser, a music player, and a code editor. Which
    OS functions are involved in managing these applications?
2.  Your computer becomes slow when many applications are open. Which
    resource may be under pressure?
3.  You save a document and switch off your computer. Which component
    keeps the document available?
4.  You connect a USB drive. Which OS function helps the computer
    communicate with it?
5.  You type `pwd` in Terminal. What information does it display?
6.  You type `whoami`. What are you checking?
7.  You type `uname -a`. What kind of information can you expect?
8.  You run `ls -la`. What additional information does it show compared
    with `ls`?
9.  Why can the same basic commands work on both Linux and macOS?
10. Why is Ubuntu called a Linux distribution rather than the Linux
    kernel itself?

## 24. Final Learning Checklist

After completing these lectures, you should be able to:

-   [ ] Explain what a computer does using the Input--Process--Output
    model.
-   [ ] Identify hardware and software components.
-   [ ] Explain the roles of CPU, RAM, storage, motherboard, and I/O
    devices.
-   [ ] Describe what happens when an application is opened.
-   [ ] Find basic specifications of your own computer.
-   [ ] Define an operating system and explain why it is needed.
-   [ ] Describe process, memory, file, and device management.
-   [ ] Differentiate between CLI and GUI.
-   [ ] Explain Linux, the Linux kernel, and Linux distributions.
-   [ ] Explain the basic Linux architecture.
-   [ ] Use `whoami`, `pwd`, `date`, `uname`, `clear`, and `ls`.
-   [ ] Identify basic differences between Linux and macOS file-system
    paths.

------------------------------------------------------------------------

**End of Notes --- 1 Computer Fundamentals**

*Learning tip: Do not only memorize command names. Run each command,
observe its output, and explain in your own words what the computer has
shown you.*
