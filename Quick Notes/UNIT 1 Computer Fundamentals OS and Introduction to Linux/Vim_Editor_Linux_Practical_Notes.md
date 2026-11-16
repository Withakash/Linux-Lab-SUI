# Linux Practical Notes: Vim Editor in Ubuntu

**Course:** Unix/Linux Programming\
**Topic:** Vim Text Editor\
**Level:** Beginner\
**Suggested Duration:** 60--90 minutes\
**Platform:** Ubuntu Terminal

------------------------------------------------------------------------

## Learning Objectives

By the end of this practical, students should be able to:

1.  Explain what Vim is and why it is used.
2.  Identify and switch between Vim's commonly used modes.
3.  Create, open, edit, save, and close files.
4.  Navigate through a file using keyboard shortcuts.
5.  Delete, copy, paste, undo, and redo text.
6.  Search for text and replace words.
7.  Select text using Visual Mode.
8.  Use basic indentation and window commands.

------------------------------------------------------------------------

# 1. Introduction to Vim

## What is Vim?

**Vim** stands for **Vi Improved**. It is a keyboard-oriented,
command-line text editor commonly used on Linux and Unix-like systems.

Vim is used to:

-   Create and edit text files.
-   Edit Linux configuration files.
-   Write and modify shell scripts.
-   Edit source code.
-   Work with files on remote servers through SSH.

## Why use Vim?

  -----------------------------------------------------------------------
  Feature                             Explanation
  ----------------------------------- -----------------------------------
  Lightweight                         Uses relatively few system
                                      resources

  Terminal-based                      Works directly inside the terminal

  Keyboard-oriented                   Most editing tasks can be performed
                                      without a mouse

  Powerful                            Supports search, replacement,
                                      macros, and advanced editing

  Widely available                    Commonly found on Linux and
                                      Unix-like systems
  -----------------------------------------------------------------------

## Check whether Vim is installed

``` bash
vim --version
```

If Vim is not installed, install it using:

``` bash
sudo apt update
sudo apt install vim -y
```

Open Vim:

``` bash
vim
```

To exit an empty Vim session, press `Esc`, type `:q`, and press `Enter`.

------------------------------------------------------------------------

# 2. Understanding Vim Modes

Vim is a **modal text editor**. This means that the keyboard behaves
differently depending on the active mode.

The four commonly used modes are:

  -----------------------------------------------------------------------
  Mode                                Purpose
  ----------------------------------- -----------------------------------
  Normal Mode                         Navigation and text-editing
                                      commands

  Insert Mode                         Typing and inserting text

  Visual Mode                         Selecting text

  Command-Line Mode                   Saving, quitting, searching, and
                                      running Ex commands
  -----------------------------------------------------------------------

## 2.1 Normal Mode

Normal Mode is the default mode when Vim opens. It is used for
navigation and editing commands.

Examples:

``` vim
h
j
k
l
dd
yy
p
```

Press `Esc` to return to Normal Mode from Insert or Visual Mode.

## 2.2 Insert Mode

Insert Mode is used to type and insert text.

  Shortcut   Action
  ---------- ----------------------------------------
  `i`        Insert before the cursor
  `I`        Insert at the beginning of the line
  `a`        Append after the cursor
  `A`        Append at the end of the line
  `o`        Open a new line below the current line
  `O`        Open a new line above the current line

Press `Esc` to leave Insert Mode.

## 2.3 Visual Mode

Visual Mode is used to select text.

  Shortcut     Action
  ------------ ---------------------------------------
  `v`          Character-wise selection
  `V`          Line-wise selection
  `Ctrl + v`   Block-wise selection
  `d`          Delete selected text
  `y`          Copy (yank) selected text
  `>`          Indent selected text
  `<`          Remove indentation from selected text

Press `Esc` to leave Visual Mode.

## 2.4 Command-Line Mode

Press `:` from Normal Mode to enter Command-Line Mode.

  Command         Action
  --------------- ------------------------------------
  `:w`            Save the file
  `:q`            Quit Vim
  `:wq`           Save and quit
  `:q!`           Quit without saving changes
  `:w filename`   Save the file with another name
  `:x`            Save and quit if changes were made

**Important:** Press `Enter` after typing a command.

------------------------------------------------------------------------

# 3. Creating and Opening Files

Create a practice directory:

``` bash
mkdir vim_practice
cd vim_practice
```

Create or open a file:

``` bash
vim student.txt
```

Follow these steps:

1.  Vim opens in Normal Mode.
2.  Press `i` to enter Insert Mode.
3.  Type some text.
4.  Press `Esc` to return to Normal Mode.
5.  Type `:wq` and press `Enter` to save and exit.

Example file content:

``` text
Name: Akash
Course: Linux Programming
Subject: Operating System
University: SAGE University
Semester: VI

Learning Vim Editor
Linux is an open-source operating system.
Vim is a powerful text editor.
```

To display the saved file in the terminal:

``` bash
cat student.txt
```

------------------------------------------------------------------------

# 4. Cursor Movement and Navigation

Vim provides keyboard shortcuts for moving through a file.

## 4.1 Basic movement

  Shortcut     Action
  ------------ -------------------------------------
  `h`          Move left
  `j`          Move down
  `k`          Move up
  `l`          Move right
  Arrow keys   Move in the corresponding direction

The `h`, `j`, `k`, and `l` keys are arranged together on the keyboard.

## 4.2 Line navigation

  Shortcut   Action
  ---------- ---------------------------------------
  `0`        Move to the beginning of the line
  `^`        Move to the first non-blank character
  `$`        Move to the end of the line
  `gg`       Move to the first line of the file
  `G`        Move to the last line of the file
  `5G`       Move to line 5
  `:5`       Move to line 5

## 4.3 Word navigation

  Shortcut   Action
  ---------- ---------------------------------------------
  `w`        Move to the beginning of the next word
  `b`        Move to the beginning of the previous word
  `e`        Move to the end of the current or next word

## 4.4 Screen navigation

  Shortcut     Action
  ------------ --------------------------
  `Ctrl + f`   Move one screen forward
  `Ctrl + b`   Move one screen backward
  `Ctrl + d`   Move half a screen down
  `Ctrl + u`   Move half a screen up

### Practice

Open `student.txt` and try these commands:

``` vim
gg
G
0
^
$
5G
```

Observe how the cursor moves.

------------------------------------------------------------------------

# 5. Editing Text in Vim

The following editing commands are generally used in Normal Mode.

## 5.1 Delete commands

  Shortcut   Action
  ---------- ----------------------------------------------------------
  `x`        Delete the character under the cursor
  `X`        Delete the character before the cursor
  `dd`       Delete the current line
  `2dd`      Delete two lines
  `3dd`      Delete three lines
  `dw`       Delete from the cursor to the beginning of the next word
  `d$`       Delete from the cursor to the end of the line
  `d0`       Delete from the cursor to the beginning of the line
  `D`        Delete from the cursor to the end of the line
  `dG`       Delete from the current line to the end of the file

### Understand the command structure

-   `d` means delete.
-   `w` represents a word movement.
-   `dd` deletes a complete line.
-   `d$` deletes from the cursor to the end of the line.

## 5.2 Copy (Yank) commands

In Vim, copying text is called **yanking**.

  Shortcut   Action
  ---------- --------------------------------------------------------
  `yy`       Copy the current line
  `2yy`      Copy two lines
  `3yy`      Copy three lines
  `yw`       Copy from the cursor to the beginning of the next word
  `y$`       Copy from the cursor to the end of the line
  `y0`       Copy from the cursor to the beginning of the line

## 5.3 Paste commands

  Shortcut   Action
  ---------- ----------------------------------------------------------
  `p`        Paste after the cursor; for line-wise text, paste below
  `P`        Paste before the cursor; for line-wise text, paste above

## 5.4 Undo and Redo

  -----------------------------------------------------------------------
  Shortcut                            Action
  ----------------------------------- -----------------------------------
  `u`                                 Undo the last change

  `Ctrl + r`                          Redo an undone change

  `U`                                 Restore the current line to its
                                      earlier state in the current
                                      editing session (legacy behavior)

  `.`                                 Repeat the last change
  -----------------------------------------------------------------------

### Practice

1.  Delete one line using `dd`.
2.  Undo the deletion using `u`.
3.  Copy a line using `yy`.
4.  Paste it using `p`.
5.  Delete two lines using `2dd`.
6.  Undo the deletion.
7.  Redo it using `Ctrl + r`.

------------------------------------------------------------------------

# 6. Searching in Vim

Searching is useful when working with long files, source code, and
configuration files.

## 6.1 Forward search

Type `/` followed by the word and press `Enter`.

``` vim
/Linux
```

## 6.2 Backward search

Type `?` followed by the word and press `Enter`.

``` vim
?Linux
```

## 6.3 Search navigation

  Shortcut   Action
  ---------- ----------------------------------------------------
  `/word`    Search forward for a word
  `?word`    Search backward for a word
  `n`        Move to the next match in the search direction
  `N`        Move to the previous match in the search direction

### Search example

Suppose a file contains:

``` text
Linux is an operating system.
Linux supports multiple users.
Linux supports multitasking.
Vim is a text editor.
```

Search for Linux:

``` vim
/Linux
```

Press `n` to move to the next match.

## 6.4 Search and Replace

  Command             Action
  ------------------- --------------------------------------------------
  `:s/old/new/`       Replace the first occurrence in the current line
  `:s/old/new/g`      Replace all occurrences in the current line
  `:%s/old/new/g`     Replace all occurrences in the entire file
  `:%s/old/new/gc`    Ask for confirmation before each replacement
  `:n,ms/old/new/g`   Replace occurrences from line n through line m

Example:

``` vim
:%s/Linux/Ubuntu/g
```

This replaces every occurrence of `Linux` with `Ubuntu` in the file.

For confirmation before each replacement:

``` vim
:%s/Linux/Ubuntu/gc
```

Common confirmation responses:

  Key   Action
  ----- -----------------------------------
  `y`   Replace this occurrence
  `n`   Skip this occurrence
  `a`   Replace all remaining occurrences
  `q`   Quit the replacement operation

------------------------------------------------------------------------

# 7. Visual Mode -- Selecting Text

Visual Mode allows users to select text using the keyboard.

## Three types of Visual Mode

  Shortcut     Selection type
  ------------ --------------------------
  `v`          Character-wise selection
  `V`          Line-wise selection
  `Ctrl + v`   Block-wise selection

## Example 1: Character-wise selection

1.  Move the cursor to a word.
2.  Press `v`.
3.  Move the cursor using `h`, `j`, `k`, and `l`.
4.  Press `d` to delete the selection or `y` to copy it.

## Example 2: Line-wise selection

1.  Press `V`.
2.  Select multiple lines using `j` or `k`.
3.  Press `d` to delete the selected lines.

## Example 3: Block-wise selection

1.  Press `Ctrl + v`.
2.  Move down to select multiple lines.
3.  Move horizontally to select columns.
4.  Press `d` to delete the selected block.

Block selection is useful for editing text arranged in columns.

------------------------------------------------------------------------

# 8. Indentation and Formatting

Indentation improves the readability of source code and shell scripts.

  Shortcut / Command   Action
  -------------------- ------------------------------------------
  `>>`                 Indent the current line
  `<<`                 Remove indentation from the current line
  `3>>`                Indent three lines
  `3<<`                Remove indentation from three lines
  `gg=G`               Auto-indent the entire file

## Useful Vim settings

  Command                 Purpose
  ----------------------- -----------------------------------------
  `:set number`           Show line numbers
  `:set nonumber`         Hide line numbers
  `:set relativenumber`   Show relative line numbers
  `:set tabstop=4`        Set tab display width to four spaces
  `:set shiftwidth=4`     Set indentation width to four spaces
  `:set expandtab`        Insert spaces instead of tab characters
  `:set paste`            Enable paste mode

Example:

``` vim
:set number
:set tabstop=4
:set shiftwidth=4
:set expandtab
```

------------------------------------------------------------------------

# 9. Working with Multiple Files and Windows

Vim can open multiple files and display multiple editing windows.

## 9.1 Open multiple files

``` bash
vim file1.txt file2.txt
```

Useful commands:

  Command      Action
  ------------ -------------------------------
  `:next`      Open the next file
  `:prev`      Open the previous file
  `:first`     Open the first file
  `:last`      Open the last file
  `:buffers`   Display open buffers
  `:bnext`     Switch to the next buffer
  `:bprev`     Switch to the previous buffer

## 9.2 Split windows

  Command                Action
  ---------------------- -------------------------------
  `:split`               Split the window horizontally
  `:vsplit`              Split the window vertically
  `Ctrl + w`, then `w`   Switch between windows
  `Ctrl + w`, then `h`   Move to the left window
  `Ctrl + w`, then `j`   Move to the lower window
  `Ctrl + w`, then `k`   Move to the upper window
  `Ctrl + w`, then `l`   Move to the right window
  `:close`               Close the current window

------------------------------------------------------------------------

# 10. Advanced Vim Shortcuts

These commands are useful after students understand the basics.

  Shortcut   Action
  ---------- ----------------------------------------------------
  `ciw`      Change the word under the cursor
  `diw`      Delete the word under the cursor
  `yiw`      Copy the word under the cursor
  `cw`       Change text from the cursor to the end of the word
  `cc`       Change the entire current line
  `C`        Change from the cursor to the end of the line
  `r`        Replace one character
  `R`        Enter Replace Mode
  `J`        Join the current line with the next line
  `~`        Toggle the case of the character under the cursor
  `.`        Repeat the last change

## Vim's operator and motion combination

Vim commands often combine an operator with a movement.

  Operator   Meaning
  ---------- -------------
  `d`        Delete
  `c`        Change
  `y`        Yank (copy)

Examples:

  Command   Meaning
  --------- ----------------------------------
  `dw`      Delete a word
  `cw`      Change a word
  `yw`      Copy a word
  `dd`      Delete a line
  `cc`      Change a line
  `yy`      Copy a line
  `ciw`     Change the word under the cursor
  `diw`     Delete the word under the cursor

This operator-and-motion combination system is one of Vim's most
powerful features.

------------------------------------------------------------------------

# 11. Complete Classroom Practical -- Create a Student Record

**Objective:** Create and edit a student record using Vim commands.

## Step 1: Create a file

``` bash
vim student_record.txt
```

## Step 2: Insert the following content

Press `i` and type:

``` text
STUDENT RECORD

Name: Rahul
Course: B.Tech
Semester: VI
University: SAGE University

SUBJECTS
1. Linux
2. Operating System
3. Java
4. Data Structures

Linux is an open-source operating system.
Vim is a powerful text editor.
```

## Step 3: Save the file

Press `Esc`, then type:

``` vim
:w
```

Press `Enter`.

## Step 4: Perform editing operations

Perform the following tasks:

1.  Move to the first line using `gg`.
2.  Move to the last line using `G`.
3.  Move to the beginning of the line using `0`.
4.  Move to the end of the line using `$`.
5.  Position the cursor at the beginning of `Rahul` and delete the word
    using `dw`.
6.  Undo the deletion using `u`.
7.  Copy the line containing `Course` using `yy`.
8.  Paste it below using `p`.
9.  Search for `Linux` using `/Linux`.
10. Replace `Rahul` with your own name using `:%s/Rahul/YourName/g`.
11. Show line numbers using `:set number`.
12. Save and exit using `:wq`.

Replace `YourName` with your actual name in the replacement command.

## Step 5: Verify the file outside Vim

``` bash
cat student_record.txt
```

Observe the updated file content.

------------------------------------------------------------------------

# 12. Common Beginner Problems and Solutions

  -----------------------------------------------------------------------
  Problem                             Solution
  ----------------------------------- -----------------------------------
  Cannot type text                    Press `i` to enter Insert Mode

  Editing commands are not working    Press `Esc` to return to Normal
                                      Mode

  Cannot exit Vim                     Press `Esc`, then type `:q`

  Changes are not saved               Use `:w`

  Want to exit without saving         Use `:q!`

  Accidentally deleted text           Press `u` to undo

  Search is not working               Use `/word` and press `Enter`

  Cannot find the next match          Press `n`
  -----------------------------------------------------------------------

**Remember:** When confused about the current mode, press `Esc` before
entering a Normal Mode command or a command-line instruction.

------------------------------------------------------------------------

# 13. Practical Assignment

## Task: Create an Employee Record Using Vim

Create a file named `employee.txt` and add at least eight lines of
employee information.

Include:

-   Employee name
-   Employee ID
-   Department
-   Designation
-   Salary
-   Joining date
-   Skills
-   Contact information (use sample data)

### Requirements

1.  Create the file using Vim.
2.  Enter employee information using Insert Mode.
3.  Use navigation shortcuts to move through the file.
4.  Delete one line and undo the operation.
5.  Copy and paste two lines.
6.  Search for a particular word.
7.  Replace one word throughout the file.
8.  Enable line numbers.
9.  Save and exit the file.
10. Verify the content using `cat employee.txt`.

## Evaluation Scheme

  Activity                              Marks
  ---------------------------------- --------
  File creation and text insertion          3
  Navigation shortcuts                      3
  Delete, copy, and paste                   4
  Search and replace                        4
  Undo and redo                             2
  Save and exit                             2
  Viva questions                            2
  **Total**                            **20**

------------------------------------------------------------------------

# 14. Viva Questions

1.  What is Vim?
2.  What is the difference between Vi and Vim?
3.  What is a modal text editor?
4.  What are the four commonly used Vim modes?
5.  What is the purpose of Insert Mode?
6.  What is the difference between `i` and `a`?
7.  What does `dd` do?
8.  What is the difference between `yy` and `p`?
9.  How do you save a file in Vim?
10. How do you exit without saving?
11. What is the difference between `u` and `Ctrl + r`?
12. What is the purpose of `gg` and `G`?
13. How do you search for a word?
14. What is the difference between `v` and `V`?
15. What does `:%s/old/new/g` do?

------------------------------------------------------------------------

# 15. Vim Quick Reference Cheat Sheet

These are the most important shortcuts beginners should remember.

  Category     Shortcut      Purpose
  ------------ ------------- -------------------------
  Mode         `i`           Enter Insert Mode
  Mode         `Esc`         Return to Normal Mode
  Mode         `a`           Append text
  Mode         `o`           Create a new line below
  Navigation   `h j k l`     Left, down, up, right
  Navigation   `gg`          First line
  Navigation   `G`           Last line
  Navigation   `0`           Beginning of line
  Navigation   `$`           End of line
  Navigation   `w`           Next word
  Editing      `x`           Delete character
  Editing      `dd`          Delete line
  Editing      `dw`          Delete word
  Editing      `yy`          Copy line
  Editing      `p`           Paste
  Editing      `u`           Undo
  Editing      `Ctrl + r`    Redo
  Selection    `v`           Character selection
  Selection    `V`           Line selection
  Selection    `Ctrl + v`    Block selection
  Search       `/word`       Search forward
  Search       `n`           Next match
  Search       `N`           Previous match
  Command      `:w`          Save
  Command      `:q`          Quit
  Command      `:wq`         Save and quit
  Command      `:q!`         Quit without saving
  Command      `:%s/a/b/g`   Replace all occurrences

------------------------------------------------------------------------

# 16. Suggested Teaching Flow -- 90 Minutes

  -----------------------------------------------------------------------
  Time                    Topic                   Teaching Method
  ----------------------- ----------------------- -----------------------
  0--5 min                Introduction to Vim     Explain use cases

  5--15 min               Installation and        Live terminal
                          opening Vim             demonstration

  15--30 min              Four Vim modes          Demonstrate each mode

  30--40 min              Navigation shortcuts    Student practice

  40--55 min              Delete, copy, paste,    Live editing
                          undo                    

  55--65 min              Search and replace      Demonstration

  65--75 min              Visual Mode and         Practical exercise
                          formatting              

  75--85 min              Student record          Individual exercise
                          practical               

  85--90 min              Viva and recap          Questions and revision
  -----------------------------------------------------------------------

------------------------------------------------------------------------

## Teaching Recommendation

Do not ask beginners to memorize every shortcut at once. Focus on these
skills first:

1.  Understand the four modes.
2.  Enter and exit Insert Mode.
3.  Navigate through a file.
4.  Delete, copy, and paste text.
5.  Undo and redo changes.
6.  Search and replace words.
7.  Save and exit correctly.

Make every student complete the student-record practical independently.
Hands-on practice is more valuable than memorizing a long shortcut list.

**Next Topic:** Creating and editing Bash Shell Scripts in Ubuntu.
