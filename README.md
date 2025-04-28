

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

# Visual Diagram: **User → Shell → OS → Files (`vi` editor too)**

```
+------------------------------------------------+
|                   USER                         |
| (You typing commands on keyboard)              |
+------------------------------------------------+
                     |
                     v
+------------------------------------------------+
|                   SHELL                        |
| (Reads your commands, passes to OS, shows output) |
+------------------------------------------------+
                     |
                     v
+------------------------------------------------+
|           UNIX OPERATING SYSTEM (OS)           |
| (The heart of the computer: manages hardware, files) |
+------------------------------------------------+
                     |
                     v
+------------------------------------------------+
|                 FILE SYSTEM                    |
| (Where your text files, programs, folders are stored) |
+------------------------------------------------+
```

---

# Where Does `vi` Fit In?

**`vi` is a program that you run through the Shell.**  
It helps you **edit files** in the **File System**.

### So:

1. You **type** `vi file.txt` in the Shell.
2. The **Shell** starts the `vi` editor program.
3. `vi` allows you to **create/edit/save** text files.
4. Files are stored in the **File System**.

**Flow when using `vi`:**

```
You → Shell → Start vi → Edit File → Save to File System
```

---

# Full Example (Real Life Steps)

Let's say you want to write a note on your server:

1. **You open Terminal** (Shell starts automatically).
2. You type:
   ```bash
   vi notes.txt
   ```
   (Shell starts the `vi` editor)

3. Inside `vi`:
   - Press `i` to insert.
   - Write:
     ```
     Meeting at 5 PM today
     ```
   - Press `Esc`, then type `:wq` to save and quit.

4. Now your file **notes.txt** is saved in your system.

**Everything done with simple commands!**

---

# Simple Mind Map

Here’s a mind map view for even quicker memory:

```
USER
  |
  |---> Shell
         |
         |---> Runs commands like:
               |--> vi (edit files)
               |--> ls (list files)
               |--> cd (move directories)
         |
         |---> Sends work to OS
                  |
                  |---> Manages Files, Hardware, System
```

---

# Final Words:

- **Shell**: Your messenger — tells Unix what you want.
- **`vi` editor**: Special tool for editing text files — called from Shell.
- **Unix OS**: The brain that actually does the hard work.
- **Files/Folders**: What you create, edit, manage.

---
  ---
---
----
---
---

🧑🏻‍🎤


# Part 1: What is the Shell Process in Unix?

---

## 1. What is a "Process"?

- A **process** is simply a **program that is running**.
- When you open a program or command, Unix **creates a process**.
- Example:  
  - When you run `vi notes.txt`, the **`vi` editor becomes a process**.
  - When you run `ls`, **listing files becomes a process**.

---

## 2. What is a "Shell Process"?

- The **shell** itself is also a **program**.  
- When you open a **Terminal** (command line), the **shell process starts**.
- This shell waits for your commands.

**Simply:**
- **Shell** is **a special process** that **takes your commands**, **sends them to Unix**, and **shows you the results**.

---

## 3. How the Shell Process Works (Simple Step-by-Step)

Here’s what happens in simple language:

1. **User opens Terminal** → A **Shell Process starts**.
2. **User types a command** (like `ls`).
3. **Shell reads the command**.
4. **Shell creates a new process** for that command.
5. **Unix does the job** (like listing files).
6. **Shell shows the result** on screen.
7. **Shell waits for the next command.**

---

### Diagram View:

```
[User types command] 
       ↓
[Shell reads command]
       ↓
[Shell creates new process to run the command]
       ↓
[Command runs and finishes]
       ↓
[Shell shows output and waits for next command]
```

---

## 4. Types of Processes Started by Shell

There are **two types of processes**:

| Type | Explanation | Example |
|:---|:---|:---|
| **Foreground process** | Runs directly in front; you wait until it finishes. | Running `vi file.txt` |
| **Background process** | Runs in the background; you can keep working while it runs. | Running `backup.sh &` |

**Tip:**  
To run something in the background, you **add `&`** at the end.

Example:

```bash
./long_task.sh &
```

---

## 5. Managing Shell Processes

You can control processes:

| Command | Action |
|:---|:---|
| `ps` | Show all processes |
| `jobs` | Show background jobs |
| `kill PID` | Kill (stop) a process by its PID (Process ID) |
| `fg` | Bring background job to foreground |
| `bg` | Send stopped job to background |

**Example:**
```bash
ps
```
shows a list of running processes.

---

# Part 2: Customizing the Shell Environment

---

## 1. What is the Shell Environment?

- The **Shell Environment** means **settings** that control **how the shell behaves** for you.
- You can **customize** it to:
  - Change how your command prompt looks.
  - Set shortcuts for commands.
  - Set the default editor (`vi` or `nano`).
  - Set your favorite directories or paths.

---
  
## 2. Environment Variables

- **Environment Variables** are **like settings** stored inside the shell.
- They control things like:
  - Where programs are found.
  - Your username.
  - Your home directory.
  - Which editor opens by default.

---

### Some Important Environment Variables:

| Variable | Meaning | Example |
|:---|:---|:---|
| `HOME` | Your home directory | `/home/username` |
| `USER` | Your username | `alex` |
| `PATH` | Where to look for commands | `/usr/bin:/bin:/usr/local/bin` |
| `SHELL` | Which shell you are using | `/bin/bash` |
| `EDITOR` | Default text editor | `vi` or `nano` |

---

## 3. How to See Environment Variables

- To see all environment variables:

```bash
printenv
```
or
```bash
env
```

- To see a specific variable:

```bash
echo $HOME
```

It will show your home directory.

---

## 4. How to Set Environment Variables

If you want to **set a new variable** or **change an existing one**, you can do:

```bash
export VARIABLE_NAME=value
```

Example:

```bash
export EDITOR=vi
```
This sets your default editor to `vi`.

**Note:**  
- This change is **temporary** (only for current Terminal session).

---

## 5. Making Changes Permanent

To make environment changes **permanent**, you have to put them inside special files.

For **bash shell**, these files are:

| File | Purpose |
|:---|:---|
| `~/.bashrc` | Settings for every new terminal window |
| `~/.bash_profile` | Settings for login shell (when you log in) |

You can edit `.bashrc` like this:

```bash
vi ~/.bashrc
```

And add a line like:

```bash
export PATH=$PATH:/home/username/myprograms
```

After saving, apply changes using:

```bash
source ~/.bashrc
```

or simply restart the terminal.

---

## 6. Customizing the Shell Prompt (`PS1`)

You can change **how your terminal prompt looks** using the `PS1` variable.

Example:

```bash
export PS1="[\u@\h \W]$ "
```

- `\u` = username
- `\h` = hostname
- `\W` = current directory

This will show a prompt like:

```
[alex@server Documents]$
```

You can make your prompt colorful and stylish!

---

# Final Simple Diagram: Shell Process + Customizing Environment

```
[User types command]
         ↓
[Shell reads and runs the process]
         ↓
[Process finishes and shell waits]
         ↓
Meanwhile:
         ↓
[User customizes environment using variables like PATH, HOME, EDITOR]
         ↓
[Customization saved in ~/.bashrc or ~/.bash_profile]
```

---

# Very Short Summary

| Topic | Key Point |
|:---|:---|
| **Shell Process** | Shell reads your command, creates a new process, waits for the result. |
| **Customizing Shell** | You can set environment variables (like PATH, EDITOR) to control behavior. Changes are saved in files like `.bashrc`. |

---

# Quick Practice Questions for You (Optional)

1. How to view all environment variables?
2. How to set the default editor to `nano` permanently?
3. How to see your home directory using a shell command?
4. How to send a running process to the background?

  
---
---
---
---
---

🧑🏻‍🎤



---

# What is Shell Programming?

---

- **Shell programming** (also called **Shell scripting**) is the **art of writing a group of Unix commands** into a **text file**.
- Later, you can **run that file** like a small **program**.
- Instead of typing commands one by one every time, you write all commands in a file and **run the file**.  
**It saves time and makes work automatic!**

---

# Why Shell Programming is Useful?

- **Automation**: You don't need to manually type 10–20 commands again and again.
- **Batch Processing**: Do lots of work (copy files, backups, cleanups) with just **one click**.
- **Simple Programming**: Shell programming is much easier than C, Java, or Python.
- **System Administration**: All system admins use shell scripts to manage servers.

---

# Example of What Shell Programming Does

Suppose every morning you:
- Login
- Check disk space
- Check memory
- List today's files

Instead of typing 4 commands every day,  
**you can write a shell script once, and run it every morning with one command!**

---

# How to Create a Shell Program (Step-by-Step)

---

### Step 1: Open a text editor (like `vi`)

Example:

```bash
vi myscript.sh
```

---

### Step 2: Write the script

Inside the file, write:

```bash
#!/bin/bash
# This is a simple shell script

echo "Good Morning!"
date
df -h
free -m
```

**Explanation:**
- `#!/bin/bash` → Tells Unix this is a bash shell script.
- `#` → Anything after `#` is a **comment** (just for information; shell ignores it).
- `echo` → Prints text on screen.
- `date` → Shows current date and time.
- `df -h` → Shows disk space (in human-readable format).
- `free -m` → Shows memory usage (in MB).

---

### Step 3: Save and Exit

- In `vi`, press `Esc`, type `:wq`, and hit Enter.

---

### Step 4: Make the script executable

You must give permission to run the script:

```bash
chmod +x myscript.sh
```

---

### Step 5: Run the script

Now you can run it:

```bash
./myscript.sh
```

**Output will be:**
```
Good Morning!
Tue Apr 29 09:42:15 IST 2025
[Disk space info]
[Memory info]
```

---

# Important Parts of Shell Programming

---

## 1. Comments

- Use `#` to write comments (notes for humans).
- Comments are **ignored by the shell** when running the script.

Example:

```bash
# This script checks the server health
```

---

## 2. Variables

- You can **store data** in variables.

Example:

```bash
name="John"
echo "Hello, $name"
```

- This will print:
```
Hello, John
```

**Important**: No spaces on both sides of `=` when setting a variable.

---

## 3. Taking Input from User

You can **ask user** to enter something:

Example:

```bash
echo "Enter your name:"
read username
echo "Welcome, $username"
```

When you run it:
- It will ask for your name.
- It will welcome you.

---

## 4. Decision Making (if-else)

You can **make decisions** inside scripts.

Example:

```bash
echo "Enter a number:"
read num

if [ $num -gt 10 ]
then
    echo "Number is greater than 10."
else
    echo "Number is 10 or smaller."
fi
```

**Explanation:**
- `-gt` means "greater than."
- `[ ... ]` are needed around the condition.

---

## 5. Loops

You can **repeat things** using loops.

**For loop example:**

```bash
for i in 1 2 3 4 5
do
    echo "Number: $i"
done
```

**Output:**
```
Number: 1
Number: 2
Number: 3
Number: 4
Number: 5
```

**While loop example:**

```bash
count=1
while [ $count -le 5 ]
do
    echo "Count: $count"
    count=$((count + 1))
done
```

This keeps running while `count <= 5`.

---

# Types of Shell Programs (Simple Examples)

---

| Type of Script | What it Does | Example |
|:---|:---|:---|
| Startup script | Runs when the system starts | Launch servers, load settings |
| Backup script | Takes backup of files | Copy important files daily |
| Monitoring script | Watches system health | Check CPU, memory, disk usage |
| Automation script | Repeats tasks automatically | Rename files, send emails |

---

# Real-World Mini Example: Backup Script

Suppose you want to copy your "project" folder every day to a backup folder.

Script:

```bash
#!/bin/bash

cp -r /home/user/project /home/user/backup/project_$(date +%F)
echo "Backup completed at $(date)"
```

- `cp -r` → Copy folder.
- `$(date +%F)` → Current date like `2025-04-29` (nice for naming).
- `echo` → Print message.

Run this script every evening to **automatically backup your project**!

---

# Final Simple Summary

| Concept | Simple Meaning |
|:---|:---|
| **Shell Programming** | Writing many commands into one file to run them together. |
| **Script File** | A text file (like `myscript.sh`) containing your commands. |
| **Variables** | Store and reuse values easily. |
| **If-Else** | Make decisions inside the script. |
| **Loops** | Repeat actions many times. |
| **Automation** | Do big work with one small command. |

---

# Tiny Visual Mindmap:

```
[Shell Programming]
      |
      |-- [Create script file]
      |-- [Write commands]
      |-- [Use variables, if-else, loops]
      |-- [Save and make executable]
      |-- [Run the script]
      |-- [Automate tasks]
```

---

---
---
---
---
---

🧑🏻‍🎤



