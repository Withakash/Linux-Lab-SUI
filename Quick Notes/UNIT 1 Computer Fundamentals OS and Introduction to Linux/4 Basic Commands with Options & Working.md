# Linux Basic Commands — Options & Working

> **Note:** The options below primarily describe GNU/Linux commands. macOS and Termux can have different implementations and available options. Verify with `command --help` and `man command`.

## 1. `pwd` — Print Working Directory

| Option | Meaning | Working |
|---|---|---|
| `-L` | Logical | Shows logical path, preserving symbolic links |
| `-P` | Physical | Shows physical path, resolving symbolic links |

```bash
pwd
pwd -L
pwd -P
```

---

## 2. `ls` — List Directory Contents

| Option | Meaning | Working |
|---|---|---|
| `-a` | All | Shows hidden files |
| `-A` | Almost all | Shows hidden files except `.` and `..` |
| `-l` | Long | Shows detailed information |
| `-h` | Human-readable | Shows sizes as KB, MB, GB, etc. |
| `-R` | Recursive | Shows contents of subdirectories |
| `-r` | Reverse | Reverses sorting order |
| `-t` | Time | Sorts by modification time |
| `-S` | Size | Sorts by file size |
| `-X` | Extension | Sorts by file extension |
| `-1` | One per line | Shows one entry per line |
| `-F` | Classify | Adds indicators such as `/` for directories |
| `-d` | Directory | Shows the directory itself instead of its contents |
| `-i` | Inode | Shows inode number |
| `-s` | Size | Shows allocated size |
| `-n` | Numeric | Shows numeric UID/GID |
| `-G` | No group | Does not show group information |
| `-Q` | Quote | Quotes file names |
| `-b` | Escape | Shows non-printing characters using escapes |

### Common combinations

```bash
ls -l
ls -a
ls -la
ls -lh
ls -lah
ls -ltr
ls -lhS
ls -R
```

### Example breakdown

```bash
ls -lh /home
```

```text
ls       → Command
-l       → Option → Long format
-h       → Option → Human-readable sizes
/home    → Argument
```

---

## 3. `cd` — Change Directory

`cd` is normally a shell builtin, so options depend on the shell.

| Option / Form | Working |
|---|---|
| `cd` | Goes to home directory |
| `cd ~` | Goes to home directory |
| `cd /` | Goes to root directory |
| `cd ..` | Goes to parent directory |
| `cd .` | Refers to current directory |
| `cd -` | Goes to previous directory |
| `cd -L` | Uses logical path |
| `cd -P` | Uses physical path |

```bash
cd Documents
cd ..
cd ~
cd /
cd -
```

---

## 4. `mkdir` — Make Directory

| Option | Meaning | Working |
|---|---|---|
| `-p` | Parents | Creates missing parent directories |
| `-v` | Verbose | Shows what was created |
| `-m` | Mode | Sets permissions while creating |
| `-Z` | SELinux context | Sets security context where supported |

```bash
mkdir test
mkdir -p project/src/java
mkdir -v practice
mkdir -m 755 project
```

---

## 5. `touch` — Create / Update File

| Option | Meaning | Working |
|---|---|---|
| `-a` | Access time | Changes access time |
| `-m` | Modification time | Changes modification time |
| `-c` | No create | Does not create a file if it doesn't exist |
| `-d` | Date | Uses specified date/time |
| `-r` | Reference | Uses timestamp from another file |
| `-t` | Timestamp | Specifies timestamp manually |

```bash
touch file.txt
touch file1.txt file2.txt
touch -c file.txt
touch -r reference.txt file.txt
```

---

## 6. `cp` — Copy

| Option | Meaning | Working |
|---|---|---|
| `-i` | Interactive | Asks before overwriting |
| `-f` | Force | Forces overwrite where possible |
| `-n` | No-clobber | Does not overwrite existing files |
| `-v` | Verbose | Shows what is being copied |
| `-r` | Recursive | Copies directories recursively |
| `-R` | Recursive | Same general purpose as `-r` |
| `-a` | Archive | Preserves attributes and copies recursively |
| `-p` | Preserve | Preserves file attributes |
| `-u` | Update | Copies when source is newer |
| `-b` | Backup | Backs up destination before overwrite |
| `-l` | Link | Creates hard links instead of copying |
| `-s` | Symbolic link | Creates symbolic links |
| `-t` | Target directory | Copies sources into specified directory |
| `-T` | No target directory | Treats destination as a normal file |

```bash
cp file.txt backup.txt
cp -i file.txt backup.txt
cp -v file.txt backup.txt
cp -r project project_backup
cp -a project project_backup
```

---

## 7. `mv` — Move / Rename

| Option | Meaning | Working |
|---|---|---|
| `-i` | Interactive | Asks before overwriting |
| `-f` | Force | Does not prompt before overwriting |
| `-n` | No-clobber | Does not overwrite destination |
| `-v` | Verbose | Shows what is being moved |
| `-b` | Backup | Backs up destination before overwrite |
| `-t` | Target directory | Moves sources into specified directory |
| `-T` | No target directory | Treats destination as a normal file |

```bash
mv old.txt new.txt
mv file.txt Documents/
mv -i file.txt Documents/
mv -v old.txt new.txt
```

---

## 8. `rm` — Remove

| Option | Meaning | Working |
|---|---|---|
| `-i` | Interactive | Asks before deletion |
| `-I` | Interactive once | Asks once before large/multiple deletion |
| `-f` | Force | Suppresses many prompts/errors for nonexistent files |
| `-r` | Recursive | Deletes directories and their contents |
| `-R` | Recursive | Same general purpose as `-r` |
| `-d` | Directory | Removes empty directories |
| `-v` | Verbose | Shows what is being deleted |

```bash
rm file.txt
rm -i file.txt
rm -r folder
rm -ri folder
```

### Warning

```bash
rm -rf folder
```

`-r` = recursive, `-f` = force. This can permanently delete a directory and its contents.

For an empty directory:

```bash
rmdir folder
```

---

## 9. `cat` — Concatenate

| Option | Meaning | Working |
|---|---|---|
| `-n` | Number | Numbers all lines |
| `-b` | Number nonblank | Numbers only non-empty lines |
| `-s` | Squeeze blank | Compresses repeated blank lines |
| `-E` | Show ends | Shows `$` at line ends |
| `-T` | Show tabs | Displays tab characters |
| `-v` | Show non-printing | Displays non-printing characters |
| `-A` | Show all | Equivalent to `-vET` |
| `-e` | Show ends | Similar to `-vE` |
| `-t` | Show tabs | Similar to `-vT` |

```bash
cat file.txt
cat -n file.txt
cat file1.txt file2.txt
```

---

## 10. `echo` — Display Text

`echo` is usually a shell builtin.

| Option | Working |
|---|---|
| `-n` | Does not print a trailing newline |
| `-e` | Interprets escape sequences |
| `-E` | Does not interpret escape sequences |

```bash
echo "Hello Linux"
echo -n "Hello"
echo -e "Hello
Linux"
```

### Redirection

```bash
echo "Hello Linux" > file.txt
```

`>` overwrites.

```bash
echo "Second line" >> file.txt
```

`>>` appends.

---

## 11. `whoami` — Current User

Displays the current effective username.

```bash
whoami
```

There are no important options for beginner use.

---

## 12. `date` — Date and Time

| Option | Meaning | Working |
|---|---|---|
| `-d` | Date string | Displays a specified date/time |
| `-u` | UTC | Displays UTC time |
| `-r` | Reference | Shows modification time of a file |
| `-I` | ISO format | Displays ISO-style date |
| `-R` | RFC format | Displays RFC-style date |
| `-s` | Set | Sets system date/time where permitted |
| `+FORMAT` | Format | Customizes output |

```bash
date
date -u
date "+%Y-%m-%d"
date "+%d-%m-%Y %H:%M:%S"
```

---

## 13. `uname` — Unix Name

| Option | Long Option | Working |
|---|---|---|
| `-a` | `--all` | Shows all available information |
| `-s` | `--kernel-name` | Shows kernel name |
| `-n` | `--nodename` | Shows network hostname |
| `-r` | `--kernel-release` | Shows kernel release |
| `-v` | `--kernel-version` | Shows kernel version |
| `-m` | `--machine` | Shows machine hardware name |
| `-p` | `--processor` | Shows processor type |
| `-i` | `--hardware-platform` | Shows hardware platform |
| `-o` | `--operating-system` | Shows operating system |

```bash
uname -a
```

---

## 14. `clear` — Clear Terminal

```bash
clear
```

Keyboard shortcut:

```text
Ctrl + L
```

There are no important options for beginner use.

---

## 15. `history` — Command History

`history` is generally a shell builtin.

| Option | Working in Bash |
|---|---|
| `-c` | Clears the history list |
| `-d OFFSET` | Deletes a history entry |
| `-a` | Appends new commands to history file |
| `-n` | Reads new entries from history file |
| `-r` | Reads history file |
| `-w` | Writes history list to history file |
| `-p` | Performs history expansion |
| `-s` | Adds arguments as one history entry |

```bash
history
history 10
```

Run a previous command:

```bash
!5
```

Search history:

```text
Ctrl + R
```

---

## 16. `man` — Manual

| Option | Meaning | Working |
|---|---|---|
| `-f` | What is | Shows a short description |
| `-k` | Apropos | Searches manual descriptions |
| `-a` | All | Displays all matching manual pages |
| `-w` | Where | Shows manual page location |
| `-W` | Where | Shows manual location without opening it |

```bash
man ls
man mkdir
man -k copy
```

Exit:

```text
q
```

---

# Quick Reference — Most Useful Options

| Command | Important Options |
|---|---|
| `pwd` | `-L`, `-P` |
| `ls` | `-a`, `-l`, `-h`, `-R`, `-r`, `-t`, `-S`, `-d` |
| `cd` | `-L`, `-P` |
| `mkdir` | `-p`, `-v`, `-m` |
| `touch` | `-a`, `-m`, `-c`, `-d`, `-r`, `-t` |
| `cp` | `-i`, `-f`, `-n`, `-v`, `-r`, `-a`, `-p`, `-u` |
| `mv` | `-i`, `-f`, `-n`, `-v`, `-b` |
| `rm` | `-i`, `-I`, `-f`, `-r`, `-d`, `-v` |
| `cat` | `-n`, `-b`, `-s`, `-E`, `-T`, `-v` |
| `echo` | `-n`, `-e`, `-E` |
| `whoami` | Usually none |
| `date` | `-d`, `-u`, `-r`, `-I`, `-R` |
| `uname` | `-a`, `-s`, `-n`, `-r`, `-v`, `-m` |
| `clear` | Usually none |
| `history` | `-c`, `-d`, `-a`, `-r`, `-w` |
| `man` | `-f`, `-k`, `-a`, `-w` |

---

# Command + Option + Argument

```text
COMMAND
   ↓
What do I want to do?

OPTION
   ↓
How do I want to do it?

OPTION VALUE
   ↓
What setting/value should the option use?

ARGUMENT
   ↓
What or where should the command operate?
```

### Example

```bash
ls -lh /home
```

```text
ls       → Command
-l       → Option → Long/detailed format
-h       → Option → Human-readable sizes
/home    → Argument → Target directory
```

Another example:

```bash
mkdir -pv project/src
```

```text
mkdir       → Command
-p          → Option → Create missing parent directories
-v          → Option → Show what is created
project/src → Argument → Directory path
```

---

# Linux vs macOS vs Termux

The same command name does not guarantee the same options on every Unix-like system.

Useful verification commands:

```bash
command --help
```

and:

```bash
man command
```

Examples:

```bash
ls --help
man ls
```

This habit is more useful than memorizing every option.
