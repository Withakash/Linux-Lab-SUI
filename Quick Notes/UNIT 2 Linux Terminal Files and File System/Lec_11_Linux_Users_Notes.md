# Lec 11: Linux Users – Root User, Normal User, UID & GID

**Level:** Beginner  
**Total lecture time:** 40 minutes

## Learning Objectives

By the end of this lecture, students will be able to:

- Explain what a Linux user is.
- Differentiate between the root user and a normal user.
- Explain **UID (User ID)** and **GID (Group ID)**.
- Differentiate between primary and supplementary groups.
- Use `whoami`, `id`, `groups`, and `who`.
- Identify their own user details and file ownership.

---

## 1. Introduction: What is a User in Linux?

Think about a college computer lab:

- Students have their own accounts.
- Teachers may have different permissions.
- The lab administrator can install software and change system settings.
- Every person has a separate identity.

Linux works in a similar way. It supports multiple users, and each user has a specific identity and permissions.

A **user** is an identity through which a person or process accesses a Linux system.

### Example: Multiple users on one computer

```text
                  LINUX COMPUTER
                        |
          +-------------+-------------+
          |                           |
       Akash                         Rahul
      UID: 1001                     UID: 1002
          |                           |
     Files & access              Files & access
     permissions                 permissions
```

Linux identifies each user using a unique number called a **UID (User ID)**.

Every user account can have:

- A username
- A UID
- A primary group
- Additional groups
- A home directory
- A login shell
- Specific permissions

### Example user account

```text
Username: akash
UID:      1001
GID:      1001
Home:     /home/akash
Shell:    /bin/bash
```

This information helps Linux identify the user and control what they can access.

---

## 2. Root User vs Normal User

Linux distinguishes between the administrator account (**root**) and ordinary user accounts.

### 2.1 Root User

The **root user** is the superuser or system administrator in Linux. It has **UID 0**.

Root can:

- Install and uninstall software.
- Create and delete user accounts.
- Modify system configuration.
- Access protected system files.
- Manage other users and permissions.
- Start and stop system services.

Think of root as the principal of a college who has administrative control over the entire institution.

### 2.2 Normal User

A **normal user** is an account created for everyday activities, such as:

- Writing programs
- Creating files
- Browsing the internet
- Running applications
- Working on assignments

A normal user generally cannot modify protected system files or install system-wide software without administrator privileges.

Think of a normal user as a student who can use college facilities but cannot change the college's administrative records.

### Root vs Normal User

| Feature | Root User | Normal User |
|---|---|---|
| UID | `0` | Usually `1000` or higher on Ubuntu |
| Permissions | Full administrative privileges | Limited permissions |
| Install system software | Yes | Requires authorization |
| Modify system files | Yes | Usually restricted |
| Create other users | Yes | Usually restricted |
| Access protected files | Yes | Usually restricted |

> **Important:** UID `0` is what gives an account root-level identity. The username `root` is the conventional name for this account.

### 2.3 How to use administrative privileges

On Ubuntu, temporarily execute a command with elevated privileges:

```bash
sudo apt update
```

- `sudo` means execute a command with elevated privileges.
- `apt update` refreshes package information.

Open a root login shell on Ubuntu:

```bash
sudo -i
```

Check the current effective user:

```bash
whoami
```

Exit the root shell:

```bash
exit
```

**Safety rule:** Do not perform everyday activities as root. A mistake made with administrative privileges can damage the system.

---

## 3. What is UID (User ID)?

**UID** stands for **User ID**.

Linux does not internally depend only on usernames. It uses numeric IDs to identify users.

### Example

| Username | UID |
|---|---:|
| `root` | `0` |
| `akash` | `1000` |
| `rahul` | `1001` |
| `amit` | `1002` |

When a user creates a file, Linux associates that file with the user's identity.

### How UID relates to file ownership

Suppose Akash creates a file:

```bash
touch notes.txt
```

Check its ownership:

```bash
ls -l notes.txt
```

Example output:

```text
-rw-r--r--  1 akash  akash  0 Nov 3 notes.txt
```

Here:

- `akash` – file owner.
- The second `akash` – group owner.
- `rw-r--r--` – file permissions.

Linux can use the UID internally to identify the actual owner.

**Real-life analogy:** A college has student names, but every student also has a unique enrollment number. Even if two students have similar names, their enrollment numbers distinguish them. Similarly, UID uniquely identifies a user.

---

## 4. What is GID (Group ID)?

**GID** stands for **Group ID**.

Linux allows users to be organized into groups. Groups make permission management easier.

Imagine 50 students working on a common project. Instead of assigning permissions to each student separately, an administrator can create a group and give that group access.

### Example: Users organized into groups

```text
                    LINUX SYSTEM
                         |
              +----------+----------+
              |                     |
           Students               Teachers
              |                     |
          +---+---+             +---+---+
          |       |             |       |
        Akash    Amit          Rahul   Priya
```

### Example user and group details

| Username | UID | Primary Group | GID |
|---|---:|---|---:|
| Akash | 1000 | students | 2000 |
| Rahul | 1001 | students | 2000 |
| Priya | 1002 | teachers | 2001 |

Here:

- Akash and Rahul belong to the `students` group.
- Priya belongs to the `teachers` group.
- Akash and Rahul share the same primary GID.

### 4.1 Primary Group vs Supplementary Groups

A user has one **primary group** and can also belong to additional **supplementary groups**.

Example:

```text
User: akash

Primary Group:
    students

Supplementary Groups:
    developers
    docker
    sudo
```

This means Akash belongs to the `students` group by default, but also has membership in other groups.

### Why are groups useful?

Suppose five developers need access to a shared project folder. Instead of changing permissions for every developer individually, an administrator can assign access to the `developers` group.

---

## 5. How UID and GID Work Together

Suppose Akash creates a file:

```bash
touch project.txt
```

The file can have ownership information such as:

```text
Owner: Akash
Group: Students
UID:   1000
GID:   2000
```

Linux uses this ownership information when deciding whether a user can read, modify, or execute the file.

### Ownership and permission decision – conceptual diagram

```text
                  FILE: project.txt
                         |
                +--------+--------+
                |                 |
             Owner              Group
             Akash             Students
             UID 1000          GID 2000
                |                 |
                +--------+--------+
                         |
                   Permissions
                         |
             Read / Write / Execute
```

Remember:

- **UID** identifies the owner.
- **GID** identifies the group associated with the file.
- **Permissions** determine what the owner, group members, and others can do.

File permissions will be studied in more detail in a later lecture.

---

## 6. Practical Commands – Identifying Linux Users

The four commands in this lecture are:

1. `whoami`
2. `id`
3. `groups`
4. `who`

### Command 1: `whoami`

**Purpose:** Displays the username of the current effective user.

**Syntax:**

```bash
whoami
```

Example output:

```text
akash
```

This means the current effective user is `akash`.

Try:

```bash
sudo whoami
```

Example output:

```text
root
```

**Why does the output change?**

Because `sudo` runs the command with elevated privileges, and `whoami` reports the effective user executing it.

### Command 2: `id`

**Purpose:** Displays the UID, GID, and group memberships of the current user.

**Syntax:**

```bash
id
```

Example output on a Linux system:

```text
uid=1000(akash) gid=1000(akash) groups=1000(akash),27(sudo),1001(developers)
```

| Output | Meaning |
|---|---|
| `uid=1000` | User ID is 1000 |
| `(akash)` | Username is akash |
| `gid=1000` | Primary Group ID is 1000 |
| `(akash)` | Primary group name |
| `groups=` | All group memberships |

You can also check another user's information:

```bash
id root
```

Or:

```bash
id username
```

### Command 3: `groups`

**Purpose:** Displays the groups to which a user belongs.

**Syntax:**

```bash
groups
```

Example output:

```text
akash sudo developers
```

This means Akash belongs to:

- `akash`
- `sudo`
- `developers`

To check another user:

```bash
groups root
```

Remember:

- `id` displays UID, GID, and groups.
- `groups` focuses on group memberships.

### Command 4: `who`

**Purpose:** Displays users currently logged into the system.

**Syntax:**

```bash
who
```

Example output:

```text
akash    console    Nov 3 10:30
rahul    pts/0      Nov 3 11:15
```

| Column | Meaning |
|---|---|
| Username | Logged-in user |
| Terminal | Login terminal/session |
| Date | Login date |
| Time | Login time |

**What is `pts/0`?**

`pts` means a pseudo-terminal session. For example, when a user connects to a Linux machine through SSH, a pseudo-terminal may be allocated.

**What is `console`?**

It generally represents a local console login session.

> **Important:** `who` shows login sessions, not every process or application currently running.

### Command comparison

| Command | Main purpose | Information shown |
|---|---|---|
| `whoami` | Current effective user | Username |
| `id` | User identity details | UID, GID, groups |
| `groups` | Group membership | Group names |
| `who` | Active login sessions | Logged-in users and sessions |

---

## 7. How to Practise This Lecture on macOS

The commands can also be practised in macOS Terminal. However, **Linux and macOS may show different UID/GID values and group names**.

Open Terminal and execute the following commands.

### Step 1: Identify your current user

```bash
whoami
```

Example:

```text
akash
```

### Step 2: Check your UID and GID

```bash
id
```

Example output on macOS:

```text
uid=501(akash) gid=20(staff) groups=20(staff),12(everyone),80(admin)
```

Your actual output may be different.

Notice:

- UID `501` identifies the account in this example.
- GID `20` identifies the primary group.
- `admin` indicates membership in the administrator group.

### Step 3: Check your groups

```bash
groups
```

This displays all groups associated with your current account.

### Step 4: Check logged-in users

```bash
who
```

This displays active login sessions.

### Step 5: Check root privileges

```bash
sudo whoami
```

Enter your Mac login password when prompted.

Expected output:

```text
root
```

This demonstrates the difference between your normal account and elevated administrative execution.

### Step 6: Check file ownership

```bash
touch myfile.txt
ls -l myfile.txt
```

Observe the username and group displayed in the output.

### Linux vs macOS

| Concept | Ubuntu (typical) | macOS (typical) |
|---|---|---|
| Root UID | `0` | `0` |
| Normal user UID | Often `1000` or higher | Often starts at `501` |
| Primary group | Often same name as user | Often `staff` |
| Administrator group | `sudo` | `admin` |
| Default shell | Often Bash | Often Zsh |
| Elevated command | `sudo` | `sudo` |

macOS has a root account, but direct root login is normally disabled by default. You can use `sudo` if your account has administrator privileges.

### macOS note: `sudo -i` and `sudo -s`

On macOS, `sudo -i` may not behave as expected in some terminal or shell configurations. To open a root shell, try:

```bash
sudo -s
```

Enter your Mac login password when prompted.

Your prompt may change from something like:

```text
akash@MacBook ~ %
```

to a root shell prompt, for example:

```text
sh-3.2#
```

Now check:

```bash
whoami
```

Expected output:

```text
root
```

Exit the root shell:

```bash
exit
```

Check again:

```bash
whoami
```

It should display your normal username again.

**Important:** `sudo -s` gives the current terminal session root privileges. Use it only when needed and exit with `exit` when finished.

If `sudo -s` also fails, check the exact error message and your account's administrator privileges.

### Ubuntu vs macOS: privilege commands

| Command | Ubuntu | macOS |
|---|---|---|
| `sudo -i` | Opens a root login shell | Usually available; behavior can vary |
| `sudo -s` | Opens a root shell | Opens a root shell |
| `sudo whoami` | Prints `root` | Prints `root` |
| `whoami` | Prints current effective user | Prints current effective user |

---

## 8. Hands-on Exercise: Identify Your User Details

**Class practical – 10 minutes**

Ask students to execute all four commands and record their outputs.

| # | Command | What to observe |
|---:|---|---|
| 1 | `whoami` | Current username |
| 2 | `id` | UID, GID, and groups |
| 3 | `groups` | Group memberships |
| 4 | `who` | Logged-in users |

### Additional challenges

1. Execute `id root`. What UID does root have?
2. Execute `sudo whoami`. Why does the output change?
3. Compare the output of `id` and `groups`.
4. Create a file using `touch demo.txt`. Who owns this file?
5. Check whether your account belongs to an administrator group.

---

## 9. Independent Assignment: Linux User Investigation

**Level:** Beginner

**Objective:** Understand how Linux identifies users and manages group memberships.

Complete the following tasks independently:

1. Find your current username.
2. Identify your UID and GID.
3. List all groups associated with your account.
4. Find the UID of the root user.
5. Check the currently logged-in users.
6. Execute `sudo whoami` and explain the output.
7. Create a file named `user_info.txt`.
8. Check the owner and group of the created file.
9. Write a short explanation of root vs normal user.
10. Explain why Linux uses UID and GID instead of depending only on usernames.

### Submission requirements

- Terminal screenshots.
- Output of all four commands.
- Short written answers to the 10 tasks.
- Submit as one PDF or document.

---

## 10. Quick Revision Questions

1. What is a user in Linux?
2. What is the root user?
3. What is the UID of root?
4. What is the difference between root and a normal user?
5. What is UID?
6. What is GID?
7. Why do we use groups in Linux?
8. What is the difference between a primary group and supplementary groups?
9. What is the purpose of `whoami`?
10. What information does `id` display?
11. What is the difference between `id` and `groups`?
12. What is the purpose of the `who` command?
13. What does `sudo` do?
14. Why should we avoid using root for everyday tasks?

---

## 11. Key Takeaways

| Term / Command | Remember |
|---|---|
| UID | User ID – identifies a user |
| GID | Group ID – identifies a group |
| `root` | Superuser identity; UID is `0` |
| `sudo` | Runs a command with elevated privileges |
| `whoami` | Who am I? |
| `id` | What are my UID, GID, and groups? |
| `groups` | Which groups do I belong to? |
| `who` | Who is logged in? |

### The user identification flow

```text
             USER LOGS IN
                   |
                   v
            Linux identifies
                the user
                   |
             +-----+-----+
             |           |
             v           v
          Username      UID
                         |
                         v
                 Group membership
                         |
                    +----+----+
                    |         |
                    v         v
                Primary   Supplementary
                 group       groups
                    |         |
                    +----+----+
                         |
                         v
                Access is checked
                using permissions
```

### Teaching suggestion

Start this lecture by asking students:

> "If 50 students use the same Linux computer, how does Linux know which student created a file?"

Let them think about it first. Then introduce:

**Username → UID → Groups → GID**

This makes the entire lecture easier to understand.

---

## 12. Next Lecture

**Next logical lecture:** Linux User Management – Creating, Modifying, and Deleting Users.

Topics to be covered:

- `useradd`
- `usermod`
- `userdel`
- `passwd`

---

## Quick Command Practice Sheet

Run these commands in your terminal, one by one:

```bash
# Display the current effective username
whoami

# Display UID, GID, and group memberships
id

# Display group memberships
groups

# Display currently logged-in sessions
who

# Display root as the effective user for this command
sudo whoami

# Create a sample file and inspect its ownership
touch demo.txt
ls -l demo.txt
```

**Practice safely:** Do not experiment with deleting users or changing system files during this lecture. Use only the commands and sample files specified in the practical.
