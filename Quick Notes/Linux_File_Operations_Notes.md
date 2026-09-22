# Linux File Operations — Student Notes

> **Goal:** Learn how to create, view, edit, copy, move, rename, delete, search, compare, and manage files and directories from the Linux terminal.

---

## 1. File Operation Workflow

A common Linux file-management workflow is:

```text
Create → Write/Edit → View → Copy/Move → Search → Permissions → Archive/Delete
```

The most important commands are:

| Category | Commands | Purpose |
|---|---|---|
| Create | `touch`, `mkdir` | Create files/directories |
| Edit | `nano`, `vim` | Edit file contents |
| View | `cat`, `less`, `more` | Read files |
| Partial View | `head`, `tail` | Read beginning/end |
| Write | `echo`, `printf` | Write text |
| Copy | `cp` | Copy files/directories |
| Move/Rename | `mv` | Move or rename |
| Delete | `rm`, `rmdir` | Delete files/directories |
| Information | `file`, `stat`, `ls -l` | Inspect files |
| Search | `find`, `grep` | Find files/text |
| Compare | `diff`, `cmp` | Compare files |
| Redirection | `>`, `>>`, `<` | Work with file input/output |
| Permissions | `chmod`, `chown`, `chgrp` | Manage access |
| Links | `ln` | Create links |
| Archive | `tar` | Archive files |
| Compression | `gzip`, `zip`, `unzip` | Compress/extract |

---

# 2. Creating Files — `touch`

`touch` creates an empty file.

### Basic syntax

```bash
touch filename
```

### Example

```bash
touch notes.txt
```

Check the file:

```bash
ls
```

### Create multiple files

```bash
touch file1.txt file2.txt file3.txt
```

### Important point

If the file already exists, `touch` does not erase its contents. It updates the file's timestamps.

---

# 3. Creating Directories — `mkdir`

`mkdir` means **make directory**.

### Basic syntax

```bash
mkdir directory_name
```

### Example

```bash
mkdir documents
```

### Create multiple directories

```bash
mkdir java python linux
```

### Create nested directories

```bash
mkdir -p college/semester3/java
```

The `-p` option creates parent directories if they do not already exist.

---

# 4. Editing Files — `nano`

`nano` is a beginner-friendly terminal text editor.

```bash
nano notes.txt
```

If `notes.txt` does not exist, Nano will create it when you save.

## Important Nano shortcuts

| Shortcut | Purpose |
|---|---|
| `Ctrl + O` | Save |
| `Ctrl + X` | Exit |
| `Ctrl + K` | Cut current line |
| `Ctrl + U` | Paste |
| `Ctrl + W` | Search |

### Practice

```bash
nano student.txt
```

Write:

```text
Name: Akash
Course: Linux
Semester: 3
```

Save and exit.

---

# 5. Viewing File Contents — `cat`

`cat` displays the contents of a file.

```bash
cat notes.txt
```

### Display multiple files

```bash
cat file1.txt file2.txt
```

### Combine files

```bash
cat file1.txt file2.txt > combined.txt
```

This creates `combined.txt` containing the contents of both files.

---

# 6. Creating/Writing a File Using `cat`

You can use `cat` with redirection to create a file.

```bash
cat > notes.txt
```

Type:

```text
Hello Linux
This is my first file.
```

Press:

```text
Ctrl + D
```

to finish the input.

## Append using `cat`

```bash
cat >> notes.txt
```

Add more text and press `Ctrl + D`.

### Difference

```bash
cat > notes.txt
```

Overwrites/replaces the file content.

```bash
cat >> notes.txt
```

Appends to existing content.

---

# 7. Viewing Large Files — `less`

`less` is useful for reading large files one screen at a time.

```bash
less notes.txt
```

Useful keys:

| Key | Purpose |
|---|---|
| `↑` / `↓` | Move |
| `Space` | Next page |
| `b` | Previous page |
| `/word` | Search |
| `q` | Quit |

Example:

```bash
less /var/log/syslog
```

---

# 8. Viewing Files — `more`

`more` also displays files page by page.

```bash
more notes.txt
```

For beginners:

```text
cat   → Small/simple files
less  → Large files
more  → Page-by-page viewing
```

---

# 9. View Beginning of File — `head`

`head` displays the beginning of a file.

```bash
head notes.txt
```

By default, it displays the first 10 lines.

### Display first 5 lines

```bash
head -n 5 notes.txt
```

### Display first 20 lines

```bash
head -n 20 notes.txt
```

---

# 10. View End of File — `tail`

`tail` displays the end of a file.

```bash
tail notes.txt
```

By default, it displays the last 10 lines.

### Display last 5 lines

```bash
tail -n 5 notes.txt
```

### Follow a file

```bash
tail -f application.log
```

`-f` continuously monitors the file for new content.

This is especially useful for log files.

Press:

```text
Ctrl + C
```

to stop following the file.

---

# 11. Writing Text — `echo`

`echo` prints text to the terminal.

```bash
echo "Hello Linux"
```

### Write into a file

```bash
echo "Hello Linux" > notes.txt
```

### Append to a file

```bash
echo "Second line" >> notes.txt
```

---

# 12. Writing Formatted Text — `printf`

`printf` provides more control over formatting.

```bash
printf "Hello Linux\n"
```

Example:

```bash
printf "Name: Akash\nCourse: Linux\nSemester: 3\n"
```

Write to a file:

```bash
printf "Name: Akash\nCourse: Linux\n" > student.txt
```

---

# 13. Redirection Operators

Redirection sends input/output between commands and files.

## `>` — Overwrite

```bash
echo "Hello" > file.txt
```

If `file.txt` already contains data, the old content is replaced.

## `>>` — Append

```bash
echo "New line" >> file.txt
```

The existing content is preserved.

## `<` — Input from a file

```bash
sort < names.txt
```

Think of it as:

```text
>   command → file
>>  command → file (append)
<   file → command
```

---

# 14. Copy Files — `cp`

`cp` means **copy**.

### Copy a file

```bash
cp notes.txt backup.txt
```

### Copy a file into a directory

```bash
cp notes.txt documents/
```

### Copy multiple files

```bash
cp file1.txt file2.txt documents/
```

### Copy a directory

```bash
cp -r project backup/
```

`-r` means **recursive**.

It is required when copying directories and their contents.

---

# 15. Move Files — `mv`

`mv` is used to move files/directories.

```bash
mv notes.txt documents/
```

The file is moved from the current directory into `documents`.

---

# 16. Rename Files Using `mv`

Linux commonly uses `mv` for renaming.

```bash
mv oldname.txt newname.txt
```

Example:

```bash
mv assignment1.txt assignment01.txt
```

No separate normal `rename` command is required for this operation.

---

# 17. Move and Rename at the Same Time

```bash
mv notes.txt documents/linux-notes.txt
```

This:

1. Moves `notes.txt` into `documents`
2. Renames it to `linux-notes.txt`

---

# 18. Delete Files — `rm`

`rm` means **remove**.

```bash
rm notes.txt
```

### Delete multiple files

```bash
rm file1.txt file2.txt
```

### Ask before deleting

```bash
rm -i notes.txt
```

The terminal asks for confirmation.

### Force delete

```bash
rm -f notes.txt
```

`-f` means force.

---

# 19. Delete Directories

## `rmdir`

`rmdir` removes an **empty** directory.

```bash
rmdir test
```

If the directory contains files, `rmdir` will not remove it.

## `rm -r`

Remove a directory and its contents:

```bash
rm -r project/
```

### Force + recursive

```bash
rm -rf project/
```

> ⚠️ **Warning:** Be extremely careful with `rm -rf`. Deleted files normally do not go to a recycle bin.

---

# 20. File Information — `file`

`file` tells you what type of file Linux detects.

```bash
file notes.txt
```

Example output:

```text
notes.txt: ASCII text
```

Try:

```bash
file image.jpg
file program
file document.pdf
```

---

# 21. File Metadata — `stat`

`stat` displays detailed file information.

```bash
stat notes.txt
```

It can show:

- File size
- Permissions
- Owner
- Group
- Access time
- Modification time
- Change time

Example:

```bash
stat student.txt
```

---

# 22. File Listing and Details — `ls -l`

Although `ls` is primarily a directory-listing command, it is essential for file operations.

```bash
ls -l
```

Example:

```text
-rw-r--r-- 1 akash akash 120 Sep 22 notes.txt
```

Important parts include:

```text
-rw-r--r--
  │││ │││
  │││ └── Others
  ││└──── Group
  └────── Owner
```

Permissions will be studied in detail with `chmod`.

---

# 23. Finding Files — `find`

`find` searches for files and directories.

### Search by name

```bash
find . -name "notes.txt"
```

Here:

```text
. = current directory
```

### Find all `.txt` files

```bash
find . -name "*.txt"
```

### Find files only

```bash
find . -type f
```

### Find directories only

```bash
find . -type d
```

### Find files larger than 10 MB

```bash
find . -type f -size +10M
```

---

# 24. Searching Text Inside Files — `grep`

`grep` searches for text inside files.

### Basic search

```bash
grep "java" notes.txt
```

This displays lines containing `java`.

### Case-insensitive search

```bash
grep -i "java" notes.txt
```

This matches:

```text
java
Java
JAVA
```

### Show line numbers

```bash
grep -n "java" notes.txt
```

### Search recursively in a directory

```bash
grep -r "Hello" project/
```

This searches files inside `project/`.

---

# 25. Difference Between `find` and `grep`

This is important.

### `find`

Searches for **files/directories**.

```bash
find . -name "*.java"
```

Meaning:

> Find Java files.

### `grep`

Searches for **text inside files**.

```bash
grep -r "main" .
```

Meaning:

> Find files containing the text `main`.

---

# 26. Comparing Files — `diff`

`diff` compares two text files.

```bash
diff file1.txt file2.txt
```

Example:

```bash
diff original.txt modified.txt
```

Useful for finding what changed between two files.

---

# 27. Comparing Files — `cmp`

`cmp` compares files byte by byte.

```bash
cmp file1.txt file2.txt
```

If there is no output, the files may be identical.

For normal text-file comparison, `diff` is generally easier for students to understand.

---

# 28. File Permissions — `chmod`

`chmod` means **change mode**.

First check permissions:

```bash
ls -l notes.txt
```

Give execute permission:

```bash
chmod +x script.sh
```

Remove write permission:

```bash
chmod -w notes.txt
```

Set numeric permissions:

```bash
chmod 644 notes.txt
```

A basic permission model is:

```text
Owner | Group | Others
```

For example:

```text
-rw-r--r--
```

means:

```text
Owner  → read + write
Group  → read
Others → read
```

---

# 29. Ownership — `chown`

`chown` means **change owner**.

```bash
sudo chown user1 notes.txt
```

Change owner and group:

```bash
sudo chown user1:students notes.txt
```

> Usually `sudo` is required when changing ownership of files you do not own.

---

# 30. Change Group — `chgrp`

Change the group associated with a file:

```bash
sudo chgrp students notes.txt
```

---

# 31. Hard Links — `ln`

Create a hard link:

```bash
ln original.txt hardlink.txt
```

Both names refer to the same underlying file data.

---

# 32. Symbolic/Soft Links

Create a symbolic link:

```bash
ln -s original.txt shortcut.txt
```

Think of it like:

```text
original.txt
     ↑
     │
shortcut.txt
```

The symbolic link points to the original path.

---

# 33. Archive Files — `tar`

`tar` is commonly used to collect multiple files/directories into one archive.

### Create an archive

```bash
tar -cf backup.tar documents/
```

### Extract an archive

```bash
tar -xf backup.tar
```

Common options:

```text
-c → create
-x → extract
-f → specify archive file
```

---

# 34. Create a Compressed TAR Archive

```bash
tar -czf backup.tar.gz documents/
```

Here:

```text
-c → create
-z → gzip compression
-f → archive filename
```

Extract:

```bash
tar -xzf backup.tar.gz
```

---

# 35. GZIP Compression

Compress:

```bash
gzip notes.txt
```

This normally produces:

```text
notes.txt.gz
```

Decompress:

```bash
gunzip notes.txt.gz
```

---

# 36. ZIP Files

Create a ZIP archive:

```bash
zip notes.zip notes.txt
```

Multiple files:

```bash
zip project.zip *.java
```

Extract:

```bash
unzip project.zip
```

---

# 37. Useful Command Combinations

Linux becomes powerful when commands are combined.

### Create a file and write into it

```bash
echo "Hello Linux" > notes.txt
```

### View the file

```bash
cat notes.txt
```

### Append data

```bash
echo "Linux is powerful" >> notes.txt
```

### Search inside it

```bash
grep "Linux" notes.txt
```

### Find all Java files

```bash
find . -name "*.java"
```

### Find Java files containing `main`

```bash
grep -r "main" --include="*.java" .
```

---

# 38. Pipe Operator `|`

The pipe sends the output of one command as input to another command.

Example:

```bash
ls | less
```

Meaning:

```text
ls output
    ↓
   pipe
    ↓
 less
```

Another example:

```bash
ls | grep ".txt"
```

This displays entries containing `.txt`.

---

# 39. Practical Example — Student Notes File

Create a directory:

```bash
mkdir linux-practice
```

Enter it:

```bash
cd linux-practice
```

Create a file:

```bash
touch student.txt
```

Write data:

```bash
echo "Name: Akash" > student.txt
```

Append more data:

```bash
echo "Course: Linux" >> student.txt
echo "Semester: 3" >> student.txt
```

View:

```bash
cat student.txt
```

Check information:

```bash
stat student.txt
```

Make a backup:

```bash
cp student.txt student-backup.txt
```

Rename it:

```bash
mv student-backup.txt backup.txt
```

Search for the file:

```bash
find . -name "backup.txt"
```

Search for text:

```bash
grep "Linux" student.txt
```

---

# 40. Command Cheat Sheet

| Command | Example | Use |
|---|---|---|
| `touch` | `touch file.txt` | Create file |
| `mkdir` | `mkdir folder` | Create directory |
| `nano` | `nano file.txt` | Edit file |
| `cat` | `cat file.txt` | Display file |
| `less` | `less file.txt` | Read large file |
| `more` | `more file.txt` | Page-by-page view |
| `head` | `head file.txt` | First lines |
| `tail` | `tail file.txt` | Last lines |
| `echo` | `echo "Hi"` | Print/write text |
| `printf` | `printf "Hi\n"` | Formatted output |
| `cp` | `cp a.txt b.txt` | Copy |
| `mv` | `mv a.txt b.txt` | Move/rename |
| `rm` | `rm file.txt` | Delete file |
| `rmdir` | `rmdir folder` | Delete empty directory |
| `file` | `file image.jpg` | Identify type |
| `stat` | `stat file.txt` | File metadata |
| `find` | `find . -name "*.txt"` | Find files |
| `grep` | `grep "Linux" file.txt` | Search text |
| `diff` | `diff a.txt b.txt` | Compare files |
| `cmp` | `cmp a.txt b.txt` | Byte comparison |
| `chmod` | `chmod 644 file.txt` | Change permissions |
| `chown` | `sudo chown user file` | Change owner |
| `chgrp` | `sudo chgrp group file` | Change group |
| `ln` | `ln a b` | Hard link |
| `ln -s` | `ln -s a b` | Symbolic link |
| `tar` | `tar -cf a.tar folder/` | Archive |
| `gzip` | `gzip file.txt` | Compress |
| `zip` | `zip a.zip file.txt` | ZIP archive |
| `unzip` | `unzip a.zip` | Extract ZIP |

---

# 41. Important Differences to Remember

### `>` vs `>>`

```bash
>    → overwrite
>>   → append
```

### `cat` vs `less`

```text
cat   → quickly display file
less  → browse large file
```

### `cp` vs `mv`

```text
cp → copy; original remains
mv → move; original location no longer has the file
```

### `rm` vs `rmdir`

```text
rm     → remove files
rmdir  → remove empty directories
```

### `find` vs `grep`

```text
find → find files/directories
grep → find text inside files
```

### `gzip` vs `tar`

```text
tar   → archive/collect files
gzip  → compress data
```

A common combination is:

```bash
tar -czf backup.tar.gz project/
```

---

# 42. Practice Exercises

## Exercise 1 — Basic File Operations

Perform the following:

1. Create a directory called `linux-files`.
2. Enter the directory.
3. Create three files:
   - `notes.txt`
   - `commands.txt`
   - `practice.txt`
4. Add at least 5 lines to `notes.txt`.
5. Display the complete file using `cat`.
6. Display the first 2 lines using `head`.
7. Display the last 2 lines using `tail`.
8. Append two more lines.
9. Display the updated file.

---

## Exercise 2 — Copy, Move and Rename

1. Create `original.txt`.
2. Add some text to it.
3. Create a copy called `backup.txt`.
4. Create a directory called `backup`.
5. Move `backup.txt` into the `backup` directory.
6. Rename it to `notes-backup.txt`.
7. Verify the final location using `ls`.

---

## Exercise 3 — Search Practice

Create several files:

```text
java.txt
python.txt
linux.txt
database.txt
```

Then:

1. Find all `.txt` files using `find`.
2. Put the word `Linux` in at least two files.
3. Search for `Linux` using `grep`.
4. Search without considering uppercase/lowercase.
5. Display matching line numbers.

---

## Exercise 4 — File Information

For a file of your choice:

1. Use `ls -l`.
2. Use `file`.
3. Use `stat`.
4. Identify its:
   - Size
   - Owner
   - Group
   - Permissions
   - Modification time

---

## Exercise 5 — Archive and Compression

Create a directory:

```text
project/
```

Put at least three files inside it.

Then:

1. Create `project.tar`.
2. Extract the archive.
3. Create `project.tar.gz`.
4. Extract it.
5. Create `project.zip`.
6. Extract the ZIP file.

---

# 43. Quick Revision

Remember this sequence:

```text
CREATE
  ↓
touch / mkdir
  ↓
WRITE / EDIT
  ↓
echo / printf / nano
  ↓
VIEW
  ↓
cat / less / head / tail
  ↓
COPY / MOVE
  ↓
cp / mv
  ↓
SEARCH
  ↓
find / grep
  ↓
INFORMATION
  ↓
file / stat / ls -l
  ↓
PERMISSIONS
  ↓
chmod / chown / chgrp
  ↓
ARCHIVE
  ↓
tar / gzip / zip
  ↓
DELETE
  ↓
rm / rmdir
```

> **Golden Rule:** Before using `rm`, `mv`, `cp`, or `chmod`, understand exactly which file/directory you are operating on. Use `pwd` and `ls -l` whenever you are unsure about your current location or the target.
