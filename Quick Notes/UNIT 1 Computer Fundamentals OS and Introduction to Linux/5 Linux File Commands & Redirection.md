# Linux File Commands & Redirection

> **Topic:** Working with Files in Terminal
> **Level:** Beginner
> **Platform:** Linux / Ubuntu

---

## 1. Learning Objectives

After completing this topic, you should be able to:

* Read files using `cat` and `less`
* Display the beginning of a file using `head`
* Display the end of a file using `tail`
* Print text using `echo`
* Create files using redirection
* Understand `>`, `>>`, and `<`
* Write content into files from the terminal
* Append new content without deleting existing content
* Combine commands using redirection

---

# 2. Why Do We Need These Commands?

In Linux, we frequently work with files directly from the terminal.

For example:

```text
Create a file
      ↓
Write data
      ↓
Read data
      ↓
Add more data
      ↓
Check beginning/end of file
```

Instead of opening a graphical text editor every time, we can perform all these operations directly from the terminal.

---

# 3. `cat` Command

`cat` stands for **concatenate**.

It is commonly used to:

* Display file contents
* Create a file
* Combine files
* Append/redirect content

## 3.1 Display File Content

Suppose we have:

```text
student.txt
```

Run:

```bash
cat student.txt
```

Output:

```text
Akash
Rahul
Priya
```

---

## 3.2 Create a File Using `cat`

```bash
cat > student.txt
```

Now type:

```text
Akash
Rahul
Priya
```

Press:

```text
Ctrl + D
```

`Ctrl + D` tells the terminal that you have finished entering input.

Now:

```bash
cat student.txt
```

Output:

```text
Akash
Rahul
Priya
```

---

## 3.3 Append Using `cat`

Use `>>` instead of `>`:

```bash
cat >> student.txt
```

Now type:

```text
Aman
Riya
```

Press:

```text
Ctrl + D
```

Check the file:

```bash
cat student.txt
```

Output:

```text
Akash
Rahul
Priya
Aman
Riya
```

---

# 4. `less` Command

`less` is used to **view large files page by page**.

```bash
less file.txt
```

For example:

```bash
less student.txt
```

Unlike `cat`, `less` does not print the entire file at once.

This is especially useful for:

* Large text files
* Log files
* Configuration files
* System information

---

## 4.1 Important `less` Keys

While inside `less`:

| Key     | Action             |
| ------- | ------------------ |
| `↑`     | Move up            |
| `↓`     | Move down          |
| `Space` | Next page          |
| `b`     | Previous page      |
| `/word` | Search for word    |
| `n`     | Next search result |
| `q`     | Quit               |

### Example

```bash
less /var/log/syslog
```

Press:

```text
q
```

to exit.

---

# 5. `head` Command

`head` displays the **beginning of a file**.

```bash
head file.txt
```

By default, it displays the first **10 lines**.

---

## 5.1 Display First 5 Lines

```bash
head -n 5 file.txt
```

or:

```bash
head -5 file.txt
```

Both work.

---

## 5.2 Example

Suppose:

```text
numbers.txt
```

contains:

```text
1
2
3
4
5
6
7
8
9
10
11
12
```

Run:

```bash
head -n 5 numbers.txt
```

Output:

```text
1
2
3
4
5
```

---

# 6. `tail` Command

`tail` displays the **end of a file**.

```bash
tail file.txt
```

By default, it displays the last **10 lines**.

---

## 6.1 Display Last 5 Lines

```bash
tail -n 5 file.txt
```

or:

```bash
tail -5 file.txt
```

---

## 6.2 Example

```bash
tail -n 3 numbers.txt
```

Output:

```text
10
11
12
```

---

# 7. `tail -f`

One very useful option of `tail` is:

```bash
tail -f file.txt
```

`-f` means **follow**.

It continuously watches the file for new content.

This is commonly used for **log files**.

For example:

```bash
tail -f application.log
```

If another program adds a new line to the log, you can see it immediately.

Press:

```text
Ctrl + C
```

to stop following the file.

---

# 8. `echo` Command

`echo` is used to **print text to the terminal**.

```bash
echo "Hello Linux"
```

Output:

```text
Hello Linux
```

---

## 8.1 Echo with Variables

```bash
name="Akash"
echo $name
```

Output:

```text
Akash
```

Here:

```text
$name
```

means the value stored inside the variable `name`.

---

# 9. Using `echo` to Create a File

We can redirect the output of `echo` into a file.

```bash
echo "Hello Linux" > hello.txt
```

Now:

```bash
cat hello.txt
```

Output:

```text
Hello Linux
```

---

# 10. Redirection

Linux allows us to redirect the input/output of commands.

Normally:

```text
Command
   ↓
Terminal
```

With redirection:

```text
Command
   ↓
File
```

For example:

```bash
echo "Hello" > file.txt
```

The output goes into:

```text
file.txt
```

instead of being displayed on the terminal.

---

# 11. `>` Operator

`>` is called the **output redirection operator**.

It sends command output into a file.

### Example

```bash
echo "Hello" > file.txt
```

Now:

```bash
cat file.txt
```

Output:

```text
Hello
```

---

## ⚠️ Important: `>` Overwrites

Suppose the file contains:

```text
Hello
```

Now run:

```bash
echo "Linux" > file.txt
```

The previous content is replaced.

Now:

```bash
cat file.txt
```

Output:

```text
Linux
```

So remember:

```text
>  → Create / overwrite
```

---

# 12. `>>` Operator

`>>` is used to **append** output to a file.

Append means:

> Add new content at the end without deleting existing content.

Example:

```bash
echo "Hello" > file.txt
```

Then:

```bash
echo "Linux" >> file.txt
```

Now:

```bash
cat file.txt
```

Output:

```text
Hello
Linux
```

Remember:

```text
>   → Overwrite
>>  → Append
```

---

# 13. Difference Between `>` and `>>`

| Operator | Meaning         | Existing Content |
| -------- | --------------- | ---------------- |
| `>`      | Redirect output | Replaced         |
| `>>`     | Append output   | Preserved        |

### Example

```bash
echo "A" > test.txt
echo "B" > test.txt
```

Result:

```text
B
```

But:

```bash
echo "A" > test.txt
echo "B" >> test.txt
```

Result:

```text
A
B
```

---

# 14. `<` Input Redirection

`<` is called **input redirection**.

It takes input from a file and gives it to a command.

General syntax:

```bash
command < file
```

For example:

```bash
cat < student.txt
```

This tells Linux:

```text
student.txt
     ↓
   input
     ↓
    cat
     ↓
  terminal
```

The result is the same as:

```bash
cat student.txt
```

---

# 15. Understanding `<` with `wc`

`wc` can count lines, words, and characters.

For example:

```bash
wc -l student.txt
```

Now using input redirection:

```bash
wc -l < student.txt
```

The file provides input to `wc`.

### Important Difference

```bash
wc -l student.txt
```

may display:

```text
5 student.txt
```

while:

```bash
wc -l < student.txt
```

may display only:

```text
5
```

Because the filename itself was not passed as a command-line argument; the file was provided through standard input.

---

# 16. Standard Input and Output

Linux commands generally work with three standard streams:

```text
             Linux Command
            /      |       \
           /       |        \
          ↓        ↓         ↓
       stdin    stdout    stderr
       input    output     error
```

### Standard Input

```text
stdin
```

Usually comes from the keyboard.

### Standard Output

```text
stdout
```

Usually goes to the terminal.

### Standard Error

```text
stderr
```

Used for error messages.

For this topic, focus mainly on:

```text
stdin  → <
stdout → > and >>
```

---

# 17. Hands-on Practice

Let's create a student file.

## Step 1: Create File

```bash
touch students.txt
```

Check:

```bash
ls
```

---

## Step 2: Write First Line

```bash
echo "Akash" > students.txt
```

---

## Step 3: Append More Students

```bash
echo "Rahul" >> students.txt
echo "Priya" >> students.txt
echo "Aman" >> students.txt
```

---

## Step 4: Read File

```bash
cat students.txt
```

Output:

```text
Akash
Rahul
Priya
Aman
```

---

## Step 5: View First 2 Lines

```bash
head -n 2 students.txt
```

Output:

```text
Akash
Rahul
```

---

## Step 6: View Last 2 Lines

```bash
tail -n 2 students.txt
```

Output:

```text
Priya
Aman
```

---

# 18. Practical Example: Creating a Log File

Create a log:

```bash
echo "Application started" > app.log
```

Append more logs:

```bash
echo "Database connected" >> app.log
echo "User logged in" >> app.log
echo "Application stopped" >> app.log
```

Read it:

```bash
cat app.log
```

View the latest entries:

```bash
tail app.log
```

For a continuously running log:

```bash
tail -f app.log
```

---

# 19. Combining Commands

Linux commands become more powerful when combined.

For example:

```bash
cat students.txt | less
```

This sends the output of `cat` to `less`.

However, for simply viewing a large file, you can directly use:

```bash
less students.txt
```

The important idea is:

```text
Command 1
   ↓
Output
   ↓
Command 2
```

This concept will become more important when learning **pipes (`|`)**.

---

# 20. Quick Command Cheat Sheet

| Command                    | Purpose                |
| -------------------------- | ---------------------- |
| `cat file.txt`             | Display complete file  |
| `cat > file.txt`           | Create/write file      |
| `cat >> file.txt`          | Append to file         |
| `less file.txt`            | View file page by page |
| `head file.txt`            | First 10 lines         |
| `head -n 5 file.txt`       | First 5 lines          |
| `tail file.txt`            | Last 10 lines          |
| `tail -n 5 file.txt`       | Last 5 lines           |
| `tail -f file.txt`         | Follow new content     |
| `echo "Hello"`             | Print text             |
| `echo "Hello" > file.txt`  | Write/overwrite        |
| `echo "Hello" >> file.txt` | Append                 |
| `cat < file.txt`           | Input redirection      |

---

# 21. Remember This

The easiest way to remember the redirection operators:

```text
>   = PUT output into file
>>  = PUT output at END of file
<   = TAKE input FROM file
```

Or:

```text
          > 
Command ───────→ File
          output


          >>
Command ───────→ File
          append


          <
File ──────────→ Command
          input
```

---

# 22. Assignment

## Assignment 1 — Student File

Create a file:

```text
students.txt
```

Requirements:

1. Add at least 5 student names.
2. Use `>` for the first entry.
3. Use `>>` for the remaining entries.
4. Display the complete file using `cat`.
5. Display the first 3 students using `head`.
6. Display the last 2 students using `tail`.

**Do not use a graphical text editor.**

---

## Assignment 2 — My Linux Notes

Create a file:

```text
linux-notes.txt
```

Using only terminal commands:

1. Add a title.
2. Add at least 5 Linux commands and their purpose.
3. Append at least 3 more commands later.
4. Display the complete file.
5. Display only the first 5 lines.
6. Display only the last 5 lines.
7. Open the file using `less` and navigate through it.

### Challenge

Try creating the file using:

```bash
cat > linux-notes.txt
```

instead of `nano`.

---

## Assignment 3 — Application Log

Create:

```text
application.log
```

Simulate an application's log using `echo`.

Your file should contain events such as:

```text
Application started
Database connected
User logged in
File uploaded
User logged out
Application stopped
```

Requirements:

1. Create the first log entry using `>`.
2. Add all other entries using `>>`.
3. Display the complete log using `cat`.
4. Display the first 3 entries using `head`.
5. Display the last 3 entries using `tail`.
6. Use `less` to inspect the log.
7. Use `tail -f` and observe how it works.

### Challenge

Keep:

```bash
tail -f application.log
```

running in one terminal.

Open another terminal and append a new log:

```bash
echo "New user registered" >> application.log
```

Observe what happens in the first terminal.

---

# 23. Final Practice

Try to understand this complete flow:

```text
                FILE
                 ↑
                 |
        ┌────────┴────────┐
        |                 |
       > / >>             |
        |                 |
     Write/Append         |
                          |
                          ↓
                       Read
                    /    |    \
                  cat   less  head/tail
                          
              < 
              ↑
          Input from
             file
```

Once you understand this, you have the basic foundation for **Linux file handling and I/O redirection**.
