# Day 5: Linux File & Directory Management

In Linux, almost everything is treated as a **file**. Learning how to create, read, and delete files & directories is one of the most important skills for every Linux and DevOps engineer.

---

# File Creation - `touch`

## Definition

The `touch` command is used to:

- Create an empty file.
- Update the timestamp of an existing file.

## Syntax

```bash
touch <file_name>
```

## Create a Single File

```bash
touch file1.txt
```

Output

```
file1.txt
```

---

## Create Multiple Files

```bash
touch file1.txt file2.txt file3.txt
```

or

```bash
touch linux{1..10}.txt
```

Output

```
linux1.txt
linux2.txt
linux3.txt
...
linux10.txt
```

---

## Create Files in Different Locations

```bash
touch /mnt/file1.txt /media/file2.txt
```

---

## Verify

```bash
ls
```

---

# Directory Creation - `mkdir`

## Definition

The `mkdir` (Make Directory) command is used to create directories (folders).

## Syntax

```bash
mkdir <directory_name>
```

---

## Create a Single Directory

```bash
mkdir project
```

Output

```
project/
```

---

## Create Multiple Directories

```bash
mkdir demo data practice
```

or

```bash
mkdir {demo,data,practice}
```

Output

```
demo/
data/
practice/
```

---

## Create Multiple Directories Using Numbers

```bash
mkdir session{1..10}
```

Output

```
session1
session2
session3
...
session10
```

---

## Create Directories in Different Locations

```bash
mkdir /root/dir1 /mnt/dir2 /media/dir3
```

---

## Create Nested Directories

```bash
mkdir -p project/backend/java
```

Output

```
project/
└── backend
    └── java
```

The `-p` option creates parent directories automatically if they do not exist.

---

# Remove Command - `rm`

## Definition

The `rm` command is used to delete files and directories.

> **Warning:** Deleted files cannot be recovered easily.

---

## Remove a Single File

```bash
rm file1.txt
```

---

## Remove Multiple Files

```bash
rm file1.txt file2.txt file3.txt
```

---

## Remove All Files Matching a Pattern

```bash
rm linux*
```

Deletes

```
linux1.txt
linux2.txt
linux3.txt
...
```

---

# rm Options

## 1. `rm -f`

### Meaning

`-f` = Force

Deletes files forcefully without asking for confirmation.

Example

```bash
rm -f linux*
```

---

## 2. `rm -r`

### Meaning

`-r` = Recursive

Deletes directories along with everything inside them.

Example

```bash
rm -r project
```

Before

```
project/
├── file1.txt
├── file2.txt
└── images/
```

After

```
project removed
```

---

## 3. `rm -rv`

### Meaning

- `-r` → Recursive
- `-v` → Verbose (shows what is being deleted)

Example

```bash
rm -rv project
```

Output

```
removed 'project/file1.txt'
removed 'project/file2.txt'
removed directory 'project/images'
removed directory 'project'
```

---

## 4. `rm -rvf`

### Meaning

- `-r` → Recursive
- `-v` → Verbose
- `-f` → Force

Deletes everything inside a directory without asking for confirmation while displaying what is being deleted.

Example

```bash
rm -rvf project
```

Output

```
removed 'project/file1.txt'
removed 'project/file2.txt'
removed directory 'project'
```

---

# Remove Empty Directory - `rmdir`

## Definition

The `rmdir` command deletes **only empty directories**.

## Syntax

```bash
rmdir <directory_name>
```

Example

```bash
mkdir demo
rmdir demo
```

---

## Delete Multiple Empty Directories

```bash
rmdir session*
```

Deletes

```
session1
session2
session3
...
```

---

## Difference Between rm and rmdir

| Command | Works On | Can Delete Files? |
|----------|----------|-------------------|
| rmdir | Empty Directory | ❌ No |
| rm | Files | ✅ Yes |
| rm -r | Directory + Files | ✅ Yes |

---

# Read Operation

Reading means viewing the contents of a file without modifying it.

---

# 1. cat

## Definition

Displays the complete content of a file on the terminal.

## Syntax

```bash
cat <file_name>
```

Example

```bash
cat file1.txt
```

Output

```
Hello Linux
Welcome to DevOps
```

---

## Display Multiple Files

```bash
cat file1.txt file2.txt
```

---

# 2. more

## Definition

Displays a file one page at a time.

Navigation is only **downward**.

## Syntax

```bash
more <file_name>
```

Example

```bash
more notes.txt
```

### Shortcut Keys

| Key | Action |
|------|--------|
| Space | Next Page |
| Enter | Next Line |
| q | Quit |

---

# 3. less

## Definition

Similar to `more` but allows both upward and downward navigation.

## Syntax

```bash
less <file_name>
```

Example

```bash
less notes.txt
```

### Shortcut Keys

| Key | Action |
|------|--------|
| Up Arrow | Scroll Up |
| Down Arrow | Scroll Down |
| Page Up | Previous Page |
| Page Down | Next Page |
| q | Quit |

---

# 4. head

## Definition

Displays the first 10 lines of a file.

## Syntax

```bash
head <file_name>
```

Example

```bash
head notes.txt
```

---

## Display First 5 Lines

```bash
head -n 5 notes.txt
```

---

## Display First 15 Lines

```bash
head -n 15 notes.txt
```

---

# 5. tail

## Definition

Displays the last 10 lines of a file.

## Syntax

```bash
tail <file_name>
```

Example

```bash
tail notes.txt
```

---

## Display Last 5 Lines

```bash
tail -n 5 notes.txt
```

---

## Display Last 15 Lines

```bash
tail -n 15 notes.txt
```

---

# 6. sort

## Definition

Sorts the contents of a file alphabetically.

## Syntax

```bash
sort <file_name>
```

Example

File Content

```
Orange
Apple
Banana
Mango
```

Command

```bash
sort fruits.txt
```

Output

```
Apple
Banana
Mango
Orange
```

---

## Reverse Sorting

```bash
sort -r fruits.txt
```

Output

```
Orange
Mango
Banana
Apple
```

---

# Practice Example

## Step 1: Create a Directory

```bash
mkdir project
```

---

## Step 2: Create Files

```bash
touch project/file1.txt
touch project/file2.txt
```

---

## Step 3: View Files

```bash
ls project
```

Output

```
file1.txt
file2.txt
```

---

## Step 4: Delete Directory with Files

```bash
rm -rv project
```

Output

```
removed 'project/file1.txt'
removed 'project/file2.txt'
removed directory 'project'
```

---

# Linux Shortcut Keys

| Shortcut | Description |
|----------|-------------|
| **Tab** | Auto-complete command or filename |
| **Ctrl + C** | Stop the currently running command |
| **Ctrl + Z** | Suspend the running process (move to background) |
| **Ctrl + D** | Logout or exit the current terminal |
| **Ctrl + L** | Clear the terminal screen |
| **history** | Display command history |

---

# Interview Questions

### Q1. What is the difference between `rm` and `rmdir`?

**Answer**

- `rm` deletes files and directories.
- `rmdir` deletes only empty directories.

---

### Q2. What is the purpose of `touch`?

**Answer**

- Creates an empty file.
- Updates the timestamp of an existing file.

---

### Q3. Which command creates parent directories automatically?

**Answer**

```bash
mkdir -p
```

---

### Q4. What does `rm -rvf` mean?

- **-r** → Recursive
- **-v** → Verbose
- **-f** → Force

---

### Q5. Which command allows both upward and downward scrolling?

**Answer**

```bash
less
```

---

### Q6. Which command shows the first 10 lines of a file?

**Answer**

```bash
head
```

---

### Q7. Which command shows the last 10 lines?

**Answer**

```bash
tail
```

---

### Q8. Which command sorts file contents alphabetically?

**Answer**

```bash
sort
```

---

# Summary

| Command | Purpose |
|----------|----------|
| touch | Create file |
| mkdir | Create directory |
| mkdir -p | Create nested directories |
| rm | Delete file |
| rm -f | Force delete |
| rm -r | Delete directory recursively |
| rm -rv | Recursive delete with output |
| rm -rvf | Recursive + Verbose + Force |
| rmdir | Delete empty directory |
| cat | View complete file |
| more | View file page by page (down only) |
| less | View file with up/down navigation |
| head | First 10 lines |
| tail | Last 10 lines |
| sort | Sort file alphabetically |
