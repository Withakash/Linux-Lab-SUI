# Linux Lab – Lecture 4
## VirtualBox Deep Dive, ISO Files & Virtual Machine Management

**Duration:** 40 Minutes  
**Previous Classes Completed:**
1. Virtualization, Hypervisors, VirtualBox installation
2. Creating a VM and installing Ubuntu
3. Guest Additions, Shared Folders, Snapshots, and first Terminal commands

---

## Lecture Goal

Students have already created an Ubuntu virtual machine. This lecture helps them understand **what is happening behind the interface** and what else they can do with VirtualBox.

By the end of the class, students should understand:

- What a virtual machine actually contains
- What an ISO file is and why it is used
- How VirtualBox emulates hardware
- Important VirtualBox features and settings
- The difference between a VM, ISO, virtual disk, and snapshot
- How to safely manage, copy, clone, export, and restore virtual machines

---

# 40-Minute Teaching Flow

| Time | Topic | What to Teach / Demonstrate |
|---|---|---|
| 0–5 min | Quick Recap | VM created, Ubuntu installed, Guest Additions, shared folders, snapshots |
| 5–12 min | What is an ISO File? | Explain ISO as a disk image; bootable installation media |
| 12–22 min | What is Inside a Virtual Machine? | Virtual RAM, vCPU, virtual disk, virtual network card, display, USB |
| 22–32 min | Important VirtualBox Features | Settings, snapshots, clone, export/import, networking, shared clipboard, drag & drop |
| 32–37 min | Live Demo | Explore VM settings and show one practical feature |
| 37–40 min | Recap + Practical | Students inspect their own VM configuration |

---

# 1. Start with a Simple Question

Ask students:

> “We installed Ubuntu without formatting our real laptop. So where is Ubuntu actually stored?”

Explain:

Your physical laptop is called the **Host Machine**.

The Ubuntu running inside VirtualBox is called the **Guest Machine**.

```text
+--------------------------------------+
| Physical Laptop                      |
|                                      |
|  Host Operating System               |
|  Windows / macOS / Linux             |
|                                      |
|       +----------------------+       |
|       | Oracle VirtualBox    |       |
|       |                      |       |
|       |   Ubuntu VM          |       |
|       |   Guest OS           |       |
|       +----------------------+       |
+--------------------------------------+
```

---

# 2. What is an ISO File?

An **ISO file** is a digital copy of an optical disk such as a CD or DVD.

For operating systems, an ISO commonly contains:

- Boot files
- Operating system installer
- Installation packages
- System configuration files

Example:

```text
ubuntu-24.xx-desktop-amd64.iso
```

When we attach the ISO to a VM, VirtualBox treats it like a DVD inserted into a virtual DVD drive.

```text
Ubuntu ISO
     |
     v
Virtual DVD Drive
     |
     v
Boot Ubuntu Installer
     |
     v
Install Ubuntu
     |
     v
Virtual Hard Disk
```

## Important Concept

The ISO is mainly used for installation.

After Ubuntu is installed, the operating system is stored on the **virtual hard disk**, not inside the ISO.

### Analogy

- ISO = Installation CD/DVD
- Virtual Disk = Laptop's hard disk
- VirtualBox = Virtual computer environment
- Ubuntu = Guest operating system

---

# 3. What Is Inside a Virtual Machine?

A VM is not just one program. VirtualBox creates a complete virtual computer.

Students should understand these components.

## Virtual CPU

The VM receives a portion of the host computer's CPU.

Example:

```text
Host Laptop: 8 CPU Cores
VM: 2 Virtual CPUs
```

Do not allocate all CPU cores to one VM.

## Virtual RAM

The VM receives part of the physical RAM.

Example:

```text
Host RAM: 16 GB
Ubuntu VM: 4 GB
```

Too much RAM for the VM can slow down the host system.

## Virtual Hard Disk

Ubuntu is installed on a file that behaves like a real hard disk.

Common VirtualBox disk format:

```text
VDI = Virtual Disk Image
```

Other formats include:

- VMDK
- VHD

## Virtual Network Adapter

The VM can access networks using a virtual network card.

## Virtual Display

VirtualBox creates a virtual graphics/display environment.

## Virtual USB Controller

USB devices can potentially be connected to the guest machine.

---

# 4. VM Settings Students Should Explore

Open:

```text
VirtualBox
→ Select Ubuntu VM
→ Settings
```

## System

Explore:

- Base Memory
- Processor count
- Boot Order

Explain boot order:

```text
Optical Drive → Hard Disk
```

During installation:

```text
ISO boots first
```

After installation:

```text
Virtual Hard Disk boots Ubuntu
```

## Display

Explore:

- Video Memory
- Graphics Controller
- Screen settings

Guest Additions improve display integration.

## Storage

This is one of the most important sections.

Show:

```text
Controller
 ├── Ubuntu ISO
 └── Ubuntu Virtual Disk (.vdi)
```

Explain clearly:

```text
ISO = Installer
VDI = Installed Ubuntu
```

## Network

Introduce the idea without going too deep.

Main modes:

- NAT
- Bridged Adapter
- Host-Only Adapter

For beginners, explain NAT first.

```text
Host Laptop → Internet
        |
        v
     VirtualBox
        |
        v
    Ubuntu VM
```

---

# 5. Important VirtualBox Features

## A. Snapshots

Already covered, but revise:

A snapshot is like a restore point for the VM.

Example:

```text
Fresh Install
     |
     v
Install Software
     |
     v
Experiment
     |
     v
Problem Occurs
     |
     v
Restore Snapshot
```

Important:

Snapshots are useful before risky experiments.

---

## B. Shared Clipboard

Allows copying text between:

```text
Host ↔ Guest
```

Modes may include:

- Disabled
- Host to Guest
- Guest to Host
- Bidirectional

Demo:

Copy a command from the host and paste it into Ubuntu.

---

## C. Drag and Drop

Files may be moved between host and guest when supported and configured.

```text
Host → Guest
Guest → Host
Bidirectional
```

Guest Additions may be required.

---

## D. Shared Folders

A folder on the host can be made accessible inside Ubuntu.

```text
Host Folder
     |
     | Shared
     v
Ubuntu VM
```

Use case:

Students can keep assignments on their real laptop and access them inside Ubuntu.

---

## E. Full-Screen Mode and Seamless Integration

With Guest Additions:

- Better screen resolution
- Dynamic resizing
- Full-screen mode
- Better mouse integration

Useful shortcut to mention:

```text
Host Key + F
```

The default Host Key is commonly Right Ctrl, but students should check their VirtualBox configuration.

---

# 6. Clone a Virtual Machine

Cloning creates a copy of an existing VM.

Example:

```text
Ubuntu Fresh
      |
      +---- Ubuntu Lab Copy
      |
      +---- Ubuntu Testing Copy
```

Use case:

Create a clean Ubuntu VM and use clones for experiments.

This prevents students from repeatedly reinstalling Ubuntu.

---

# 7. Export and Import a VM

A complete VM can be packaged and moved to another system.

Concept:

```text
Virtual Machine
      |
      v
Export Appliance
      |
      v
OVA / OVF
      |
      v
Transfer
      |
      v
Import into VirtualBox
```

Possible use:

The teacher can prepare a configured Linux environment and students can import it instead of installing everything manually.

---

# 8. Virtual Disk Concepts

Important formats:

| Format | Meaning |
|---|---|
| VDI | VirtualBox's native virtual disk format |
| VMDK | Common VMware disk format |
| VHD | Virtual Hard Disk format |

Explain one key idea:

The `.vdi` file behaves like the VM's hard disk.

Inside it are:

- Ubuntu operating system
- Installed applications
- Student files
- System configuration

---

# 9. Dynamic vs Fixed Virtual Disk

## Dynamically Allocated

The virtual disk grows as data is added.

Example:

```text
Maximum size: 50 GB
Currently used: 12 GB
Host disk usage: approximately based on actual VM data
```

## Fixed Size

VirtualBox reserves the configured disk size earlier.

Example:

```text
50 GB fixed disk
```

For most student laptops, dynamically allocated storage is usually easier to manage.

---

# 10. What Happens When You Start a VM?

Show the complete flow:

```text
Click Start
     |
     v
VirtualBox Creates Virtual Hardware
     |
     +---- Virtual CPU
     +---- Virtual RAM
     +---- Virtual Disk
     +---- Virtual Display
     +---- Virtual Network
     |
     v
Boot Process Starts
     |
     v
Ubuntu Kernel Loads
     |
     v
Ubuntu Desktop Starts
```

This connects the previous virtualization theory with the practical VM.

---

# 11. Power Options: Important Difference

When closing a VM, students may see options such as:

## Save the Machine State

Like pausing the VM.

Later it resumes from approximately the same state.

## Send Shutdown Signal

Requests the guest operating system to shut down properly.

## Power Off

Similar to suddenly removing power.

Avoid using this regularly because it may cause data loss or file-system problems.

---

# 12. Suggested Live Demo for Today's Class

Use your own Ubuntu VM.

### Demo Checklist

1. Open VM Settings.
2. Show allocated RAM.
3. Show allocated processors.
4. Open Storage and identify:
   - Ubuntu ISO
   - Ubuntu `.vdi` virtual disk
5. Open Network and show NAT.
6. Show Shared Clipboard setting.
7. Show Snapshots.
8. Demonstrate Save State or proper Shutdown.
9. If time permits, show Clone or Export options.

---

# 13. Student Practical Activity

Ask every student to open:

```text
VirtualBox → Ubuntu VM → Settings
```

They should identify and note:

1. How much RAM is allocated?
2. How many processors/vCPUs are allocated?
3. What is the virtual disk size?
4. Is an ISO currently attached?
5. What network mode is selected?
6. What is the name of their latest snapshot?

Optional:

```text
Create a new snapshot:
"Before Linux Commands"
```

---

# 14. Suggested Assignment

## Virtual Machine Configuration Report

Students should submit:

- Screenshot of VirtualBox Manager
- Screenshot of System settings showing RAM and CPU
- Screenshot of Storage settings
- Screenshot of Network settings
- A short answer:

> Explain the difference between an ISO file, a virtual disk, and a snapshot.

---

# 15. Key Concepts to Ensure Students Understand

By the end of the lecture, students should be able to answer:

### What is the Host OS?

The real operating system running on the physical computer.

### What is the Guest OS?

The operating system running inside the virtual machine.

### What is an ISO?

A disk image commonly used as bootable installation media.

### What is a VDI?

A VirtualBox virtual hard disk file.

### What is a Snapshot?

A saved state/checkpoint that can be used to restore the VM.

### Why Guest Additions?

To improve integration between host and guest.

### What is a Clone?

A copy of an existing virtual machine.

### Why use a Virtual Machine?

To safely run and experiment with another operating system without replacing the main operating system.

---

# Recommended Next Lecture

After this lecture, students should move into actual Linux usage:

## Linux Basics & File System Navigation

Suggested flow:

1. What is a Shell?
2. Terminal vs GUI
3. Linux file system overview
4. `/`, `/home`, `/etc`, `/bin`, `/tmp`
5. `pwd`
6. `ls`
7. `cd`
8. Absolute vs relative paths
9. `mkdir`
10. `touch`
11. `clear`
12. Basic practical navigation challenge

This creates a smooth transition from:

```text
Virtual Machine Setup
        ↓
Understanding Linux Environment
        ↓
Terminal Basics
        ↓
Linux Commands
        ↓
File System
        ↓
Users and Permissions
        ↓
Processes and Shell Scripting
```
