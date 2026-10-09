# Day 12: Links, Ownership, and sudo in Linux

## Learning Objectives

After completing this lesson, you will be able to:

- Understand what an inode is
- Understand link count
- Differentiate between Hard Links and Soft Links
- Create and verify links
- Change ownership using `chown`
- Understand privilege escalation using `sudo`
- Configure sudo access safely

---

# Understanding Inodes

Every file and directory in Linux has a unique **inode**.

An inode stores the metadata of a file, such as:

- File owner
- Group
- File permissions
- File size
- Creation/Modification time
- Link count
- Location of the data blocks on disk

> **Note:** The inode does **not** store the file name. The filename is simply an entry that points to an inode.

---

## View Inode Number

```bash
ls -li
```

Example:

```text
206911876 -rw-r--r-- 1 labex labex 15 Jul 30 10:00 file1.txt
```

Here,

- **206911876** → Inode Number
- **1** → Link Count

You can also view detailed inode information:

```bash
stat file1.txt
```

---

# What is Link Count?

The **link count** is the number of directory entries (names) pointing to the same inode.

Think of it like this:

```
One House (Inode)
      ▲
      │
 ┌────┴────┐
 │         │
Name1   Name2
```

Both names refer to the same file.

---

# Link Count for Files

A newly created file has a link count of **1** because it has only one name.

Example:

```bash
touch file1.txt
ls -li file1.txt
```

Output:

```text
206911876 -rw-r--r-- 1 labex labex 0 Jul 30 10:00 file1.txt
```

Link count = **1**

---

# Link Count for Directories

Every directory starts with **2 links**:

- `.` → Current directory
- `..` → Parent directory

Each **subdirectory** increases the parent directory's link count by **1**.

---

## Example

```bash
mkdir dir1
ls -ld dir1
```

Output:

```text
drwxr-xr-x 2 labex labex 4096 Jul 30 10:00 dir1
```

Link count = **2**

Now create a subdirectory:

```bash
mkdir dir1/subdir1
ls -ld dir1
```

Output:

```text
drwxr-xr-x 3 labex labex 4096 Jul 30 10:05 dir1
```

The link count increased to **3** because `subdir1` contains a `..` entry pointing back to `dir1`.

---

# Hard Link vs Soft Link

| Feature | Hard Link | Soft Link |
|---------|-----------|-----------|
| Command | `ln` | `ln -s` |
| Inode | Same | Different |
| Stores | Same inode | Path to original file |
| Link Count | Increases | No change |
| Works Across Filesystems | ❌ No | ✅ Yes |
| Works for Directories | ❌ No | ✅ Yes |
| Delete Original | File remains accessible | Link becomes broken |

---

# What is a Hard Link?

A **hard link** is another name for the **same file**.

Both names point to the **same inode**.

```
file1.txt
      │
      ▼
   Inode 1050
      ▲
      │
hardlink.txt
```

Both names share:

- Same inode
- Same data
- Same permissions
- Same owner

---

## Create a Hard Link

```bash
echo "Hello Linux" > file1.txt
```

Check inode:

```bash
ls -li file1.txt
```

Create a hard link:

```bash
ln file1.txt file1_hard.txt
```

Verify:

```bash
ls -li file1.txt file1_hard.txt
```

Observation:

- Same inode number
- Link count becomes **2**

---

## Modify Through Hard Link

```bash
echo "Hard Link Test" >> file1_hard.txt
```

View original:

```bash
cat file1.txt
```

The changes appear because both names refer to the same file.

---

## Delete Original File

```bash
rm file1.txt
```

Now check:

```bash
cat file1_hard.txt
```

The file still exists because the inode is still referenced by one remaining hard link.

---

# What is a Soft Link?

A **soft link (symbolic link)** is a shortcut that stores the **path** of another file or directory.

```
soft.txt
    │
    ▼
Path → file2.txt
        │
        ▼
      Inode
```

A soft link has its own inode.

---

## Create a Soft Link

```bash
echo "Hello Soft Link" > file2.txt
```

Create the link:

```bash
ln -s file2.txt file2_soft.txt
```

Verify:

```bash
ls -li file2.txt file2_soft.txt
```

Observation:

- Different inode numbers
- Original file's link count does not change
- Soft link file type is `l`

---

## Delete Original File

```bash
rm file2.txt
```

Now:

```bash
cat file2_soft.txt
```

Output:

```text
No such file or directory
```

The soft link becomes a **broken link** because the path stored in it no longer exists.

---

# Soft Link for Directories

A symbolic link can also point to a directory.

```bash
mkdir project
ln -s project project_link
```

Verify:

```bash
ls -ld project project_link
```

---

# Why Can't Hard Links Be Created for Directories?

Linux does not allow hard links for directories because they could create **filesystem loops**, making directory traversal and backups difficult.

---

# Ownership in Linux

Every file has:

- Owner (User)
- Group

View ownership:

```bash
ls -l
```

Example:

```text
-rw-r--r-- 1 labex developers 120 Jul 30 file1.txt
```

Owner = **labex**

Group = **developers**

---

# chown Command

The `chown` command changes the owner and/or group of a file or directory.

## Syntax

```bash
sudo chown owner:group file
```

---

## Examples

Change owner:

```bash
sudo chown chetan file1.txt
```

Change group:

```bash
sudo chown :devops file1.txt
```

Change owner and group:

```bash
sudo chown chetan:devops file1.txt
```

Recursive ownership change:

```bash
sudo chown -R chetan:devops project/
```

---

# chown vs chgrp

| Command | Purpose |
|----------|---------|
| `chown` | Change owner (and optionally group) |
| `chgrp` | Change only the group |

Example:

```bash
sudo chgrp developers file1.txt
```

---

# Why is sudo Required?

Changing ownership is a **security-sensitive operation**.

Only the **root user** or a user with **sudo privileges** can change ownership.

---

# What is sudo?

`sudo` stands for **Super User Do**.

It allows an authorized user to temporarily execute commands with elevated privileges.

Example:

```bash
sudo apt update
```

---

# Regular User vs sudo

Without sudo:

```bash
ls /root
```

Output:

```text
Permission denied
```

With sudo:

```bash
sudo ls /root
```

Now access is allowed.

---

# Principle of Least Privilege

Users should be given **only the permissions they need**, and nothing more.

This reduces accidental mistakes and improves system security.

---

# Managing sudo Access

Edit the sudoers file safely:

```bash
sudo visudo
```

Example:

```text
username ALL=(ALL) ALL
```

Passwordless sudo:

```text
username ALL=(ALL) NOPASSWD: ALL
```

---

# Add User to sudo Group (Ubuntu)

```bash
sudo usermod -aG sudo username
```

Verify:

```bash
groups username
```

---


# Commands Covered

```bash
ls -li
stat
ln
ln -s
rm
cat
chown
chgrp
sudo
visudo
usermod
groups
```
