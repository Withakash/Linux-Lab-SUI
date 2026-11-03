# Linux Command Line – Commands, Options & Arguments

## 1. General Command Structure

A useful beginner-friendly model for Linux commands is:

```text
command [options] [arguments]
   │        │          │
   │        │          └── What to operate on
   │        └───────────── How to operate
   └────────────────────── What program/action to execute
```

Example:

```bash
ls -l /home
```

Breakdown:

```text
ls       → Command
-l       → Option
/home    → Argument
```

Meaning:

> Run `ls`, use long-listing format, and list the contents of `/home`.

> **Important:** This is a useful general model, not a universal grammar. Individual commands can have their own syntax.

---

# 2. What is a Command?

A **command** is generally the name of a program or shell builtin that tells the shell what action to perform.

Examples:

```bash
ls
pwd
cd
mkdir
cp
mv
rm
cat
echo
```

When you type:

```bash
ls
```

the shell interprets the command and executes the appropriate program/builtin.

```text
User
  ↓
Types command
  ↓
Shell
  ↓
Finds / interprets command
  ↓
Executes it
  ↓
Output
```

---

# 3. What is an Option?

An **option** modifies the behavior of a command.

Example:

```bash
ls
```

lists directory contents.

```bash
ls -l
```

lists directory contents using a detailed/long format.

So:

```text
Command → What to do
Option  → How to do it
```

Options are also called:

- Flags
- Switches
- Command-line options

---

# 4. Short Options

Short options normally begin with one hyphen:

```text
-
```

Examples:

```bash
ls -l
ls -a
ls -h
```

Meaning:

```text
-l → long format
-a → all entries
-h → human-readable sizes
```

---

# 5. Long Options

Long options normally begin with two hyphens:

```text
--
```

Examples:

```bash
ls --all
ls --human-readable
```

Common equivalences:

| Short option | Long option | Meaning |
|---|---|---|
| `-a` | `--all` | Show hidden entries |
| `-h` | `--human-readable` | Use human-readable sizes |
| `-R` | `--recursive` | List recursively |
| `-r` | `--reverse` | Reverse sorting order |

Long options are usually easier to understand because their names are descriptive.

---

# 6. Combining Options

Several short options can often be combined.

Instead of:

```bash
ls -l -a -h
```

you can usually write:

```bash
ls -lah
```

This means:

```text
-l → Long format
-a → All entries
-h → Human-readable sizes
```

> **Note:** Option-combining rules depend on the command. Do not assume every command supports every combination.

---

# 7. Options with Values

Some options require a value.

Example:

```bash
head -n 5 file.txt
```

Breakdown:

```text
head       → Command
-n         → Option
5          → Option value
file.txt   → Argument
```

Meaning:

> Display the first 5 lines of `file.txt`.

Another example:

```bash
grep -n "Linux" notes.txt
```

Here:

```text
grep        → Command
-n          → Option
"Linux"     → Argument
notes.txt   → Argument
```

The exact role of a value depends on the command.

---

# 8. What is an Argument?

An **argument** is information supplied to a command that tells it what data, file, directory, target, text, or other value to operate on.

Example:

```bash
cd Documents
```

```text
cd          → Command
Documents   → Argument
```

The argument answers:

> Which directory should `cd` enter?

---

# 9. Types of Arguments

## 9.1 File Argument

```bash
cat notes.txt
```

```text
cat        → Command
notes.txt  → Argument
```

The argument tells `cat` which file to read.

---

## 9.2 Directory Argument

```bash
cd Documents
```

`Documents` is the directory argument.

---

## 9.3 Path Argument

```bash
ls /home/akash/Documents
```

`/home/akash/Documents` is a path argument.

---

## 9.4 Multiple Arguments

```bash
rm file1.txt file2.txt file3.txt
```

There are three file arguments:

```text
file1.txt → Argument 1
file2.txt → Argument 2
file3.txt → Argument 3
```

---

# 10. Arguments Can Have Positions

Some commands expect arguments in a specific order.

Example:

```bash
cp file1.txt backup.txt
```

General syntax:

```text
cp SOURCE DESTINATION
```

Therefore:

```text
file1.txt  → Source
backup.txt → Destination
```

Changing the order can change the operation.

Similarly:

```bash
mv old.txt new.txt
```

means:

```text
old.txt → Source
new.txt → Destination
```

---

# 11. Options vs Arguments

A simple way to remember:

```text
OPTION   → HOW?
ARGUMENT → WHAT / WHERE?
```

Example:

```bash
ls -l /home
```

```text
ls       → WHAT?  List
-l       → HOW?   Detailed format
/home    → WHAT?  The /home directory
```

Another example:

```bash
cp -v file.txt backup.txt
```

```text
cp          → WHAT?  Copy
-v          → HOW?   Verbose output
file.txt    → FROM?  Source
backup.txt  → TO?    Destination
```

---

# 12. `ls` Command

## Purpose

`ls` lists files and directories.

### Basic syntax

```bash
ls [OPTION]... [FILE]...
```

Example:

```bash
ls
```

---

# 13. `ls` Options – Important Reference

The following table covers the commonly used GNU/Linux `ls` options. Exact behavior and availability can vary slightly on macOS/BSD systems.

| Option | Long option | Working / Meaning |
|---|---|---|
| `-a` | `--all` | Include hidden entries |
| `-A` | `--almost-all` | Include hidden entries except `.` and `..` |
| `-l` | `--format=long` | Use long/detailed listing |
| `-h` | `--human-readable` | Show sizes in readable units such as KB, MB |
| `-H` | `--dereference-command-line` | Follow symbolic links given on command line |
| `-R` | `--recursive` | List subdirectories recursively |
| `-r` | `--reverse` | Reverse the sorting order |
| `-t` | — | Sort by modification time |
| `-S` | `--sort=size` | Sort by file size |
| `-X` | `--sort=extension` | Sort by file extension |
| `-v` | `--sort=version` | Natural/version-number sorting |
| `-U` | `--sort=none` | Do not sort; directory order |
| `-f` | — | Do not sort; implies `-a` |
| `-1` | — | One entry per line |
| `-C` | — | List entries in columns |
| `-x` | — | List entries by lines instead of columns |
| `-m` | — | Separate entries with commas |
| `-F` | `--classify` | Append indicators such as `/` to directories |
| `-p` | — | Append `/` to directories |
| `-d` | `--directory` | List directories themselves, not their contents |
| `-i` | `--inode` | Show inode number |
| `-n` | `--numeric-uid-gid` | Show numeric user/group IDs |
| `-o` | — | Long format without group information |
| `-g` | — | Long format without owner information |
| `-G` | `--no-group` | Do not print group names |
| `-s` | `--size` | Show allocated blocks for each file |
| `-k` | `--block-size=1K` | Use 1 KB block size |
| `-L` | `--dereference` | Follow all symbolic links |
| `-P` | `--physical` | Do not follow symbolic links |
| `-n` | `--numeric-uid-gid` | Display numeric UID/GID |
| `-Z` | `--context` | Display security context where supported |
| `-Q` | `--quote-name` | Enclose entry names in quotes |
| `-b` | `--escape` | Print C-style escapes for non-printing characters |
| `-q` | `--hide-control-chars` | Print `?` instead of non-printing characters |
| `-N` | `--literal` | Print names without quoting |
| `--color` | `--color[=WHEN]` | Colorize output when supported |
| `--time-style` | `--time-style=STYLE` | Control displayed timestamp format |
| `--full-time` | — | Show full date/time information |

### Most useful beginner options

Start with:

```bash
ls
ls -l
ls -a
ls -h
ls -lh
ls -la
ls -lah
```

Later:

```bash
ls -lt
ls -ltr
ls -lhS
ls -R
```

---

# 14. `ls` Examples

### Detailed listing

```bash
ls -l
```

### Show hidden files

```bash
ls -a
```

### Human-readable sizes

```bash
ls -lh
```

### Detailed + hidden + readable sizes

```bash
ls -lah
```

### Sort by modification time

```bash
ls -lt
```

### Reverse time order

```bash
ls -ltr
```

### Sort by size

```bash
ls -lS
```

### Recursively list subdirectories

```bash
ls -R
```

---

# 15. `pwd` Command

## Purpose

Print the current working directory.

```bash
pwd
```

Example:

```text
/home/akash
```

### Common GNU/Linux options

| Option | Meaning |
|---|---|
| `-L` | Use logical path |
| `-P` | Use physical path |

Examples:

```bash
pwd -L
pwd -P
```

For beginners, the most important command is simply:

```bash
pwd
```

---

# 16. `cd` Command

## Purpose

Change the current working directory.

```bash
cd Documents
```

### Common forms

```bash
cd
```

Go to the user's home directory.

```bash
cd ~
```

Go to the user's home directory.

```bash
cd ..
```

Go to the parent directory.

```bash
cd /
```

Go to the root directory.

```bash
cd -
```

Go to the previous working directory.

### Important

`cd` is normally a shell builtin, so its options and behavior depend on the shell.

---

# 17. `mkdir` Command

## Purpose

Create directories.

Basic syntax:

```bash
mkdir directory_name
```

Example:

```bash
mkdir linux
```

### Common GNU/Linux options

| Option | Long option | Working |
|---|---|---|
| `-p` | `--parents` | Create parent directories as needed |
| `-m` | `--mode=MODE` | Set directory permission mode |
| `-v` | `--verbose` | Display a message for each created directory |
| `-Z` | `--context=CTX` | Set security context where supported |

### Examples

Create nested directories:

```bash
mkdir -p project/src/java
```

Verbose output:

```bash
mkdir -v linux
```

Set permissions while creating:

```bash
mkdir -m 755 project
```

---

# 18. `touch` Command

## Purpose

Create an empty file or update file timestamps.

Example:

```bash
touch notes.txt
```

### Common GNU/Linux options

| Option | Long option | Working |
|---|---|---|
| `-a` | `--time=access` | Change access time |
| `-m` | `--time=modify` | Change modification time |
| `-c` | `--no-create` | Do not create file if it does not exist |
| `-d` | `--date=STRING` | Use specified date/time |
| `-r` | `--reference=FILE` | Use timestamps from another file |
| `-t` | `[[CC]YY]MMDDhhmm[.ss]` | Use specified timestamp |
| `--time=WORD` | — | Select timestamp type |

### Examples

Create multiple files:

```bash
touch file1.txt file2.txt file3.txt
```

Do not create a missing file:

```bash
touch -c file.txt
```

---

# 19. `cp` Command

## Purpose

Copy files and directories.

Basic syntax:

```bash
cp SOURCE DESTINATION
```

Example:

```bash
cp file.txt backup.txt
```

### Common GNU/Linux options

| Option | Long option | Working |
|---|---|---|
| `-i` | `--interactive` | Ask before overwriting |
| `-f` | `--force` | Force replacement when possible |
| `-n` | `--no-clobber` | Do not overwrite existing destination |
| `-v` | `--verbose` | Show what is being copied |
| `-r` | `--recursive` | Copy directories recursively |
| `-R` | `--recursive` | Copy directories recursively |
| `-a` | `--archive` | Preserve attributes and copy recursively |
| `-p` | `--preserve` | Preserve specified file attributes |
| `-u` | `--update` | Copy only when source is newer or destination missing |
| `-b` | `--backup` | Make backup before overwriting |
| `-l` | `--link` | Create hard links instead of copying |
| `-s` | `--symbolic-link` | Create symbolic links instead of copying |
| `-T` | `--no-target-directory` | Treat destination as a normal file |
| `-t DIR` | `--target-directory=DIR` | Copy all sources into DIR |
| `-S SUFFIX` | `--suffix=SUFFIX` | Override backup suffix |

### Examples

Copy a file:

```bash
cp file.txt backup.txt
```

Copy directory:

```bash
cp -r project project_backup
```

Ask before overwrite:

```bash
cp -i file.txt backup.txt
```

Verbose copy:

```bash
cp -v file.txt backup.txt
```

Archive copy:

```bash
cp -a project project_backup
```

---

# 20. `mv` Command

## Purpose

Move or rename files/directories.

Basic syntax:

```bash
mv SOURCE DESTINATION
```

Example:

```bash
mv old.txt new.txt
```

### Common GNU/Linux options

| Option | Long option | Working |
|---|---|---|
| `-i` | `--interactive` | Ask before overwriting |
| `-f` | `--force` | Do not prompt before overwriting |
| `-n` | `--no-clobber` | Do not overwrite existing destination |
| `-v` | `--verbose` | Show what is being moved |
| `-b` | `--backup` | Make a backup before overwriting |
| `-S` | `--suffix=SUFFIX` | Change backup suffix |
| `-t` | `--target-directory=DIR` | Move all sources into DIR |
| `-T` | `--no-target-directory` | Treat destination as a normal file |

### Examples

Rename:

```bash
mv old.txt new.txt
```

Move:

```bash
mv notes.txt Documents/
```

Interactive:

```bash
mv -i old.txt new.txt
```

Verbose:

```bash
mv -v old.txt new.txt
```

---

# 21. `rm` Command

## Purpose

Remove/delete files or directories.

Basic syntax:

```bash
rm filename
```

### Common GNU/Linux options

| Option | Long option | Working |
|---|---|---|
| `-i` | `--interactive=always` | Ask before every removal |
| `-I` | `--interactive=once` | Prompt once in certain cases |
| `-f` | `--force` | Ignore nonexistent files and suppress prompts |
| `-r` | `--recursive` | Remove directories and their contents |
| `-R` | `--recursive` | Remove directories recursively |
| `-d` | `--dir` | Remove empty directories |
| `-v` | `--verbose` | Explain what is being removed |

### Examples

Delete a file:

```bash
rm file.txt
```

Ask before deleting:

```bash
rm -i file.txt
```

Delete a directory recursively:

```bash
rm -r project
```

Verbose:

```bash
rm -v file.txt
```

### ⚠️ Safety

Be extremely careful with:

```bash
rm -r
rm -rf
```

Especially when running as root.

There is generally no normal recycle-bin recovery mechanism provided by `rm`.

---

# 22. `cat` Command

## Purpose

Display, concatenate, or create text streams/files.

Basic syntax:

```bash
cat filename
```

### Common GNU/Linux options

| Option | Long option | Working |
|---|---|---|
| `-n` | `--number` | Number all output lines |
| `-b` | `--number-nonblank` | Number only non-empty lines |
| `-s` | `--squeeze-blank` | Reduce repeated blank lines |
| `-E` | `--show-ends` | Show `$` at line endings |
| `-T` | `--show-tabs` | Show tab characters |
| `-v` | `--show-nonprinting` | Show non-printing characters |
| `-A` | `--show-all` | Equivalent to `-vET` |
| `-e` | — | Similar to `-vE` |
| `-t` | — | Similar to `-vT` |

### Examples

Display file:

```bash
cat notes.txt
```

Number lines:

```bash
cat -n notes.txt
```

Display multiple files:

```bash
cat file1.txt file2.txt
```

Combine files into another file:

```bash
cat file1.txt file2.txt > combined.txt
```

---

# 23. `echo` Command

## Purpose

Print text or variable values.

Example:

```bash
echo "Hello Linux"
```

### Common Bash options

| Option | Working |
|---|---|
| `-n` | Do not print the trailing newline |
| `-e` | Enable interpretation of backslash escape sequences |
| `-E` | Disable interpretation of backslash escapes |

Example:

```bash
echo -n "Hello"
```

The prompt appears on the same line.

Example:

```bash
echo -e "Hello\nLinux"
```

The `\n` is interpreted as a newline in shells where this option is supported.

> **Important:** `echo` is commonly a shell builtin, and behavior/options can differ between Bash, Zsh, macOS, and other shells. For portable scripts, `printf` is often more predictable.

---

# 24. `whoami` Command

## Purpose

Display the effective username of the current user.

```bash
whoami
```

Example:

```text
akash
```

The command generally has no important options for beginner use.

---

# 25. `date` Command

## Purpose

Display or format the system date and time.

Basic:

```bash
date
```

### Common GNU/Linux options

| Option | Working |
|---|---|
| `-d` | Display a date/time described by a string |
| `-u` | Display UTC instead of local time |
| `--date=STRING` | Same concept as `-d` |
| `-I` | Output ISO-style date |
| `-R` | Output RFC-style date |
| `-r FILE` | Display file's modification time |
| `-s STRING` | Set system time on systems where permitted |
| `+FORMAT` | Format the output |

Examples:

```bash
date
```

```bash
date -u
```

```bash
date "+%Y-%m-%d"
```

Example output:

```text
2026-09-01
```

---

# 26. `uname` Command

## Purpose

Display system/kernel information.

Basic:

```bash
uname
```

### Options

| Option | Long option | Working |
|---|---|---|
| `-a` | `--all` | Display all available information |
| `-s` | `--kernel-name` | Kernel/system name |
| `-n` | `--nodename` | Network hostname |
| `-r` | `--kernel-release` | Kernel release |
| `-v` | `--kernel-version` | Kernel version |
| `-m` | `--machine` | Machine hardware name |
| `-p` | `--processor` | Processor type, when available |
| `-i` | `--hardware-platform` | Hardware platform, when available |
| `-o` | `--operating-system` | Operating system |

Most useful:

```bash
uname -a
```

---

# 27. `clear` Command

## Purpose

Clear the visible terminal screen.

```bash
clear
```

Common shortcut:

```text
Ctrl + L
```

`clear` has no important options for beginner-level use.

---

# 28. `history` Command

## Purpose

Display previously executed shell commands.

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

### Bash options

| Option | Working |
|---|---|
| `-c` | Clear the current shell history list |
| `-d OFFSET` | Delete a history entry |
| `-a` | Append new history entries to the history file |
| `-n` | Read new history entries from the history file |
| `-r` | Read the history file and append to history list |
| `-w` | Write current history list to history file |
| `-p ARG` | Perform history expansion without executing |
| `-s ARG` | Add arguments to history as a single entry |

Examples:

```bash
history
```

Repeat a command by history number:

```bash
!5
```

Search interactively in Bash:

```text
Ctrl + R
```

> **Shell-specific:** `history` is a shell builtin and its exact options can differ between Bash, Zsh, and other shells.

---

# 29. `man` Command

## Purpose

Display the manual page for a command.

Example:

```bash
man ls
```

Common options include:

| Option | Working |
|---|---|
| `-f` | Display a short description |
| `-k KEYWORD` | Search manual descriptions for a keyword |
| `-a` | Display all matching manual pages |
| `-w` | Show the location of the manual page |
| `-W` | Show manual location without opening it |

Examples:

```bash
man ls
```

Search for commands related to copying:

```bash
man -k copy
```

### Exiting `man`

Press:

```text
q
```

---

# 30. `--help`

Many GNU/Linux commands support:

```bash
command --help
```

Example:

```bash
ls --help
```

This provides quick information about:

- Command syntax
- Available options
- Arguments
- Usage examples in some programs

---

# 31. Special Path Arguments

Linux provides special path symbols.

| Symbol | Meaning | Example |
|---|---|---|
| `/` | Root directory | `cd /` |
| `~` | Current user's home directory | `cd ~` |
| `.` | Current directory | `ls .` |
| `..` | Parent directory | `cd ..` |
| `-` | Previous directory in `cd` | `cd -` |

---

# 32. Absolute vs Relative Arguments

## Absolute Path

Starts from `/`.

```bash
ls /home/akash/Documents
```

This is an absolute path.

## Relative Path

Starts from the current directory.

```bash
ls Documents
```

This depends on the current location.

Example:

```text
/home/akash
       |
       └── Documents
```

If the current directory is:

```text
/home/akash
```

then:

```bash
ls Documents
```

works.

---

# 33. Quoted Arguments

The shell normally separates arguments using spaces.

Consider:

```bash
echo Hello Linux
```

The shell sees:

```text
echo
├── Hello    → Argument 1
└── Linux    → Argument 2
```

With quotes:

```bash
echo "Hello Linux"
```

the shell sees:

```text
echo
└── "Hello Linux" → One argument
```

Quotes are therefore important when an argument contains spaces.

---

# 34. The `--` Separator

Many command-line programs recognize:

```bash
--
```

as:

> Stop interpreting subsequent text as options.

Example:

```bash
rm -- -file.txt
```

Here:

```text
rm        → Command
--        → Stop option processing
-file.txt → Filename argument
```

Without `--`, a filename beginning with `-` may be interpreted as an option.

---

# 35. Complete Command Breakdown Examples

## Example 1

```bash
ls -lah /home
```

```text
ls       → Command
-l       → Option: long format
-a       → Option: show hidden entries
-h       → Option: human-readable sizes
/home    → Argument: target directory
```

---

## Example 2

```bash
cp -v file.txt backup.txt
```

```text
cp          → Command
-v          → Option: verbose output
file.txt    → Argument: source
backup.txt  → Argument: destination
```

---

## Example 3

```bash
mkdir -p project/src/java
```

```text
mkdir           → Command
-p              → Option: create parent directories
project/src/java → Argument: directory path
```

---

## Example 4

```bash
grep -n "Linux" notes.txt
```

```text
grep        → Command
-n          → Option: show line numbers
"Linux"     → Argument: search pattern
notes.txt   → Argument: file to search
```

---

## Example 5

```bash
head -n 5 notes.txt
```

```text
head        → Command
-n          → Option
5           → Option value
notes.txt   → Argument
```

Meaning:

> Show the first 5 lines of `notes.txt`.

---

# 36. Command-Line Mental Model

Remember:

```text
                 COMMAND LINE
                      │
        ┌─────────────┴─────────────┐
        │                           │
     COMMAND                    OPTIONS
        │                           │
     WHAT TO DO                HOW TO DO IT
                                    │
                              Option values
                                    │
                                    ▼
                              Configuration

                  ARGUMENTS
                      │
              WHAT / WHERE / DATA
                      │
        ┌─────────────┼─────────────┐
        │             │             │
      Files       Directories      Text
        │             │             │
      Paths         Targets       Patterns
```

---

# 37. Quick Reference – Day 1 Commands

| Command | Main Purpose | Example |
|---|---|---|
| `pwd` | Show current directory | `pwd` |
| `ls` | List files/directories | `ls -la` |
| `cd` | Change directory | `cd Documents` |
| `mkdir` | Create directory | `mkdir project` |
| `touch` | Create/update file timestamp | `touch notes.txt` |
| `cp` | Copy | `cp a.txt b.txt` |
| `mv` | Move/rename | `mv old.txt new.txt` |
| `rm` | Delete | `rm file.txt` |
| `cat` | Display file content | `cat notes.txt` |
| `echo` | Print text | `echo "Hello"` |
| `whoami` | Show current user | `whoami` |
| `date` | Show date/time | `date` |
| `uname` | Show system information | `uname -a` |
| `clear` | Clear terminal | `clear` |
| `history` | Show command history | `history` |
| `man` | Read command manual | `man ls` |

---

# 38. The Most Important Rule

Do not try to memorize every option.

When you don't know an option:

```bash
command --help
```

or:

```bash
man command
```

For example:

```bash
ls --help
```

```bash
man ls
```

A strong Linux user knows **how to discover information**, not just how to memorize commands.

---

# 39. Day 1 Practice

Starting from your home directory:

1. Create a directory named `linux_practice`.
2. Enter the directory.
3. Create:
   - `student.txt`
   - `linux.txt`
   - `commands.txt`
4. Display all files.
5. Display detailed information.
6. Display hidden files.
7. Rename `linux.txt` to `linux_commands.txt`.
8. Copy `student.txt` to `student_backup.txt`.
9. Write this into `student.txt`:

```text
I am learning Linux Command Line.
```

10. Display the contents of `student.txt`.
11. Append:

```text
Linux is widely used in servers and cloud computing.
```

12. Display the file again.
13. Go to the parent directory.
14. Enter `linux_practice` again.
15. Display all files in detailed format with human-readable sizes.

Commands you should be able to use:

```bash
pwd
ls
ls -la
ls -lh
ls -lah
cd
mkdir
touch
cp
mv
rm
echo
cat
```

---

# 40. Final Summary

### Command

**What should I do?**

```text
ls
cp
mv
rm
```

### Option

**How should I do it?**

```text
-l
-a
-r
-v
```

### Option Value

**What value should this option use?**

```bash
head -n 5
```

Here `5` is the value for `-n`.

### Argument

**What/where should the command operate on?**

```bash
ls /home
```

`/home` is the argument.

### Remember

```text
COMMAND  → WHAT TO DO
OPTION   → HOW TO DO IT
VALUE    → HOW MUCH / WHICH SETTING
ARGUMENT → WHAT / WHERE / TARGET
```
