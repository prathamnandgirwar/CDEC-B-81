# Day 14: Archiving and Compression in Linux

## 📌 Overview

In this session, we will learn about **Archiving** and **Compression** in Linux.

These concepts are very important for:

- Server backups
- Packaging multiple files into one file
- Transferring data between servers
- Saving storage space
- Managing large amounts of data
- Uploading backups to cloud storage

---

# 1. 📦 Archiving in Linux

## What is Archiving?

**Archiving** means combining multiple files and directories into **one single file**.

For example, suppose we have:

    project/
    ├── file1.txt
    ├── file2.txt
    ├── file3.txt
    └── logs/
        ├── app.log
        └── error.log

Instead of transferring every file separately, we can combine everything into one archive:

    project.tar

### Important Point

> **Archiving does NOT necessarily reduce file size.**

It mainly combines multiple files and directories into a single file.

---

## Why Do We Use Archiving?

### 1. Backup

We can combine important directories into one archive.

    /etc
       ↓
    etc_backup.tar

### 2. Data Transfer

Instead of transferring hundreds of files:

    file1
    file2
    file3
    file4
    ...
    file100

we can create:

    backup.tar

and transfer one file.

### 3. Organization

Archiving makes it easier to manage a large collection of files.

---

# 2. 🛠️ `tar` Command

The most commonly used command for archiving in Linux is:

    tar

`tar` originally means:

> **Tape Archive**

Today, `tar` is commonly used for creating backups, packaging files, and handling compressed archives.

---

## Basic Syntax

    tar [options] archive_name.tar files/directories

Example:

    tar -cvf backup.tar file1.txt file2.txt

---

# 3. 🔑 Important `tar` Options

| Option | Meaning |
|---|---|
| `-c` | Create an archive |
| `-f` | Specify archive file name |
| `-v` | Verbose – display files being processed |
| `-t` | List contents of archive |
| `-x` | Extract archive |
| `-C` | Specify destination directory |

### Easy Way to Remember

    -c → Create
    -x → Extract
    -t → List contents
    -v → Verbose
    -f → File name
    -C → Change destination directory

---

# 4. 📏 Check Directory Size

Before creating a backup, we can check the size of a directory using:

    du -sh /etc

### Example

    100M    /etc

### Meaning

- `du` → Disk Usage
- `-s` → Summary
- `-h` → Human-readable

So:

    du -sh /etc

means:

> Show the total size of `/etc` in a human-readable format.

---

# 5. 🗄️ Create a TAR Archive

Suppose we want to archive `/etc`.

    tar -cvf /mnt/etc_bkp.tar /etc

### Explanation

    tar
    │
    ├── -c → Create archive
    ├── -v → Show files
    ├── -f → Archive file name
    │
    └── /mnt/etc_bkp.tar → Archive name
            /etc → Directory to archive

The result will be:

    /etc
       ↓
    /mnt/etc_bkp.tar

---

# 6. 📏 Check Archive Size

After creating the archive:

    du -sh /mnt/etc_bkp.tar

We can also use:

    ls -lh /mnt/etc_bkp.tar

### Difference

`du -sh` shows disk usage.

`ls -lh` shows file size along with other file information.

---

# 7. 📋 List Contents of a TAR Archive

We don't need to extract an archive just to see what is inside it.

Use:

    tar -tvf /mnt/etc_bkp.tar

For large archives:

    tar -tvf /mnt/etc_bkp.tar | less

### Explanation

    -t → List contents
    -v → Verbose output
    -f → Specify archive

---

# 8. 📤 Extract a TAR Archive

## Extract in Current Directory

    tar -xvf etc_bkp.tar

### Explanation

    -x → Extract
    -v → Verbose
    -f → Archive file

---

## Extract to Another Directory

Suppose we want to extract the archive into `/media/etc`.

    tar -xvf etc_bkp.tar -C /media/etc

### Important

The destination directory should normally exist before extraction.

For example:

    mkdir -p /media/etc

Then:

    tar -xvf etc_bkp.tar -C /media/etc

---

# 9. 🗜️ What is Compression?

**Compression** means reducing the amount of storage space required to represent data.

For example:

    Original file
         ↓
       100 MB
         ↓
      Compression
         ↓
        40 MB

The exact reduction depends on the type and contents of the data.

---

## Benefits of Compression

### 💽 1. Saves Storage

Compressed files generally require less disk space.

### 🚀 2. Faster Transfer

Smaller files can generally be transferred faster.

### 💰 3. Reduces Storage Cost

Less storage space may be required for backups and archives.

### ☁️ 4. Useful for Cloud Backups

Compressed archives are commonly used before uploading backups to cloud storage.

---

# 10. 📦 Archiving vs Compression

These two concepts are different.

## Archiving

Combines multiple files/directories into one file.

    file1
    file2
    file3
       ↓
    archive.tar

## Compression

Reduces the size of data.

    100 MB
       ↓
    Compression
       ↓
     40 MB

## Combining Both

In Linux, we commonly do both:

    Multiple Files
          ↓
       Archive
          ↓
        .tar
          ↓
      Compression
          ↓
       .tar.gz

For example:

    tar -czvf backup.tar.gz project/

This command:

1. Creates an archive
2. Compresses it using gzip
3. Produces `backup.tar.gz`

---

# 11. 🗜️ Common Compression Methods

Linux commonly uses the following compression methods with `tar`:

| Compression | `tar` Option | Extension |
|---|---:|---|
| gzip | `-z` | `.tar.gz` |
| bzip2 | `-j` | `.tar.bz2` |
| xz | `-J` | `.tar.xz` |

---

# 12. 🟢 Gzip Compression

`gzip` is one of the most commonly used compression methods.

## Create a gzip-compressed archive

    tar -cvzf /mnt/etc_bkp.tar.gz /etc

### Option Meaning

    -c → Create
    -v → Verbose
    -z → gzip compression
    -f → File name

### Check Size

    du -sh /mnt/etc_bkp.tar.gz

---

## Extract Gzip Archive

    tar -xvzf /mnt/etc_bkp.tar.gz

Extract to a specific directory:

    tar -xvzf /mnt/etc_bkp.tar.gz -C /media

---

# 13. 🔵 Bzip2 Compression

Bzip2 generally provides stronger compression than gzip but can be slower.

## Create Bzip2 Archive

    tar -cvjf /mnt/etc_bkp.tar.bz2 /etc

### Option Meaning

    -c → Create
    -v → Verbose
    -j → bzip2 compression
    -f → File name

### Check Size

    du -sh /mnt/etc_bkp.tar.bz2

---

## Extract Bzip2 Archive

    tar -xvjf /mnt/etc_bkp.tar.bz2

Extract to another directory:

    tar -xvjf /mnt/etc_bkp.tar.bz2 -C /media

---

# 14. 🟣 XZ Compression

`xz` generally provides high compression, but it can require more CPU time.

## Create XZ Archive

    tar -cvJf /mnt/etc_bkp.tar.xz /etc

### Option Meaning

    -c → Create
    -v → Verbose
    -J → xz compression
    -f → File name

### Check Size

    du -sh /mnt/etc_bkp.tar.xz

---

## Extract XZ Archive

    tar -xvJf /mnt/etc_bkp.tar.xz

Extract to another directory:

    tar -xvJf /mnt/etc_bkp.tar.xz -C /media

---

# 15. ⚖️ Compression Comparison

| Tool | Compression Level | Speed | CPU Usage | Common Use |
|---|---|---|---|---|
| gzip | Good | Fast | Low | Logs, daily backups |
| bzip2 | Better | Slower | Medium | Backup/storage |
| xz | High | Slower | Higher | Long-term archives |

### Simple Rule

    gzip  → Faster
    bzip2 → Balanced
    xz    → Better compression

> The best option depends on whether you care more about speed, compression ratio, or CPU usage.

---

# 16. 📊 Important File Extensions

| Extension | Meaning |
|---|---|
| `.tar` | Archive without compression |
| `.tar.gz` | TAR + gzip |
| `.tgz` | Short form of `.tar.gz` |
| `.tar.bz2` | TAR + bzip2 |
| `.tar.xz` | TAR + xz |

---

# 17. 🧠 Important Interview Concept

## Is TAR compression?

**No.**

`tar` itself is primarily an **archiving tool**.

For example:

    tar -cvf backup.tar project/

This creates an archive but does not apply gzip/bzip2/xz compression.

When we use:

    tar -czvf backup.tar.gz project/

we are doing:

    tar  → Archive
    gzip → Compress

---

# 18. 🔥 Practical Demo

Let's create a small project for practice.

## Step 1: Create Directory

    mkdir project

## Step 2: Create Files

    touch project/file1.txt
    touch project/file2.txt
    touch project/file3.txt

## Step 3: Check Files

    ls -l project/

## Step 4: Create TAR Archive

    tar -cvf project.tar project/

## Step 5: List Archive Contents

    tar -tvf project.tar

## Step 6: Create Gzip Archive

    tar -czvf project.tar.gz project/

## Step 7: Check Files

    ls -lh project.tar*

## Step 8: Create Extraction Directory

    mkdir extracted

## Step 9: Extract Archive

    tar -xzvf project.tar.gz -C extracted/

## Step 10: Verify

    ls -R extracted/

---

# 19. 🔄 Complete Workflow

A common Linux backup workflow looks like this:

    Files / Directory
           │
           ▼
       Archiving
           │
           ▼
        project.tar
           │
           ▼
      Compression
           │
           ▼
      project.tar.gz
           │
           ▼
      Backup / Transfer
           │
           ▼
      Extract when needed

---

# 20. 📝 Quick Command Reference

| Task | Command |
|---|---|
| Check directory size | `du -sh directory/` |
| Create TAR | `tar -cvf backup.tar directory/` |
| List TAR | `tar -tvf backup.tar` |
| Extract TAR | `tar -xvf backup.tar` |
| Extract to directory | `tar -xvf backup.tar -C /path` |
| Create gzip archive | `tar -czvf backup.tar.gz directory/` |
| Extract gzip | `tar -xzvf backup.tar.gz` |
| Create bzip2 archive | `tar -cjvf backup.tar.bz2 directory/` |
| Extract bzip2 | `tar -xjvf backup.tar.bz2` |
| Create xz archive | `tar -cJvf backup.tar.xz directory/` |
| Extract xz | `tar -xJvf backup.tar.xz` |

---

# 🎯 Key Takeaways

By the end of this session, you should understand:

- ✅ What is **Archiving**
- ✅ What is **Compression**
- ✅ Difference between Archiving and Compression
- ✅ Why `tar` is used
- ✅ How to create a `.tar` archive
- ✅ How to list archive contents
- ✅ How to extract an archive
- ✅ How to extract to a specific directory
- ✅ What are `gzip`, `bzip2`, and `xz`
- ✅ Difference between `.tar`, `.tar.gz`, `.tar.bz2`, and `.tar.xz`
- ✅ How to create and extract compressed archives
- ✅ How archiving and compression are useful for **backup and data transfer**

---


# 📚 Summary

    Archiving
        ↓
    Combines multiple files/directories
        ↓
    tar
        ↓
    backup.tar

    Compression
        ↓
    Reduces data size
        ↓
    gzip / bzip2 / xz
        ↓
    backup.tar.gz
    backup.tar.bz2
    backup.tar.xz

> **Remember:** `tar` = Archive, while `gzip/bzip2/xz` = Compression.
