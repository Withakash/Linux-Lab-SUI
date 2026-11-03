# Lec 12: Linux File Permissions

**Level:** Beginner  
**Total lecture time:** 40 minutes

## Learning Objectives

By the end of this lecture, students will be able to:

- Understand the output of the `ls -l` command.
- Identify the file type and permission string.
- Differentiate between **owner**, **group**, and **others**.
- Explain **read (`r`)**, **write (`w`)**, and **execute (`x`)** permissions.
- Inspect permissions on files and directories.
- Complete a practical permission-inspection exercise.

---

## 1. Introduction: Why Do We Need File Permissions?

Imagine a college computer lab where multiple students use the same computer.

- A student should be able to read their own assignment.
- A project team may need shared access to a common folder.
- Other students should not necessarily be allowed to modify someone else's files.
- The system administrator needs control over important system files.

Linux uses **file permissions** to control who can access a file or directory and what actions they can perform.

### Basic idea

```text
                 LINUX FILE
                     |
           Who can access it?
                     |
        +------------+------------+
        |            |            |
      Owner         Group        Others
        |            |            |
      r w x         r w x        r w x
```

Linux permissions are commonly represented using three permission categories:

1. **Owner** – the user who owns the file.
2. **Group** – users who belong to the file's associated group.
3. **Others** – everyone else.

---

## 2. Understanding `ls -l` Output

The `ls` command lists files and directories.

Use the `-l` option to display information in long format:

```bash
ls -l
```

Example output:

```text
-rw-r--r--  1 akash students  1200 Nov 3 10:30 notes.txt
drwxr-xr-x  2 akash students  4096 Nov 3 10:35 projects
-rwxr-xr-x  1 akash developers 2500 Nov 3 10:40 script.sh
```

Each line provides details about one file or directory.

### Structure of `ls -l`

```text
-rw-r--r--  1  akash  students  1200  Nov 3 10:30  notes.txt
|---------|  |    |       |       |        |            |
     |       |    |       |       |        |            |
 Permissions Links Owner  Group   Size   Date/Time     Name
```

### Meaning of each column

| Part | Meaning |
|---|---|
| `-rw-r--r--` | File type and permissions |
| `1` | Number of hard links |
| `akash` | File owner |
| `students` | Group associated with the file |
| `1200` | File size in bytes |
| `Nov 3 10:30` | Last modification date and time |
| `notes.txt` | File name |

For this lecture, the most important part is the **first column**: the file type and permission string.

---

## 3. Understanding the Permission String

Consider this permission string:

```text
-rw-r--r--
```

It contains 10 characters.

```text
Position:  1  2  3  4  5  6  7  8  9  10
           |  |-----|  |-----|  |-----|
           |   Owner    Group    Others
        File type
```

The positions are divided as follows:

| Positions | Meaning |
|---|---|
| 1 | File type |
| 2–4 | Owner permissions |
| 5–7 | Group permissions |
| 8–10 | Others permissions |

### Example breakdown

```text
-rw-r--r--
 |
 +-- File type: - (regular file)

    rw-  -> Owner
    r--  -> Group
    r--  -> Others
```

Interpretation:

- Owner can read and write.
- Group can only read.
- Others can only read.
- Nobody has execute permission.

### Common file-type characters

| Character | Meaning |
|---|---|
| `-` | Regular file |
| `d` | Directory |
| `l` | Symbolic link |
| `c` | Character device |
| `b` | Block device |
| `p` | Named pipe (FIFO) |
| `s` | Socket |

For beginner-level permission inspection, focus mainly on `-` and `d`.

### Important examples

**Example 1: Regular file**

```text
-rw-r--r-- 1 akash students 1200 Nov 3 notes.txt
```

- `-` means regular file.
- `rw-` means owner can read and write.
- `r--` means group can read.
- `r--` means others can read.

**Example 2: Directory**

```text
drwxr-xr-x 2 akash students 4096 Nov 3 projects
```

- `d` means directory.
- `rwx` means owner has read, write, and execute permissions.
- `r-x` means group has read and execute permissions.
- `r-x` means others have read and execute permissions.

---

## 4. Understanding Read, Write, and Execute (`rwx`)

Linux uses three basic permission types:

- `r` – Read
- `w` – Write
- `x` – Execute

### 4.1 Read (`r`)

Read permission allows a user to view the contents of a file.

Example:

```bash
cat notes.txt
```

If the user has read permission, they can normally view the file contents.

For a directory, read permission allows the user to list the names of entries inside it, subject to the relevant directory access requirements.

### 4.2 Write (`w`)

Write permission allows a user to modify a file.

Example:

```bash
nano notes.txt
```

A user with write permission can modify the file contents.

For a directory, write permission allows creating, deleting, or renaming entries inside it, generally together with execute permission.

### 4.3 Execute (`x`)

Execute permission allows a user to run an executable file or script.

Example:

```bash
./script.sh
```

For a directory, execute permission allows a user to enter or traverse the directory and access items inside it when the other required permissions are present.

### Permission summary

| Permission | Symbol | For a file | For a directory |
|---|---|---|---|
| Read | `r` | View file contents | List directory entries |
| Write | `w` | Modify file contents | Create, delete, or rename entries (normally with `x`) |
| Execute | `x` | Run a program or script | Enter/traverse the directory |

> **Important:** The meaning of permissions differs between regular files and directories. In particular, directory `x` means traversal/search permission; it does not mean "run the directory."

---

## 5. How to Read Permission Combinations

Each category (owner, group, and others) can have a combination of `r`, `w`, and `x`.

| Permission string | Meaning |
|---|---|
| `rwx` | Read, write, and execute |
| `rw-` | Read and write |
| `r-x` | Read and execute |
| `r--` | Read only |
| `-wx` | Write and execute |
| `-w-` | Write only |
| `--x` | Execute only |
| `---` | No permissions |

### Example 1

```text
-rw-r--r--
```

| Category | Permission | Explanation |
|---|---|---|
| Owner | `rw-` | Read and write |
| Group | `r--` | Read only |
| Others | `r--` | Read only |

### Example 2

```text
-rwxr-x---
```

| Category | Permission | Explanation |
|---|---|---|
| Owner | `rwx` | Read, write, and execute |
| Group | `r-x` | Read and execute |
| Others | `---` | No permissions |

### Example 3

```text
drwxr-xr-x
```

| Category | Permission | Explanation |
|---|---|---|
| Owner | `rwx` | List, create/remove entries, and traverse (subject to directory rules) |
| Group | `r-x` | List and traverse |
| Others | `r-x` | List and traverse |

---

## 6. Permission Inspection Commands

### Command 1: List files with detailed information

```bash
ls -l
```

Displays files in the current directory with permissions, owner, group, size, and modification time.

### Command 2: Inspect one specific file

```bash
ls -l notes.txt
```

Displays detailed information for `notes.txt`.

### Command 3: Inspect directories too

```bash
ls -ld projects
```

Displays information about the directory itself rather than listing its contents.

### Command 4: Show hidden files with details

```bash
ls -la
```

- `-l` displays long-format details.
- `-a` includes hidden entries (names beginning with a dot).

### Command 5: Create sample files

```bash
touch file1.txt
touch file2.txt
mkdir practice_dir
```

Inspect them:

```bash
ls -l file1.txt file2.txt
ls -ld practice_dir
```

The exact permission values may differ depending on the system's default settings and `umask`.

---

## 7. Hands-on Lab: Permission Inspection Exercise

**Duration:** 18 minutes

### Objective

Inspect the permissions of at least three files and explain what the owner, group, and others can do.

### Step 1: Create a practice directory

```bash
mkdir permission_lab
cd permission_lab
```

### Step 2: Create three files and one directory

```bash
touch public.txt
touch private.txt
touch script.sh
mkdir shared_folder
```

### Step 3: Inspect permissions

```bash
ls -l
```

For the directory itself:

```bash
ls -ld shared_folder
```

### Step 4: Record the output

Students should select three different files from their output and complete this table.

| File name | Permission string | Owner permissions | Group permissions | Others permissions |
|---|---|---|---|---|
| File 1 |  |  |  |  |
| File 2 |  |  |  |  |
| File 3 |  |  |  |  |

### Step 5: Answer the inspection questions

1. Which file has the most permissions for its owner?
2. Can others read `public.txt`?
3. Does `script.sh` have execute permission?
4. Which file has the most restricted permissions?
5. What is the difference between a file and a directory permission string?
6. What does the first character of the permission string represent?

> **Note:** `touch` does not automatically make a file executable. The actual permission string depends on the system's default creation permissions and `umask`. Students must interpret their own terminal output rather than assume every system will show identical values.

---

## 8. Understanding the Permission Decision

Linux checks permissions based on the relationship between the current user and the file:

1. Is the user the file owner?
2. If not, is the user a member of the file's group?
3. If neither applies, the others permissions are considered.

Conceptual flow:

```text
                 USER ACCESSES FILE
                         |
                         v
                Is the user the owner?
                    /          \
                  Yes           No
                  |              |
                  v              v
            Check Owner     Is user in file's
            Permissions       group?
                              /     \
                            Yes      No
                            |         |
                            v         v
                       Check Group  Check Others
                       Permissions  Permissions
                            \         /
                             \       /
                              v     v
                         Access decision
```

This is a simplified model of ordinary Unix permission checks. Special permissions, ACLs, capabilities, and other security rules can also affect access.

---

## 9. Common Mistakes to Avoid

1. **Confusing owner with group:** The owner is a user account; the group is a collection of users.
2. **Ignoring the first character:** `-` and `d` identify different file types.
3. **Assuming `x` means the same thing everywhere:** For files it allows execution; for directories it allows traversal/search.
4. **Assuming all files have the same permissions:** Permissions can differ from file to file.
5. **Assuming `ls -l` changes permissions:** It only displays information; it does not modify permissions.
6. **Assuming `touch` creates an executable file:** It normally creates a regular file without execute bits.

---

## 10. Quick Revision Questions

1. What is the purpose of file permissions in Linux?
2. What does the `ls -l` command display?
3. What is the meaning of the first character in `-rw-r--r--`?
4. How many characters are present in a standard permission string?
5. Which positions represent owner permissions?
6. Which positions represent group permissions?
7. Which positions represent others permissions?
8. What does `r` represent?
9. What does `w` represent?
10. What does `x` represent for a regular file?
11. What does `x` represent for a directory?
12. What is the difference between owner and group?
13. What is the difference between `ls -l` and `ls -ld`?
14. What does `drwxr-xr-x` indicate?
15. Does `ls -l` modify file permissions?

---

## 11. Key Takeaways

| Concept | Remember |
|---|---|
| `ls -l` | Displays detailed file information |
| First character | Identifies file type |
| `-` | Regular file |
| `d` | Directory |
| Owner | User who owns the file |
| Group | Group associated with the file |
| Others | Everyone outside the owner and group categories |
| `r` | Read |
| `w` | Write |
| `x` | Execute for files; traverse/search for directories |
| Permission positions | 1 = type, 2–4 = owner, 5–7 = group, 8–10 = others |

### One-line revision

```text
-rwxr-xr--
 |  |  |  |
 |  |  |  +-- Others: read
 |  |  +----- Group: read and execute
 |  +-------- Owner: read, write, and execute
 +----------- Regular file
```

---

## 12. Assignment / Practical

**Assignment: Inspect Permissions of Three Files**

Run:

```bash
ls -l
```

Select three files and explain each permission set.

For every file, record:

- File name
- Complete permission string
- File type
- Owner
- Group
- Owner permissions
- Group permissions
- Others permissions

### Submission

- Terminal screenshot showing `ls -l` output.
- Completed permission-analysis table.
- Short answers to the revision questions.

**Expected learning outcome:** Students should be able to read a permission string such as `-rw-r--r--` and explain exactly what the owner, group, and others are allowed to do.

---

## Next Logical Lecture

**Changing File Permissions – `chmod`**

Suggested topics:

- Why permissions need to be changed
- Symbolic permission notation (`u`, `g`, `o`, `a`)
- Numeric/octal permission notation (`4`, `2`, `1`)
- Using `chmod` with practical examples
