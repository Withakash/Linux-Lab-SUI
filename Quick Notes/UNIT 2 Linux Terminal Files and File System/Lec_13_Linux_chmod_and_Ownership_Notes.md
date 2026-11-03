# Lec 13: `chmod` & Ownership in Linux

**Level:** Beginner  
**Total lecture time:** 40 minutes  
**Environment:** Ubuntu/Linux and macOS Terminal

## Learning Objectives

By the end of this lecture, students will be able to:

- Change file permissions using `chmod`.
- Use **symbolic mode** (`u`, `g`, `o`, `a`).
- Use **numeric/octal mode** (`4`, `2`, `1`).
- Calculate permissions using the `4-2-1` method.
- Change file ownership using `chown`.
- Change group ownership using `chgrp`.
- Practise permission and ownership changes on Ubuntu and macOS.
- Verify changes using `ls -l` and `id`.

---

## 1. Recap: Linux Permissions

In the previous lecture, we learned that Linux permissions control what users can do with files and directories.

A permission string has 10 characters:

```text
-rwxr-xr--
 |  |  |  |
 |  |  |  +-- Others: read
 |  |  +----- Group: read and execute
 |  +-------- Owner: read, write, and execute
 +----------- File type: regular file
```

The three permission categories are:

| Category | Symbol | Meaning |
|---|---|---|
| Owner / User | `u` | The user who owns the file |
| Group | `g` | Users in the file's group |
| Others | `o` | Everyone else |
| All | `a` | Owner, group, and others |

The three basic permissions are:

| Permission | Symbol | Meaning |
|---|---|---|
| Read | `r` | View file contents |
| Write | `w` | Modify file contents |
| Execute | `x` | Run an executable file |

---

## 2. What is `chmod`?

`chmod` stands for **change mode**.

It is used to change the permissions of a file or directory.

### Syntax

```bash
chmod [options] permissions filename
```

Example:

```bash
chmod u+x script.sh
```

This adds execute permission for the file owner.

### Permission change flow

```text
             chmod command
                   |
                   v
           Select permission
                   |
          +--------+--------+
          |                 |
          v                 v
      Symbolic           Numeric
        Mode               Mode
          |                 |
          v                 v
     u+x, g-w,          755, 644,
     o=r, a+r           700, 600
          |                 |
          +--------+--------+
                   |
                   v
          File permissions change
                   |
                   v
              Verify with
                ls -l
```

There are two common ways to use `chmod`:

1. **Symbolic mode**
2. **Numeric mode (octal mode)**

---

## 3. Symbolic Mode

Symbolic mode changes permissions using letters and operators.

### 3.1 Permission categories

| Symbol | Category |
|---|---|
| `u` | Owner (user) |
| `g` | Group |
| `o` | Others |
| `a` | All |

### 3.2 Operators

| Operator | Meaning |
|---|---|
| `+` | Add permission |
| `-` | Remove permission |
| `=` | Set permissions exactly |

### 3.3 Examples

**Example 1: Add execute permission to owner**

```bash
chmod u+x script.sh
```

**Example 2: Remove write permission from group**

```bash
chmod g-w notes.txt
```

**Example 3: Add read permission to everyone**

```bash
chmod a+r notes.txt
```

**Example 4: Set owner permissions to read and write only**

```bash
chmod u=rw notes.txt
```

**Example 5: Remove all permissions from others**

```bash
chmod o-rwx private.txt
```

**Example 6: Set exact permissions for all categories**

```bash
chmod u=rwx,g=rx,o=r script.sh
```

This sets:

- Owner: read, write, execute.
- Group: read and execute.
- Others: read only.

### Symbolic mode quick reference

| Command | Result |
|---|---|
| `chmod u+x file` | Add execute to owner |
| `chmod g-w file` | Remove write from group |
| `chmod o-r file` | Remove read from others |
| `chmod a+r file` | Add read to everyone |
| `chmod u=rw file` | Set owner to read and write |
| `chmod o= file` | Remove all permissions from others |

---

## 4. Numeric Mode – The 4-2-1 Method

Numeric mode uses numbers to represent permissions.

Remember:

| Permission | Number |
|---|---:|
| Read (`r`) | 4 |
| Write (`w`) | 2 |
| Execute (`x`) | 1 |
| No permission (`-`) | 0 |

Add the numbers to create a permission value.

### 4.1 Understanding 4-2-1

```text
          PERMISSION VALUES

        Read     Write    Execute
         r         w         x
         4         2         1
         |         |         |
         +---------+---------+
                   |
             Add the values
                   |
                   v

 r-- = 4
 -w- = 2
 --x = 1
 rw- = 4 + 2 = 6
 r-x = 4 + 1 = 5
 -wx = 2 + 1 = 3
 rwx = 4 + 2 + 1 = 7
 --- = 0
```

### 4.2 Permission values

| Permission | Calculation | Numeric value |
|---|---:|---:|
| `---` | 0 | 0 |
| `--x` | 1 | 1 |
| `-w-` | 2 | 2 |
| `-wx` | 2 + 1 | 3 |
| `r--` | 4 | 4 |
| `r-x` | 4 + 1 | 5 |
| `rw-` | 4 + 2 | 6 |
| `rwx` | 4 + 2 + 1 | 7 |

### 4.3 Three-digit permission format

A numeric permission normally has three digits:

```text
             chmod 755 file
                  |
          +-------+-------+
          |       |       |
          v       v       v
        Owner   Group   Others
          7       5       5
         rwx     r-x     r-x
```

The first digit represents the owner, the second the group, and the third others.

### 4.4 Common numeric permissions

| Numeric | Symbolic | Meaning |
|---:|---|---|
| `777` | `rwxrwxrwx` | Everyone has all permissions |
| `755` | `rwxr-xr-x` | Owner all; group and others read/execute |
| `750` | `rwxr-x---` | Owner all; group read/execute; others none |
| `700` | `rwx------` | Only owner has permissions |
| `644` | `rw-r--r--` | Owner read/write; group and others read |
| `640` | `rw-r-----` | Owner read/write; group read; others none |
| `600` | `rw-------` | Only owner can read/write |

> **Security note:** Avoid using `chmod 777` as a routine fix. It grants read, write, and execute permissions to everyone and can expose files to unwanted modification or execution.

### 4.5 Practical numeric examples

Give the owner full permissions and group/others read and execute:

```bash
chmod 755 script.sh
```

Give the owner read/write and everyone else read-only:

```bash
chmod 644 notes.txt
```

Allow only the owner to read and write:

```bash
chmod 600 private.txt
```

Verify:

```bash
ls -l
```

---

## 5. Symbolic Mode vs Numeric Mode

| Feature | Symbolic Mode | Numeric Mode |
|---|---|---|
| Uses | Letters and operators | Numbers |
| Example | `chmod u+x file` | `chmod 755 file` |
| Best for | Changing selected permissions | Setting a complete permission set |
| Readability | Descriptive | Compact |

Both methods change the same permission bits. Choose the method that makes the intended change clearest.

---

## 6. What is File Ownership?

Every file and directory has an owner and an associated group.

Example:

```text
-rw-r--r-- 1 akash students 1200 Nov 3 notes.txt
             |       |
             |       +-- Group owner
             +---------- User owner
```

- **Owner:** The user account that owns the file.
- **Group:** The group associated with the file.

Linux uses ownership and permissions together when deciding access.

### Ownership structure

```text
                 FILE: notes.txt
                       |
               +-------+-------+
               |               |
             Owner            Group
             akash            students
               |               |
               +-------+-------+
                       |
                 Permission check
                       |
                Owner / Group /
                    Others
```

---

## 7. `chown` – Change Owner

`chown` stands for **change owner**.

It changes the owner of a file or directory. It can also change the group at the same time.

### Syntax

```bash
sudo chown new_owner filename
```

### Example

```bash
sudo chown rahul notes.txt
```

This changes the owner of `notes.txt` to `rahul`.

Verify:

```bash
ls -l notes.txt
```

### Change owner and group together

```bash
sudo chown rahul:developers notes.txt
```

This changes:

- Owner to `rahul`.
- Group to `developers`.

### Change ownership of a directory and its contents

```bash
sudo chown -R rahul:developers project/
```

`-R` means recursive: apply the ownership change to the directory and its contents.

**Caution:** Recursive ownership changes can affect many files. Practise only on a test directory you created.

---

## 8. `chgrp` – Change Group

`chgrp` stands for **change group**.

It changes the group ownership of a file or directory without changing its user owner.

### Syntax

```bash
sudo chgrp new_group filename
```

### Example

```bash
sudo chgrp developers notes.txt
```

This changes the group of `notes.txt` to `developers`.

Verify:

```bash
ls -l notes.txt
```

### Change group recursively

```bash
sudo chgrp -R developers project/
```

This changes the group ownership of the directory and its contents.

### `chown` vs `chgrp`

| Command | Purpose | Example |
|---|---|---|
| `chown` | Change user owner; can also change group | `sudo chown rahul notes.txt` |
| `chgrp` | Change group owner | `sudo chgrp developers notes.txt` |

> **Important:** Changing ownership generally requires administrator privileges or specific ownership-related privileges. Use `sudo` where appropriate. A normal user cannot arbitrarily assign files to another user.

---

## 9. Live Practical – Ubuntu/Linux

**Goal:** Create a script, inspect its initial permissions, make it executable using symbolic and numeric modes, then practise changing owner and group.

### Step 1: Create a safe practice folder

```bash
mkdir -p ~/linux_permission_lab
cd ~/linux_permission_lab
```

All changes in this practical are limited to this folder.

### Step 2: Create a script

```bash
touch demo.sh
```

Add content:

```bash
cat > demo.sh <<'EOF'
#!/bin/bash
echo "Hello from Linux permissions lab!"
EOF
```

### Step 3: Inspect its permissions

```bash
ls -l demo.sh
```

The file will normally not have execute permission when created with `cat` or `touch`, but the exact initial permissions depend on the system's `umask`.

Example:

```text
-rw-r--r-- 1 akash akash 54 Nov 3 demo.sh
```

### Step 4: Try to execute it before adding execute permission

```bash
./demo.sh
```

If the file lacks execute permission, the shell should report a permission error.

### Step 5: Add execute permission using symbolic mode

```bash
chmod u+x demo.sh
```

Check:

```bash
ls -l demo.sh
```

The owner permission section should now include `x`.

Run:

```bash
./demo.sh
```

Expected output:

```text
Hello from Linux permissions lab!
```

### Step 6: Remove execute permission again

```bash
chmod u-x demo.sh
```

Verify:

```bash
ls -l demo.sh
```

### Step 7: Add execute permission using numeric mode

Set the permissions to `755`:

```bash
chmod 755 demo.sh
```

Verify:

```bash
ls -l demo.sh
```

Expected permission string:

```text
-rwxr-xr-x
```

Run the script:

```bash
./demo.sh
```

### Step 8: Practise a few more numeric permissions

```bash
chmod 644 demo.sh
ls -l demo.sh

chmod 600 demo.sh
ls -l demo.sh

chmod 755 demo.sh
ls -l demo.sh
```

Observe how the permission string changes.

### Step 9: Inspect the current user and groups

```bash
whoami
id
groups
```

This helps identify the current account and the groups available for the ownership exercise.

### Step 10: Practise changing ownership (administrator access required)

First inspect the current owner:

```bash
ls -l demo.sh
```

To change the owner to an existing account, use:

```bash
sudo chown EXISTING_USERNAME demo.sh
```

Replace `EXISTING_USERNAME` with an actual account on your machine.

To change both owner and group:

```bash
sudo chown EXISTING_USERNAME:EXISTING_GROUP demo.sh
```

To change only the group:

```bash
sudo chgrp EXISTING_GROUP demo.sh
```

Verify after each change:

```bash
ls -l demo.sh
```

**Important:** Do not copy the placeholder names literally. The user and group must already exist. If you are using a shared classroom computer, do not change ownership of files outside your practice folder.

---

## 10. Live Practical – macOS Terminal

The `chmod`, `chown`, and `chgrp` commands are available on macOS too. The basic syntax is the same, but default users, groups, and administrator-group names can differ from Ubuntu.

### Step 1: Create a practice folder

```bash
mkdir -p ~/mac_permission_lab
cd ~/mac_permission_lab
```

### Step 2: Create a script

```bash
cat > demo.sh <<'EOF'
#!/bin/bash
echo "Hello from macOS permissions lab!"
EOF
```

### Step 3: Inspect initial permissions

```bash
ls -l demo.sh
```

Example output may look like:

```text
-rw-r--r--  1 akash  staff  52 Nov 3 10:30 demo.sh
```

The username and group will depend on the Mac account.

### Step 4: Try running the script before adding execute permission

```bash
./demo.sh
```

If execute permission is absent, macOS should deny direct execution.

### Step 5: Add execute permission using symbolic mode

```bash
chmod u+x demo.sh
ls -l demo.sh
```

Run it:

```bash
./demo.sh
```

Expected output:

```text
Hello from macOS permissions lab!
```

### Step 6: Remove execute permission

```bash
chmod u-x demo.sh
ls -l demo.sh
```

### Step 7: Add execute permission using numeric mode

```bash
chmod 755 demo.sh
ls -l demo.sh
```

Expected permission string:

```text
-rwxr-xr-x
```

Run:

```bash
./demo.sh
```

### Step 8: Practise other numeric modes

```bash
chmod 644 demo.sh
ls -l demo.sh

chmod 600 demo.sh
ls -l demo.sh

chmod 755 demo.sh
ls -l demo.sh
```

### Step 9: Check your macOS user and groups

```bash
whoami
id
groups
```

A typical Mac account may have a primary group such as `staff`, but always use the actual output from your machine.

### Step 10: Change group ownership on macOS

To change the group, use a group that exists on the Mac:

```bash
sudo chgrp EXISTING_GROUP demo.sh
```

For example, if `staff` is a group shown by your system:

```bash
sudo chgrp staff demo.sh
```

Verify:

```bash
ls -l demo.sh
```

### Step 11: Change owner on macOS

Changing a file's owner normally requires administrator privileges:

```bash
sudo chown EXISTING_USERNAME demo.sh
```

Replace the placeholder with an existing local account.

To change owner and group together:

```bash
sudo chown EXISTING_USERNAME:EXISTING_GROUP demo.sh
```

Verify:

```bash
ls -l demo.sh
```

**macOS safety note:** Use `sudo` only for the ownership demonstration. Do not change ownership of macOS system files or folders. If you only have one local account, demonstrate `chgrp` and explain `chown` rather than creating or modifying accounts just for this exercise.

### Ubuntu vs macOS quick comparison

| Task | Ubuntu | macOS |
|---|---|---|
| Add owner execute permission | `chmod u+x file` | `chmod u+x file` |
| Set numeric permissions | `chmod 755 file` | `chmod 755 file` |
| Change owner | `sudo chown user file` | `sudo chown user file` |
| Change group | `sudo chgrp group file` | `sudo chgrp group file` |
| Inspect permissions | `ls -l file` | `ls -l file` |
| Check current user | `whoami` | `whoami` |

---

## 11. Hands-on Lab: Permission Modification Challenge

**Duration:** 15 minutes

### Objective

Students must create a script, modify its permissions using both symbolic and numeric modes, and inspect ownership.

### Task A: Create a script

```bash
mkdir -p ~/permission_challenge
cd ~/permission_challenge

cat > runme.sh <<'EOF'
#!/bin/bash
echo "Permission challenge completed!"
EOF
```

### Task B: Inspect initial permissions

```bash
ls -l runme.sh
```

Record the permission string.

### Task C: Symbolic mode challenge

1. Add execute permission to the owner.
2. Add read permission to the group.
3. Remove write permission from others.

Commands:

```bash
chmod u+x runme.sh
chmod g+r runme.sh
chmod o-w runme.sh
```

Verify:

```bash
ls -l runme.sh
```

### Task D: Numeric mode challenge

Set these permission values one by one and observe the output:

```bash
chmod 755 runme.sh
ls -l runme.sh

chmod 644 runme.sh
ls -l runme.sh

chmod 700 runme.sh
ls -l runme.sh
```

### Task E: Ownership inspection

```bash
whoami
id
ls -l runme.sh
```

If an appropriate existing test user or group is available, demonstrate:

```bash
sudo chown EXISTING_USERNAME runme.sh
sudo chgrp EXISTING_GROUP runme.sh
```

Verify:

```bash
ls -l runme.sh
```

### Student observation table

| # | Command | What should be observed |
|---:|---|---|
| 1 | `chmod u+x runme.sh` | Owner receives execute permission |
| 2 | `chmod g+r runme.sh` | Group receives read permission |
| 3 | `chmod o-w runme.sh` | Others lose write permission |
| 4 | `chmod 755 runme.sh` | `rwxr-xr-x` |
| 5 | `chmod 644 runme.sh` | `rw-r--r--` |
| 6 | `chmod 700 runme.sh` | `rwx------` |
| 7 | `sudo chown USER runme.sh` | Owner changes, if authorized |
| 8 | `sudo chgrp GROUP runme.sh` | Group changes, if authorized |

Replace `USER` and `GROUP` with existing account and group names.

---

## 12. Common Errors and Troubleshooting

### Error 1: Permission denied

Possible reason: You do not have the required permission to execute or access the file.

Inspect:

```bash
ls -l demo.sh
```

For a script that should be directly executable:

```bash
chmod u+x demo.sh
```

### Error 2: Operation not permitted

Possible reasons:

- The current account does not have the required privileges.
- The file has ownership or filesystem restrictions.
- macOS privacy or security controls may affect some locations.

For a file you own, inspect:

```bash
whoami
ls -l demo.sh
```

Use `sudo` only when administrator privileges are appropriate.

### Error 3: Invalid user or group

The account or group name does not exist.

Check:

```bash
id USERNAME
```

For a group, inspect the groups available to your account:

```bash
groups
```

On macOS, you can also inspect a specific group with:

```bash
dscl . -read /Groups/GROUPNAME
```

Replace `GROUPNAME` with the actual group name.

### Error 4: Script still does not run

Check:

```bash
ls -l demo.sh
head -n 1 demo.sh
```

The first line should point to a valid interpreter, such as:

```bash
#!/bin/bash
```

Also check that you are in the correct directory and using:

```bash
./demo.sh
```

---

## 13. Important Safety Rules

1. Do not use `chmod 777` as a general solution to permission errors.
2. Do not run recursive `chown -R` or `chgrp -R` on system directories.
3. Practise only inside your own lab directory.
4. Do not change ownership of operating-system files.
5. Verify every change using `ls -l`.
6. Use `sudo` only when required and only for commands you understand.

---

## 14. Quick Revision Questions

1. What is the purpose of `chmod`?
2. What is the difference between symbolic and numeric modes?
3. What do `u`, `g`, `o`, and `a` represent?
4. What is the meaning of `+`, `-`, and `=` in symbolic mode?
5. What are the numeric values of read, write, and execute?
6. How is `rwx` represented numerically?
7. What does `chmod 755 file` do?
8. What does `chmod 644 file` do?
9. What is the purpose of `chown`?
10. What is the purpose of `chgrp`?
11. What is the difference between `chown` and `chgrp`?
12. What does the `-R` option do?
13. Why should `chmod 777` be avoided?
14. How can you verify a permission change?
15. Are `chmod`, `chown`, and `chgrp` available on macOS?

---

## 15. Key Takeaways

| Command / Concept | Remember |
|---|---|
| `chmod` | Changes file or directory permissions |
| `u` | Owner |
| `g` | Group |
| `o` | Others |
| `a` | All categories |
| `+` | Add permission |
| `-` | Remove permission |
| `=` | Set permission exactly |
| `r = 4` | Read |
| `w = 2` | Write |
| `x = 1` | Execute |
| `chown` | Changes owner; can also change group |
| `chgrp` | Changes group |
| `ls -l` | Verifies permissions and ownership |

### Final revision diagram

```text
                 FILE PERMISSIONS
                        |
             +----------+----------+
             |                     |
          chmod                 Ownership
             |                     |
       +-----+-----+          +----+----+
       |           |          |         |
   Symbolic     Numeric     chown     chgrp
       |           |          |         |
   u+x, g-w      755, 644   Change    Change
   o-rwx         700, 600   owner     group
       |           |          |         |
       +-----------+----------+---------+
                        |
                        v
                  Verify with
                    ls -l
```

---

## 16. Assignment / Practical

**Assignment: Permission and Ownership Investigation**

Complete the following tasks:

1. Create a file named `assignment.sh`.
2. Add a simple shell script to it.
3. Display its initial permissions using `ls -l`.
4. Remove execute permission from the owner.
5. Add execute permission using symbolic mode.
6. Set permissions to `755` using numeric mode.
7. Set permissions to `644` and explain the difference.
8. Check your current username and groups using `whoami` and `id`.
9. Change the group of a test file using `chgrp`, if an appropriate group is available.
10. Demonstrate `chown` using an existing test account, if available.

### Submission requirements

- Terminal screenshots for each major step.
- Before-and-after permission strings.
- Explanation of symbolic and numeric modes.
- Output of `whoami`, `id`, and `ls -l`.
- A short explanation of `chown` vs `chgrp`.

**Expected learning outcome:** Students should be able to change file permissions confidently using both symbolic and numeric modes and understand how file ownership is managed.

---

## Next Logical Lecture

**Linux Process Management**

Suggested topics:

- What is a process?
- Foreground vs background processes
- `ps`
- `top`
- `jobs`
- `bg` and `fg`
- `kill` and process IDs (PID)
