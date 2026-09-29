# Day 11 - Managing Permissions in Linux

## Learning Objectives


- Understand Linux file permissions
- Read and interpret permission strings
- Change permissions using Symbolic Mode
- Change permissions using Numeric (Octal) Mode
- Manage permissions for files and directories
- Understand Linux file types
- Understand the sudoers file

---

# Why Do We Need File Permissions?

Linux is a **multi-user operating system**.

Many users can use the same system simultaneously. To protect files and system resources, Linux uses **permissions**.

Permissions answer three questions:

- Who can view the file?
- Who can modify the file?
- Who can execute the file?

Without permissions:

- Anyone could delete important files.
- Anyone could modify application data.
- Anyone could access confidential information.

---

# Importance of File Permissions

## 1. System Security

Prevent unauthorized users from accessing files.

Example:

Only HR employees should access employee salary data.

---

## 2. Data Integrity

Only authorized users should modify important files.

Example:

Developers should not accidentally modify production configuration files.

---

## 3. System Stability

Critical Linux system files should not be modified by normal users.

Example:

```
/etc/passwd
/etc/shadow
```

---

# Viewing Permissions

Use:

```bash
ls -l
```

Example:

```bash
-rwxr-xr-- 1 labex developers 1200 Jul 30 10:00 demo.sh
```

Let's understand each field.

| Field | Meaning |
|--------|---------|
| - | File Type |
| rwx | Owner Permission |
| r-x | Group Permission |
| r-- | Others Permission |
| 1 | Hard Link Count |
| labex | Owner |
| developers | Group |
| 1200 | File Size |
| Jul 30 10:00 | Last Modified |
| demo.sh | File Name |

---

# Understanding rwx

Linux permissions consist of three permissions.

| Permission | Symbol | Value |
|------------|--------|------|
| Read | r | 4 |
| Write | w | 2 |
| Execute | x | 1 |

---

# Permission Categories

Linux divides permissions into three categories.

| Category | Symbol | Description |
|-----------|--------|-------------|
| User | u | File Owner |
| Group | g | Group Members |
| Others | o | Everyone Else |

Example

```
rwx r-x r--
```

Owner

```
rwx
```

Group

```
r-x
```

Others

```
r--
```

---

# Understanding File Permissions

| Permission | Meaning |
|------------|----------|
| r | Read file contents |
| w | Modify file |
| x | Execute the file |

Example

```
script.sh
```

Permission

```
rwx
```

Owner can

- Read
- Edit
- Execute

---

# Understanding Directory Permissions

Directory permissions are different from file permissions.

| Permission | Meaning |
|------------|----------|
| r | List files inside directory |
| w | Create/Delete/Rename files |
| x | Enter directory (cd) |

Example

```bash
cd project
```

Requires

```
x permission
```

Example

```bash
ls project
```

Requires

```
r permission
```

Example

```bash
touch project/file1
```

Requires

```
w + x permission
```

> **Important:** Write permission on a directory is usually useful only when Execute (`x`) permission is also available.

---

# Permission Summary

| Permission | File | Directory |
|------------|------|-----------|
| Read | Read contents | List files |
| Write | Modify file | Create/Delete/Rename files |
| Execute | Run file | Enter directory |

---

# Default Permissions

## File

```
666
```


## Directory

```
777
```

---

# Changing Permissions (Symbolic Mode)

## Syntax

```bash
chmod [ugoa][+-=][rwx] file
```

Symbols

| Symbol | Meaning |
|---------|----------|
| u | User |
| g | Group |
| o | Others |
| a | All |
| + | Add Permission |
| - | Remove Permission |
| = | Assign Permission |

---

## Examples

Add execute permission to owner

```bash
chmod u+x script.sh
```

Remove write permission from group

```bash
chmod g-w file.txt
```

Remove read permission from others

```bash
chmod o-r file.txt
```

Give execute permission to everyone

```bash
chmod a+x script.sh
```

Assign only read permission to group

```bash
chmod g=r file.txt
```

Assign full permission to owner

```bash
chmod u=rwx file.txt
```

---

# Multiple Permission Changes

Example

```bash
chmod g+rwx,o+r demo.txt
```

Meaning

- Group → Read Write Execute
- Others → Read

---

Example

```bash
chmod g-x,o-wx demo.txt
```

Meaning

- Remove execute from group
- Remove write and execute from others

---

# Recursive Permission Change

Used for directories.

```bash
chmod -R 755 project
```

Changes permission of

- Directory
- Subdirectories
- Files

---

# Numeric (Octal) Method

Each permission has a value.

| Permission | Value |
|------------|------|
| r | 4 |
| w | 2 |
| x | 1 |

Example

```
rwx
```

```
4+2+1=7
```

Example

```
rw-
```

```
4+2=6
```

Example

```
r-x
```

```
4+1=5
```

---

# Octal Table

| Number | Permission |
|----------|------------|
|0|---|
|1|--x|
|2|-w-|
|3|-wx|
|4|r--|
|5|r-x|
|6|rw-|
|7|rwx|

---

# Examples

```
777
```

```
rwx rwx rwx
```

---

```
755
```

```
rwx r-x r-x
```

---

```
644
```

```
rw- r-- r--
```

---

```
600
```

```
rw-------
```

---

# Ownership Commands

## Change Owner

```bash
sudo chown user file.txt
```

Example

```bash
sudo chown student1 notes.txt
```

---

## Change Group

```bash
sudo chgrp developers file.txt
```

---

## Change Owner and Group Together

```bash
sudo chown student1:developers notes.txt
```

---


## Introduction to File Types in Linux

Linux files are categorized based on their purpose and usage.

### File Types Shown by `ls -l`

#### User Defined Files
- **Regular File (-)** → Normal file
- **Directory (d)** → Folder
- **Symbolic Link (l)** → Shortcut to another file

#### System Defined Files
- **Socket (s)** → Inter-process communication
- **Pipe (p)** → Data flow between processes
- **Block Device (b)** → Storage devices (HDD)
- **Character Device (c)** → Input devices (keyboard)
---

# Understanding sudo

## What is sudo?

sudo means

```
Super User Do
```

It allows a normal user to execute commands with root privileges.

Example

```bash
sudo apt update
```

---

# sudoers File

Location

```bash
/etc/sudoers
```

Never edit directly.

Always use

```bash
sudo visudo
```

---

## Format

```
user host=(run_as_user) command
```

---

## Example

```
labex ALL=(ALL) ALL
```

Meaning

- User = labex
- Host = Any
- Run As = Any User
- Commands = All Commands

---

Passwordless sudo

```
student1 ALL=(ALL) NOPASSWD: ALL
```

---

# Demo

Create User

```bash
sudo useradd -m student1
```

Set Password

```bash
sudo passwd student1
```

Check User

```bash
id student1
```

Switch User

```bash
su - student1
```

Try Root Directory

```bash
sudo ls /root
```

Initially

```
student1 is not in the sudoers file
```

Now add

```
student1 ALL=(ALL) ALL
```

using

```bash
sudo visudo
```

Again

```bash
sudo ls /root
```

Now it works.

---
