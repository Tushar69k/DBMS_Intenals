

## What are File Attributes?
In Unix (and Linux), **file attributes** are special properties or settings that control how files behave. They tell the system and users **what can be done** with the file — like who can read it, who can write to it, and who can execute (run) it.

---

## The Basic File Attributes
When you list files in a directory using `ls -l`, you see something like this:

```
-rw-r--r-- 1 user group 4096 Apr 29 09:00 example.txt
```

Let’s understand this part-by-part:

### 1. **File Type and Permissions (`-rw-r--r--`)**
This is **10 characters** long:

- **First character** shows the **type of file**:
  - `-` : Regular file (like a document or program)
  - `d` : Directory (folder)
  - `l` : Link (shortcut to another file)
  - `c` : Character device (for hardware like keyboard)
  - `b` : Block device (for storage like hard disk)

- **Next 9 characters** are **permissions**, divided into 3 sets:
  - First 3 characters (`rw-`) = permissions for **Owner** (the person who created the file)
  - Next 3 (`r--`) = permissions for **Group** (a set of users)
  - Last 3 (`r--`) = permissions for **Others** (everyone else)

Each character means:
  - `r` = read (can open/view the file)
  - `w` = write (can edit or delete the file)
  - `x` = execute (can run the file if it’s a program)
  - `-` = no permission

**Example:**  
`rw-` = read and write allowed, but not execute.

---

### 2. **Number of Links (`1`)**
This shows **how many links** point to this file. (Think of it like "shortcuts" to the file.)

---

### 3. **Owner Name (`user`)**
This shows the **username** of the person who owns the file.

---

### 4. **Group Name (`group`)**
This shows the **group name** that the file belongs to. Groups allow you to manage permissions for multiple users easily.

---

### 5. **File Size (`4096`)**
This is the **size of the file in bytes**.

---

### 6. **Last Modified Date and Time (`Apr 29 09:00`)**
This shows **when the file was last edited**.

---

### 7. **File Name (`example.txt`)**
Finally, the name of the file!

---

## Special Attributes (Advanced but easy to understand)
Unix also allows **special file attributes** that change behavior beyond normal permissions. You can set them using `chattr` command.

Examples:
- **i (immutable)**: You **cannot modify, delete, or rename** the file if this is set.
- **a (append-only)**: You can **only add** to the file, not remove anything.
- **t (no tail-merging)**: Used in specific filesystems to protect file contents.

You can check special attributes using `lsattr` command.

---

## Quick Summary
| Part | Meaning |
|:----|:------|
| `-` | Type of file |
| `rw-` | Owner can read and write |
| `r--` | Group can only read |
| `r--` | Others can only read |
| `1` | Number of links |
| `user` | Owner of file |
| `group` | Group of file |
| `4096` | File size in bytes |
| `Apr 29 09:00` | Last modified time |
| `example.txt` | File name |

---
---
---
---
---
---
---
---
---

🧑🏻‍🎤


# Filters in Unix (Detailed and Simple)

---

## What is a Filter?

In Unix, a **filter** is a **program that takes some data (input), does something to it (processing), and gives back the result (output)**.

- **Input** → **Filter** → **Output**

Just like a **water filter**:
- Dirty water goes in → Clean water comes out.

In Unix:
- Raw data (input) goes into a filter → Processed or cleaned data comes out.

---

## Why are Filters Useful?

- **They save time** — No need to edit files manually.
- **They work automatically** — They handle very big files quickly.
- **They can be combined** — You can use many filters together to do complex tasks easily.
- **They are simple** — Each filter does one small job, very well.

---

## How do Filters Work in Unix?

Filters **usually**:

- Read data from **Standard Input** (like from a file or another command).
- Write the processed result to **Standard Output** (like your screen or another command).

**Standard Input** = Where the command gets its data from.  
**Standard Output** = Where the command sends the result.

You can also **connect** filters using a **pipe (`|`)** symbol.  
This passes the output of one command **directly into** another command.

Example:

```bash
cat data.txt | sort | uniq
```

- `cat` reads the file
- `sort` arranges the lines
- `uniq` removes repeated lines

Each filter works one after another, automatically!

---

## Some Important Unix Filters (Explained Very Simply)

Let’s go through some of the **most used filters**:

| Filter | What it does | Easy Example |
|:---|:---|:---|
| `cat` | Shows the content of a file | `cat file.txt` shows all lines in the file |
| `sort` | Sorts lines alphabetically or numerically | `sort names.txt` sorts the names A-Z |
| `uniq` | Removes repeated lines | `uniq sorted_names.txt` removes duplicate names |
| `wc` | Counts lines, words, and characters | `wc file.txt` tells you how big the file is |
| `grep` | Searches for specific words or patterns | `grep "apple" fruits.txt` finds all lines with "apple" |
| `cut` | Cuts out sections (columns) from a file | `cut -d',' -f1 data.csv` shows only the first column (before the comma) |
| `tr` | Changes or replaces characters | `tr a-z A-Z` changes all small letters to capital |
| `head` | Shows the first few lines of a file | `head file.txt` shows first 10 lines |
| `tail` | Shows the last few lines of a file | `tail file.txt` shows last 10 lines |

---

### Let's see a few filters in action with examples:

1. **`cat`** – View a file:

```bash
cat groceries.txt
```
Output:
```
milk
bread
apple
apple
banana
milk
```

---

2. **`sort`** – Sort the list:

```bash
sort groceries.txt
```
Output:
```
apple
apple
banana
bread
milk
milk
```

---

3. **`uniq`** – Remove duplicates:

**First**, you should sort before using `uniq`!

```bash
sort groceries.txt | uniq
```
Output:
```
apple
banana
bread
milk
```

---

4. **`grep`** – Find specific word:

```bash
grep "milk" groceries.txt
```
Output:
```
milk
milk
```

---

5. **`wc`** – Count lines, words, characters:

```bash
wc groceries.txt
```
Output:
```
6  6  33 groceries.txt
```
Here:
- `6` = number of lines
- `6` = number of words
- `33` = number of characters

---

6. **Using multiple filters together:**

Suppose you want to:
- Find all "apple" entries
- Sort them
- Remove duplicates

You can use:

```bash
grep "apple" groceries.txt | sort | uniq
```
This will:
- Search for "apple"
- Sort them
- Remove any repeated "apple" lines

---

## Key Concepts to Remember

| Term | Simple meaning |
|:---|:---|
| **Input** | Data going into the filter |
| **Processing** | What the filter does to the data |
| **Output** | The result after filtering |
| **Pipe (`|`)** | Sends output from one command as input to another |

---

# Final Example - Big Picture

Suppose you have a **huge log file** from a server (server_logs.txt) and you want to:

- Find all lines containing "error"
- Sort those lines
- Remove duplicate error messages
- Count how many different errors happened

You could write:

```bash
grep "error" server_logs.txt | sort | uniq | wc -l
```

This entire line uses **four filters**, linked together with pipes, to quickly and easily get the answer.

---

# Summary

- **Filters** take input → process it → give output.
- Filters can be **combined** using pipes (`|`) to create powerful tools.
- Some common filters are `cat`, `sort`, `uniq`, `grep`, `wc`, `cut`, `tr`, `head`, `tail`.
- They make Unix very powerful and flexible for handling text and data.

---
---
---
---
---
---

🧑🏻‍🎤



#  The `vi` Editor in Unix (Detailed and Simple)

---

## What is `vi`?

- `vi` stands for "**Visual Editor**."
- It is a **text editor** — a tool to **create**, **edit**, and **save** text files.
- It is very **popular** because:
  - It is **always available** on Unix/Linux systems.
  - It is **fast**, even on old computers.
  - It uses only the **keyboard**, not the mouse.

**Example:**  
If you want to write a program in Unix or change a system file, you often use `vi`.

---

## Two Main Modes in `vi`

**Important:** `vi` has two working styles, called **modes**:

| Mode | Purpose | What you do |
|:---|:---|:---|
| **Command Mode** | Give commands (save, delete, move) | Not writing text, only controlling |
| **Insert Mode** | Write text | You can type like in Notepad |

**At start:**  
- When you open `vi`, you are in **Command Mode**.
- You must **press `i`** to **go into Insert Mode** to start typing.

---

## How to Open and Create Files with `vi`

If you want to **open a file** or **create a new one**, type:

```bash
vi filename.txt
```

- If the file exists, it opens it.
- If it doesn’t exist, `vi` creates a new file.

---

## Moving Around in `vi`

In **Command Mode** (after pressing `Esc`):

| Key | Action |
|:---|:---|
| `h` | Move cursor left |
| `l` | Move cursor right |
| `j` | Move cursor down |
| `k` | Move cursor up |

You **navigate** the file using just the keyboard.

---

## Important Commands in `vi`

| Action | Command | Meaning |
|:---|:---|:---|
| Start typing | Press `i` | Go into Insert Mode |
| Save file | Press `Esc`, then type `:w` | Write (save) the file |
| Quit `vi` | Press `Esc`, then type `:q` | Quit (only if no changes) |
| Save and quit | Press `Esc`, then type `:wq` | Save and exit |
| Quit without saving | Press `Esc`, then type `:q!` | Force quit without saving |
| Delete a line | In Command Mode, type `dd` | Deletes the whole line |
| Copy a line | In Command Mode, type `yy` | Copies (yanks) a line |
| Paste copied line | In Command Mode, type `p` | Pastes below the cursor |
| Search for text | In Command Mode, type `/word` | Finds "word" in the file |

---

## Example of Full Work

Suppose you want to create a new file and write something:

1. Open `vi`:
   ```bash
   vi hello.txt
   ```

2. Press `i` to **start typing**.

3. Type your text:
   ```
   This is my first vi file.
   ```

4. Press `Esc` to **stop typing** (back to Command Mode).

5. Save and quit:
   - Type `:wq`
   - Press `Enter`

**Done!** You just created and saved a file with `vi`.

---

## Why is `vi` Powerful?

- It is **always available**.
- It **uses less memory** (works on old computers too).
- It is **super fast** once you practice.

Even today, many professionals use `vi` because it’s very efficient for coding and server management.

---

# The Unix Shell (Detailed and Simple)

---

## What is a Shell?

- A **shell** is a **program** that **connects you** (the user) with the **Unix operating system**.
- You **type commands**, and the shell **runs them**.
- The shell **shows the results** on your screen.

Think of the Shell as:
- **Your assistant**: You give an order → The assistant does it.

---

## How Shell Works (Easy View)

1. You type a command like `ls`.
2. Shell sends this command to the Unix system.
3. Unix executes the command.
4. Shell shows the output to you.

---

## Popular Shell Types

| Shell Name | Details |
|:---|:---|
| **sh** | The original shell (Bourne Shell) |
| **bash** | Improved shell (Bourne Again SHell) — Most common today |
| **csh** | C Shell, looks like the C programming language |
| **ksh** | Korn Shell, very powerful for scripting |

**Most people today use `bash` shell** because it is simple and powerful.

---

## Common Shell Commands

You can **do many things** using shell commands:

| Command | Action |
|:---|:---|
| `pwd` | Show current location (directory) |
| `ls` | List files and folders |
| `cd foldername` | Move into another folder |
| `mkdir newfolder` | Create a new folder |
| `rmdir foldername` | Remove (empty) folder |
| `rm filename` | Remove a file |
| `cp oldfile newfile` | Copy a file |
| `mv oldfile newfile` | Move or rename a file |
| `cat file.txt` | Display file content |
| `echo "Hello"` | Show text on screen |

---

## More About Shell

The shell is **not just for running simple commands** — it can also **run scripts**.

---

### What is a Shell Script?

- A **Shell Script** is a **file that contains many shell commands**.
- Instead of typing commands one-by-one, you **put them into a script file** and **run it**.

Example:

**1. Create a file named `myscript.sh`**:

```bash
vi myscript.sh
```

**2. Inside, write:**
```bash
#!/bin/bash
echo "Hello, World!"
date
ls
```

**3. Save and exit (`:wq`).**

**4. Make the script executable:**
```bash
chmod +x myscript.sh
```

**5. Run the script:**
```bash
./myscript.sh
```

**Output will be:**
```
Hello, World!
[shows current date and time]
[list of files]
```

---

## Shell Environment Variables

Shell uses **variables** to store temporary data:

| Variable | What it Stores |
|:---|:---|
| `HOME` | Your home directory location |
| `PATH` | Where the system looks for programs |
| `USER` | Your username |

You can see them using:

```bash
echo $HOME
```
or
```bash
echo $USER
```

---

## Why Shell is Very Important

- **Automate work** (scripting).
- **Manage files and system** easily.
- **Control servers** remotely.
- **Customize** your Unix/Linux environment.

Without shell, using Unix would be very slow and difficult!

---

# Final Summary (Cheat Sheet)

| Topic | Summary |
|:---|:---|
| **vi Editor** | Tool to create, edit, save files. Two modes: Command and Insert. Commands like `:wq`, `dd`, `/search`, `yy`, `p`. |
| **Shell** | Program that runs your commands and shows results. You can create folders, files, run programs, or automate tasks. |
| **Shell Scripting** | Writing many commands inside a file and running it automatically. |

---

# A Small Real World Example:

Suppose you are working on a server:

1. You use the **shell** to log in and check server status.
2. You open configuration files using **vi editor** to make changes.
3. You write a **shell script** to backup files every night automatically.

This is how Unix/Linux admins work every day!

---

